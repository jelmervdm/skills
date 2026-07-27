# Enterprise and Cloud Firewall Platforms

Comparative technical guide for configuring enterprise Next-Generation Firewalls (NGFW), open-source firewalls, Linux server-native packet filters, and cloud infrastructure security policies.

---

## 1. Enterprise Next-Generation Firewalls (NGFW)

Enterprise firewalls combine traditional stateful filtering with Layer 7 Application Visibility, Threat Intelligence, Intrusion Prevention (IPS), and Identity-Based Policy Enforcements.

| Platform | Core Configuration Paradigm | Key Administrative Features | Policy Structure |
| --- | --- | --- | --- |
| **Sophos XGS / XG** | Zone-based Security Architecture | FastPath Xstream Architecture, Synchronized Security (Heartbeat), WAF, Web Control | Combined Firewall & NAT rules with linked Security Profiles |
| **pfSense / OPNsense** | Open-source FreeBSD Packet Filter (`pf`) | CARP High Availability, Unbound DNS, Suricata/Snort IPS, WireGuard/OpenVPN | Per-interface rule tabs + Floating Rules + Outbound NAT |
| **Palo Alto PAN-OS** | Single Pass Architecture (SP3) | App-ID, User-ID, Content-ID, WildFire Threat Intelligence, Device Groups | Security Policy Rules (Source/Dest Zone, App, Service, Profile) |
| **Fortinet FortiGate** | ASIC Accelerated Processing | FortiGuard Labs, Security Fabric, VDOMs (Virtual Domains), SD-WAN | Policy ID based rules with inline IPS, Antivirus, & Application profiles |

---

## 2. Linux Server-Native Firewalls

Linux firewalls operate in netfilter kernel space, allowing administrators to harden servers, routers, and container hosts directly.

### Comparison of Linux Firewall Toolchains

```text
┌─────────────────────────────────────────────────────────────┐
│ High-Level Wrappers:  UFW (Ubuntu)  │  firewalld (RHEL/Fed) │
├─────────────────────────────────────────────────────────────┤
│ Unified Kernel CLI:   nftables (nft)                        │
├─────────────────────────────────────────────────────────────┤
│ Legacy Tooling:       iptables / ip6tables / arptables      │
├─────────────────────────────────────────────────────────────┤
│ Kernel Processing:    Netfilter Subsystem                   │
└─────────────────────────────────────────────────────────────┘
```

### 1. `nftables` Syntax & Structure (Modern Default)

`nftables` replaces legacy `iptables`, providing higher performance, atomic rule updates, and unified IPv4/IPv6 address family rulesets.

```bash
# Create table and chains
nft add table inet filter
nft add chain inet filter input { type filter hook input priority 0 \; policy drop \; }
nft add chain inet filter forward { type filter hook forward priority 0 \; policy drop \; }
nft add chain inet filter output { type filter hook output priority 0 \; policy accept \; }

# Allow loopback and established connections
nft add rule inet filter input iifname "lo" accept
nft add rule inet filter input ct state established,related accept

# Allow inbound SSH and HTTPS
nft add rule inet filter input tcp dport { 22, 443 } ct state new accept
```

### 2. `iptables` Syntax (Legacy Reference)

```bash
# Set default policies
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Allow loopback and established traffic
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Allow SSH and Web
iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -m conntrack --ctstate NEW -j ACCEPT
```

### 3. UFW (Uncomplicated Firewall)

```bash
ufw default deny incoming
ufw default allow outgoing
ufw allow 22/tcp
ufw allow 443/tcp
ufw enable
```

---

## 3. Cloud and Virtualization Security Rules

Cloud firewalls provide software-defined packet filtering operating at the hypervisor or cloud network infrastructure level.

### AWS Security Groups vs. Network ACLs (NACLs)

| Feature | AWS Security Group (SG) | AWS Network ACL (NACL) |
| --- | --- | --- |
| **Operational Layer** | Instance / ENI Level | Subnet Boundary Level |
| **State Tracking** | Stateful (Return traffic allowed automatically) | Stateless (Inbound & Outbound rules required) |
| **Rule Processing** | Evaluates all rules before deciding | Evaluates rules sequentially by rule number |
| **Action Types** | ALLOW rules only (Implicit deny) | ALLOW and DENY rules |

### Proxmox VE Hypervisor Firewall

Proxmox VE integrates datacenter, cluster, host, and VM/LXC container firewall protection using `pve-firewall`.

- **Cluster Level**: Defines datacenter security aliases, IP sets, and global rules.
- **Host Level**: Protects hypervisor nodes (management web GUI port 8006, SSH port 22, cluster sync).
- **VM / Container Level**: Filters traffic on virtual network interfaces (`tapX`, `vethX`) before packets hit virtual switches.
