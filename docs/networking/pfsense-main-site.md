# pfSense #1 - Main Site Router

pfSense #1 is the Main Site gateway, DHCP authority, firewall, and WAN router for VMnet1.

## Configuration

| Setting | Value |
| --- | --- |
| WAN | VMnet0 / Bridged |
| LAN | VMnet1 / Host-only |
| LAN IP | 192.168.1.1/24 |
| DHCP scope | 192.168.1.100-192.168.1.199 |
| DHCP DNS server | 192.168.1.10 |
| VMware DHCP on VMnet1 | Disabled |

## Static Mappings

| System | Hostname | IP Address | Role |
| --- | --- | --- | --- |
| Windows Server 2022 | winsrv | 192.168.1.10 | Domain Controller and DNS |
| Ubuntu Server | ubuntusrv | 192.168.1.20 | Linux infrastructure |

Windows Server and Ubuntu Server use stable addresses so AD, DNS, Docker, and logging services can be referenced consistently.

## DNS Handoff

After Windows Server was promoted to Domain Controller, pfSense #1 DHCP was updated to hand out `192.168.1.10` as the DNS server.

This allows Main Site clients to resolve `lab.local` and locate domain services.

## Verification

- Main Site clients receive `192.168.1.x` leases from pfSense #1
- Windows Server is reachable at `192.168.1.10`
- Ubuntu Server is reachable at `192.168.1.20`
- Domain clients use `192.168.1.10` for DNS

## Troubleshooting

| Issue | Fix |
| --- | --- |
| VMnet1 did not match the intended Main Site subnet | Reconfigured VMnet1 for `192.168.1.0/24` |
| VMware DHCP conflicted with pfSense DHCP | Disabled VMware DHCP on VMnet1 |
| Clients pulled incorrect leases | Confirmed pfSense #1 as the only DHCP authority |
| DNS server was entered as `192.169.1.10` | Corrected it to `192.168.1.10` |