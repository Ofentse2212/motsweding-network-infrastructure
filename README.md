# Motsweding Event Management — Network Infrastructure

Enterprise network infrastructure design and Cisco Packet Tracer simulation for **Motsweding Event Management, Potchefstroom**.

The project focuses on designing a scalable, segmented, and resilient enterprise network using VLANs, Router-on-a-Stick inter-VLAN routing, structured IPv4 addressing, dedicated POS connectivity, guest Wi-Fi, and supporting server infrastructure.

---

## Project Information

| Item | Details |
|---|---|
| Organisation | Motsweding Event Management |
| Location | Potchefstroom |
| Industry | Entertainment |
| Project ID | CMPG325-2026-123 |
| Client ID | CLI-123 |
| Student | Ofentse Seko |
| Assigned Challenge | Router-on-a-Stick |
| Addressing Block | 10.48.0.0/16 |

---

## Project Overview

Motsweding Event Management requires a network infrastructure capable of supporting different organisational functions while maintaining appropriate segmentation, scalability, connectivity, and reliable Point-of-Sale (POS) operations.

The proposed design separates organisational functions into VLANs and IP subnets. Router-on-a-Stick is used to provide inter-VLAN routing for the main office network.

The design also introduces supporting infrastructure, including a dedicated server network and Guest Wi-Fi network, to provide a more realistic enterprise environment while remaining aligned with the requirements of the project brief.

---

## Client Requirements

The design addresses the following core requirements:

- Use the assigned `10.48.0.0/16` IPv4 addressing block.
- Implement the network using Cisco Packet Tracer.
- Provide appropriate connectivity and network services.
- Implement and demonstrate Router-on-a-Stick.
- Keep POS systems operational if the main office LAN fails.
- Accommodate eight additional staff members without redesigning the network.
- Produce a working and testable network implementation.
- Maintain professional documentation and evidence in GitHub.

The detailed requirements are documented in:

**[Client Requirements](docs/client-requirements.md)**

---

## Network Architecture

The proposed network is divided into the following logical segments:

| VLAN | Segment | Network |
|---:|---|---|
| 10 | Administration | 10.48.10.0/24 |
| 20 | Operations | 10.48.20.0/24 |
| 30 | Finance | 10.48.30.0/24 |
| 40 | IT / Technical | 10.48.40.0/24 |
| 50 | POS | 10.48.50.0/24 |
| 60 | Guest Wi-Fi | 10.48.60.0/24 |
| 70 | Server Infrastructure | 10.48.70.0/24 |

The third octet intentionally corresponds to the VLAN number. For example:

`VLAN 20 → 10.48.20.0/24`

This makes the addressing scheme easier to understand, implement, and troubleshoot.

---

## Network Architecture Components

### Core Routing

A Cisco 2911 Router-Core provides the central routing function.

Router-on-a-Stick is implemented using a trunk-facing router interface and VLAN-specific sub-interfaces for the main office VLANs.

### Core Switching

A central Core-Switch aggregates the departmental access switches and supporting network segments.

The departmental switches extend connectivity to end devices within their respective VLANs.

### Departmental Segmentation

Separate VLANs are used for:

- Administration
- Operations
- Finance
- IT / Technical
- Guest Wi-Fi

This creates separate broadcast domains and provides a structured foundation for network management and security.

### POS Network

POS systems are placed in VLAN 50 and connected through a dedicated physical network path.

This architecture addresses the requirement that POS systems must remain operational if the main office LAN or its trunk path becomes unavailable.

### Server Infrastructure

VLAN 70 is dedicated to server infrastructure.

The server network contains:

- DHCP-SRV
- FILE-SRV
- WEB-SRV

The servers are connected through a dedicated Server-Switch.

### Guest Wi-Fi

Guest Wi-Fi is isolated in VLAN 60 and is represented by the AP-GUEST access point.

This prevents guest devices from being placed directly into an internal departmental network.

---

## IP Addressing

The project uses the assigned:

`10.48.0.0/16`

Each major network segment is allocated a `/24` subnet, providing:

**254 usable host addresses per subnet.**

The `/24` allocation provides substantial spare capacity for future expansion.

The Operations network, VLAN 20, is the target of Change Request CR1 and therefore has sufficient unused address capacity to accommodate eight additional staff members without changing the subnet or gateway.

The complete addressing plan is documented in:

**[IP Addressing Plan](docs/ip-addressing-plan.md)**

---

## Router-on-a-Stick

Router-on-a-Stick is the assigned technical challenge for the project.

The office VLANs are carried over an IEEE 802.1Q trunk between the Router-Core and the Core-Switch.

The router uses VLAN-specific sub-interfaces to provide default gateways and inter-VLAN routing.

The planned office VLAN sub-interfaces are:

| Sub-interface | VLAN | Gateway |
|---|---:|---|
| G0/0/1.10 | 10 | 10.48.10.1 |
| G0/0/1.20 | 20 | 10.48.20.1 |
| G0/0/1.30 | 30 | 10.48.30.1 |
| G0/0/1.40 | 40 | 10.48.40.1 |
| G0/0/1.60 | 60 | 10.48.60.1 |
| G0/0/1.70 | 70 | 10.48.70.1 |

The exact interface numbering will be verified against the selected Packet Tracer router model during implementation.

---

## Design Decisions

The network design was developed from the client requirements and then extended with supporting infrastructure where this improves the realism and completeness of the proposed enterprise network.

Important design decisions include:

- Using VLANs to separate organisational functions.
- Introducing departmental access switches beneath the Core-Switch.
- Allocating VLAN 70 to server infrastructure.
- Providing a dedicated Server-Switch.
- Separating Guest Wi-Fi into VLAN 60.
- Providing a dedicated POS network path.
- Using `/24` networks to provide substantial expansion capacity.
- Using a consistent relationship between VLAN numbers and subnet third octets.

Detailed design reasoning is documented in:

**[Design Decisions](docs/design-decisions.md)**

---

## Topology Documentation

### Physical Topology

The physical topology represents actual network devices, connections, interfaces, switch ports, servers, access points, and the physical network paths.

**[View Physical Topology](docs/physical-topology.svg)**

### Logical Topology

The logical topology represents VLANs, broadcast domains, IP networks, routing relationships, and logical segmentation rather than physical device placement.

**[View Logical Topology](docs/logical-topology.svg)**

---

## Repository Structure

```text
motsweding-network-infrastructure/
│
├── README.md
│
├── docs/
│   ├── client-requirements.md
│   ├── design-decisions.md
│   ├── ip-addressing-plan.md
│   ├── logical-topology.svg
│   └── physical-topology.svg
│
├── packet-tracer/
│   └── [Packet Tracer implementation]
│
├── configs/
│   └── [configuration evidence]
│
└── testing/
    └── [testing evidence]