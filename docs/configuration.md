# Network Configuration Documentation

## 1. Overview
This document outlines the architecture and configuration details for the Motsweding Event Management campus network (address block 10.48.0.0/16)[cite: 7]. It implements an Advanced Router-on-a-Stick inter-VLAN routing challenge[cite: 7].

## 2. VLAN & Subnet Summary
| VLAN ID | Name | Subnet / Gateway | Router Interface | Attached To |
| :--- | :--- | :--- | :--- | :--- |
| 10 | Administration | 10.48.10.0/24 | Gi0/1.10 | SW-ADMIN[cite: 7] |
| 20 | Operations | 10.48.20.0/24 | Gi0/1.20 | SW-OPS (10 workstations)[cite: 7] |
| 30 | Finance | 10.48.30.0/24 | Gi0/1.30 | SW-FIN[cite: 7] |
| 40 | IT Technical | 10.48.40.0/24 | Gi0/1.40 | SW-IT[cite: 7] |
| 50 | POS Network | 10.48.50.0/24 | Gi0/2 (Dedicated routed) | SWITCH-POS[cite: 7] |
| 60 | Guest WiFi | 10.48.60.0/24 | Gi0/1.60 | SW-GUEST / AP-GUEST[cite: 7] |
| 70 | Server Infrastructure | 10.48.70.0/24 | Gi0/1.70 | SERVER-SWITCH[cite: 7] |
| n/a | Router Link | 10.48.0.0/30 | Gi0/0 (Core: 10.48.0.2) | Router-Edge (10.48.0.1)[cite: 7] |

## 3. Architecture Decisions
* **Router-on-a-Stick:** GigabitEthernet0/1 handles six office VLANs via 802.1Q sub-interfaces[cite: 7].
* **Independent POS Path:** To ensure point-of-sale systems stay online even if the office LAN fails, the POS VLAN (50) bypasses the office trunk and utilizes a dedicated physical interface (`GigabitEthernet0/2`) on Router-Core[cite: 7].
* **DHCP & Services:** Central DHCP server (DHCP-SRV, 10.48.70.10) dynamically assigns addresses across office sub-interfaces via `ip helper-address`[cite: 7].
