# Network Design

This lab uses segmented VMware networks to simulate a small multi-site environment with a MainSite LAN, Branch Site LAN, NAT testing network, and bridged WAN access.

## Network Segments

| Network | Purpose | Subnet |
| --- | --- | --- |
| VMnet0 | Bridged WAN access through the physical network | Home network |
| VMnet1 | MainSite LAN | 192.168.1.0/24 |
| BranchLAN | Branch Site LAN | 192.168.2.0/24 |
| VMnet8 | NAT network for isolated testing | 192.168.80.0/24 |

## MainSite

| Setting | Value |
| --- | --- |
| Router | pfSense #1 |
| LAN IP | 192.168.1.1/24 |
| DHCP scope | 192.168.1.100-192.168.1.199 |
| Network | VMnet1 |
| VMware DHCP | Disabled |

MainSite hosts the primary Windows, Linux, and security systems. pfSense #1 provides gateway, DHCP, DNS forwarding, and firewall control for this network.

## Branch Site

| Setting | Value |
| --- | --- |
| Router | pfSense #2 |
| LAN IP | 192.168.2.1/24 |
| DHCP scope | 192.168.2.100-192.168.2.199 |
| Network | BranchLAN |
| VMware network type | LAN segment |

BranchLAN is isolated from the host and MainSite networks. Access between BranchLAN and MainSite will require routing, firewall rules, or a site-to-site VPN.

## Design Notes

VMware DHCP is disabled on VMnet1 so pfSense #1 remains the only DHCP authority for the MainSite LAN.

BranchLAN uses a VMware LAN segment to simulate a separate branch office network instead of a directly reachable host-only network.