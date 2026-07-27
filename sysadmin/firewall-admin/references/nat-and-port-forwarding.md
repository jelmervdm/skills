# Network Address Translation (NAT) and Port Forwarding

Detailed technical reference for Source NAT (SNAT), Destination NAT (DNAT), 1:1 Static NAT, Hairpin NAT (Reflection), and Application Layer Gateway (ALG) management.

---

## 1. Source NAT (SNAT) and Masquerade

Source Network Address Translation rewrites the IP packet header's source address as outbound traffic exits a network boundary. It enables hosts on private subnets (RFC 1918) to communicate across public networks.

### SNAT Types

| NAT Mechanism | Use Case | IP Address Mapping | Example Target |
| --- | --- | --- | --- |
| **Masquerade** | Dynamic WAN interface IP (DHCP/PPPoE) | Dynamic 1:N binding | `masquerade` |
| **Static SNAT** | Static WAN public IP pool | Static 1:N or N:N mapping | `to-source 203.0.113.10` |
| **IP Pool SNAT** | High-concurrency enterprise egress | Multi-IP round-robin pool | `to-source 203.0.113.10-203.0.113.20` |

### Source NAT Processing Flow

1. Packet originates from private client (`192.168.1.50:52100` -> `93.184.216.34:443`).
2. Firewall checks routing table and matches outbound SNAT rule on WAN interface.
3. Firewall assigns ephemeral source port and rewrites header (`203.0.113.10:41200` -> `93.184.216.34:443`).
4. Firewall updates NAT translation table entry.
5. Inbound reply (`93.184.216.34:443` -> `203.0.113.10:41200`) is matched in NAT table, translated back to `192.168.1.50:52100`, and forwarded to client.

---

## 2. Destination NAT (DNAT) and Port Forwarding

Destination NAT translates the destination IP and/or destination TCP/UDP port of incoming WAN traffic before forwarding it to an internal server in a DMZ or LAN.

### Key Components of a DNAT Rule

- **Original Inbound Service**: External Public IP address, incoming port (e.g., `203.0.113.10:8443`).
- **Translated Service**: Internal Private IP address, internal service port (e.g., `192.168.10.15:443`).
- **Associated Firewall Rule**: DNAT changes packet routing; an explicit firewall filter rule must still permit traffic to `192.168.10.15:443`.

### Example DNAT Configuration Logic

```text
Incoming WAN Packet: Source 198.51.100.55 -> Dest 203.0.113.10:443
                        │
                        ▼
            ┌──────────────────────┐
            │  DNAT Translation    │ (Rewrite Dest IP: 192.168.10.20:443)
            └───────────┬──────────┘
                        │
                        ▼
            ┌──────────────────────┐
            │ Firewall Filter Rule │ (Check WAN->DMZ rule: Allow 443 to 192.168.10.20)
            └───────────┬──────────┘
                        │
                        ▼
            Forwarded to Web Server (192.168.10.20:443)
```

---

## 3. Advanced NAT Architectures

### 1:1 Static NAT (Bi-Directional NAT)

Maps a dedicated public IPv4 address directly to an internal host address for both inbound and outbound traffic.

- **Inbound**: Traffic targeting `203.0.113.25` is rewritten to `172.16.1.100`.
- **Outbound**: Traffic originating from `172.16.1.100` exits WAN with source IP `203.0.113.25`.

### Hairpin NAT (NAT Reflection)

Enables internal LAN clients (`192.168.1.0/24`) to access an internal web server using the server's public IP address (`203.0.113.10`), without traffic failing or routing out to the Internet ISP.

- **Mechanism**: Firewall performs BOTH Destination NAT (rewriting destination from public IP to private server IP) AND Source NAT (rewriting source IP to gateway IP) so that server replies return through the firewall rather than directly across LAN.

---

## 4. Application Layer Gateways (ALG) Handling

Application Layer Gateways inspect application payload data (Layer 7) to dynamically open secondary firewall ports and rewrite embedded IP addresses inside control packets (e.g., SIP SDP, FTP PORT commands).

### Common ALG Pitfalls and Disabling Recommendations

- **SIP ALG**: Frequently corrupts VoIP SIP headers, breaks registration, and causes one-way audio. **Recommended Action**: Disable SIP ALG on commercial and enterprise firewalls; rely on STUN/TURN or VPN.
- **FTP ALG**: Rewrites `PORT` and `PASV` payload commands for active/passive FTP. **Recommended Action**: Restrict FTP to Passive Mode (PASV) over TLS/SFTP and use static port ranges.
- **H.323 / RTSP ALG**: Can cause significant CPU overhead and session dropouts. Disable unless legacy hardware requires it.
