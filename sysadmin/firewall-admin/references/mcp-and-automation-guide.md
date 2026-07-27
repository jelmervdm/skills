# MCP Tooling and Firewall Automation Guide

Comprehensive reference for managing firewalls via Model Context Protocol (MCP) servers (`sophos-firewall-mcp`, `proxmox-mcp`), REST APIs, High Availability (HA) failover monitoring, and Infrastructure-as-Code (IaC) automation.

---

## 1. Interfacing with MCP Firewall Servers

Model Context Protocol (MCP) servers enable AI agents to safely query firewall state, retrieve live connection logs, inspect host object definitions, and propose policy modifications.

### MCP Operational Workflow

```text
┌─────────────────────────┐        MCP JSON-RPC        ┌──────────────────────────┐
│                         │ ─────────────────────────► │                          │
│ AI Agent / Firewall Skill│                            │  Firewall MCP Server     │
│                         │ ◄───────────────────────── │ (e.g., Sophos/Proxmox)   │
└─────────────────────────┘                            └────────────┬─────────────┘
                                                                    │ HTTPS REST API
                                                                    ▼
                                                       ┌──────────────────────────┐
                                                       │  Firewall Appliance      │
                                                       └──────────────────────────┘
```

### Typical MCP Tools for Firewall Administration

- `firewall_list_rules`: Fetches active rule base, priority ordering, state (enabled/disabled), hit counters, and security profiles.
- `firewall_get_rule_details`: Retrieves specific parameters for a rule (source/dest objects, ports, NAT bindings, action).
- `firewall_query_logs`: Queries drop, deny, or threat logs filtered by source IP, destination port, time range, or rule ID.
- `firewall_list_objects`: Enumerates host objects, network definitions, IP ranges, and service groups.
- `firewall_update_rule_status`: Safely enables or disables a firewall rule (requires change approval).
- `firewall_create_host_object`: Adds a single IP or network subnet object to the firewall object store.

---

## 2. High Availability (HA) and Failover Management

Enterprise firewalls deploy HA pairs to eliminate single points of failure.

### HA Configuration Models

| Model | Active Nodes | Standby Nodes | Session Synchronization | Heartbeat Protocol |
| --- | --- | --- | --- | --- |
| **Active-Passive** | 1 Node (Master) | 1 Node (Backup) | Full Conntrack / IPsec state sync | Dedicated HA Link |
| **Active-Active** | All Nodes | None | Distributed connection table | Dedicated HA Link |
| **CARP / VRRP** | Master Virtual IP | Backup Nodes | State table dynamic sync (pfsync) | Multicast Advertisements |

### HA Monitoring and Failover Diagnostics

- **Heartbeat Timeout**: If the primary firewall fails to send keepalive heartbeats within the configured window (e.g., 3 seconds), the backup node promotes its interfaces and assumes virtual MAC/IP addresses.
- **Connection State Synchronization**: Ensure state synchronization (`pfsync` or vendor equivalent) is active over a dedicated, direct network link so existing active connections do not drop during failover.

---

## 3. Infrastructure-as-Code (IaC) and Automation

Managing firewall policies with code ensures auditing, version control, and reproducible change deployment across environments.

### Ansible Firewall Management (`nftables` Example)

```yaml
- name: Apply Hardened Firewall Ruleset
  hosts: firewalls
  become: true
  tasks:
    - name: Deploy nftables configuration
      ansible.builtin.template:
        src: templates/nftables.conf.j2
        dest: /etc/nftables.conf
        owner: root
        group: root
        mode: '0600'
      notify: Reload nftables

  handlers:
    - name: Reload nftables
      ansible.builtin.systemd:
        name: nftables
        state: reloaded
```

### Safe Automated Change Practices

1. **Pre-Change State Backup**: Always archive current running configurations prior to applying automated API changes.
2. **Automated Commit-Confirm / Rollback**: Use `commit confirm <minutes>` mechanisms when updating firewall rules remotely. If connectivity is lost during a change, the firewall automatically rolls back to the previous known good configuration.
3. **Staging Validation**: Test firewall policy changes in a non-production virtual lab environment before deploying to production firewalls.
