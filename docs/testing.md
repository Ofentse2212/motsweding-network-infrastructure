# Network Testing & Verification

## 1. Connectivity & Layer Verification
* **VLANs & Trunks:** Verified via `show vlan brief` and `show interfaces trunk` on Core-Switch and access switches, confirming proper 802.1Q encapsulation and native VLAN assignments[cite: 7].
* **Inter-VLAN & Same-VLAN Pings:** Tested successfully between hosts across different subnets (e.g., PC-FIN-01 to PC-ADMIN-02) showing correct TTL decrement (TTL=127)[cite: 7].
* **Server & Service Access:** Verified HTTP web traffic rendering from office workstations to WEB-SRV (`10.48.70.12`)[cite: 7].
* **Change Request CR1:** Verified scalability by adding 8 extra workstations (PC-OPS-03 to PC-OPS-10) to the Operations department, confirming successful DHCP allocation and inter-VLAN pings without network redesign[cite: 7].

## 2. Simulated Internet Testing
* **External Path:** Router-Core default route (`0.0.0.0 0.0.0.0 10.48.0.1`) forwards external traffic through Router-Edge to ISP-Router and Internet-Test-Server (`203.0.113.10`)[cite: 7].
* **Verification:** Office clients successfully pinged and loaded web content from `203.0.113.10`[cite: 7].

## 3. Constraint CR2: POS Resilience Test
* **Outage Simulation:** Administratively shut down Router-Core `GigabitEthernet0/1` to drop the office LAN trunk[cite: 7].
* **Result:** POS-01 maintained 0% loss connectivity to its gateway (`10.48.50.1`) and peer terminal (`10.48.50.12`), while an office workstation (PC-FIN-01) completely lost gateway connectivity (`100% loss`), proving complete isolation of failure domains[cite: 7].
