# pfSense #2 - Branch Site Router

pfSense #2 is the Branch Site gateway, DHCP authority, firewall, and WAN router for BranchLAN.

## Configuration

| Setting | Value |
| --- | --- |
| WAN | VMnet0 / Bridged |
| LAN | BranchLAN |
| LAN IP | 192.168.2.1/24 |
| DHCP scope | 192.168.2.100-192.168.2.199 |
| VMware network type | LAN segment |

## BranchLAN Role

BranchLAN simulates a separate office network. It is isolated from the Main Site until VPN routing is configured.

| System | Network | Status |
| --- | --- | --- |
| pfSense #2 | BranchLAN | Gateway and DHCP authority |
| Win11Pro-3 | BranchLAN | Local-only workstation |

## Verification

- Win11Pro-3 received a `192.168.2.x` lease from pfSense #2
- Win11Pro-3 used `192.168.2.1` as its gateway and DHCP server
- BranchLAN remained isolated from the Main Site

## Troubleshooting

| Issue | Fix |
| --- | --- |
| Host could not reach the pfSense #2 web GUI after LAN segment placement | Temporarily allowed WAN admin access from console using `pfSsh.php playback enableallowallwan` |
| Temporary WAN access was unsafe to leave enabled | Deleted the WAN allow rules after setup and reset firewall states |
| Branch workstation cannot join `lab.local` | Site-to-site VPN is required before the Branch client can reach `192.168.1.10` |