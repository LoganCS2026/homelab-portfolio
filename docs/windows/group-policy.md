# Group Policy

A test Group Policy Object was created to verify policy delivery to domain-joined Windows clients.

## Test GPO

| Setting | Value |
| --- | --- |
| GPO name | Test-Wallpaper |
| Domain | lab.local |
| Policy type | User Configuration |
| Policy path | Administrative Templates / Desktop / Desktop |
| Setting | Desktop Wallpaper |
| Wallpaper path | C:\Windows\Web\Wallpaper\Windows\img0.jpg |
| Style | Fill |

## Scope Issue

The GPO was first linked to the Workstations OU. It did not apply because the configured setting was under User Configuration, and the test users were not in that OU.

User Configuration follows user object scope unless loopback processing is configured.

## Fix

- Removed the Workstations OU link
- Linked `Test-Wallpaper` at the `lab.local` domain root
- Ran `gpupdate /force` on the clients
- Confirmed the clients applied the wallpaper

## Verification

| Client | User | Result |
| --- | --- | --- |
| Win11Pro-1 | `LAB\John` | Wallpaper changed after policy refresh |
| Win11Pro-2 | `LAB\Sarah` | Wallpaper changed after policy refresh |
| Win11Pro-3 | `LAB\Alex` | Wallpaper changed after policy refresh across VPN |

## BranchLAN Validation

| Check | Result |
| --- | --- |
| `gpupdate /force` | Computer and user policy updated successfully |
| `gpresult /r` | `Test-Wallpaper` listed under Applied Group Policy Objects |
| Policy source | `WIN-JEEASK82S6D.lab.local` |

## Skills

- Created a Group Policy Object
- Edited User Configuration policy settings
- Linked and relinked a GPO
- Identified user-scope versus computer-scope behavior
- Forced policy refresh with `gpupdate /force`
- Verified local and cross-VPN Group Policy processing