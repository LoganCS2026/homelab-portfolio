# Windows Server 2022

Windows Server 2022 provides Active Directory, DNS, and Group Policy management for `lab.local`.

## Configuration

| Setting | Value |
| --- | --- |
| Network | VMnet1 / MainLAN |
| Static IP | 192.168.1.10 |
| Gateway | 192.168.1.1 |
| DNS | 192.168.1.10 |
| Domain | lab.local |
| NetBIOS name | LAB |
| DC hostname | WIN-JEEASK82S6D |
| Forest functional level | Windows Server 2016 |
| Domain functional level | Windows Server 2016 |

## Implemented

- Configured static IP `192.168.1.10/24`
- Installed Active Directory Domain Services
- Promoted the server to Domain Controller
- Created the `lab.local` forest
- Installed DNS during promotion
- Configured the server as a Global Catalog
- Joined Win11Pro-1, Win11Pro-2, and Win11Pro-3 to `lab.local`
- Created and managed the `Test-Wallpaper` GPO

## Verification

| Check | Result |
| --- | --- |
| `Get-ADDomain` | Confirmed `lab.local`, `LAB`, and `Windows2016Domain` |
| `nslookup lab.local` | Resolved to `192.168.1.10` |
| `dcdiag /q` | Returned only the DFSR event warning after SYSVOL creation |
| Win11Pro-1 domain join | Successful |
| Win11Pro-2 domain join | Successful |
| Win11Pro-3 domain join | Successful across VPN |
| Win11Pro-3 domain logon | `LAB\Alex` authenticated successfully |
| `nltest /dsgetdc:lab.local` from Win11Pro-3 | Returned `WIN-JEEASK82S6D.lab.local` |
| `%logonserver%` from Win11Pro-3 | Returned `\\WIN-JEEASK82S6D` |
| Group Policy application | Successful on MainLAN and BranchLAN clients |

## Troubleshooting

| Issue | Root Cause | Fix |
| --- | --- | --- |
| Windows Server installer could not find Microsoft Software License Terms | VMware Easy Install injected an `autoinst.flp` floppy image that conflicted with the evaluation ISO | Removed the floppy device and restarted the install manually |
| DNS delegation warning during promotion | New forest with no parent DNS zone | Left DNS delegation unchecked and verified DNS after promotion |
| `dcdiag /q` showed DFSREvent warning | New single-Domain Controller lab shortly after SYSVOL creation | Documented as expected for the current lab state |
| BranchLAN-to-DC ping initially failed | Windows Server 2022 VM was powered off | Powered on the server and confirmed BranchLAN could reach `192.168.1.10` |