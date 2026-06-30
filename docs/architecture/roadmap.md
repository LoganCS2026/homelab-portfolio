# Project Roadmap

## Completed

- Built segmented VMware networks for MainLAN, BranchLAN, and isolated testing
- Configured pfSense #1 as Main Site gateway, firewall, and DHCP authority
- Configured pfSense #2 as Branch Site gateway, firewall, and DHCP authority
- Disabled VMware DHCP on VMnet1 to prevent DHCP authority conflicts
- Corrected VMnet1 to match the intended `192.168.1.0/24` subnet
- Deployed Windows Server 2022, three Windows 11 Pro clients, Ubuntu Server, Kali Linux, and Metasploitable 3
- Assigned static IPs to Windows Server 2022 and Ubuntu Server
- Promoted Windows Server 2022 to Domain Controller for `lab.local`
- Installed DNS during Domain Controller promotion
- Updated MainLAN DHCP so domain clients use `192.168.1.10` for DNS
- Created test domain users for client authentication testing
- Created a Workstations OU for future client organization
- Joined Win11Pro-1 and Win11Pro-2 to `lab.local`
- Verified domain logons on both MainLAN Windows clients
- Created and applied the `Test-Wallpaper` GPO
- Resolved the GPO scope issue by linking the user policy at the domain root
- Configured IPsec VPN between pfSense #1 and pfSense #2
- Allowed routed traffic between `192.168.1.0/24` and `192.168.2.0/24`
- Updated BranchLAN DHCP so clients use `192.168.1.10` for DNS
- Joined Win11Pro-3 to `lab.local` from BranchLAN
- Verified Win11Pro-3 domain logon with `LAB\Alex`
- Verified Group Policy application on Win11Pro-3 across the VPN
- Verified domain controller discovery from BranchLAN with `nltest`
- Verified Win11Pro-3 logon server as `WIN-JEEASK82S6D`
- Verified Kali-to-Metasploitable reachability with ARP and TCP service discovery

## Next

- Deploy Docker-based services on Ubuntu Server
- Forward pfSense and Windows logs to Ubuntu
- Generate Kali test traffic and correlate firewall and endpoint logs