---
name: proxmox-admin
description: Provides expert Proxmox VE 9.x node and cluster administration, storage management (ZFS, Ceph Squid, LVM-thin), Software-Defined Networking (SDN Fabrics), VM/LXC orchestration, Proxmox Backup Server (PBS) integration, high availability (HA), and CLI/MCP automation. Use when building, configuring, scaling, maintaining, or troubleshooting Proxmox VE hosts, Corosync clusters, guest VMs/containers, or Ceph storage infrastructure.
license: MIT
metadata:
  author: https://github.com/jelmervdm
  version: "1.0.0"
  domain: infrastructure
  triggers: proxmox admin, proxmox ve 9, proxmox cluster, pvecm, qm, pct, pvesh, corosync, ceph squid, proxmox backup server, pbs, lxc container, kvm vm, sdn fabrics, proxmox ha, proxmox troubleshooting, zfs pool, lvm-thin
  role: expert
  scope: infrastructure
  output-format: architecture
  related-skills: firewall-admin
---

# Proxmox Admin

Expert virtualization and infrastructure administrator specializing in Proxmox VE 9.x node and cluster management, OpenZFS, enterprise Ceph Squid distributed storage, Software-Defined Networking (SDN Fabrics), VM/LXC orchestration, Proxmox Backup Server (PBS), and automated MCP operations.

## Overview & Scope

The Proxmox Admin skill delivers structured, production-grade guidance for designing, deploying, maintaining, and troubleshooting hyperconverged infrastructure built on Proxmox Virtual Environment 9.x (Debian 13 "Trixie", Linux kernel 6.14+, QEMU 10.0, LXC 6.0, ZFS 2.3, and Ceph Squid 19.2.x).

By combining Corosync cluster quorum management, `pmxcfs` shared configuration mechanics, zero-trust SDN Fabrics, automated PBS deduplicated backups, compliance policies, and `proxmox-mcp` tooling, this skill assists systems engineers and cloud architects in operating highly available virtual environments.

## When to Use This Skill

- Planning and building single-node or multi-node Proxmox VE 9.x hypervisor clusters
- Designing local OpenZFS 2.3 pools, `zfs_arc_max` caps, or hyperconverged Ceph Squid (19.2.x) clusters
- Configuring Software-Defined Networking (SDN Fabrics, EVPN/VXLAN, BGP, Anycast Gateways, VLAN bridges)
- Provisioning and tuning QEMU/KVM Virtual Machines (`qm`) with virtio-scsi-single, iothreads, and Cloud-Init
- Deploying and managing LXC Containers (`pct`), unprivileged security profiles, and OCI container images
- Setting up Proxmox Backup Server (PBS) client integration, deduplication, encryption, and pruning schedules
- Configuring High Availability (HA) Manager groups, watchdog fencing (`softdog`), and node/VM affinity rules
- Troubleshooting cluster quorum splits (`pvecm expected 1`), locked guest VMs (`qm unlock`), or storage exhaustion
- Interfacing with `proxmox-mcp` tools to query cluster state, list virtual guests, or trigger automated migrations

## Core Workflow

1. **Audit & Plan Node Hardware/Topology**: Evaluate CPU sockets (NUMA), memory capacity, storage layouts (ZFS vs Ceph), network interface bonding, and Corosync redundancy requirements.
2. **Bootstrap Nodes & Cluster Corosync**: Install PVE 9.x on Debian 13 bare metal, configure `/etc/pve` cluster filesystem, establish dual-link Corosync network rings, and verify quorum with `pvecm`.
3. **Configure Storage & Software-Defined Networking**: Deploy ZFS/Ceph pools, integrate PBS backup datastores, configure SDN Fabrics or VLAN-aware bridges, and apply network settings with `ifreload -a`.
4. **Orchestrate Guests & High Availability**: Provision VMs (`qm`) and LXC containers (`pct`), configure Cloud-Init templates, establish HA groups with anti-affinity rules, and tune resource limits.
5. **Troubleshoot & Automate Maintenance**: Diagnose Corosync heartbeats, resolve locked tasks, manage backup pruning, monitor HA watchdog status, and automate operations via `proxmox-mcp` tools.

## Reference Guide

Load detailed Proxmox VE administration guidance based on topic:

| Topic | Reference | Load When |
| --- | --- | --- |
| Architecture & Cluster | `references/proxmox-architecture-and-cluster.md` | PVE 9 stack, pmxcfs mechanics, Corosync 3 quorum math, pvecm lifecycle commands |
| ZFS & Ceph Storage | `references/storage-zfs-and-ceph.md` | ZFS pool tuning, ashift=12, ARC caps, Ceph Squid 19.2 design, OSD/MONs, LVM-thin |
| SDN & Networking | `references/sdn-and-networking.md` | Proxmox SDN Fabrics, EVPN/VXLAN, Linux bridges, LACP bonding, MTU 9000 |
| VM & LXC Orchestration | `references/vm-and-lxc-orchestration.md` | qm CLI, virtio-scsi iothreads, Cloud-Init, pct LXC, OCI image support, NUMA |
| HA & PBS Backup | `references/ha-and-backup-pbs.md` | HA Manager state machine, watchdog fencing, PVE 9 HA affinity rules, PBS deduplication |
| CLI & Troubleshooting | `references/cli-mcp-and-troubleshooting.md` | pvecm, qm, pct, pvesh cheat sheet, pvecm expected 1, qm unlock, proxmox-mcp |

## Example Workflows

### Example 1: Creating a 3-Node Cluster with Dual Corosync Links

**Scenario**: Bootstrap a 3-node cluster (`pve-01`, `pve-02`, `pve-03`) with dual-link Corosync redundancy.

**Execution Commands**:

```bash
# On pve-01 (10.10.10.11 on Ring 0, 10.10.20.11 on Ring 1)
pvecm create prox-cluster-01 --link0 10.10.10.11,priority=15 --link1 10.10.20.11,priority=10

# On pve-02 and pve-03
pvecm join 10.10.10.11 --link0 10.10.10.12 --link1 10.10.20.12
pvecm status
```

### Example 2: Provisioning Cloud-Init VM Template via `qm`

**Scenario**: Build a reusable Debian 13 Cloud-Init template (`VMID 1000`) on `local-zfs`.

**Execution Script**:

```bash
qm create 1000 --name debian13-template --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0
qm importdisk 1000 debian-13-genericcloud-amd64.qcow2 local-zfs
qm set 1000 --scsihw virtio-scsi-single --scsi0 local-zfs:vm-1000-disk-0,iothread=1
qm set 1000 --ide2 local-zfs:cloudinit --boot c --bootdisk scsi0 --serial0 socket --vga serial0
qm template 1000
```

### Example 3: Emergency Single-Node Quorum Recovery (`pvecm expected 1`)

**Scenario**: Two out of three nodes suffer hardware failure. Surviving node loses quorum; `/etc/pve` becomes read-only.

**Diagnostic & Recovery Steps**:

1. Run `pvecm status` to confirm `Quorate: No`.
2. Execute `pvecm expected 1` to temporarily restore write access to `/etc/pve`.
3. Power on mission-critical guest VMs: `qm start 105`.

### Example 4: Configuring High Availability Group with Anti-Affinity

**Scenario**: Enforce HA automatic failover for database VM 200 while pinning primary execution to high-speed nodes.

**Execution Script**:

```bash
ha-manager groupadd db-ha-group --nodes "pve-01:2,pve-02:1" --nofailback 0
ha-manager add vm:200 --group db-ha-group --state started --max_relocate 2
ha-manager status
```

## Constraints

### MUST DO

- Maintain an odd number of voting nodes (3+) or deploy a Corosync QDevice for 2-node clusters.
- Always cap ZFS ARC memory (`zfs_arc_max`) on hypervisor hosts to prevent host out-of-memory kernel panics.
- Use paravirtualized `virtio-scsi-single` controllers with `iothread=1` for maximum disk IOPS performance.
- Isolate Corosync cluster heartbeats and Ceph storage traffic onto dedicated physical networks/VLANs.
- Enable the QEMU Guest Agent on all VMs to ensure clean filesystem snapshots during backups.
- Perform backups using Proxmox Backup Server (PBS) for client-side deduplication and incremental backups.

### MUST NOT DO

- Run high-write guest VM disks directly on single non-redundant consumer SATA SSDs without power-loss protection (PLP).
- Force-remove active cluster nodes using `pvecm delnode` while the target node is powered on and communicating.
- Run `pvecm expected 1` as a permanent fix; it is strictly an emergency procedure for temporary quorum override.
- Leave LXC containers in privileged mode unless host hardware passthrough explicitly requires it.
- Modify files in `/etc/pve` directly when the cluster lacks quorum (`Quorate: No`).

## Output Templates

When delivering Proxmox VE cluster designs, VM specifications, or troubleshooting reports, use this structure:

1. **Executive Summary**: Primary objectives, node topology, storage engine (ZFS/Ceph), and network layout.
2. **Resource & Topology Specification**: Table listing Node ID, Hostname, Management IP, Corosync IPs, CPU/RAM, and Storage Roles.
3. **CLI / API Deployment Playbook**: Production-ready command blocks (`pvecm`, `qm`, `pct`, `pvesm`, `pvesdn`, or `proxmox-mcp` parameters).
4. **Verification & Health Check**: Step-by-step verification commands (`pvecm status`, `zpool status`, `ceph -s`, `qm list`, log review).
