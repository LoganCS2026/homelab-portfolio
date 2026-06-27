# Group Policy

A test Group Policy Object was created to verify that `lab.local` can push policy to domain-joined Windows clients.

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
- Ran `gpupdate /force` on both clients
- Confirmed both clients applied the wallpaper

## Verification

| Client | Result |
| --- | --- |
| Win11Pro-1 | Wallpaper changed after policy refresh |
| Win11Pro-2 | Wallpaper changed after policy refresh |

## What This Demonstrates

- Created a Group Policy Object
- Edited User Configuration policy settings
- Linked and relinked a GPO
- Identified user-scope versus computer-scope behavior
- Forced policy refresh with `gpupdate /force`
- Verified client-side policy application