# Metasploitable 3

Metasploitable 3 is the vulnerable target VM used for isolated testing from Kali Linux.

## Network Placement

| Setting | Value |
| --- | --- |
| Network | VMnet8 |
| IP address | 192.168.80.133 |
| Testing workstation | Kali Linux |
| Kali VMnet8 address | 192.168.80.134 |

Metasploitable 3 is kept on VMnet8 so testing traffic stays separate from MainLAN and BranchLAN systems.

## Verification

- Kali reached the target through VMnet8
- ARP confirmed Layer 2 reachability
- Nmap confirmed TCP service discovery
- ICMP ping failed, but TCP scans confirmed the host was reachable

## Confirmed Services

Nmap identified exposed services including:

- SSH
- IIS 7.5
- GlassFish 4.0
- Additional Windows services

## Current Role

Metasploitable 3 provides a controlled target for later log collection, firewall visibility, and detection practice once centralized logging is deployed.