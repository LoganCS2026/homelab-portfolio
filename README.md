# VMware IT Infrastructure Homelab

This repository documents a VMware-based IT infrastructure homelab built for hands-on practice with networking, Windows administration, Linux server setup, virtualization, troubleshooting, and technical documentation.

The lab uses segmented virtual networks, pfSense routers, Windows Server, Windows 11 clients, Ubuntu Server, Kali Linux, and Metasploitable 3. Core VM deployment is complete, and current work focuses on infrastructure configuration, network verification, Windows Server preparation, Linux services, and clean technical documentation.

## Lab Goals

* Build a segmented virtual network environment using VMware Workstation Pro
* Practice IP addressing, DHCP, routing concepts, and network troubleshooting
* Prepare Windows Server and Windows clients for Active Directory administration
* Use Ubuntu Server for future infrastructure services, Docker, and centralized logging
* Maintain clear technical documentation for setup decisions, troubleshooting, and verification
* Expand into controlled security testing after the core IT infrastructure is configured

## Current Status

Core VM deployment is complete, and the lab is now in the infrastructure configuration phase.

Completed work includes:

* Configured pfSense #1 as the MainSite router and DHCP authority
* Configured pfSense #2 as the BranchLAN router and DHCP authority
* Built separate MainSite, BranchLAN, and NAT virtual network segments
* Installed Windows Server 2022
* Installed Windows 11 Pro clients
* Installed and verified Ubuntu Server on the MainSite network
* Deployed Kali Linux for future lab testing
* Deployed Metasploitable 3 as a future vulnerable test target
* Verified DHCP behavior, network placement, and initial system reachability

Planned improvements include:

* Configure Windows Server 2022 as an Active Directory domain controller
* Join Windows 11 clients to the domain
* Configure site-to-site VPN between MainSite and BranchLAN
* Deploy Docker-based services on Ubuntu Server
* Configure centralized logging
* Use Kali Linux to generate controlled test traffic after monitoring is in place

## Network Overview

| Network   | Purpose                                                    | Subnet          |
| --------- | ---------------------------------------------------------- | --------------- |
| VMnet1    | MainSite LAN behind pfSense #1                             | 192.168.1.0/24  |
| BranchLAN | Branch office LAN behind pfSense #2                        | 192.168.2.0/24  |
| VMnet8    | NAT network reserved for isolated testing/future expansion | 192.168.80.0/24 |
| VMnet0    | Bridged WAN access to the physical network                 | Home network    |

## Systems Used

| System                 | Role                                                                                 |
| ---------------------- | ------------------------------------------------------------------------------------ |
| pfSense #1             | MainSite router and DHCP authority                                                   |
| pfSense #2             | Branch office router and DHCP authority                                              |
| Windows Server 2022    | Windows infrastructure server prepared for Active Directory services                 |
| Windows 11 Pro clients | Workstations prepared for domain join, Group Policy testing, and help desk scenarios |
| Ubuntu Server          | Linux infrastructure server prepared for Docker and centralized logging              |
| Kali Linux             | Security testing workstation for future controlled lab exercises                     |
| Metasploitable 3       | Vulnerable test target for future authorized scanning and detection practice         |

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
* Windows Server and Windows client deployment
* Linux server installation and network verification
* Troubleshooting APIPA, DHCP failures, subnet mismatches, ISO boot issues, and VM adapter placement
* Technical documentation and project organization
