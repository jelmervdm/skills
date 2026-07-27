# CLI Utilities, MCP Automation, and Troubleshooting Playbooks

Comprehensive reference for Proxmox VE CLI management tools (`pvecm`, `qm`, `pct`, `pvesh`), Model Context Protocol (`proxmox-mcp`) integration, and emergency troubleshooting procedures.

---

## 1. Proxmox VE CLI Tool Cheat Sheet

| Tool | Focus Area | Key Commands |
| --- | --- | --- |
| **`pvecm`** | Cluster Manager | `pvecm status`, `pvecm nodes`, `pvecm expected 1`, `pvecm delnode <node>` |
| **`qm`** | QEMU VM Manager | `qm list`, `qm start <id>`, `qm stop <id>`, `qm unlock <id>`, `qm migrate <id> <target>` |
| **`pct`** | LXC Container Toolkit | `pct list`, `pct start <id>`, `pct enter <id>`, `pct unlock <id>`, `pct set <id> --memory 2048` |
| **`pvesh`** | Proxmox API Shell | `pvesh get /cluster/resources`, `pvesh get /nodes/<node>/status`, `pvesh create /nodes/<node>/qemu/<id>/status/start` |
| **`pvesm`** | Storage Manager | `pvesm status`, `pvesm alloc <storage> <vmid> <file> <size>`, `pvesm list <storage>` |
| **`pvesdn`** | SDN Manager | `pvesdn reload`, `pvesdn status` |

---

## 2. Interfacing with `proxmox-mcp` Server

The Model Context Protocol (`proxmox-mcp`) server allows AI assistants to interact safely with Proxmox VE REST API endpoints.

### Key MCP Tools

- `proxmox_list_nodes`: Queries status, uptime, CPU, and RAM load of all nodes in the cluster.
- `proxmox_list_vms`: Lists all virtual machines and LXC containers with state, assigned node, and resource usage.
- `proxmox_get_vm_config`: Fetches raw configuration key-values for a guest VM (`qm.conf`).
- `proxmox_start_vm` / `proxmox_stop_vm`: Sends graceful power commands to a target guest.
- `proxmox_migrate_vm`: Initiates live migration of a VM or container to a specified target node.
- `proxmox_query_cluster_log`: Retrieves cluster-wide syslog and task log entries.

---

## 3. Emergency Troubleshooting Playbooks

### Playbook 1: Emergency Quorum Recovery (`pvecm expected 1`)

**Symptom**: Multiple cluster nodes offline. Remaining single node loses quorum; `/etc/pve` becomes read-only; VMs cannot be started or managed via GUI.

**Remediation**:

```bash
# Temporary Emergency Override: Tell Corosync expected votes is 1
pvecm expected 1

# /etc/pve will instantly become writable. Start critical VMs:
qm start 105

# IMPORTANT: Fix physical node connectivity or remove dead node permanently once investigated!
```

### Playbook 2: Clearing Locked Guest VMs (`qm unlock` / `pct unlock`)

**Symptom**: VM stuck in `lock: backup`, `lock: migrate`, or `lock: snapshot` state after an interrupted task. VM ignores start/stop commands.

**Remediation**:

```bash
# Check lock status
qm config 105 | grep lock

# Clear lock
qm unlock 105

# If unlock fails, check running tasks and kill orphaned QEMU process
ps aux | grep qemu-105
```

### Playbook 3: Node Storage Full (Root or ZFS Pool 100% Full)

**Symptom**: Hypervisor node stops responding; VMs freeze due to IO write errors; `/var/log` or ZFS pool full.

**Remediation**:

```bash
# Check filesystem and ZFS usage
df -h
zpool list

# Prune old VZDump backups or systemd logs
journalctl --vacuum-size=500M
rm -rf /var/log/vzdump/*.log

# Trim ZFS free space
zpool trim rpool
```

### Playbook 4: Corosync Network Split-Brain Recovery

**Symptom**: Nodes show as offline in `pvecm status` despite physical hosts being up.

**Remediation**:

```bash
# Check Corosync daemon status and logs
systemctl status corosync
journalctl -u corosync -n 50 --no-pager

# Restart cluster services in sequence across nodes
systemctl restart pve-cluster
systemctl restart corosync
```
