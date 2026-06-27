# Windows Server 2022

Windows Server 2022 provides Active Directory, DNS, and Group Policy management for the `lab.local` domain.

## Configuration

| Setting | Value |
| --- | --- |
| Network | VMnet1 / Main Site LAN |
| Static IP | 192.168.1.10 |
| Gateway | 192.168.1.1 |
| DNS | 192.168.1.10 |
| Domain | lab.local |
| NetBIOS name | LAB |
| Forest functional level | Windows Server 2016 |
| Domain functional level | Windows Server 2016 |

## Implemented

- Configured static IP `192.168.1.10/24`
- Installed Active Directory Domain Services
- Promoted the server to Domain Controller
- Created the `lab.local` forest
- Installed DNS during promotion
- Configured the server as a Global Catalog
- Used the server to join Win11Pro-1 and Win11Pro-2 to the domain
- Created and managed the `Test-Wallpaper` GPO

## Verification

| Check | Result |
| --- | --- |
| `Get-ADDomain` | Confirmed `lab.local`, `LAB`, and `Windows2016Domain` |
| `nslookup lab.local` | Resolved to `192.168.1.10` |
| `dcdiag /q` | Returned only the DFSR event warning after SYSVOL creation |
| Win11Pro-1 domain join | Successful |
| Win11Pro-2 domain join | Successful |
| Group Policy application | Successful on both domain-joined clients |

## Troubleshooting

| Issue | Root Cause | Fix |
| --- | --- | --- |
| Windows Server installer could not find Microsoft Software License Terms | VMware Easy Install injected an `autoinst.flp` floppy image that conflicted with the evaluation ISO | Removed the floppy device and restarted the install manually |
| DNS delegation warning during promotion | New forest with no parent DNS zone | Left DNS delegation unchecked and verified DNS after promotion |
| `dcdiag /q` showed DFSREvent warning | New single-Domain Controller lab shortly after SYSVOL creation | Documented as expected for the current lab state |