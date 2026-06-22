# pfSense #2 - Branch Site Router

pfSense #2 is the Branch Site router for this VMware IT infrastructure homelab. It provides the gateway and DHCP service for the isolated BranchLAN network.

## Role

pfSense #2 currently provides:

* BranchLAN gateway
* DHCP service for the BranchLAN subnet
* Network separation between the branch workstation and the MainSite LAN
* A future endpoint for site-to-site VPN configuration with pfSense #1

## Network Interfaces

| Interface | Network                 | Purpose                                               |
| --------- | ----------------------- | ----------------------------------------------------- |
| WAN       | VMnet0 / Bridged        | Provides upstream access through the physical network |
| LAN       | BranchLAN / LAN segment | Isolated branch office network                        |

## LAN Configuration

| Setting             | Value                       |
| ------------------- | --------------------------- |
| LAN subnet          | 192.168.2.0/24              |
| LAN gateway         | 192.168.2.1                 |
| DHCP scope          | 192.168.2.100-192.168.2.199 |
| VMware network type | LAN segment                 |

The BranchLAN network is intentionally separated from the host system and the MainSite LAN. This keeps the branch network isolated until routing, firewall rules, or site-to-site VPN connectivity are configured.

## Connected Systems

The BranchLAN network currently includes:

* Windows 11 Pro branch workstation

## Verification

Branch Site configuration was verified by checking:

* pfSense #2 LAN interface assignment
* BranchLAN DHCP lease assignment
* Correct default gateway
* Correct subnet placement
* VMware adapter placement
* Windows 11 Pro branch workstation network configuration

## Troubleshooting Performed

The host PC could not directly reach the BranchLAN network after pfSense #2 was installed because BranchLAN is an isolated VMware LAN segment.

Temporary WAN web access was enabled only long enough to complete the pfSense setup wizard. After setup was complete, the temporary WAN allow rules were removed and firewall states were reset so management access returned to LAN-only behavior.

## Planned Improvements

Planned improvements for pfSense #2 include:

* Configure site-to-site VPN connectivity with pfSense #1
* Allow controlled traffic between BranchLAN and MainSite
* Test branch workstation access to domain services
* Document VPN tunnel verification results
* Forward pfSense logs to a centralized logging platform
