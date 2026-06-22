# Windows Client Systems

This lab includes three Windows 11 Pro client VMs used to simulate MainSite workstation, secondary workstation, and Branch Site endpoint scenarios. These systems are currently installed, baseline configured, and prepared for future Active Directory domain join and Group Policy testing.

## Role

The Windows client systems are used for:

* MainSite workstation testing
* Secondary client and reference-image practice
* Branch office endpoint simulation
* Future domain join testing
* Future Group Policy validation
* Help desk and workstation administration practice

## Client Overview

| System     | Network               | Current Role                                   |
| ---------- | --------------------- | ---------------------------------------------- |
| Win11Pro-1 | VMnet1 / MainSite LAN | Primary MainSite workstation                   |
| Win11Pro-2 | VMnet1 / MainSite LAN | Secondary workstation / future reference image |
| Win11Pro-3 | BranchLAN             | Branch office workstation                      |

## Network Placement

| System     | Network Segment | Subnet         | Gateway / DHCP |
| ---------- | --------------- | -------------- | -------------- |
| Win11Pro-1 | VMnet1          | 192.168.1.0/24 | pfSense #1     |
| Win11Pro-2 | VMnet1          | 192.168.1.0/24 | pfSense #1     |
| Win11Pro-3 | BranchLAN       | 192.168.2.0/24 | pfSense #2     |

Win11Pro-1 and Win11Pro-2 are placed on the MainSite LAN behind pfSense #1. Win11Pro-3 is placed behind pfSense #2 on the isolated BranchLAN segment to simulate a remote branch office workstation.

## Current State

Completed work includes:

* Installed Windows 11 Pro on all three client VMs
* Created local accounts for baseline setup
* Installed VMware Tools
* Verified mouse and display integration
* Verified MainSite and BranchLAN network placement
* Confirmed DHCP assignment from the correct pfSense router
* Created clean baseline snapshots before domain configuration

## Verification

Client configuration was verified by checking:

* Correct VMware network adapter placement
* Correct DHCP lease assignment
* Correct subnet placement
* Correct default gateway
* MainSite workstation placement on VMnet1
* Branch workstation placement on BranchLAN

## Troubleshooting Performed

During Windows client setup, several issues were identified and resolved.

Win11Pro-1 initially received an address from the wrong subnet because VMnet1 was configured with VMware DHCP enabled and did not match the intended MainSite subnet. VMnet1 was corrected to 192.168.1.0/24, VMware DHCP was disabled, and the client received an address from pfSense #1.

Win11Pro-2 initially received an APIPA address because pfSense #1 was powered off and no DHCP server was available on VMnet1. pfSense #1 was powered on, and the client received a valid MainSite DHCP lease after renewing its network configuration.

Win11Pro-3 was placed on the BranchLAN segment behind pfSense #2. During setup, the VMware network adapter had to be corrected from Host-only to LAN segment: BranchLAN so the system would be isolated behind the branch router instead of joining the MainSite network.

A host-side VMnet1 IP conflict was also corrected by changing the Windows host VMnet1 adapter away from 192.168.1.1, which is used by pfSense #1 as the MainSite LAN gateway.

## Planned Improvements

Planned improvements for the Windows client systems include:

* Join Win11Pro-1 and Win11Pro-2 to the future Active Directory domain
* Join Win11Pro-3 after routing, DNS, and site-to-site VPN connectivity are configured
* Test domain user login
* Apply and verify basic Group Policy settings
* Test branch workstation access to MainSite domain services
* Use Win11Pro-2 for future imaging, Sysprep, or repeatable workstation configuration practice
