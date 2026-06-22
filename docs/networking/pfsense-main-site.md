# pfSense #1 - MainSite Router

pfSense #1 is the MainSite router. It provides gateway, DHCP, routing, and firewall control for systems on VMnet1.

## Role

* MainSite LAN gateway
* DHCP service for the MainSite subnet
* Routing between the MainSite LAN and bridged WAN access
* Firewall control for systems connected to VMnet1

## Network Interfaces

| Interface | Network | Purpose |
| --- | --- | --- |
| WAN | VMnet0 / Bridged | Upstream access through the physical network |
| LAN | VMnet1 / Host-only | MainSite internal network |

## LAN Configuration

| Setting | Value |
| --- | --- |
| LAN subnet | 192.168.1.0/24 |
| LAN gateway | 192.168.1.1 |
| DHCP scope | 192.168.1.100-192.168.1.199 |
| VMware DHCP on VMnet1 | Disabled |

## Verification

* DHCP lease assignment from pfSense
* Correct subnet placement
* Correct default gateway
* Basic network reachability
* VM adapter placement in VMware Workstation Pro

## Troubleshooting Performed

VMnet1 initially had to be corrected to match the intended MainSite subnet. VMware DHCP was disabled, and VMnet1 was aligned with pfSense #1 at 192.168.1.0/24.

Corrected DHCP leasing through pfSense instead of VMware’s built-in DHCP service.

## Planned Improvements

* Configure controlled firewall rules for inter-network traffic
* Configure site-to-site VPN connectivity with pfSense #2
* Allow controlled access between MainSite and BranchLAN
* Forward pfSense logs to centralized logging
* Document firewall rule behavior and verification results