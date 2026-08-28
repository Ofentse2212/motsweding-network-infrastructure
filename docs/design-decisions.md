# Network Design Decisions

## Motsweding Event Management

**Project ID:** CMPG325-2026-123  
**Student:** Ofentse Seko

---

## 1. Purpose

This document records the major design decisions made during the development of the Motsweding Event Management network.

The purpose is to demonstrate not only what was designed, but why particular architectural decisions were made.

The design began from the requirements in the project brief and was then developed into a complete enterprise network structure.

---

## 2. Design Approach

The design process followed the following sequence:

1. Identify the client requirements.
2. Identify the assigned technical challenge.
3. Identify the POS availability constraint.
4. Identify the CR1 scalability requirement.
5. Develop the logical network segmentation.
6. Develop the physical device architecture.
7. Develop the IPv4 addressing plan.
8. Add supporting infrastructure where appropriate.
9. Ensure that the physical, logical, and IP designs remain consistent.
10. Prepare the design for Cisco Packet Tracer implementation.

---

## 3. VLAN Segmentation

Separate VLANs were created for the major organisational functions.

The proposed VLAN structure is:

| VLAN | Function |
|---:|---|
| 10 | Administration |
| 20 | Operations |
| 30 | Finance |
| 40 | IT / Technical |
| 50 | POS |
| 60 | Guest Wi-Fi |
| 70 | Server Infrastructure |

The purpose of the segmentation is to create separate broadcast domains and provide a structured foundation for routing, management, and security.

---

## 4. Departmental Switches

During the topology development, the initial design represented the office network with a single office switch.

The design was refined to use a Core-Switch with separate departmental access switches.

The final architecture therefore follows a more structured hierarchy:

```text
Router-Core
     |
 Core-Switch
     |
     +--- SW-ADMIN
     |
     +--- SW-OPS
     |
     +--- SW-FINANCE
     |
     +--- SW-IT
     |
     +--- SW-GUEST
     |
     +--- Server-Switch