# pfSense #2 - Branch Site Router

pfSense #2 is the Branch Site router. It provides gateway, DHCP, and network separation for the isolated BranchLAN segment.

## Role

* BranchLAN gateway
* DHCP service for the BranchLAN subnet
* Firewall control for the branch workstation
* Branch endpoint for site-to-site VPN configuration

## Network Interfaces

| Interface | Network | Purpose |
| --- | --- | --- |
| WAN | VMnet0 / Bridged | Upstream access through the physical network |
| LAN | BranchLAN / LAN segment | Isolated branch office network |

## LAN Configuration

| Setting | Value |
| --- | --- |
| LAN subnet | 192.168.2.0/24 |
| LAN gateway | 192.168.2.1 |
| DHCP scope | 192.168.2.100-192.168.2.199 |
| VMware network type | LAN segment |

## Verification

* pfSense #2 LAN interface assignment
* BranchLAN DHCP lease assignment
* Correct default gateway
* Correct subnet placement
* VMware adapter placement
* Branch workstation network configuration

## Troubleshooting Performed

The host PC could not directly reach BranchLAN after pfSense #2 was installed because BranchLAN is an isolated VMware LAN segment.

Temporary WAN web access was enabled long enough to complete the pfSense setup wizard. After setup, the temporary WAN allow rules were removed and firewall states were reset to restore LAN-only management behavior.

## Planned Improvements

* Configure site-to-site VPN connectivity with pfSense #1
* Allow controlled traffic between BranchLAN and MainSite
* Test branch workstation access to domain services
* Document VPN tunnel verification results
* Forward pfSense logs to centralized logging