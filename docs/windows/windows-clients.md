# Windows Client Systems

Three Windows 11 Pro clients simulate Main Site, secondary workstation, and Branch Site endpoint roles. They are installed, baseline configured, and ready for later domain integration.

## Role

* Main Site workstation testing
* Secondary client and reference-image workflows
* Branch office endpoint simulation
* Domain join testing
* Group Policy validation
* Help desk troubleshooting scenarios

## Client Overview

| System | Network | Current Role |
| --- | --- | --- |
| Win11Pro-1 | VMnet1 / Main Site LAN | Primary Main Site workstation |
| Win11Pro-2 | VMnet1 / Main Site LAN | Secondary workstation / reference-image testing |
| Win11Pro-3 | BranchLAN | Branch Site workstation |

## Network Placement

| System | Network Segment | Subnet | Gateway / DHCP |
| --- | --- | --- | --- |
| Win11Pro-1 | VMnet1 | 192.168.1.0/24 | pfSense #1 |
| Win11Pro-2 | VMnet1 | 192.168.1.0/24 | pfSense #1 |
| Win11Pro-3 | BranchLAN | 192.168.2.0/24 | pfSense #2 |

## Current State

* Installed Windows 11 Pro on all three client VMs
* Created local accounts for baseline setup
* Installed VMware Tools
* Verified mouse and display integration
* Verified Main Site and BranchLAN placement
* Confirmed DHCP assignment from the correct pfSense router
* Baseline snapshots created before domain configuration

## Verification

* Correct VMware network adapter placement
* DHCP lease assignment from the correct router
* Correct subnet placement
* Correct default gateway
* Main Site workstation placement on VMnet1
* Branch workstation placement on BranchLAN

## Troubleshooting Performed

Win11Pro-1 initially received an address from the wrong subnet because VMnet1 had VMware DHCP enabled and did not match the intended Main Site subnet. VMnet1 was corrected to 192.168.1.0/24, VMware DHCP was disabled, and the client received an address from pfSense #1.

Win11Pro-2 initially received an APIPA address because pfSense #1 was powered off. After pfSense #1 was started, the client received a valid Main Site DHCP lease.

Win11Pro-3 had to be moved from Host-only networking to LAN segment: BranchLAN so it would be isolated behind pfSense #2 instead of joining Main Site.

A host-side VMnet1 IP conflict was corrected by changing the Windows host VMnet1 adapter away from 192.168.1.1, which is used by pfSense #1 as the Main Site gateway.

## Planned Improvements

* Join Win11Pro-1 and Win11Pro-2 to the Active Directory domain
* Join Win11Pro-3 after routing, DNS, and VPN connectivity are configured
* Test domain user login
* Apply and verify basic Group Policy settings
* Test Branch Site access to Main Site domain services
* Use Win11Pro-2 for imaging, Sysprep, or repeatable workstation configuration testing