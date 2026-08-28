# IP Addressing Plan

## Motsweding Event Management

**Project:** CMPG325-2026-123  
**Client:** Motsweding Event Management  
**Prepared by:** Ofentse Seko  
**Address Block:** 10.48.0.0/16

---

## 1. Addressing Strategy

The network uses the private IPv4 addressing block:

`10.48.0.0/16`

The design uses separate `/24` networks for each major logical segment.

The third octet corresponds to the VLAN number wherever a VLAN is assigned.

For example:

`VLAN 20 → 10.48.20.0/24`

This convention makes the addressing structure predictable and easier to understand and troubleshoot.

Each `/24` provides:

**254 usable host addresses**

which provides significant capacity for future expansion.

---

## 2. VLAN and Subnet Allocation

| VLAN | Segment | Network | Subnet Mask | Default Gateway | Usable Hosts |
|---:|---|---|---|---|---:|
| 10 | Administration | 10.48.10.0/24 | 255.255.255.0 | 10.48.10.1 | 254 |
| 20 | Operations | 10.48.20.0/24 | 255.255.255.0 | 10.48.20.1 | 254 |
| 30 | Finance | 10.48.30.0/24 | 255.255.255.0 | 10.48.30.1 | 254 |
| 40 | IT / Technical | 10.48.40.0/24 | 255.255.255.0 | 10.48.40.1 | 254 |
| 50 | POS | 10.48.50.0/24 | 255.255.255.0 | 10.48.50.1 | 254 |
| 60 | Guest Wi-Fi | 10.48.60.0/24 | 255.255.255.0 | 10.48.60.1 | 254 |
| 70 | Server Infrastructure | 10.48.70.0/24 | 255.255.255.0 | 10.48.70.1 | 254 |

---

## 3. Default Gateway Convention

The first usable address in every subnet is reserved for the default gateway.

Therefore:

- VLAN 10 → `10.48.10.1`
- VLAN 20 → `10.48.20.1`
- VLAN 30 → `10.48.30.1`
- VLAN 40 → `10.48.40.1`
- VLAN 50 → `10.48.50.1`
- VLAN 60 → `10.48.60.1`
- VLAN 70 → `10.48.70.1`

This consistent convention simplifies configuration and troubleshooting.

---

## 4. Device Addressing

### Administration — VLAN 10

| Device | IP Address | Gateway |
|---|---|---|
| PC-ADMIN-01 | 10.48.10.10 | 10.48.10.1 |
| PC-ADMIN-02 | 10.48.10.11 | 10.48.10.1 |

### Operations — VLAN 20

| Device | IP Address | Gateway |
|---|---|---|
| PC-OPS-01 | 10.48.20.10 | 10.48.20.1 |
| PC-OPS-02 | 10.48.20.11 | 10.48.20.1 |

### Finance — VLAN 30

| Device | IP Address | Gateway |
|---|---|---|
| PC-FIN-01 | 10.48.30.10 | 10.48.30.1 |
| PC-FIN-02 | 10.48.30.11 | 10.48.30.1 |

### IT / Technical — VLAN 40

| Device | IP Address | Gateway |
|---|---|---|
| PC-IT-01 | 10.48.40.10 | 10.48.40.1 |
| PC-IT-02 | 10.48.40.11 | 10.48.40.1 |

### POS — VLAN 50

| Device | IP Address | Gateway |
|---|---|---|
| POS-01 | 10.48.50.10 | 10.48.50.1 |
| POS-02 | 10.48.50.11 | 10.48.50.1 |
| POS-03 | 10.48.50.12 | 10.48.50.1 |

### Guest Wi-Fi — VLAN 60

| Device | IP Address | Gateway |
|---|---|---|
| AP-GUEST | 10.48.60.10 | 10.48.60.1 |

Guest client devices may receive addresses dynamically through DHCP.

---

## 5. Server Infrastructure — VLAN 70

The server infrastructure is separated into:

**VLAN 70**

Network:

`10.48.70.0/24`

Default gateway:

`10.48.70.1`

| Server | IP Address | Gateway | Purpose |
|---|---|---|---|
| DHCP-SRV | 10.48.70.30 | 10.48.70.1 | DHCP Services |
| FILE-SRV | 10.48.70.31 | 10.48.70.1 | File Services |
| WEB-SRV | 10.48.70.32 | 10.48.70.1 | Web Services |

Server addresses are statically assigned to provide predictable addressing for infrastructure services.

---

## 6. Router-on-a-Stick Sub-Interfaces

The main office VLANs and server VLAN are transported using IEEE 802.1Q tagging.

| Sub-interface | VLAN | Gateway | Purpose |
|---|---:|---|---|
| G0/0/1.10 | 10 | 10.48.10.1/24 | Administration |
| G0/0/1.20 | 20 | 10.48.20.1/24 | Operations |
| G0/0/1.30 | 30 | 10.48.30.1/24 | Finance |
| G0/0/1.40 | 40 | 10.48.40.1/24 | IT / Technical |
| G0/0/1.60 | 60 | 10.48.60.1/24 | Guest Wi-Fi |
| G0/0/1.70 | 70 | 10.48.70.1/24 | Server Infrastructure |

The exact interface numbering will be confirmed against the selected Cisco Packet Tracer router model during implementation.

---

## 7. Physical Network Interfaces

| Router Interface | Connection | Purpose |
|---|---|---|
| Gig0/0/0 | Router-Edge | WAN / Internet |
| Gig0/0/1 | Core-Switch | 802.1Q trunk |
| Gig0/0/2 | Switch-POS | Dedicated POS path |

The Core-Switch then distributes the relevant VLANs to departmental switches and the Server-Switch.

---

## 8. Trunk VLANs

The main 802.1Q trunk carries:

- VLAN 10 — Administration
- VLAN 20 — Operations
- VLAN 30 — Finance
- VLAN 40 — IT / Technical
- VLAN 60 — Guest Wi-Fi
- VLAN 70 — Server Infrastructure

VLAN 50 is kept on the dedicated POS path.

---

## 9. Change Request CR1

Operations is the selected CR1 department.

Current network:

`10.48.20.0/24`

Usable range:

`10.48.20.1 – 10.48.20.254`

There are 254 usable host addresses.

Current Operations devices include:

- `10.48.20.10`
- `10.48.20.11`

The subnet therefore has substantial remaining capacity.

The eight additional staff members can be added using unused addresses in the existing subnet without:

- Creating a new VLAN
- Changing the subnet
- Changing the gateway
- Re-addressing existing users
- Rebuilding the routing architecture

---

## 10. Address Allocation Rules

The design follows these conventions:

- `.1` is reserved for the default gateway.
- Infrastructure addresses are statically assigned.
- Server addresses use predictable static addresses.
- End-user addressing may use DHCP where appropriate.
- Network addresses are not assigned to hosts.
- Broadcast addresses are not assigned to hosts.
- `/24` subnets provide 254 usable addresses.
- VLAN and subnet numbering follows the same third-octet convention.

---

## 11. Design Rationale

The addressing plan was deliberately designed for clarity and scalability.

Using the VLAN number in the third octet makes it immediately possible to identify the relationship between the logical VLAN and its IP subnet.

The `/24` allocation provides more capacity than is currently required but allows future users and devices to be added without repeatedly changing subnet boundaries.

This is particularly important for CR1 because the Operations department can absorb eight additional staff members without requiring a network redesign.

---

## 12. Implementation Status

**Milestone 1:** Addressing plan designed.

The addresses and interface mappings will be verified during Cisco Packet Tracer implementation.

Final testing will confirm:

- Gateway reachability
- Inter-VLAN routing
- DHCP operation
- Server connectivity
- POS connectivity
- CR1 expansion