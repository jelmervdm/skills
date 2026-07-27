# High Availability and Proxmox Backup Server (PBS)

Technical reference for Proxmox VE High Availability (HA) Manager, watchdog fencing, HA affinity rules, and Proxmox Backup Server (PBS) enterprise backup architecture.

---

## 1. High Availability (HA) Architecture

The Proxmox VE HA Manager automatically monitors and recovers virtual machines and LXC containers if a hypervisor node fails.

```text
┌─────────────────────────────────────────────────────────────┐
│  pve-ha-crm (Cluster Resource Manager - Active Master)      │
├─────────────────────────────────────────────────────────────┤
│  pve-ha-lrm (Local Resource Manager - Per-Node Daemon)      │
├─────────────────────────────────────────────────────────────┤
│  Hardware Watchdog / Softdog Fencing (/dev/watchdog)        │
└─────────────────────────────────────────────────────────────┘
```

### HA State Machine

1. **`request_stop` / `stopped`**: Resource is intentionally powered off.
2. **`started`**: Resource is actively monitored. If the host node dies, CRM migrates and boots the resource on an healthy node.
3. **`fence`**: If a node stops responding to Corosync heartbeats, the HA manager forces the unresponsive node to self-reboot via hardware watchdog (fencing) before fencing-recovering guest VMs on surviving nodes.

---

## 2. PVE 9 Node and VM HA Affinity Rules

Proxmox VE 9 introduces advanced HA Group Affinity Rules:

- **Node Affinity**: Configures preferred nodes for specific workloads (e.g., Run DB VMs on `pve-01` and `pve-02` only).
- **Anti-Affinity Rules**: Prevents redundant guest VMs (e.g., dual domain controllers or Kubernetes control plane nodes) from running on the same physical host node simultaneously.

```bash
# Create HA Group with priority and restricted node fallback
ha-manager groupadd high-perf-group --nodes "pve-01:2,pve-02:1" --nofailback 0

# Add VM 105 to HA management
ha-manager add vm:105 --group high-perf-group --state started --max_relocate 2
```

---

## 3. Proxmox Backup Server (PBS) Integration

Proxmox Backup Server provides client-side deduplicated, encrypted, and incremental-forever backup storage for Proxmox VE.

```text
┌─────────────────────────┐                        ┌─────────────────────────┐
│ Proxmox VE Hypervisor   │ ── Incremental Chunks ─►│ Proxmox Backup Server   │
│ (QEMU Dirty Bitmaps)    │    (AES-256 Encrypted) │ (ZFS / Chunk Store)     │
└─────────────────────────┘                        └────────────┬────────────┘
                                                                │ Remote Sync
                                                                ▼
                                                   ┌─────────────────────────┐
                                                   │ Offsite PBS Instance    │
                                                   └─────────────────────────┘
```

### Key PBS Advantages

- **Client-Side Deduplication**: Data is split into $4\text{ MB}$ chunks and hashed (SHA-256). Only unique chunks are transferred across the network.
- **QEMU Dirty Bitmaps**: Live backups do not require full disk scans. Only modified disk blocks since the last backup snapshot are read.
- **Client-Side Encryption**: Backups are encrypted on the PVE host before network transmission using AES-256-GCM keys.

### Configuring PBS Storage on PVE

```bash
# Add PBS datastore via PVE CLI
pvesm add pbs pbs-remote \
  --server pbs.example.com \
  --datastore main-store \
  --username backup-user@pbs \
  --password SecretPassword123 \
  --fingerprint 9a:8b:7c:6d:5e:4f:3a:2b:1c:0d:fe:dc:ba:98:76:54 \
  --encryption-key autogen
```

### Pruning and Retention Policies

Configure retention schedules to prune old snapshots automatically while protecting point-in-time recovery targets:

```bash
# Keep 7 daily, 4 weekly, 12 monthly, and 1 yearly snapshot
proxmox-backup-client prune vm/105 --keep-daily 7 --keep-weekly 4 --keep-monthly 12 --keep-yearly 1
```
