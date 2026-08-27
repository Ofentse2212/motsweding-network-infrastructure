# IP Addressing Plan

## Motsweding Event Management

**Project:** CMPG325-2026-123  
**Client:** Motsweding Event Management  
**Prepared by:** Ofentse Seko  
**Address Block:** 10.48.0.0/16

---

## 1. Addressing Strategy

The network uses the private IPv4 address block `10.48.0.0/16`.

Each department is assigned a dedicated `/24` subnet. VLANs are used to separate departments into different broadcast domains while Router-on-a-Stick provides inter-VLAN routing.

The POS network is separated from the main office network using a dedicated physical router interface and dedicated POS switch.

A separate server network is also provided for shared infrastructure services.

---

## 2. VLAN and Subnet Allocation

| VLAN | Department / Purpose | Network Address | Subnet Mask | Default Gateway | Usable Host Range | Broadcast |
|---:|---|---|---|---|---|---|
| 10 | Administration | 10.48.10.0/24 | 255.255.255.0 | 10.48.10.1 | 10.48.10.2–10.48.10.254 | 10.48.10.255 |
| 20 | Operations / CR1 | 10.48.20.0/24 | 255.255.255.0 | 10.48.20.1 | 10.48.20.2–10.48.20.254 | 10.48.20.255 |
| 30 | Finance | 10.48.30.0/24 | 255.255.255.0 | 10.48.30.1 | 10.48.30.2–10.48.30.254 | 10.48.30.255 |
| 40 | IT / Technical | 10.48.40.0/24 | 255.255.255.0 | 10.48.40.1 | 10.48.40.2–10.48.40.254 | 10.48.40.255 |
| 50 | POS | 10.48.50.0/24 | 255.255.255.0 | 10.48.50.1 | 10.48.50.2–10.48.50.254 | 10.48.50.255 |
| 60 | Guest Wi-Fi | 10.48.60.0/24 | 255.255.255.0 | 10.48.60.1 | 10.48.60.2–10.48.60.254 | 10.48.60.255 |
| — | Server Network | 10.48.70.0/24 | 255.255.255.0 | 10.48.70.1 | 10.48.70.2–10.48.70.254 | 10.48.70.255 |

---

## 3. Device Addressing

### Administration — VLAN 10

| Device | IP Address | Default Gateway |
|---|---|---|
| PC-ADMIN-01 | 10.48.10.10 | 10.48.10.1 |
| PC-ADMIN-02 | 10.48.10.11 | 10.48.10.1 |

### Operations — VLAN 20

| Device | IP Address | Default Gateway |
|---|---|---|
| PC-OPS-01 | 10.48.20.10 | 10.48.20.1 |
| PC-OPS-02 | 10.48.20.11 | 10.48.20.1 |

**CR1 Capacity:**  
The `10.48.20.0/24` subnet provides 254 usable host addresses. This allows additional Operations staff to be added without redesigning the subnet.

### Finance — VLAN 30

| Device | IP Address | Default Gateway |
|---|---|---|
| PC-FIN-01 | 10.48.30.10 | 10.48.30.1 |
| PC-FIN-02 | 10.48.30.11 | 10.48.30.1 |

### IT / Technical — VLAN 40

| Device | IP Address | Default Gateway |
|---|---|---|
| PC-IT-01 | 10.48.40.10 | 10.48.40.1 |
| PC-IT-02 | 10.48.40.11 | 10.48.40.1 |

### POS — VLAN 50

| Device | IP Address | Default Gateway |
|---|---|---|
| POS-01 | 10.48.50.10 | 10.48.50.1 |
| POS-02 | 10.48.50.11 | 10.48.50.1 |
| POS-03 | 10.48.50.12 | 10.48.50.1 |

The POS devices operate within a dedicated VLAN and use a dedicated physical router interface.

### Guest Wi-Fi — VLAN 60

| Device | IP Address | Default Gateway |
|---|---|---|
| AP-GUEST | 10.48.60.10 | 10.48.60.1 |

Guest client addresses may be assigned dynamically using DHCP.

---

## 4. Server Network

The server infrastructure uses a dedicated network:

**Network:** `10.48.70.0/24`  
**Default Gateway:** `10.48.70.1`

| Server | IP Address | Default Gateway | Purpose |
|---|---|---|---|
| DHCP-SRV | 10.48.70.30 | 10.48.70.1 | DHCP Services |
| FILE-SRV | 10.48.70.31 | 10.48.70.1 | File Services |
| WEB-SRV | 10.48.70.32 | 10.48.70.1 | Web Services |

Server addresses are statically assigned so that infrastructure services remain reachable at predictable addresses.

---

## 5. Router Interface Allocation

| Router Interface | Connection | Purpose |
|---|---|---|
| Gig0/0/0 | Router-Edge | WAN / Internet connection |
| Gig0/0/1 | Switch-Office | 802.1Q trunk for VLANs 10, 20, 30, 40 and 60 |
| Gig0/0/2 | Switch-POS | Dedicated POS network connection |
| Gig0/0/3 | Server-Switch | Server network connection |

---

## 6. Router-on-a-Stick Gateway Mapping

The following logical subinterfaces will provide default gateways for the office VLANs:

| Subinterface | VLAN | Gateway |
|---|---:|---|
| Gig0/0/1.10 | 10 | 10.48.10.1 |
| Gig0/0/1.20 | 20 | 10.48.20.1 |
| Gig0/0/1.30 | 30 | 10.48.30.1 |
| Gig0/0/1.40 | 40 | 10.48.40.1 |
| Gig0/0/1.60 | 60 | 10.48.60.1 |

VLAN 50 uses the dedicated physical router interface rather than the office 802.1Q trunk.

---

## 7. Address Allocation Rules

The following conventions are used:

- `.1` is reserved for the default gateway.
- `.10–.99` is used for assigned end devices and infrastructure where appropriate.
- Server infrastructure uses `.30` onward within the server network.
- DHCP address pools will use a separate range to avoid conflicts with statically assigned infrastructure addresses.
- Network and broadcast addresses are not assigned to hosts.
- The `/24` subnet size provides 254 usable host addresses per network.

---

## 8. Scalability and Change Request CR1

The Operations department is assigned `10.48.20.0/24`.

This provides 254 usable host addresses:

`10.48.20.1–10.48.20.254`

The default gateway is:

`10.48.20.1`

Current Operations devices use:

- `10.48.20.10`
- `10.48.20.11`

The remaining address capacity allows the requested additional staff to be accommodated without changing the subnet or rebuilding the network.

---

## 9. Design Notes

The addressing plan supports the network's segmentation and resilience requirements:

1. Departments operate in separate VLANs and IP subnets.
2. Router-on-a-Stick provides inter-VLAN routing for the office VLANs.
3. POS devices are isolated in VLAN 50.
4. POS traffic uses a dedicated physical router interface and POS switch.
5. Server infrastructure is placed on a separate server network.
6. The `/24` subnet allocation provides sufficient capacity for future growth.
7. The addressing scheme follows a consistent and predictable numbering convention.

---

**Document Status:** Initial IP Addressing Plan  
**Project:** CMPG325-2026-123  
**Author:** Ofentse Seko