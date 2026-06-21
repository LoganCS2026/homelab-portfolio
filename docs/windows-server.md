# Windows Server 2022

Windows Server 2022 is the main Windows infrastructure server for this VMware IT infrastructure homelab. It is currently installed and prepared for future Active Directory, DNS, and domain services configuration.

## Role

Windows Server 2022 is intended to become the central infrastructure server for the MainSite network.

Planned responsibilities include:

* Active Directory Domain Services
* DNS services
* Domain authentication
* Group Policy management
* Windows client domain joins
* Help desk and administration practice

## Current State

Windows Server 2022 has been installed as a baseline server VM and is ready for further configuration.

Completed work includes:

* Installed Windows Server 2022 Datacenter Evaluation with Desktop Experience
* Configured the VM in VMware Workstation Pro
* Installed VMware Tools
* Verified mouse and display integration after VMware Tools installation
* Created a clean baseline state for future role configuration

## VMware Configuration

| Setting          | Value                                     |
| ---------------- | ----------------------------------------- |
| Platform         | VMware Workstation Pro                    |
| Operating system | Windows Server 2022 Datacenter Evaluation |
| Firmware         | UEFI                                      |
| CPU              | 2 vCPU                                    |
| Memory           | 4 GB                                      |
| Disk             | 60 GB                                     |
| Network          | VMnet1 / MainSite LAN                     |

## Network Placement

Windows Server 2022 is connected to the MainSite LAN behind pfSense #1.

| Setting          | Value          |
| ---------------- | -------------- |
| Network segment  | VMnet1         |
| MainSite subnet  | 192.168.1.0/24 |
| MainSite gateway | 192.168.1.1    |
| DHCP authority   | pfSense #1     |

A static IP address or DHCP reservation will be configured before installing server roles. This will keep domain and DNS services stable for the Windows client systems.

## Troubleshooting Performed

During installation, Windows Server setup failed with a licensing-terms error.

Root cause:

* VMware Easy Install added an automatic installation floppy image that conflicted with the Windows Server evaluation ISO.

Fix:

* Removed the VMware Easy Install floppy device from the VM settings.
* Restarted the installation manually.
* Completed Windows Server setup successfully.

Result:

* Windows Server installed normally after removing the conflicting Easy Install device.

## Planned Improvements

Planned improvements for Windows Server 2022 include:

* Assign a static IP address or DHCP reservation
* Install Active Directory Domain Services
* Install and configure DNS
* Promote the server to a domain controller
* Create the lab domain
* Create test users, groups, and organizational units
* Join Windows 11 clients to the domain
* Configure and test Group Policy
