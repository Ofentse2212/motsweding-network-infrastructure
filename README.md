# Motsweding Event Management — Network Infrastructure

Enterprise network infrastructure design and Cisco Packet Tracer simulation for **Motsweding Event Management, Potchefstroom**.

The project focuses on designing a scalable, segmented, and resilient enterprise network using VLANs, inter-VLAN routing, structured IPv4 addressing, and dedicated POS connectivity.

---

## Project Overview

Motsweding Event Management requires a network infrastructure that can support multiple departments while maintaining network segmentation, scalability, and reliable Point-of-Sale (POS) operations.

The network design includes:

- VLAN-based departmental segmentation
- Router-on-a-Stick inter-VLAN routing
- Structured IPv4 addressing using `10.48.0.0/16`
- Dedicated POS network connectivity
- Guest Wi-Fi segmentation
- Server infrastructure
- Scalable addressing to accommodate future staff
- Cisco Packet Tracer implementation and testing

---

## Network Architecture

The proposed network is divided into separate logical network segments:

| VLAN | Department / Purpose | Network |
|------|----------------------|---------|
| VLAN 10 | Administration | 10.48.10.0/24 |
| VLAN 20 | Operations | 10.48.20.0/24 |
| VLAN 30 | Finance | 10.48.30.0/24 |
| VLAN 40 | IT / Technical | 10.48.40.0/24 |
| VLAN 50 | POS | 10.48.50.0/24 |
| VLAN 60 | Guest Wi-Fi | 10.48.60.0/24 |
| VLAN 70 | Server Infrastructure | 10.48.70.0/24 |

The network uses **Router-on-a-Stick** to provide inter-VLAN routing for the office VLANs.

The POS network uses a dedicated physical connection to maintain POS availability independently from the main office trunk path.

---

## Key Design Features

### VLAN Segmentation

Departments are separated into individual VLANs to create distinct broadcast domains and improve network organisation and security.

### Router-on-a-Stick

The core router provides inter-VLAN routing through an IEEE 802.1Q trunk connection to the office switch.

### POS Network Resilience

The POS environment is separated from the main office network through a dedicated physical connection.

This design supports the requirement that POS systems remain operational if the main office LAN or trunk connection fails.

### Scalability

The IP addressing structure uses `/24` subnets, providing sufficient host capacity for current devices and future expansion.

---

## Network Services

The network design includes dedicated server infrastructure for:

- DHCP services
- File services
- Web services

The server infrastructure is connected through a dedicated server switch.

---

## Technologies

- Cisco Packet Tracer
- IPv4
- VLANs
- IEEE 802.1Q
- Router-on-a-Stick
- Ethernet Switching
- Git
- GitHub

---

## Project Documentation

Detailed project documentation is maintained in the `docs/` directory.

- [Client Requirements](docs/client-requirements.md)
- [IP Addressing Plan](docs/ip-addressing-plan.md)
- [Logical Network Topology](docs/logical-topology.png)
- [Physical Network Topology](docs/physical-topology.png)

---

## Project Structure

```text
motsweding-network-infrastructure/
│
├── README.md
│
├── docs/
│   ├── client-requirements.md
│   ├── ip-addressing-plan.md
│   ├── logical-topology.png
│   └── physical-topology.png
│
└── packet-tracer/
    └── ...
