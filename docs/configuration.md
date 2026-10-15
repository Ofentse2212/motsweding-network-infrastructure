# Network Configuration Documentation

## 1. Overview
This document outlines the configuration details for the Motsweding network infrastructure, including VLANs, IP addressing, trunking, and routing protocols.

## 2. VLAN & Subnet Summary
| VLAN ID | Name | Subnet / Gateway | Description |
| :--- | :--- | :--- | :--- |
| 10 | Admin | 192.168.10.0/24 | Administration department |
| 20 | POS | 192.168.20.0/24 | Point of Sale network |
| 30 | Finance | 192.168.30.0/24 | Finance department |

## 3. Device Summary
* **Router-Core / Router-Edge:** Handles inter-VLAN routing, default gateway services, and external ISP connectivity.
* **Core-Switch:** Manages core distribution and trunking to access switches.
* **SWITCH-POS & SW-FIN:** Access switches connecting department endpoints.
