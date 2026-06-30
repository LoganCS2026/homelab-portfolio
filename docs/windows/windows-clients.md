# Windows Client Systems

Three Windows 11 Pro clients simulate Main Site and Branch Site endpoints.

## Client Status

| System | Network | Domain Status | Verification |
| --- | --- | --- | --- |
| Win11Pro-1 | VMnet1 | Joined to `lab.local` | Logged in as `LAB\John`, received GPO |
| Win11Pro-2 | VMnet1 | Joined to `lab.local` | Logged in as `LAB\Sarah`, received GPO |
| Win11Pro-3 | BranchLAN | Joined to `lab.local` | Logged in as `LAB\Alex`, received GPO across VPN |

## DNS

Main Site and Branch Site clients use the Domain Controller for DNS.

| Setting | Value |
| --- | --- |
| Domain DNS server | 192.168.1.10 |
| Domain | lab.local |
| Main Site gateway | 192.168.1.1 |
| Branch gateway | 192.168.2.1 |
| Branch DHCP DNS server | 192.168.1.10 |

## Implemented

- Joined Win11Pro-1 to `lab.local`
- Joined Win11Pro-2 to `lab.local`
- Joined Win11Pro-3 to `lab.local` across the IPsec VPN
- Verified domain user logons on MainLAN and BranchLAN clients
- Applied the `Test-Wallpaper` GPO to MainLAN and BranchLAN clients
- Verified Win11Pro-3 domain controller discovery from BranchLAN

## Verification

| Check | Result |
| --- | --- |
| Win11Pro-1 logon | `LAB\John` authenticated successfully |
| Win11Pro-2 logon | `LAB\Sarah` authenticated successfully |
| Win11Pro-3 logon | `LAB\Alex` authenticated successfully |
| Win11Pro-3 `whoami` | `lab\alex` |
| Win11Pro-3 `gpupdate /force` | Computer and user policy updated successfully |
| Win11Pro-3 `gpresult /r` | `Test-Wallpaper` applied |
| Win11Pro-3 `nltest /dsgetdc:lab.local` | Returned `WIN-JEEASK82S6D.lab.local` |
| Win11Pro-3 `%logonserver%` | Returned `\\WIN-JEEASK82S6D` |

## Troubleshooting

| Issue | Fix |
| --- | --- |
| Win11Pro-1 initially received an address from the wrong subnet | Corrected VMnet1 and disabled VMware DHCP |
| Win11Pro-2 received an APIPA address | Started pfSense #1 so the client could receive a DHCP lease |
| Win11Pro-3 needed Branch isolation | Moved the VM to BranchLAN instead of host-only networking |
| Host-side VMnet1 IP conflicted with pfSense #1 | Changed the Windows host VMnet1 adapter away from `192.168.1.1` |
| Win11Pro-3 needed domain access from BranchLAN | Configured IPsec routing and BranchLAN DNS to `192.168.1.10` |