# Virtual Machine and LXC Container Orchestration

Technical guide to VM management (`qm`), LXC container management (`pct`), Cloud-Init automated provisioning, OCI container images, and resource tuning in Proxmox VE 9.x.

---

## 1. Virtual Machine Management (`qm`)

Virtual Machines run under QEMU 10.0 / KVM, providing complete hardware virtualization and OS independence.

### High-Performance VM Hardware Defaults

- **CPU Model**: `host` (exposes native CPU flags to guest, enabling AVX2/AVX-512 and nested virtualization).
- **SCSI Controller**: `virtio-scsi-single` with `iothread=1` enabled on each disk (allocates dedicated thread per disk for maximum storage IOPS).
- **Network Interface**: `virtio` (paravirtualized network driver) with firewall enabled.
- **QEMU Guest Agent**: Enabled (`agent: 1`) to provide graceful shutdowns, IP address reporting, and filesystem freezing during backups.

### Cloud-Init Automated Provisioning

Cloud-init automates OS deployment (IP address, SSH keys, user creation) upon initial VM boot.

```bash
# Download Debian cloud image
wget https://cloud.debian.org/images/cloud/trixie/daily/latest/debian-13-genericcloud-amd64.qcow2

# Create VM 1000 and import disk
qm create 1000 --name debian13-template --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0
qm importdisk 1000 debian-13-genericcloud-amd64.qcow2 local-zfs
qm set 1000 --scsihw virtio-scsi-single --scsi0 local-zfs:vm-1000-disk-0,iothread=1
qm set 1000 --ide2 local-zfs:cloudinit
qm set 1000 --boot c --bootdisk scsi0
qm set 1000 --serial0 socket --vga serial0
qm set 1000 --ciuser sysadmin --sshkeys ~/.ssh/id_rsa.pub --ipconfig0 ip=dhcp
qm template 1000

# Clone template to new VM 105
qm clone 1000 105 --name app-server-01 --full 1
qm set 105 --ipconfig0 ip=10.10.10.50/24,gw=10.10.10.1
qm start 105
```

---

## 2. LXC Container Orchestration (`pct`)

LXC containers share the host Linux kernel 6.14+, delivering near-zero performance overhead and ultra-fast boot times.

### Privileged vs. Unprivileged Containers

- **Unprivileged Containers (Default & Recommended)**: Maps root UID inside container to an unprivileged UID (`100000`) on the host node. Protects host from container breakout exploits.
- **Privileged Containers**: Runs container root as host root (`UID 0`). Required ONLY for direct host hardware passthrough or legacy NFS mounts.

### PVE 9 OCI Container Image Support

Proxmox VE 9 natively supports deploying LXC containers directly from OCI/Docker container image registries (e.g., Docker Hub, GitHub Container Registry), streamlining lightweight application deployment without Docker daemon overhead.

```bash
# Create unprivileged LXC container 200
pct create 200 local:vztmpl/debian-13-standard_13.0-1_amd64.tar.zst \
  -hostname web-ct \
  -ostype debian \
  -cores 2 \
  -memory 1024 \
  -features nesting=1 \
  -net0 name=eth0,bridge=vmbr0,firewall=1,ip=dhcp \
  -unprivileged 1 \
  -start 1
```

---

## 3. Host-to-Guest Storage Bind Mounts

Bind mounts expose host directory paths directly into LXC containers.

```ini
# Add to /etc/pve/nodes/<node>/lxc/<vmid>.conf
mp0: /tank/shared_data,mp=/mnt/data,ro=0
```

---

## 4. Resource Allocation and NUMA Tuning

- **NUMA (Non-Uniform Memory Access)**: Enable NUMA (`numa: 1`) on multi-socket CPU systems to pin VM memory allocation to local CPU sockets, avoiding cross-socket memory bus latency.
- **CPU Pinning**: Pin mission-critical real-time workloads to specific physical CPU cores (`cpulimit`, `affinity`).
- **Memory Ballooning**: Dynamically expands or shrinks guest RAM based on host pressure. Disable ballooning for high-performance databases to prevent memory fragment latency.
