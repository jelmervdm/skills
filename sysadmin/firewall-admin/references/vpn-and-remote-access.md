# VPN Architecture and Remote Access Security

Technical guide for configuring Site-to-Site IPsec VPNs, modern WireGuard tunnels, Remote Access SSL VPNs, and cryptographic security proposals.

---

## 1. Site-to-Site IPsec VPN Architecture

IPsec (Internet Protocol Security) provides encrypted, authenticated network-to-network connectivity across untrusted public networks using Phase 1 (IKE) and Phase 2 (ESP) negotiations.

### IPsec Phase 1 (IKE) vs Phase 2 (ESP)

```text
  Local Gateway                                          Remote Gateway
┌──────────────┐                                       ┌──────────────┐
│  Phase 1     │ ◄─── IKEv2 SA Negotiation (UDP 500) ───►│  Phase 1     │
│ (IKE SA)     │      Authentication, DH Key Exchange  │ (IKE SA)     │
├──────────────┤                                       ├──────────────┤
│  Phase 2     │ ◄─── ESP SA Negotiation (IP Proto 50) ──►│  Phase 2     │
│ (Child SA)   │      Bulk Subnet Data Encryption      │ (Child SA)   │
└──────────────┘                                       └──────────────┘
```

### Hardened Cryptographic Proposals

| Security Level | Phase 1 (IKEv2) Encryption & Integrity | DH Group | Phase 2 (ESP) Bulk Encryption | Perfect Forward Secrecy (PFS) |
| --- | --- | --- | --- | --- |
| **Enterprise Standard** | AES-256-GCM / SHA-256 | Group 14 (2048-bit) | AES-256-GCM | DH Group 14 |
| **High Security / Next-Gen** | AES-256-GCM / SHA-384 | Group 19 (ECP 256) / 21 | AES-256-GCM | DH Group 19 / 21 |
| **Deprecated / Insecure** | DES, 3DES, MD5, SHA-1 | Group 1, 2, 5 | DES, 3DES | Disabled |

### Route-Based (VTI) vs. Policy-Based IPsec

- **Route-Based IPsec (VTI - Virtual Tunnel Interface)**: Creates a logical interface (`vti0` or `ipsec0`). Traffic routing is controlled via standard routing tables (BGP, OSPF, static routes). Highly scalable and recommended for dynamic networks.
- **Policy-Based IPsec**: Encrypts traffic based on matched security association selectors (local subnet <-> remote subnet). Prone to Phase 2 SA mismatches when multiple subnets are added.

---

## 2. WireGuard Tunnel Configuration

WireGuard is an extremely fast, modern, and lean VPN protocol operating over UDP port 51820 using state-of-the-art cryptography (Noise protocol framework, Curve25519, ChaCha20-Poly1305, BLAKE2s).

### Example Interface Configuration (`/etc/wireguard/wg0.conf`)

```ini
[Interface]
Address = 10.200.1.1/24
PrivateKey = <Server_Private_Key>
ListenPort = 51820
PostUp = nft add rule inet filter input udp dport 51820 accept
PostDown = nft delete rule inet filter input udp dport 51820 accept

[Peer]
# Branch Office / Remote Client
PublicKey = <Remote_Client_Public_Key>
AllowedIPs = 10.200.1.2/32, 192.168.20.0/24
PersistentKeepalive = 25
```

### Key Parameters

- **`AllowedIPs`**: Acts as both a routing table target and a firewall filter. On reception, only packets with source IPs matching `AllowedIPs` are accepted. On transmission, packets targeting these IPs are routed into the tunnel.
- **`PersistentKeepalive = 25`**: Keeps NAT stateful sessions alive through NAT firewalls by sending empty packets every 25 seconds.

---

## 3. Remote Access SSL VPN

Remote Access VPNs enable mobile workers and remote endpoints to securely join internal corporate networks.

### Split-Tunneling vs. Full-Tunneling

```text
FULL TUNNELING                                SPLIT TUNNELING
┌──────────────┐                              ┌──────────────┐
│ Remote Host  │                              │ Remote Host  │
└──────┬───────┘                              └──────┬───────┘
       │ ALL Traffic                                 ├────────────────────────┐
       ▼ (Tunnel Encrypted)                          │ Internal Subnet Traffic │ Internet Traffic
┌──────────────┐                              ▼ (Tunnel Encrypted)     ▼ (Direct ISP)
│ Corporate FW │                       ┌──────────────┐         ┌─────────────┐
└──────┬───────┘                       │ Corporate FW │         │ Internet /  │
       ├──────────────┬──────────────┐ └──────────────┘         │ Public Web  │
       ▼              ▼              ▼                          └─────────────┘
      LAN            DMZ          Internet
```

- **Full Tunneling**: Directs ALL remote endpoint traffic through the corporate firewall. Ensures uniform security policy inspection, URL filtering, and IPS monitoring, but increases WAN bandwidth usage.
- **Split Tunneling**: Directs ONLY traffic bound for corporate subnets through the tunnel; internet traffic exits via the user's local ISP. Reduces corporate bandwidth requirements but bypasses corporate web filtering.

### Security Enforcements for Remote Access

1. **Multi-Factor Authentication (MFA)**: Enforce TOTP, Duo, or SAML SSO (Azure AD / Okta) for user authentication.
2. **Host Posture Assessment**: Validate OS patch level, active EDR/antivirus status, and disk encryption before authorizing network admission.
3. **Strict Client Subnet Isolation**: Assign SSL VPN users to a dedicated, isolated subnet with strict firewall rule access controls to LAN resources.
