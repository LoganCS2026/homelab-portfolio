# pfSense #1 - MainSite Router

pfSense #1 is the MainSite router for this VMware IT infrastructure homelab. It provides the gateway and DHCP service for the primary lab network used by the Windows, Linux, and testing systems.

## Role

pfSense #1 currently provides:

* MainSite LAN gateway
* DHCP service for the MainSite subnet
* Routing between the MainSite LAN and bridged WAN access
* Central network access point for systems connected to VMnet1

## Network Interfaces

| Interface | Network            | Purpose                                               |
| --------- | ------------------ | ----------------------------------------------------- |
| WAN       | VMnet0 / Bridged   | Provides upstream access through the physical network |
| LAN       | VMnet1 / Host-only | MainSite LAN for internal lab systems                 |

## LAN Configuration

| Setting               | Value                       |
| --------------------- | --------------------------- |
| LAN subnet            | 192.168.1.0/24              |
| LAN gateway           | 192.168.1.1                 |
| DHCP scope            | 192.168.1.100-192.168.1.199 |
| VMware DHCP on VMnet1 | Disabled                    |

VMware DHCP is disabled on VMnet1 so pfSense #1 remains the only DHCP authority for the MainSite LAN. This prevents conflicting DHCP leases and keeps IP assignment controlled through the lab router.

## Connected Systems

The MainSite LAN is used for the primary lab systems, including:

* Windows Server 2022
* Windows 11 Pro clients
* Ubuntu Server
* Kali Linux

## Verification

MainSite configuration was verified by checking:

* DHCP lease assignment from pfSense
* Correct subnet placement
* Correct default gateway
* Basic network reachability
* VM adapter placement in VMware Workstation Pro

## Troubleshooting Performed

During the lab build, VMnet1 had to be corrected so it matched the intended MainSite subnet. VMware DHCP was disabled and the VMnet1 subnet was aligned with pfSense #1 at 192.168.1.0/24.

This fixed incorrect IP assignment and allowed lab systems to receive addresses from pfSense instead of VMware’s built-in DHCP service.

## Planned Improvements

Planned improvements for pfSense #1 include:

* Configure controlled firewall rules for inter-network traffic
* Configure site-to-site VPN connectivity with pfSense #2
* Allow controlled access between MainSite and BranchLAN
* Forward pfSense logs to a centralized logging platform
* Document rule behavior and verification results
