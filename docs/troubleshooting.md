# Network Troubleshooting Log

## 1. Encountered Issues & Resolutions
* **Issue 1: Invalid Input Error on Switch CLI**
  * *Problem:* Entering `show running-config` while in User Exec mode (`Switch>`) resulted in an invalid input error.
  * *Resolution:* Entered `enable` to switch to Privileged EXEC mode (`Switch#`) before executing the show command.
* **Issue 2: Trunk Port Allowed VLANs**
  * *Problem:* Initial cross-VLAN communication failed due to restricted trunk configurations.
  * *Resolution:* Updated interface trunk allowed VLAN parameters to include all required network segments (`10, 20, 30, etc.`).
