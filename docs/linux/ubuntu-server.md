# Ubuntu Server

Ubuntu Server is the Linux infrastructure server for this VMware IT infrastructure homelab. It is connected to the MainSite LAN behind pfSense #1 and is prepared for future Docker, logging, SIEM, and internal service hosting.

## Role

Ubuntu Server is used for:

* Linux server administration practice
* SSH-based remote administration
* Future Docker and Docker Compose services
* Future centralized logging
* Future SIEM or monitoring services
* Future internal service hosting

## VMware Configuration

| Setting          | Value                   |
| ---------------- | ----------------------- |
| Platform         | VMware Workstation Pro  |
| Operating system | Ubuntu Server 26.04 LTS |
| VM name          | UbuntuServer            |
| CPU              | 2 vCPU                  |
| Memory           | 4 GB                    |
| Disk             | 40 GB                   |
| Disk type        | SCSI                    |
| Network          | VMnet1 / MainSite LAN   |

## Network Placement

| Setting              | Value            |
| -------------------- | ---------------- |
| Network segment      | VMnet1           |
| MainSite subnet      | 192.168.1.0/24   |
| Gateway              | 192.168.1.1      |
| DHCP authority       | pfSense #1       |
| Current IPv4 address | 192.168.1.102/24 |
| Active interface     | ens33            |

Ubuntu Server is connected to VMnet1 behind pfSense #1. VMware DHCP is disabled on VMnet1, so pfSense #1 provides DHCP, gateway, and DNS services for the MainSite network.

## Current State

Completed work includes:

* Installed Ubuntu Server
* Connected the VM to the MainSite VMnet1 network
* Enabled OpenSSH during installation
* Verified DHCP assignment from pfSense #1
* Verified gateway, DNS, and internet connectivity
* Verified Ubuntu archive connectivity
* Verified open-vm-tools integration
* Applied available package updates
* Confirmed no reboot was required after updates
* Created a clean baseline snapshot after installation and verification

## Verification

Ubuntu Server configuration was verified by checking:

* Correct VMnet1 network placement
* DHCP assignment from pfSense #1
* Correct default gateway
* pfSense gateway reachability
* Internet connectivity
* DNS resolution
* Ubuntu archive mirror access
* open-vm-tools service status
* VMware integration status
* Package update completion

## Troubleshooting Performed

During installation, DHCP autoconfiguration initially failed because pfSense #1 was powered off while Ubuntu Server was connected to VMnet1. Since VMware DHCP is disabled on VMnet1, no DHCP server was available until pfSense #1 was started.

This was resolved by powering on pfSense #1 and returning the Ubuntu network interface to automatic DHCP. Ubuntu Server then received a valid MainSite DHCP lease from pfSense #1.

After installation completed, the installer reboot process displayed a shutdown error. The VM was reset from VMware after confirming the installer was stuck. Ubuntu then booted successfully from the installed virtual disk, and no reinstall was required.

## Planned Improvements

Planned improvements for Ubuntu Server include:

* Configure a static IP address or DHCP reservation
* Install Docker and Docker Compose
* Deploy internal lab services
* Configure centralized logging for pfSense and Windows events
* Host internal web services for future lab testing
