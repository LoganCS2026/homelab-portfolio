# VMware IT Infrastructure Homelab

A VMware-based infrastructure homelab demonstrating segmented networking, pfSense routing, Active Directory, DNS, Windows domain administration, Linux server configuration, and isolated security testing preparation.

## Architecture

| Segment | Purpose | Subnet |
| --- | --- | --- |
| VMnet1 | Main Site LAN | 192.168.1.0/24 |
| BranchLAN | Branch office LAN | 192.168.2.0/24 |
| VMnet8 | Isolated testing network | 192.168.80.0/24 |
| VMnet0 | Bridged WAN access | Home network |

<img src="docs/assets/network-topology.png" alt="Network topology" width="850">

## Implemented

- Configured pfSense #1 as the Main Site router, firewall, and DHCP authority
- Configured pfSense #2 as the BranchLAN router, firewall, and DHCP authority
- Disabled VMware DHCP on VMnet1 so pfSense #1 is the sole DHCP authority
- Assigned static infrastructure IPs:
  - Windows Server 2022: `192.168.1.10`
  - Ubuntu Server: `192.168.1.20`
- Promoted Windows Server 2022 to Domain Controller for `lab.local`
- Installed DNS during Domain Controller promotion
- Updated Main Site DHCP so clients use `192.168.1.10` for DNS
- Joined Win11Pro-1 and Win11Pro-2 to `lab.local`
- Verified domain logons with separate test users
- Created and applied a test Group Policy Object
- Confirmed Kali can reach Metasploitable 3 through VMnet8 using ARP and TCP validation

## Systems

| System | Network | Verified Role |
| --- | --- | --- |
| pfSense #1 | VMnet1 / VMnet0 | Main Site gateway, DHCP, firewall |
| pfSense #2 | BranchLAN / VMnet0 | Branch gateway, DHCP, firewall |
| Windows Server 2022 | VMnet1 | Domain Controller and DNS server for `lab.local` |
| Win11Pro-1 | VMnet1 | Domain-joined workstation |
| Win11Pro-2 | VMnet1 | Domain-joined workstation |
| Win11Pro-3 | BranchLAN | Branch workstation, local-only until VPN routing exists |
| Ubuntu Server | VMnet1 | Static-addressed Linux infrastructure server |
| Kali Linux | VMnet1 + VMnet8 | Security testing workstation |
| Metasploitable 3 | VMnet8 | Lab-owned vulnerable target |

## Verification Highlights

- `Get-ADDomain` confirmed `lab.local`, `LAB`, and `Windows2016Domain`
- `nslookup lab.local` resolved to `192.168.1.10`
- `dcdiag /q` returned only the expected DFSR warning for a new single-DC lab
- Win11Pro-1 logged in with `LAB\John`
- Win11Pro-2 logged in with `LAB\Sarah`
- `gpupdate /force` applied the `Test-Wallpaper` GPO to both domain-joined clients
- Nmap confirmed exposed services on Metasploitable 3 after ICMP failed

## Current Blocker

Win11Pro-3 is on BranchLAN and cannot join `lab.local` until routing exists between `192.168.2.0/24` and the Domain Controller at `192.168.1.10`.

## Next Milestones

- Configure site-to-site VPN between pfSense #1 and pfSense #2
- Join Win11Pro-3 to `lab.local`
- Deploy Docker-based services on Ubuntu Server
- Forward pfSense and Windows logs to Ubuntu for centralized logging
- Generate Kali test traffic and correlate it with firewall and endpoint logs

## Documentation

| Area | Documentation |
| --- | --- |
| Architecture | [Network Design](docs/architecture/network-design.md), [Roadmap](docs/architecture/roadmap.md), [Verification Screenshots](docs/architecture/verification-screenshots.md) |
| Networking | [pfSense Main Site](docs/networking/pfsense-main-site.md), [pfSense Branch Site](docs/networking/pfsense-branch-site.md) |
| Windows Domain | [Windows Server](docs/windows/windows-server.md), [Windows Clients](docs/windows/windows-clients.md), [Active Directory](docs/windows/active-directory.md), [Group Policy](docs/windows/group-policy.md) |
| Linux and Security | [Ubuntu Server](docs/linux/ubuntu-server.md), [Kali Linux](docs/linux/kali-linux.md), [Metasploitable 3](docs/security/metasploitable3.md) |

## Skills Demonstrated

- Segmented VMware networking with bridged, host-only, NAT, and isolated LAN segments
- pfSense DHCP, firewall, WAN/LAN separation, and subnet troubleshooting
- Active Directory promotion, DNS integration, and domain client joins
- Group Policy scope troubleshooting and client-side verification
- Linux static networking with netplan
- Multi-homed Kali configuration for isolated ARP/TCP reachability validation and Nmap service discovery
- Troubleshooting DHCP conflicts, APIPA, subnet mismatches, DNS typos, installer issues, and GPO scope errors