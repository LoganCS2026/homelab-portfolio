# pfSense #1 - Main Site Router

pfSense #1 is the Main Site gateway, DHCP authority, firewall, and IPsec peer for VMnet1.

## Configuration

| Setting | Value |
| --- | --- |
| WAN | VMnet0 / Bridged |
| WAN IP | 192.168.50.159 |
| LAN | VMnet1 / Host-only |
| LAN IP | 192.168.1.1/24 |
| DHCP scope | 192.168.1.100-192.168.1.199 |
| DHCP DNS server | 192.168.1.10 |
| VMware DHCP on VMnet1 | Disabled |
| Block private networks on WAN | Disabled |
| Block bogon networks on WAN | Enabled |

## Static Mappings

| System | Hostname | IP Address | Role |
| --- | --- | --- | --- |
| Windows Server 2022 | WIN-JEEASK82S6D | 192.168.1.10 | Domain Controller and DNS |
| Ubuntu Server | ubuntusrv | 192.168.1.20 | Linux infrastructure |

Windows Server and Ubuntu Server use stable addresses so AD, DNS, Docker, and logging services can be referenced consistently.

## DNS Handoff

After Windows Server was promoted to Domain Controller, pfSense #1 DHCP was updated to hand out `192.168.1.10` as the DNS server.

MainLAN clients use `192.168.1.10` to resolve `lab.local`.

## Site-to-Site VPN

| Setting | Value |
| --- | --- |
| VPN type | IPsec |
| Key exchange | IKEv2 |
| Local peer | 192.168.50.159 |
| Remote peer | 192.168.50.84 |
| Local subnet | 192.168.1.0/24 |
| Remote subnet | 192.168.2.0/24 |
| Encryption | AES-256 |
| Hash | SHA256 |
| DH / PFS group | Group 14 |
| NAT/BINAT | None |

## IPsec Firewall Rule

| Setting | Value |
| --- | --- |
| Interface | IPsec |
| Action | Pass |
| Protocol | Any |
| Source | 192.168.2.0/24 |
| Destination | 192.168.1.0/24 |
| Purpose | Allow BranchLAN to MainLAN over IPsec |

## Verification

- MainLAN clients receive `192.168.1.x` leases from pfSense #1
- Windows Server is reachable at `192.168.1.10`
- Ubuntu Server is reachable at `192.168.1.20`
- Domain clients use `192.168.1.10` for DNS
- IPsec tunnel established with pfSense #2
- MainLAN can reach BranchLAN across the tunnel
- BranchLAN can reach the Domain Controller at `192.168.1.10`

## Troubleshooting

| Issue | Fix |
| --- | --- |
| VMnet1 did not match the intended MainLAN subnet | Reconfigured VMnet1 for `192.168.1.0/24` |
| VMware DHCP conflicted with pfSense DHCP | Disabled VMware DHCP on VMnet1 |
| Clients pulled incorrect leases | Confirmed pfSense #1 as the only DHCP authority |
| DNS server was entered as `192.169.1.10` | Corrected it to `192.168.1.10` |