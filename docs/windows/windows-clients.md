# Windows Client Systems

Three Windows 11 Pro clients simulate Main Site and Branch Site endpoints.

## Client Status

| System | Network | Domain Status | Verification |
| --- | --- | --- | --- |
| Win11Pro-1 | VMnet1 | Joined to `lab.local` | Logged in as `LAB\John`, received GPO |
| Win11Pro-2 | VMnet1 | Joined to `lab.local` | Logged in as `LAB\Sarah`, received GPO |
| Win11Pro-3 | BranchLAN | Not joined | Blocked until VPN routing exists |

## DNS

Main Site clients use the Domain Controller for DNS.

| Setting | Value |
| --- | --- |
| Domain DNS server | 192.168.1.10 |
| Domain | lab.local |
| Main Site gateway | 192.168.1.1 |
| Branch gateway | 192.168.2.1 |

## Implemented

- Joined Win11Pro-1 to `lab.local`
- Joined Win11Pro-2 to `lab.local`
- Verified domain user logons on both Main Site clients
- Applied the `Test-Wallpaper` GPO to both Main Site clients
- Kept Win11Pro-3 local-only because BranchLAN cannot reach the Domain Controller yet

## Verification

- Win11Pro-1 authenticated as `LAB\John`
- Win11Pro-2 authenticated as `LAB\Sarah`
- Both Main Site clients applied Group Policy after `gpupdate /force`
- Win11Pro-3 received BranchLAN addressing from pfSense #2

## Troubleshooting

| Issue | Fix |
| --- | --- |
| Win11Pro-1 initially received an address from the wrong subnet | Corrected VMnet1 and disabled VMware DHCP |
| Win11Pro-2 received an APIPA address | Started pfSense #1 so the client could receive a DHCP lease |
| Win11Pro-3 needed Branch isolation | Moved the VM to BranchLAN instead of host-only networking |
| Host-side VMnet1 IP conflicted with pfSense #1 | Changed the Windows host VMnet1 adapter away from `192.168.1.1` |
| Branch client cannot join the domain | VPN routing must be configured first |