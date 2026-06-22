# Project Roadmap

This homelab is currently in the baseline deployment stage. Core virtual machines are installed, segmented networks are configured, and initial connectivity has been verified.

## Completed

- Built segmented VMware networks for MainSite, BranchLAN, and isolated testing
- Configured pfSense #1 as the MainSite router, firewall, and DHCP authority
- Configured pfSense #2 as the BranchLAN router and DHCP authority
- Deployed Windows Server 2022, Windows 11 clients, Ubuntu Server, Kali Linux, and Metasploitable 3
- Verified BranchLAN DHCP and Kali-to-target reachability

## Planned Improvements

- Configure Windows Server 2022 as an Active Directory domain controller
- Join Windows 11 clients to the domain
- Configure site-to-site VPN between MainSite and BranchLAN
- Deploy Docker-based services on Ubuntu Server
- Forward pfSense and Windows logs to a central logging/SIEM platform
- Generate authorized test traffic from Kali Linux and correlate activity in logs
