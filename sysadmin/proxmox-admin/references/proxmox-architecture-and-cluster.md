# Proxmox VE Architecture and Cluster Management

Detailed technical reference for Proxmox VE 9.x core architecture, Proxmox Cluster File System (`pmxcfs`), Corosync 3 cluster quorum, and multi-node lifecycle operations.

---

## 1. Proxmox VE 9.x Architecture Stack

Proxmox Virtual Environment 9.x is built upon Debian 13 ("Trixie") and integrates bare-metal hypervisor capabilities, containerization, software-defined storage, and software-defined networking into a single unified stack.

```text
┌─────────────────────────────────────────────────────────────┐
│  Proxmox Web GUI (Yew Rust) / PVE REST API / pvesh / CLI   │
├─────────────────────────────────────────────────────────────┤
│  Proxmox Cluster Filesystem (pmxcfs - /etc/pve memory DB)   │
├──────────────────────────────┬──────────────────────────────┤
│ Virtual Machines (QEMU 10.0) │ LXC Containers (LXC 6.0)     │
├──────────────────────────────┴──────────────────────────────┤
│ Storage: ZFS 2.3 / Ceph Squid 19.2 / LVM-thin / PBS Client   │
├─────────────────────────────────────────────────────────────┤
│ Software-Defined Networking (SDN Fabrics / EVPN / VXLAN)    │
├─────────────────────────────────────────────────────────────┤
│ Linux Kernel 6.14+ / Debian 13 ("Trixie") Bare Metal OS    │
└─────────────────────────────────────────────────────────────┘
```

---

## 2. Proxmox Cluster File System (`pmxcfs`)

`pmxcfs` is a database-driven FUSE filesystem that replicates configuration files in real-time across all nodes in a cluster using Corosync engine consensus.

- **Mount Location**: `/etc/pve/`
- **Storage Backend**: SQLite database stored on disk at `/var/lib/pve-cluster/config.db` and cached in RAM.
- **Quorum Requirement**: `/etc/pve` becomes **Read-Only** if the cluster loses quorum. Configuration updates (starting VMs, creating users, editing rules) require an active quorum.

### Critical `/etc/pve/` Directory Paths

- `/etc/pve/corosync.conf`: Corosync cluster membership and network link definition.
- `/etc/pve/storage.cfg`: Cluster-wide storage definitions.
- `/etc/pve/sdn/`: Software-Defined Networking configuration files.
- `/etc/pve/nodes/<nodename>/qemu-server/<vmid>.conf`: VM hardware configuration files.
- `/etc/pve/nodes/<nodename>/lxc/<vmid>.conf`: LXC container configuration files.
- `/etc/pve/priv/`: Private key material, shadow files, and API tokens.

---

## 3. Corosync 3 Cluster & Quorum Mechanics

Corosync handles node membership messaging and vote tallying to maintain cluster quorum.

### Quorum Rules and Math

- **Quorum Equation**: $\text{Quorum Votes Required} = \left\lfloor \frac{\text{Total Votes}}{2} \right\rfloor + 1$
- **3-Node Cluster**: Total votes = 3. Quorum required = 2. Can sustain 1 node failure.
- **5-Node Cluster**: Total votes = 5. Quorum required = 3. Can sustain 2 node failures.
- **2-Node Cluster + QDevice**: Total votes = 3 (2 nodes + 1 external QDevice voter). Can sustain 1 node failure without split-brain.

### Dual-Link Redundant Network Topology

To prevent cluster partition (split-brain) during switch failures, Corosync must be configured with at least two independent network links on separate physical NICs and switches.

```ini
# /etc/pve/corosync.conf
nodelist {
  node {
    name: pve-01
    nodeid: 1
    ring0_addr: 10.10.10.11
    ring1_addr: 10.10.20.11
  }
  node {
    name: pve-02
    nodeid: 2
    ring0_addr: 10.10.10.12
    ring1_addr: 10.10.20.12
  }
  node {
    name: pve-03
    nodeid: 3
    ring0_addr: 10.10.10.13
    ring1_addr: 10.10.20.13
  }
}
```

---

## 4. Cluster Lifecycle Operations

### Creating a New Cluster

```bash
# On first node (pve-01)
pvecm create prox-cluster-01 --link0 10.10.10.11,priority=15 --link1 10.10.20.11,priority=10
```

### Joining a Node to the Cluster

```bash
# On joining node (pve-02)
pvecm join 10.10.10.11 --link0 10.10.10.12 --link1 10.10.20.12
```

### Setting up a QDevice (External Quorum Vote)

For 2-node clusters, install `corosync-qnetd` on an external Linux host (Debian/Raspberry Pi) and run:

```bash
# From a cluster node
pvecm qdevice setup <qnetd-host-ip>
```

### Checking Cluster & Quorum Health

```bash
pvecm status
pvecm nodes
```

### Removing a Failed Node Safely

```bash
# Power off target node permanently first
pvecm delnode pve-failed-03
# Clean up leftover configuration directory if necessary
rm -rf /etc/pve/nodes/pve-failed-03
```
