# Network Troubleshooting Log

## 1. Key Faults & Resolutions
* **CLI Privileged Mode Error:** Entering `show running-config` or `shutdown` at the user prompt (`>`) returned invalid input errors or DNS translation lookups[cite: 7]. Resolved by entering `enable` first to reach Privileged EXEC mode (`#`)[cite: 7].
* **Complex DHCP Failure Chain:** Initial DHCP failures hid four overlapping issues:
  1. Unassigned access ports and missing VLAN definitions[cite: 7].
  2. Department switch uplinks incorrectly configured as access ports instead of trunks, triggering Spanning Tree PVID inconsistencies[cite: 7].
  3. Native VLAN mismatches on trunks (e.g., mismatch between Core-Switch and SERVER-SWITCH)[cite: 7].
  4. Incorrect default Class A subnet masks (`255.0.0.0`) on servers instead of `255.255.255.0`[cite: 7].
  * *Resolution:* Corrected trunk/access modes, standardized native VLANs to `1`, fixed server subnet masks, cleared stale lease bindings, and renewed DHCP clients[cite: 7].
* **Resilience Testing Correction:** Initial testing incorrectly shut down an individual access port (`FastEthernet0/1`) rather than testing the client constraint[cite: 7]. Replaced with the formal CR2 test by shutting down the core trunk (`GigabitEthernet0/1`) to validate independent POS availability[cite: 7].
