# Software-Defined Networking (SDN) and Network Architecture

Technical guide to Proxmox VE 9.x Software-Defined Networking (SDN), SDN Fabrics, EVPN/VXLAN overlay networks, Linux bridges, and bond interfaces.

---

## 1. Network Interfaces and Linux Bridging

Proxmox VE uses `ifupdown2` for network configuration, allowing live reloads (`ifreload -a`) without rebooting host nodes.

### Core Interface Definitions

- **Physical Interfaces (`eno1`, `eth0`)**: Bare-metal network interface cards.
- **Bonds (`bond0`)**: Aggregates multiple physical NICs for high availability and throughput (LACP Mode 4 / 802.3ad).
- **Bridges (`vmbr0`)**: Virtual Layer 2 software switches connecting guest VMs/LXCs to physical host networks.
- **VLAN Interfaces (`vmbr0.100` / VLAN-aware bridge)**: Tagged 802.1Q sub-interfaces for traffic isolation.

### Production Network Configuration (`/etc/network/interfaces`)

```text
auto lo
iface lo inet loopback

iface eno1 inet manual
iface eno2 inet manual

# LACP Link Aggregation (Mode 4)
auto bond0
iface bond0 inet manual
  bond-slaves eno1 eno2
  bond-miimon 100
  bond-mode 802.3ad
  bond-xmit-hash-policy layer2+3

# Management & VM Bridge (VLAN Aware)
auto vmbr0
iface vmbr0 inet static
  address 10.10.10.15/24
  gateway 10.10.10.1
  bridge-ports bond0
  bridge-stp off
  bridge-fd 0
  bridge-vlan-aware yes
  bridge-vids 10 20 30 100
```

---

## 2. Software-Defined Networking (SDN) Stack

Proxmox VE 9.x SDN abstracts complex multi-tenant cloud networking into managed logical entities: Zones, VNets, Subnets, and Fabrics.

```text
┌─────────────────────────────────────────────────────────────┐
│ SDN Zones (EVPN / VXLAN / Simple / VLAN / QinQ / Fabrics)   │
├─────────────────────────────────────────────────────────────┤
│ VNets (Virtual Layer 2 Networks - e.g. vnet10, vnet20)      │
├─────────────────────────────────────────────────────────────┤
│ Subnets (IP Allocation / IPAM / DHCP / Anycast Gateways)   │
└─────────────────────────────────────────────────────────────┘
```

### SDN Zone Types

| Zone Type | Encapsulation | Scalability | Primary Use Case |
| --- | --- | --- | --- |
| **Simple** | Isolated local bridges | Single Host | Development / isolated test environments |
| **VLAN** | IEEE 802.1Q Tagging | Up to 4094 VLANs | Traditional hardware switch integrated VLANs |
| **QinQ** | Stacked 802.1ad (Double VLAN) | Multi-tenant VLANs | Service provider client isolation |
| **VXLAN** | UDP Port 4789 Tunneling | 16 Million VNIs | Layer 2 extension across Layer 3 networks |
| **EVPN** | BGP Control Plane + VXLAN | Enterprise Multi-site | High-scale Datacenter multitenancy & live migration |

---

## 3. Proxmox VE 9 SDN "Fabrics"

PVE 9 introduces **SDN Fabrics**, automated mesh/spine-leaf network topology configurations built on FRRouting (FRR) BGP/EVPN or OpenFabric/ISIS.

### Benefits of SDN Fabrics

- **Automated Topology Discovery**: Automatically configures routing daemons across hypervisor nodes without manual per-node BGP neighbor statements.
- **Optimized VM Live Migration**: Allows virtual machines to migrate between nodes across routed Layer 3 network boundaries while preserving their IP address and active TCP sessions.
- **Anycast Gateway Routing**: Hosts the default gateway IP on all hypervisors simultaneously, enabling local egress routing and eliminating hairpining.

```bash
# Apply SDN configuration changes cluster-wide via CLI
pvesdn reload
```

---

## 4. Network MTU and Jumbo Frames

When deploying VXLAN or Ceph, jumbo frames ($MTU = 9000$) MUST be configured on all physical switches, bond interfaces, and bridge interfaces to account for frame encapsulation overhead ($50\text{ bytes}$ for VXLAN).

- **Physical NIC / Bond MTU**: `9000`
- **VNet / VM Guest MTU**: `8950` (or `1500` if MSS clamping is enabled)
