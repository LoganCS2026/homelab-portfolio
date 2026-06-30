# Site-to-Site IPsec VPN

pfSense IPsec VPN connects MainLAN and BranchLAN for DNS, domain join, domain logon, and GPO processing.

## Networks

| Site | Router | LAN subnet | LAN IP | WAN peer |
| --- | --- | --- | --- | --- |
| Main Site | pfSense #1 | 192.168.1.0/24 | 192.168.1.1 | 192.168.50.159 |
| Branch Site | pfSense #2 | 192.168.2.0/24 | 192.168.2.1 | 192.168.50.84 |

## Phase 1

| Setting | Value |
| --- | --- |
| Key exchange | IKEv2 |
| Protocol | IPv4 |
| Interface | WAN |
| Authentication | Mutual PSK |
| Encryption | AES-256 |
| Hash | SHA256 |
| DH group | Group 14 |
| Lifetime | 28800 |

Pre-shared key omitted.

## Phase 2

| Site | Local network | Remote network |
| --- | --- | --- |
| pfSense #1 | 192.168.1.0/24 | 192.168.2.0/24 |
| pfSense #2 | 192.168.2.0/24 | 192.168.1.0/24 |

| Setting | Value |
| --- | --- |
| Mode | Tunnel IPv4 |
| Protocol | ESP |
| Encryption | AES-256 |
| Hash | SHA256 |
| PFS group | Group 14 |
| Lifetime | 3600 |
| NAT/BINAT | None |

## Firewall Rules

### pfSense #1

| Setting | Value |
| --- | --- |
| Interface | IPsec |
| Action | Pass |
| Protocol | Any |
| Source | 192.168.2.0/24 |
| Destination | 192.168.1.0/24 |
| Description | Allow BranchLAN to MainLAN over IPsec |

### pfSense #2

| Setting | Value |
| --- | --- |
| Interface | IPsec |
| Action | Pass |
| Protocol | Any |
| Source | 192.168.1.0/24 |
| Destination | 192.168.2.0/24 |
| Description | Allow MainLAN to BranchLAN over IPsec |

## BranchLAN DNS

| Setting | Value |
| --- | --- |
| Branch DHCP server | 192.168.2.1 |
| Branch DHCP DNS server | 192.168.1.10 |
| Domain DNS server | 192.168.1.10 |
| Domain | lab.local |

Win11Pro-3 received `192.168.1.10` as DNS and resolved `lab.local` across the VPN.

## Validation

| Check | Result |
| --- | --- |
| pfSense #1 to pfSense #2 WAN | Successful |
| pfSense #2 to pfSense #1 WAN | Successful |
| IPsec tunnel status | Established |
| Child SA status | Connected |
| pfSense #1 LAN to pfSense #2 LAN | Successful |
| pfSense #2 LAN to Domain Controller | Successful |
| Win11Pro-3 DNS for `lab.local` | Resolved to `192.168.1.10` |
| Win11Pro-3 domain join | Successful |
| Win11Pro-3 domain logon | `LAB\Alex` |
| `whoami` | `lab\alex` |
| `gpupdate /force` | Computer and user policy updated successfully |
| `gpresult /r` | `Test-Wallpaper` applied |
| `nltest /dsgetdc:lab.local` | Returned `WIN-JEEASK82S6D.lab.local` |
| `%logonserver%` | `\\WIN-JEEASK82S6D` |

## Troubleshooting

| Issue | Fix |
| --- | --- |
| BranchLAN-to-Domain Controller ping initially failed | Powered on the Windows Server 2022 VM, then confirmed pfSense #2 could reach `192.168.1.10` |

## Result

Win11Pro-3 reached MainLAN over IPsec, used `192.168.1.10` for DNS, joined `lab.local`, logged in as `LAB\Alex`, discovered the DC, and applied Group Policy.