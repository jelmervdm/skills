# Proxmox Storage Architecture: ZFS, Ceph Squid, and Shared Storage

Comprehensive guide to storage design, local ZFS pool tuning, enterprise Ceph Squid (19.2.x) distributed storage, LVM-thin, and PVE 9 snapshot mechanisms.

---

## 1. Local ZFS Pool Design and Optimization

OpenZFS 2.3 provides robust checksumming, copy-on-write (CoW) snapshots, self-healing, and inline compression (zstd/lz4) for local node storage.

### ZFS Pool Topologies

| Topology | Fault Tolerance | Read IOPS | Write IOPS | Storage Efficiency | Recommended Use Case |
| --- | --- | --- | --- | --- | --- |
| **Mirrored (RAID10)** | 1-N disk per vdev | Highest ($N \times \text{Disks}$) | High | 50% | High-IOPS VMs, Databases |
| **RAIDZ1 (RAID5)** | 1 disk per vdev | Moderate | Single disk speed | $\frac{N-1}{N}$ | Large sequential data, ISOs |
| **RAIDZ2 (RAID6)** | 2 disks per vdev | Moderate | Single disk speed | $\frac{N-2}{N}$ | High-density bulk storage |

### Critical ZFS Performance Tuning

1. **Sector Alignment (`ashift=12`)**: Always specify `ashift=12` (4096-byte sectors) during pool creation to match modern Advanced Format HDDs/SSDs.
2. **ARC Memory Capping (`zfs_arc_max`)**: By default, ZFS ARC consumes up to 50% of system RAM. On PVE nodes, limit ARC to prevent host OOM kills:

   ```ini
   # /etc/modprobe.d/zfs.conf
   options zfs zfs_arc_max=17179869184  # Cap ARC to 16 GB
   ```

3. **ZFS Special VDEV**: Add mirror NVMe SSDs as a `special` vdev to store metadata and small files ($< 64\text{ KB}$), accelerating HDD pool random IOPS by $10\times$.

```bash
# Create mirrored ZFS pool with ashift=12 and lz4 compression
zpool create -f -o ashift=12 -O compression=lz4 -O atime=off rpool mirror /dev/nvme0n1 /dev/nvme1n1
```

---

## 2. Distributed Ceph Squid (19.2.x) Architecture

Ceph Squid (19.2.x) integrated into Proxmox VE 9 provides hyperconverged, highly available object, block (RBD), and file (CephFS) storage across cluster nodes.

```text
                               Ceph Cluster Network (10.20.10.0/24)
                        ┌─────────────────────────────────────────────────┐
                        │                                                 │
                        ▼                                                 ▼
┌───────────────────────────────┐                 ┌───────────────────────────────┐
│ Node 1: MON / MGR / OSD 0-3   │                 │ Node 2: MON / MGR / OSD 4-7   │
└───────────────┬───────────────┘                 └───────────────┬───────────────┘
                │                                                 │
                └───────────────────────┬─────────────────────────┘
                                        ▼
                       Ceph Public Network (10.10.10.0/24)
                                        │
                                        ▼
                           Proxmox VE KVM / QEMU RBD
```

### Key Ceph Components

- **MON (Monitors)**: Maintains cluster map state. Requires an odd number of monitors (minimum 3).
- **MGR (Managers)**: Runs metrics, dashboard API, and auto-balancing modules.
- **OSD (Object Storage Daemon)**: Manages individual physical drives (NVMe/SSD). Minimum 3 nodes with 4+ OSDs per node recommended.
- **CRUSH Map Rules**: Defines replica placement. Standard rule: `size=3`, `min_size=2` (stores 3 copies of data, allows writes when at least 2 copies are healthy).

### Ceph Network Separation

Ceph MUST utilize two dedicated, unthrottled 10GbE/25GbE+ network interfaces:

- **Public Network**: Handles VM read/write traffic between hypervisors and Ceph OSDs.
- **Cluster Network**: Handles OSD data replication, heartbeats, and background rebalancing/scrubbing.

---

## 3. LVM-Thin and PVE 9 Snapshot Handling

- **LVM-Thin**: Provides block-level thin-provisioned storage with low overhead. Ideal for local SSD installations where ZFS RAM overhead is constrained.
- **Thick-Provisioned LVM Snapshots**: Proxmox VE 9 introduces vendor-agnostic VM snapshot support on thick-provisioned LVM storage, allowing snapshot capabilities on legacy shared block storage (SAN/iSCSI) without full migration.

---

## 4. Storage Content Types in PVE

| Content Type Code | Description | Supported Storage Backends |
| --- | --- | --- |
| `images` | Virtual Machine raw/qcow2 disk images | ZFS, Ceph RBD, LVM-thin, NFS |
| `rootdir` | LXC container root directory filesystems | ZFS, CephFS, LVM-thin, Directory |
| `iso` | Installation ISO image files | Directory, NFS, SMB/CIFS |
| `vztmpl` | LXC OS template archives | Directory, NFS, SMB/CIFS |
| `backup` | VZDump / PBS backup archive files | Proxmox Backup Server, NFS, Directory |
