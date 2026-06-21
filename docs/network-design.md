# Network Design

This homelab is built in VMware Workstation Pro and uses segmented virtual networks to simulate a small enterprise-style environment with a main site, a branch site, and dedicated security testing systems.

## Network Segments

| Network   | Purpose                                                    | Subnet          |
| --------- | ---------------------------------------------------------- | --------------- |
| VMnet0    | Bridged WAN access to the physical network                 | Home network    |
| VMnet1    | MainSite LAN behind pfSense #1                             | 192.168.1.0/24  |
| BranchLAN | Branch office LAN behind pfSense #2                        | 192.168.2.0/24  |
| VMnet8    | NAT network reserved for isolated testing/future expansion | 192.168.80.0/24 |

## MainSite

pfSense #1 is the main router and firewall for the primary network.

* LAN IP: 192.168.1.1/24
* DHCP scope: 192.168.1.100-192.168.1.199
* Network: VMnet1
* VMware DHCP: Disabled
* Purpose: Central routing, DHCP, DNS forwarding, and firewall control for the main systems

## Branch Site

pfSense #2 is the branch office router.

* LAN IP: 192.168.2.1/24
* DHCP scope: 192.168.2.100-192.168.2.199
* Network: BranchLAN
* Purpose: A remote office network that will later connect back to the main site through a site-to-site VPN

## Design Notes

VMware DHCP is disabled on VMnet1 so pfSense #1 remains the only DHCP authority for the main LAN. This prevents DHCP conflicts and better simulates a real network where routing and IP assignment are controlled by the firewall.

The BranchLAN segment is intentionally separate from the host system so that branch access requires routing, firewall rules, or a site-to-site VPN instead of simple direct host access.
