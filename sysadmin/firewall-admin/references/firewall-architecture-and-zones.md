# Firewall Architecture and Security Zones

Comprehensive guide to network security segmentation, zone definitions, stateful packet inspection mechanics, and top-down policy rule evaluation.

---

## 1. Security Zones and Trust Boundaries

Modern firewall policies rely on zone-based security architecture (ZFW) to group interfaces sharing common trust requirements. All inter-zone traffic is blocked by default until an explicit firewall policy is configured.

| Zone Identifier | Default Trust Level | Primary Purpose & Scope | Interface Type & Exposure |
| --- | --- | --- | --- |
| **LAN (Internal)** | High | Trusted corporate workstations, internal servers, directory services | Physical / VLAN (802.1Q) |
| **WAN (External)** | Zero / Untrusted | Internet egress/ingress, untrusted provider transport | Public IPv4/v6, PPPoE, DHCP |
| **DMZ (Demilitarized)** | Low to Medium | Publicly accessible services (Web, Mail, Reverse Proxy, DNS) | Isolated Subnet / VLAN |
| **IoT / OT** | Very Low | Smart hardware, sensors, cameras, HVAC, industrial control systems | Isolated VLAN / No LAN route |
| **Management** | Maximum | Out-of-band management (SSH, HTTPS, IPMI, SNMP, Console) | Dedicated physical interface |
| **VPN** | Medium to High | Remote user sessions, site-to-site tunnels | Virtual Tunnel Interface (VTI) |

### Traffic Flow Matrix (Default Security Posture)

1. **LAN to WAN**: Allowed (with Source NAT / Masquerade enabled).
2. **LAN to DMZ**: Allowed for administration and internal application access.
3. **DMZ to LAN**: Explicitly DENIED. DMZ servers must never initiate connections to the internal network.
4. **WAN to DMZ**: Selectively allowed via Destination NAT (DNAT / Port Forwarding) to public services.
5. **WAN to LAN**: Explicitly DENIED (except ESTABLISHED/RELATED stateful replies).
6. **IoT to LAN/DMZ**: Explicitly DENIED. IoT devices reach the Internet only if strictly required.

---

## 2. Stateful Packet Inspection (SPI) Mechanics

Stateful firewalls maintain a Connection Tracking Table (Conntrack) in kernel memory to monitor layer 3 and layer 4 session states.

```text
  Incoming Packet
        │
        ▼
┌─────────────────────────┐
│ Check Connection Table  │
└───────────┬─────────────┘
            │
    ┌───────┴───────┐
    │ Match Found?  │
    └───┬───────┬───┘
        │       │
    YES │       │ NO (NEW Packet)
        │       │
        │       ▼
        │   ┌──────────────────────────┐
        │   │ Evaluate Firewall Rules  │
        │   └───────────┬──────────────┘
        │               │
        │       ┌───────┴───────┐
        │       │ Allowed?      │
        │       └───┬───────┬───┘
        │       YES │       │ NO
        │           │       │
        ▼           ▼       ▼
    ┌────────┐  ┌────────┐  ┌────────┐
    │ ACCEPT │  │ ACCEPT │  │ DROP / │
    │        │  │ & SAVE │  │ REJECT │
    └────────┘  └────────┘  └────────┘
```

### Connection States

- **`NEW`**: Packet attempting to initiate a new connection (e.g., TCP SYN). Must traverse full rule base evaluation.
- **`ESTABLISHED`**: Packet belongs to an existing, validated connection present in the connection tracking table. Fast-path processed.
- **`RELATED`**: Packet initiating a secondary connection associated with an existing active connection (e.g., FTP data channels, ICMP error messages).
- **`INVALID`**: Packet does not match any known connection state or exhibits corrupted headers/invalid TCP flags (e.g., SYN-FIN, NULL scan). Instantly DROPPED.

---

## 3. Policy Evaluation and Rule Ordering

Firewall rule bases are evaluated sequentially from top to bottom (first-match evaluation). Once a packet matches all criteria of a rule, the designated action is executed, and processing halts.

### Optimal Rule Ordering Strategy

```text
┌─────────────────────────────────────────────────────────┐
│ 1. Anti-Spoofing & Invalid Packet Drops (Edge Hygiene)  │
├─────────────────────────────────────────────────────────┤
│ 2. High-Frequency Local Traffic (DNS, NTP, DHCP)        │
├─────────────────────────────────────────────────────────┤
│ 3. Explicit Management Access (Admin SSH/HTTPS)         │
├─────────────────────────────────────────────────────────┤
│ 4. DMZ Ingress Services (Web, Reverse Proxy)            │
├─────────────────────────────────────────────────────────┤
│ 5. Outbound User Traffic (LAN to WAN HTTP/S)            │
├─────────────────────────────────────────────────────────┤
│ 6. Cross-Zone Inter-VLAN Rules                          │
├─────────────────────────────────────────────────────────┤
│ 7. Explicit Egress Restrictions & Deny Log Rules        │
├─────────────────────────────────────────────────────────┤
│ 8. Implicit Catch-All DENY ALL (Cleanup Rule)           │
└─────────────────────────────────────────────────────────┘
```

### Rule Ordering Best Practices

- **Place High-Volume Rules Near the Top**: Evaluate DNS (UDP 53) and HTTP/S rules early to minimize CPU overhead per packet traversal.
- **Avoid Shadow Rules**: Ensure broad rules (e.g., `Allow LAN to ANY`) do not precede specific restrictive rules (e.g., `Block LAN to Bad_IP`).
- **Use Object Groups**: Group IPs, subnets, ports, and domain names into named objects rather than creating duplicate individual rules.
- **Audit Hit-Counts Regularly**: Periodically review hit counters to identify zero-hit stale rules and remove obsolete access control entries.

---

## 4. Egress Filtering and Hardening

Egress filtering restricts outbound traffic originating from internal networks to prevent compromised endpoints from exfiltrating data, communicating with Command and Control (C2) servers, or launching outbound attacks.

### Mandatory Egress Controls

- **Block Outbound SMTP (TCP 25)**: Restrict direct TCP port 25 outbound to authorized email relays only.
- **Restrict Outbound DNS (UDP/TCP 53)**: Force internal hosts to resolve DNS through trusted internal resolvers; block direct outbound DNS to arbitrary public resolvers.
- **Filter Outbound SMB/RPC (TCP 135, 139, 445, UDP 137, 138)**: Strictly drop all SMB/NetBIOS traffic at the WAN boundary.
- **Strict Outbound ICMP Control**: Allow necessary ICMP types (Echo Request type 8, Time Exceeded type 11, Destination Unreachable type 3) while throttling rates.
