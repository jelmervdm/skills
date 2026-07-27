# Threat Prevention and Deep Packet Inspection

Technical reference for configuring Intrusion Prevention Systems (IPS), SSL/TLS Decryption (DPI), Web Filtering, Application Control, and GeoIP Threat Protection.

---

## 1. Intrusion Prevention System (IPS) Engine

IPS engines inspect packet payloads in real-time against threat signatures and protocol anomaly detection heuristics to identify and block exploits, shellcode, remote code execution (RCE), and malicious scans.

### Signature Categories and Action Policies

| Signature Category | Threat Severity | Recommended Policy Action | Examples |
| --- | --- | --- | --- |
| **Critical / High** | High Risk RCE, Buffer Overflows | **Drop / Block Packet** | Log4Shell, EternalBlue (MS17-010), Apache Struts |
| **Medium** | Known Malware C2, Port Scans | **Drop & Alert** | Nmap SYN scans, Cobalt Strike beacons |
| **Low / Info** | Protocol Anomaly, Non-standard Headers | **Alert Only / Allow** | Non-standard HTTP headers, TCP window anomalies |

### Tuning IPS to Prevent False Positives

1. **Baseline Phase**: Run new IPS rulesets in **Audit / Alert Only** mode for 7–14 days to identify benign traffic triggers.
2. **Exclusion Customization**: Disable or bypass specific signature IDs for internal legacy applications that trigger false alarms.
3. **Performance Optimization**: Apply IPS policies only to relevant zone traffic (e.g., disable database signatures on LAN-to-WAN web browsing policies).

---

## 2. SSL/TLS Decryption (Deep Packet Inspection - DPI)

Over 90% of web traffic is encrypted with TLS. Threat actors frequently conceal malware downloads, C2 channels, and data exfiltration within HTTPS sessions. DPI decrypts, inspects, and re-encrypts HTTPS traffic.

### DPI Architecture and Trust Chain

```text
  Client Workstation                    Firewall DPI Engine                   External Web Server
┌──────────────────┐                   ┌────────────────────┐                ┌──────────────────┐
│  Browser Request │ ─── HTTPS Port 443 ──►│ Decrypt & Inspect  │ ─── HTTPS 443 ──►│ Destination Server│
│                  │                   ├────────────────────┤                │ (e.g., GitHub)   │
│ Validates CA Cert│ ◄── Re-encrypted ────│ Re-sign with Local │ ◄── Server Cert──│ Validates Server │
│ from Root Store  │     Subordinate CA│ Subordinate CA Cert│     from Target    │ TLS Session      │
└──────────────────┘                   └────────────────────┘                └──────────────────┘
```

### Critical SSL/TLS Decryption Rules

- **Deploy Subordinate Certificate Authority (CA)**: Export the firewall's internal CA root certificate and distribute it to all managed endpoints via Active Directory Group Policy (GPO), MDM, or configuration scripts.
- **Mandatory Decryption Bypass List**: NEVER decrypt privacy-sensitive categories:
  - Financial & Banking Institutions (`finance.yahoo.com`, `chase.com`, online banking)
  - Healthcare & Medical Services (`mychart`, medical portals)
  - Personal Communication & Government Portals
  - Hardcoded Certificate Pinning Applications (e.g., Apple Update, Microsoft Teams, Adobe CC)

---

## 3. Web Filtering, App Control, and GeoIP Blocking

### Web & Category Filtering

- **Block High-Risk Categories**: Malicious Sites, Phishing, Command and Control, Cryptomining, Tor Exit Nodes, Darknet.
- **Quarantine Unrated / Newly Registered Domains (NRDs)**: Domains registered within the last 30 days statistically carry an extremely high threat weight. Throttling or blocking NRD access stops zero-day phishing campaigns.

### Application Control (Layer 7 Filtering)

Application Control identifies software applications (e.g., BitTorrent, Tor Browser, TeamViewer, SSH over non-standard port 443) regardless of the port, protocol, or encryption used.

### GeoIP and Threat Intelligence Filtering

- **GeoIP Blocking**: Restrict inbound WAN connection attempts from countries where your organization has no operational footprint.
- **Dynamic IP Reputation Feeds**: Subscribe firewall engines to automated threat intelligence feeds (e.g., Spamhaus EDROP, Abuse.ch, AlienVault OTX) to drop known malicious IP sets automatically.
