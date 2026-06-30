# Active Directory

Windows Server 2022 is promoted as the Domain Controller for `lab.local`.

## Domain Configuration

| Setting | Value |
| --- | --- |
| Domain | lab.local |
| NetBIOS domain | LAB |
| Domain Controller | Windows Server 2022 |
| Domain Controller hostname | WIN-JEEASK82S6D |
| Domain Controller IP | 192.168.1.10 |
| Forest functional level | Windows Server 2016 |
| Domain functional level | Windows Server 2016 |
| DNS installed during promotion | Yes |
| Global Catalog | Enabled |
| DSRM password | Redacted from public documentation |

`lab.local` was used instead of `homelab.arpa` to avoid overlapping with the pfSense DHCP domain value.

## Current AD Structure

| Object Type | Current State |
| --- | --- |
| Domain users | Test users created for client logon validation |
| Workstations OU | Created for workstation organization and future GPO targeting |
| Default Users container | Holds current test users |
| Default Computers container | Holds joined computer objects before OU organization |

## Test Users

| User | Purpose |
| --- | --- |
| John | Win11Pro-1 domain logon test |
| Sarah | Win11Pro-2 domain logon test |
| Alex | Win11Pro-3 branch domain logon test |

## DNS

| DNS Item | Value |
| --- | --- |
| Domain | lab.local |
| DNS server | 192.168.1.10 |
| Main Site client DNS | 192.168.1.10 |
| Branch Site client DNS | 192.168.1.10 |
| Main Site gateway | 192.168.1.1 |
| Branch Site gateway | 192.168.2.1 |

DHCP provides `192.168.1.10` as client DNS for domain resolution.

## AD Sites

| Setting | Current State |
| --- | --- |
| DC Site Name | Default-First-Site-Name |
| Branch client site | Default-First-Site-Name |
| Separate AD sites/subnets | Not configured yet |

The VPN validates routed branch access to Active Directory. Separate AD Sites and Services design has not been implemented yet.

## Verification

| Command / Test | Result |
| --- | --- |
| `Get-ADDomain` | Confirmed `lab.local`, `LAB`, DomainSID, and Windows Server 2016 domain mode |
| `nslookup lab.local` | Resolved to `192.168.1.10` |
| `dcdiag /q` | Returned only the DFSR event warning after SYSVOL creation |
| Win11Pro-1 logon | `LAB\John` authenticated successfully |
| Win11Pro-2 logon | `LAB\Sarah` authenticated successfully |
| Win11Pro-3 logon | `LAB\Alex` authenticated successfully across VPN |
| `nltest /dsgetdc:lab.local` from Win11Pro-3 | Returned `WIN-JEEASK82S6D.lab.local` |
| `%logonserver%` from Win11Pro-3 | Returned `\\WIN-JEEASK82S6D` |

## Troubleshooting

| Issue | Explanation / Fix |
| --- | --- |
| DNS delegation warning during promotion | Expected for a new forest with no parent DNS zone |
| Incorrect pfSense DNS entry | Corrected `192.169.1.10` to `192.168.1.10` |
| Branch workstation needed domain access | Resolved with IPsec VPN and BranchLAN DNS set to `192.168.1.10` |