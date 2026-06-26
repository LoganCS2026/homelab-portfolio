# Project Roadmap

Core VM deployment is complete. The lab is now focused on infrastructure configuration, domain services, routing, logging, and controlled security testing.

## Completed

* Built segmented VMware networks for Main Site, BranchLAN, and isolated testing
* Configured pfSense #1 as the Main Site router, firewall, and DHCP authority
* Configured pfSense #2 as the Branch Site router, firewall, and DHCP authority
* Deployed Windows Server 2022
* Deployed three Windows 11 Pro clients
* Deployed Ubuntu Server
* Deployed Kali Linux
* Deployed Metasploitable 3
* Verified Main Site DHCP behavior
* Verified BranchLAN DHCP behavior
* Verified Kali-to-target reachability on the testing network

## Planned Improvements

* Assign stable addressing for infrastructure servers
* Configure Windows Server 2022 for Active Directory Domain Services
* Configure DNS for the lab domain
* Create test users, groups, and organizational units
* Join Windows 11 clients to the domain
* Configure and test Group Policy
* Configure site-to-site VPN between Main Site and BranchLAN
* Deploy Docker-based services on Ubuntu Server
* Forward pfSense and Windows logs to centralized logging
* Generate authorized test traffic from Kali Linux
* Correlate test traffic with firewall and endpoint logs