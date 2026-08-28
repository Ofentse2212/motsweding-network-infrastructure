# Client Requirements

## Motsweding Event Management

**Project ID:** CMPG325-2026-123  
**Client ID:** CLI-123  
**Organisation:** Motsweding Event Management  
**Location:** Potchefstroom  
**Industry:** Entertainment  
**Student:** Ofentse Seko  
**Addressing Block:** 10.48.0.0/16

---

## 1. Purpose

This document records the client requirements, assigned technical challenge, design constraint, change request, and supporting design requirements used as the basis for the Motsweding Event Management network design.

The core requirements originate from the CMPG325 project brief. Supporting network components such as VLAN assignments, departmental switches, server infrastructure, and Guest Wi-Fi are documented as design decisions developed to create an appropriate and realistic network solution.

---

## 2. Client Requirements

### R1 — Assigned Organisation

The network must be designed specifically for Motsweding Event Management in Potchefstroom.

### R2 — Appropriate Network Design

The network must provide an appropriate topology and device arrangement for an entertainment and event-management environment.

### R3 — IPv4 Addressing

The assigned IPv4 addressing block is:

`10.48.0.0/16`

All network addressing must be based on this block.

### R4 — Connectivity and Network Services

The network must provide appropriate connectivity and network services required by the scenario.

The design incorporates:

- Inter-VLAN routing
- DHCP
- DNS/Web services
- File services
- Internet/WAN connectivity
- Guest Wi-Fi
- POS connectivity

### R5 — Cisco Packet Tracer

The network must be implemented and simulated using Cisco Packet Tracer.

### R6 — Router-on-a-Stick

The assigned technical challenge is:

**Router-on-a-Stick (sub-interface Inter-VLAN routing).**

The final implementation must configure, verify, and demonstrate this technology.

### R7 — Testing

The final implementation must provide evidence of successful network operation, connectivity, configuration, and troubleshooting.

---

## 3. Design Constraint — POS Availability

The client requirement states that:

> Point-of-Sale systems must stay online even if the office LAN fails.

This requirement directly influences the network architecture.

The proposed design places POS devices in:

**VLAN 50 — POS**

The POS network uses a dedicated physical path rather than relying solely on the main office trunk.

This provides an independent connectivity path for the POS environment.

The design is intended to reduce the dependency of POS operations on the main office LAN.

The effectiveness of this design will be verified during Packet Tracer implementation and testing.

---

## 4. Change Request — CR1

The client has added eight staff members to one department.

The network must accommodate these additional users without requiring a network redesign.

The Operations department has been selected as the CR1 target department.

Operations uses:

`VLAN 20`

with:

`10.48.20.0/24`

A `/24` network provides:

`254 usable host addresses`

This provides significantly more capacity than the current number of Operations devices and allows the eight additional staff members to be added without changing the VLAN, subnet, or default gateway.

---

## 5. Supporting Design Decisions

The following elements were developed as part of the network design rather than being treated as replacements for the assigned requirements:

### VLAN Segmentation

Separate VLANs are used for organisational functions to create separate broadcast domains.

### Departmental Switches

A Core-Switch aggregates departmental access switches.

The departmental switches provide access connectivity to devices within their respective VLANs.

### Server Infrastructure

A dedicated server network, VLAN 70, is introduced for infrastructure services.

The proposed servers are:

- DHCP-SRV
- FILE-SRV
- WEB-SRV

### Guest Wi-Fi

Guest users are separated into VLAN 60 using AP-GUEST.

### POS Network

POS devices are separated into VLAN 50 and provided with a dedicated physical path.

These additions strengthen the realism and organisation of the proposed enterprise network while keeping the assigned technical challenge and client requirements unchanged.

---

## 6. Project Success Criteria

The design will be considered successful when:

- [ ] The network is implemented in Cisco Packet Tracer.
- [ ] The `10.48.0.0/16` addressing block is used.
- [ ] Appropriate connectivity is demonstrated.
- [ ] Router-on-a-Stick is configured and verified.
- [ ] VLAN segmentation is correctly implemented.
- [ ] POS availability is tested against the stated constraint.
- [ ] CR1 can be accommodated without redesigning the network.
- [ ] Network services operate correctly.
- [ ] Testing evidence is captured.
- [ ] Important troubleshooting is documented.
- [ ] The final Packet Tracer file opens and reproduces the solution.
- [ ] The GitHub repository contains professional documentation and evidence.

---

## 7. Verification

Milestone 1 establishes the design baseline.

The physical and logical diagrams describe the proposed architecture, but implementation claims will be verified in Cisco Packet Tracer.

Testing will include:

- Intra-VLAN connectivity
- Inter-VLAN connectivity
- Router-on-a-Stick operation
- DHCP operation
- Server reachability
- POS connectivity
- POS behaviour when the main office path is isolated
- CR1 expansion

Results will be documented as implementation evidence in later project stages.