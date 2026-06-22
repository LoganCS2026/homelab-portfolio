# Windows Server 2022

Windows Server 2022 is the main Windows infrastructure server. It is installed and ready for Active Directory, DNS, and domain services configuration.

## Role

* Active Directory Domain Services
* DNS services
* Domain authentication
* Group Policy management
* Windows client domain joins
* Help desk administration scenarios

## Current State

* Installed Windows Server 2022 Datacenter Evaluation with Desktop Experience
* Configured the VM in VMware Workstation Pro
* Installed VMware Tools
* Verified mouse and display integration
* Baseline state created before role configuration

## VMware Configuration

| Setting | Value |
| --- | --- |
| Platform | VMware Workstation Pro |
| Operating system | Windows Server 2022 Datacenter Evaluation |
| Firmware | UEFI |
| CPU | 2 vCPU |
| Memory | 4 GB |
| Disk | 60 GB |
| Network | VMnet1 / MainSite LAN |

## Network Placement

| Setting | Value |
| --- | --- |
| Network segment | VMnet1 |
| MainSite subnet | 192.168.1.0/24 |
| MainSite gateway | 192.168.1.1 |
| DHCP authority | pfSense #1 |

A static IP address or DHCP reservation will be configured before installing server roles.

## Troubleshooting Performed

Windows Server setup failed with a licensing-terms error during installation.

Root cause:

* VMware Easy Install added an automatic installation floppy image that conflicted with the Windows Server evaluation ISO.

Fix:

* Removed the VMware Easy Install floppy device from the VM settings.
* Restarted the installation manually.
* Completed Windows Server setup successfully.

## Planned Improvements

* Assign a static IP address or DHCP reservation
* Install Active Directory Domain Services
* Install and configure DNS
* Promote the server to a domain controller
* Create the lab domain
* Create test users, groups, and organizational units
* Join Windows 11 clients to the domain
* Configure and test Group Policy