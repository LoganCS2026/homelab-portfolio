# Active Directory

Windows Server 2022 is promoted as the Domain Controller for `lab.local`.

## Domain Configuration

| Setting | Value |
| --- | --- |
| Domain | lab.local |
| NetBIOS domain | LAB |
| Domain Controller | Windows Server 2022 |
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

## DNS

| DNS Item | Value |
| --- | --- |
| Domain | lab.local |
| DNS server | 192.168.1.10 |
| Main Site client DNS | 192.168.1.10 |
| Main Site gateway | 192.168.1.1 |

Main Site DHCP hands out the Domain Controller as DNS so clients can resolve `lab.local`.

## Verification

| Command / Test | Result |
| --- | --- |
| `Get-ADDomain` | Confirmed `lab.local`, `LAB`, DomainSID, and Windows Server 2016 domain mode |
| `nslookup lab.local` | Resolved to `192.168.1.10` |
| `dcdiag /q` | Returned only the DFSR event warning after SYSVOL creation |
| Win11Pro-1 logon | `LAB\John` authenticated successfully |
| Win11Pro-2 logon | `LAB\Sarah` authenticated successfully |

## Troubleshooting

| Issue | Explanation / Fix |
| --- | --- |
| DNS delegation warning during promotion | Expected for a new forest with no parent DNS zone |
| Incorrect pfSense DNS entry | Corrected `192.169.1.10` to `192.168.1.10` |
| Branch workstation cannot join domain | BranchLAN has no route to `192.168.1.10` until VPN is configured |