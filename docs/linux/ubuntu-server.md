# Ubuntu Server

Ubuntu Server is the Linux infrastructure server. It is installed on the Main Site LAN and ready for Docker, logging, and internal service hosting.

## Role

* Linux server administration
* SSH-based administration
* Docker and Docker Compose services
* Centralized logging
* Internal service hosting

## VMware Configuration

| Setting | Value |
| --- | --- |
| Platform | VMware Workstation Pro |
| Operating system | Ubuntu Server 26.04 LTS |
| VM name | UbuntuServer |
| CPU | 2 vCPU |
| Memory | 4 GB |
| Disk | 40 GB |
| Disk type | SCSI |
| Network | VMnet1 / Main Site LAN |

## Network Placement

| Setting | Value |
| --- | --- |
| Network segment | VMnet1 |
| Main Site subnet | 192.168.1.0/24 |
| Gateway | 192.168.1.1 |
| DHCP authority | pfSense #1 |

## Current State

* Installed Ubuntu Server
* Connected the VM to VMnet1
* Enabled OpenSSH during installation
* Applied available package updates
* Verified open-vm-tools integration
* Confirmed no reboot was required after updates
* Baseline snapshot created

## Verification

* DHCP assignment from pfSense #1
* Correct default gateway
* pfSense gateway reachability
* Internet connectivity
* DNS resolution
* Ubuntu archive mirror access
* VMware integration status
* Package update completion

## Troubleshooting Performed

DHCP autoconfiguration initially failed because pfSense #1 was powered off while Ubuntu Server was connected to VMnet1. Since VMware DHCP is disabled on VMnet1, no DHCP server was available until pfSense #1 was started.

After pfSense #1 was started and DHCP was restored, Ubuntu Server received a valid Main Site DHCP lease.

The installer reboot process displayed a shutdown error after installation completed. The VM was reset from VMware after confirming the installer was stuck. Ubuntu then booted successfully from the installed virtual disk, and no reinstall was required.

## Planned Improvements

* Configure a static IP address or DHCP reservation
* Install Docker and Docker Compose
* Deploy internal lab services
* Configure centralized logging for pfSense and Windows events
* Host internal web services for lab testing