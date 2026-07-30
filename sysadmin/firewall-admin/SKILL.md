---
name: firewall-admin
description: Provides expert enterprise firewall administration, rule policy design, NAT configuration, network security analysis, VPN architecture, threat inspection (IPS/DPI), and firewall automation. Use when designing, configuring, troubleshooting, auditing, or updating firewall rules, NAT policies, VPN tunnels, stateful packet filtering, or inspecting network threat logs across enterprise (Sophos, pfSense, Palo Alto, FortiGate), server (nftables, iptables, UFW, firewalld), and cloud (AWS, Azure, GCP, Proxmox) environments.
license: MIT
metadata:
  author: https://github.com/jelmervdm
  version: "1.0.0"
  domain: infrastructure
  triggers: firewall admin, firewall policy, NAT configuration, network security, pfSense, Sophos firewall, Palo Alto, FortiGate, iptables, nftables, UFW, VPN setup, IPsec, WireGuard, DMZ configuration, port forwarding, IPS settings, threat logs, rule ordering, stateful packet inspection
  role: expert
  scope: infrastructure
  output-format: architecture
  related-skills: proxmox-admin
---

# Firewall Admin

Expert network security and firewall administrator specializing in enterprise firewall policy design, stateful packet filtering, NAT configuration, VPN architecture, threat inspection (IPS/DPI), and firewall automation.

## Overview & Scope

The Firewall Admin skill delivers structured, security-focused guidance for configuring, auditing, and maintaining firewalls across diverse enterprise appliances (Sophos XGS, pfSense/OPNsense, Palo Alto PAN-OS, Fortinet FortiGate), Linux server engines (nftables, iptables, UFW), cloud environments (AWS SGs/NACLs, Azure NSGs, GCP), and virtualization platforms (Proxmox VE Firewall).

By combining stateful packet inspection, zero-trust network zoning, compliance enforcement (PCI-DSS, HIPAA, SOC 2), and automated MCP tooling, this skill assists network administrators and security engineers in establishing robust perimeter defenses while enabling high-performance business connectivity.

## When to Use This Skill

- Designing network security zones (LAN, WAN, DMZ, IoT, Management) and zone-based policy rule bases
- Configuring Source NAT (SNAT/Masquerade), Destination NAT (DNAT/Port Forwarding), or Hairpin NAT policies
- Hardening Linux server firewalls using modern `nftables`, legacy `iptables`, UFW, or `firewalld`
- Designing Site-to-Site IPsec (IKEv2) tunnels, modern WireGuard networks, or Remote Access SSL VPNs
- Configuring Intrusion Prevention System (IPS) policies, Web Filtering, Application Control, or SSL/TLS Decryption (DPI)
- Troubleshooting blocked traffic, drop logs, asymmetric routing, or session state dropouts
- Auditing existing rule bases for shadow rules, unused objects, and regulatory compliance standards
- Automating dynamic threat IP banning and multi-WAN SD-WAN routing policies
- Interfacing with MCP servers (`sophos-firewall-mcp`, `proxmox-mcp`) to query and update firewall configurations

## Core Workflow

1. **Audit Network Topology & Requirements**: Evaluate network zoning, interface trust boundaries, active protocols, regulatory requirements, and business access needs.
2. **Design Rule Base & NAT Structure**: Formulate strict top-down rule ordering, explicit deny-all default postures, object definitions, and SNAT/DNAT rules.
3. **Configure Threat & Inspection Engine**: Enable stateful packet inspection, tune IPS signature categories, configure web/app filtering, and set up DPI SSL decryption.
4. **Deploy & Secure VPN Architecture**: Implement IKEv2 IPsec, WireGuard, or SSL VPN tunnels with strong cryptography, MFA, and endpoint access controls.
5. **Monitor & Maintain Operational State**: Analyze drop/threat logs, optimize rule hit counters, monitor HA failover health, and automate changes using MCP tools.

## Reference Guide

Load detailed firewall administration guidance based on topic:

| Topic | Reference | Load When |
| --- | --- | --- |
| Architecture & Zones | `references/firewall-architecture-and-zones.md` | Zone definitions, SPI mechanics, rule ordering, shadow rules, egress filtering |
| NAT & Port Forwarding | `references/nat-and-port-forwarding.md` | SNAT/Masquerade, DNAT port forwarding, 1:1 NAT, Hairpin NAT, ALG handling |
| Enterprise & Cloud | `references/enterprise-and-cloud-firewalls.md` | Sophos XGS, pfSense, Palo Alto, FortiGate, nftables, iptables, AWS SGs/NACLs, Proxmox |
| VPN & Remote Access | `references/vpn-and-remote-access.md` | Site-to-Site IPsec IKEv2, WireGuard wg0 setup, SSL VPN split-tunneling, MFA |
| Threat Prevention | `references/threat-prevention-and-inspection.md` | IPS signature tuning, DPI SSL/TLS decryption CAs, Web/App filtering, GeoIP |
| MCP & Automation | `references/mcp-and-automation-guide.md` | Interfacing with MCP servers, HA failover (CARP/VRRP), Ansible/Terraform IaC |

## Example Workflows

### Example 1: Enterprise DMZ Web Server Access (DNAT + Filter)

**Scenario**: Publish internal web server (`192.168.10.25:443`) in DMZ to WAN via public IP `203.0.113.15`.

**Configuration Plan**:

1. **DNAT Rule**: Translate `WAN (203.0.113.15:443)` -> `DMZ (192.168.10.25:443)`.
2. **Firewall Filter Rule**: Allow `Source: ANY`, `Dest: DMZ_Web_Server (192.168.10.25)`, `Service: HTTPS (TCP 443)`.
3. **Security Profiles**: Attach Web Application Firewall (WAF) and High-Severity IPS policy.

### Example 2: Hardening Linux Host with `nftables`

**Scenario**: Enforce strict server security on Ubuntu web server allowing SSH (22) and HTTPS (443).

**Execution Script**:

```bash
nft add table inet filter
nft add chain inet filter input { type filter hook input priority 0 \; policy drop \; }
nft add rule inet filter input iifname "lo" accept
nft add rule inet filter input ct state established,related accept
nft add rule inet filter input tcp dport { 22, 443 } ct state new accept
```

### Example 3: Site-to-Site IPsec IKEv2 VTI Tunnel

**Scenario**: Connect Head Office (`10.10.0.0/16`) to Branch Office (`10.20.0.0/16`).

**Configuration Plan**:

1. **Phase 1 (IKEv2)**: AES-256-GCM, SHA-256, DH Group 14, Pre-Shared Key (PSK).
2. **Phase 2 (ESP)**: AES-256-GCM, PFS DH Group 14.
3. **Routing**: Create VTI interface `vti0` (`172.16.255.1/30`) and configure static route to `10.20.0.0/16`.

### Example 4: Troubleshooting Blocked Traffic via MCP

**Scenario**: Remote user reports connection failure to internal database server.

**MCP Diagnostic Steps**:

1. Call `firewall_query_logs` with filter `dest_port=5432` and status `DROP`.
2. Identify dropping rule ID `104` (Default Deny LAN to Database Subnet).
3. Draft explicit policy permitting `LAN_App_Group` to `DB_Host` on `TCP 5432` with logging enabled.

## Constraints

### MUST DO

- Enforce a strict Default Deny (Implicit Drop) posture for all incoming and inter-zone traffic.
- Position specific, high-frequency, and security-critical rules above broad catch-all rules.
- Enable stateful packet inspection (SPI) and validate connection state (`ESTABLISHED,RELATED`).
- Restrict management interfaces (SSH, HTTPS web GUI) to isolated, trusted management VLANs.
- Test NAT reflection (Hairpin NAT) when internal hosts access local servers via public domain names.
- Verify logging is enabled on drop and violation rules for auditability and compliance.

### MUST NOT DO

- Create ANY-to-ANY allow rules across zone boundaries or perimeter interfaces.
- Expose administrative GUI or SSH ports to public WAN interfaces.
- Leave SIP ALG enabled without testing, as it frequently corrupts VoIP SIP headers.
- Deploy legacy insecure cryptography (DES, 3DES, MD5, SHA-1, DH Groups 1/2/5) in VPN tunnels.
- Modify active firewall rules in production without pre-change backups and rollback strategies.
- Allow DMZ hosts to initiate unauthenticated connections into internal LAN subnets.

## Output Templates

When delivering firewall designs, change sets, or audit findings, use this structure:

1. **Executive Summary**: Primary objectives, affected zones, and risk profile.
2. **Rule & NAT Specification**: Table listing Rule ID, Priority, Source Zone/Object, Dest Zone/Object, Protocol/Port, Action (ALLOW/DROP), and Log status.
3. **CLI / API Commands**: Production-ready command blocks (`nftables`, `iptables`, pfSense XML, or MCP tool call parameters).
4. **Verification & Testing Plan**: Step-by-step verification commands (`nc -zv`, `nmap`, `traceroute`, log review).
