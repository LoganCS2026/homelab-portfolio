# VMware IT Infrastructure Homelab

This repository documents a VMware-based IT infrastructure homelab focused on networking, Windows administration, Linux server setup, virtualization, troubleshooting, and technical documentation.

The lab uses segmented virtual networks, pfSense routers, Windows Server, Windows 11 clients, Ubuntu Server, Kali Linux, and Metasploitable 3. Core VM deployment is complete. Current work focuses on infrastructure configuration, Windows Server preparation, Linux services, routing, and logging.

## Lab Goals

* Build a segmented virtual network environment using VMware Workstation Pro
* Practice IP addressing, DHCP, routing, and network troubleshooting
* Prepare Windows Server and Windows clients for Active Directory administration
* Use Ubuntu Server for infrastructure services, Docker, and centralized logging
* Maintain clear technical documentation for setup decisions, troubleshooting, and verification
* Add controlled security testing after the core infrastructure is configured

## Current Status

Core VM deployment is complete, and the lab is in the infrastructure configuration phase.

Completed work includes:

* Configured pfSense #1 as the MainSite router and DHCP authority
* Configured pfSense #2 as the BranchLAN router and DHCP authority
* Built separate MainSite, BranchLAN, and NAT virtual network segments
* Installed Windows Server 2022
* Installed three Windows 11 Pro clients
* Installed and verified Ubuntu Server on the MainSite network
* Deployed Kali Linux for authorized lab testing
* Deployed Metasploitable 3 as a vulnerable lab target
* Verified DHCP behavior, network placement, and initial system reachability

Planned improvements include:

* Configure Windows Server 2022 for Active Directory Domain Services
* Join Windows 11 clients to the domain
* Configure site-to-site VPN between MainSite and BranchLAN
* Deploy Docker-based services on Ubuntu Server
* Configure centralized logging
* Generate controlled test traffic from Kali Linux after monitoring is in place

## Network Overview

| Network | Purpose | Subnet |
| --- | --- | --- |
| VMnet1 | MainSite LAN | 192.168.1.0/24 |
| BranchLAN | Branch office LAN | 192.168.2.0/24 |
| VMnet8 | NAT network for isolated testing | 192.168.80.0/24 |
| VMnet0 | Bridged WAN access | Home network |

## Systems Used

| System | Role |
| --- | --- |
| pfSense #1 | MainSite router and DHCP authority |
| pfSense #2 | Branch Site router and DHCP authority |
| Windows Server 2022 | Windows infrastructure server prepared for Active Directory services |
| Windows 11 Pro clients | MainSite and Branch Site workstations prepared for domain testing |
| Ubuntu Server | Linux infrastructure server prepared for Docker and logging services |
| Kali Linux | Security assessment workstation for authorized lab testing |
| Metasploitable 3 | Vulnerable target for controlled scanning and detection practice |

## Documentation

* [Network Design](docs/architecture/network-design.md)
* [Project Roadmap](docs/architecture/roadmap.md)
* [pfSense MainSite Router](docs/networking/pfsense-main-site.md)
* [pfSense Branch Site Router](docs/networking/pfsense-branch-site.md)
* [Windows Server 2022](docs/windows/windows-server.md)
* [Windows Client Systems](docs/windows/windows-clients.md)
* [Ubuntu Server](docs/linux/ubuntu-server.md)
* [Kali Linux](docs/linux/kali-linux.md)
* [Metasploitable 3](docs/security/metasploitable3.md)

## Skills Demonstrated

* VMware Workstation Pro virtualization
* Virtual network segmentation using bridged, host-only, NAT, and LAN segment networks
* pfSense router deployment and interface assignment
* DHCP scope configuration and lease verification
* Windows Server 2022 and Windows 11 VM deployment
* Ubuntu Server deployment with SSH, updates, and VMware tools verification
* Kali Linux deployment and controlled testing preparation
* Troubleshooting DHCP failures, APIPA, subnet mismatches, ISO boot issues, VM adapter placement, and package update problems
* Technical documentation and project organization