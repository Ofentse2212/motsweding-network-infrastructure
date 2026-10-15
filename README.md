# Motsweding Event Management — Network Infrastructure

Enterprise network infrastructure design, implementation, and testing using **Cisco Packet Tracer** for **Motsweding Event Management, Potchefstroom**.

This project implements a segmented enterprise network using VLANs, Router-on-a-Stick inter-VLAN routing, structured IPv4 addressing, dedicated Point-of-Sale (POS) connectivity, guest Wi-Fi, and supporting server infrastructure. It also documents network testing, change requests, troubleshooting, and POS resilience.

---

## Project Information

| Item | Details |
|---|---|
| Organisation | Motsweding Event Management |
| Location | Potchefstroom, South Africa |
| Industry | Entertainment |
| Project ID | CMPG325-2026-123 |
| Client ID | CLI-123 |
| Student | Ofentse Seko |
| Assigned Challenge | Router-on-a-Stick |
| Addressing Block | `10.48.0.0/16` |
| Simulation Platform | Cisco Packet Tracer |

---

## Project Overview

Motsweding Event Management requires a network infrastructure that supports its organisational functions while providing appropriate network segmentation, connectivity, scalability, and reliable POS operations.

The network separates departmental devices, guest access, POS systems, and servers into distinct IP networks. Router-on-a-Stick provides inter-VLAN routing for the office network, while a dedicated routed connection separates POS connectivity from the main office trunk.

The project also addresses the addition of eight Operations staff members through Change Request CR1 and evaluates network behaviour during the failure of the office trunk through Change Request CR2.

The implementation and its verification are documented through the project report, Packet Tracer simulation, configuration evidence, and network testing results.

---

## Client Requirements

The network design and implementation address the following requirements:

- Use the assigned `10.48.0.0/16` IPv4 addressing block.
- Implement and demonstrate the network using Cisco Packet Tracer.
- Provide appropriate connectivity between authorised network segments.
- Implement Router-on-a-Stick inter-VLAN routing.
- Support DHCP, DNS, web services, and file-sharing requirements.
- Keep POS systems operational if the main office LAN or its trunk path fails.
- Accommodate eight additional Operations staff members without redesigning the network.
- Provide supporting infrastructure for guest Wi-Fi and internal servers.
- Maintain professional documentation, testing evidence, and project files in GitHub.

See [Client Requirements](docs/client-requirements.md) for the detailed requirements.

---

## Network Architecture

The network is divided into seven logical segments.

| VLAN | Segment | Network | Default Gateway |
|---:|---|---|---|
| 10 | Administration | `10.48.10.0/24` | `10.48.10.1` |
| 20 | Operations | `10.48.20.0/24` | `10.48.20.1` |
| 30 | Finance | `10.48.30.0/24` | `10.48.30.1` |
| 40 | IT / Technical | `10.48.40.0/24` | `10.48.40.1` |
| 50 | POS | `10.48.50.0/24` | `10.48.50.1` |
| 60 | Guest Wi-Fi | `10.48.60.0/24` | `10.48.60.1` |
| 70 | Server Infrastructure | `10.48.70.0/24` | `10.48.70.1` |

The third octet corresponds to the VLAN number. For example, VLAN 20 uses `10.48.20.0/24`. This consistent addressing scheme makes the network easier to understand, manage, and troubleshoot.

Each `/24` subnet provides 254 usable host addresses, leaving room for future expansion.

---

## Core Network Components

### Router-Core

The Cisco 2911 Router-Core provides the central routing function for the office network.

Router-on-a-Stick is implemented using an IEEE 802.1Q trunk and VLAN-specific subinterfaces. These subinterfaces provide default gateways and enable inter-VLAN routing.

The documented interfaces include:

- `GigabitEthernet0/0` — routed connection to Router-Edge.
- `GigabitEthernet0/1` — office network trunk.
- `GigabitEthernet0/2` — dedicated routed POS connection.

Confirm interface names against the saved Packet Tracer topology and device configuration before using them as configuration instructions.

### Core-Switch and Access Switches

The Core-Switch aggregates the departmental access switches and supporting network connections. Access switches connect end devices to their designated VLANs.

This layered arrangement supports departmental segmentation and provides a structured basis for network management.

### POS Network

POS devices use VLAN 50 and a dedicated routed connection through `GigabitEthernet0/2` on Router-Core.

The POS network is designed to remain operational when the main office trunk is unavailable. Its resilience must be evaluated using the documented failure test, including external connectivity if that is part of the final Internet simulation.

### Server Infrastructure

VLAN 70 provides a dedicated network for internal services.

| Server | IP Address | Purpose |
|---|---|---|
| DHCP-SRV | `10.48.70.10` | DHCP services |
| FILE-SRV | `10.48.70.11` | File-sharing services |
| WEB-SRV | `10.48.70.12` | Internal web services |

The servers connect through a dedicated Server-Switch. DNS and other service settings should be verified against the actual Packet Tracer configuration.

### Guest Wi-Fi

Guest Wi-Fi is assigned to VLAN 60 and represented by the AP-GUEST access point. The separate VLAN keeps guest devices logically distinct from departmental networks.

---

## Router-on-a-Stick

Router-on-a-Stick is the assigned technical challenge for this project.

The office network uses an IEEE 802.1Q trunk between Router-Core and Core-Switch. VLAN-specific router subinterfaces provide gateways for the office VLANs and allow traffic to be routed between them.

| Router Subinterface | VLAN | Default Gateway |
|---|---:|---|
| `GigabitEthernet0/1.10` | 10 | `10.48.10.1` |
| `GigabitEthernet0/1.20` | 20 | `10.48.20.1` |
| `GigabitEthernet0/1.30` | 30 | `10.48.30.1` |
| `GigabitEthernet0/1.40` | 40 | `10.48.40.1` |
| `GigabitEthernet0/1.60` | 60 | `10.48.60.1` |
| `GigabitEthernet0/1.70` | 70 | `10.48.70.1` |

VLAN 50 is intentionally excluded from the office trunk because POS uses its dedicated routed connection.

---

## Change Requests

### CR1 — Operations Expansion

Change Request CR1 adds eight Operations staff members to VLAN 20 without requiring a subnet redesign.

The `10.48.20.0/24` network provides sufficient address capacity for the additional devices while retaining the existing subnet and default gateway.

The change is evaluated using device addressing and connectivity tests, including access to the internal web server where supported by the recorded evidence.

### CR2 — POS Resilience

Change Request CR2 evaluates the behaviour of the network when the office trunk between Router-Core and Core-Switch is unavailable.

The test checks whether POS connectivity remains available through its dedicated routed connection while office devices that depend on the trunk lose access to their gateway.

Any claim about continued Internet access must be supported by a successful external connectivity test during the outage.

---

## IP Addressing Plan

The project uses the assigned address block:

`10.48.0.0/16`

Each major network segment is allocated a `/24` subnet. The addressing plan documents the network ranges, default gateways, and server addresses.

See [IP Addressing Plan](docs/ip-addressing-plan.md) for the detailed allocation.

---

## Design Decisions

Key design decisions include:

- Using VLANs to separate organisational functions.
- Implementing Router-on-a-Stick for office inter-VLAN routing.
- Providing a dedicated routed connection for POS systems.
- Allocating VLAN 70 to server infrastructure.
- Using a dedicated Server-Switch.
- Separating Guest Wi-Fi into VLAN 60.
- Using `/24` subnets to allow future expansion.
- Aligning subnet third octets with VLAN numbers for easier troubleshooting.

See [Design Decisions](docs/design-decisions.md) for further explanation.

---

## Topology Documentation

### Physical Topology

The physical topology documents the devices, interfaces, switch ports, servers, access points, and physical connections.

[View Physical Topology](docs/physical-topology.svg)

### Logical Topology

The logical topology documents the VLANs, IP networks, broadcast domains, and routing relationships.

[View Logical Topology](docs/logical-topology.svg)

---

## Testing and Evidence

Testing covers the network's core implementation and the behaviour required by the change requests.

Evidence should be consistent with the final saved Packet Tracer file and implementation report.

Relevant test areas include:

- VLAN and trunk configuration.
- Router subinterfaces and routing table.
- Same-VLAN and inter-VLAN connectivity.
- DHCP addressing and internal web access.
- Operations expansion under CR1.
- POS connectivity during the CR2 office-trunk failure.
- Internet or external-server connectivity, if implemented in the final simulation.

See [Testing Documentation](docs/testing.md) and the project's evidence directory for the recorded results. Tests not yet demonstrated should be identified as pending rather than described as successful.

---

## Repository Structure

```text
motsweding-network-infrastructure/
├── README.md
├── .gitignore
├── client-requirements.md
├── configs/
│   └── device configuration evidence
├── docs/
│   ├── client-requirements.md
│   ├── configuration.md
│   ├── design-decisions.md
│   ├── ip-addressing-plan.md
│   ├── logical-topology.svg
│   ├── physical-topology.svg
│   ├── testing.md
│   ├── troubleshooting.md
│   └── video-demonstration-plan.md
├── evidence/
│   └── network test screenshots
└── packet-tracer/
    └── Packet Tracer implementation
```

The structure above describes the intended organisation of project files. Keep the repository tree aligned with the files actually committed to GitHub.

---

## Demonstration Video

The final demonstration should explain the client requirements, network design, Router-on-a-Stick implementation, connectivity and services, CR1 expansion, and CR2 POS resilience test.

The video should show the relevant Packet Tracer configuration and test evidence, clearly distinguishing verified results from any functionality that remains incomplete.

See [Video Demonstration Plan](docs/video-demonstration-plan.md) for the proposed sequence.

---

## Project Deliverables

The project documentation and deliverables include:

- Client requirements and design decisions.
- Physical and logical network topology.
- IPv4 addressing plan.
- Cisco Packet Tracer implementation.
- Device configuration evidence.
- Network testing and troubleshooting documentation.
- Change Request CR1 and CR2 evidence.
- Final implementation report.
- Final demonstration video.

---

## Author

**Ofentse Seko**  
CMPG325 — Network Infrastructure Project  
Project ID: `CMPG325-2026-123`

└── testing/
    └── [testing evidence]
