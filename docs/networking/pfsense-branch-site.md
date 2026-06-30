# pfSense #2 - Branch Site Router

pfSense #2 is the Branch Site gateway, DHCP authority, firewall, and IPsec peer for BranchLAN.

## Configuration

| Setting | Value |
| --- | --- |
| WAN | VMnet0 / Bridged |
| WAN IP | 192.168.50.84 |
| LAN | BranchLAN |
| LAN IP | 192.168.2.1/24 |
| DHCP scope | 192.168.2.100-192.168.2.199 |
| DHCP DNS server | 192.168.1.10 |
| VMware network type | LAN segment |
| Block private networks on WAN | Disabled |
| Block bogon networks on WAN | Enabled |

## BranchLAN Role

BranchLAN simulates a separate office network connected to MainLAN through IPsec VPN.

| System | Network | Status |
| --- | --- | --- |
| pfSense #2 | BranchLAN | Gateway, DHCP authority, and IPsec peer |
| Win11Pro-3 | BranchLAN | Domain-joined branch workstation |

## Site-to-Site VPN

| Setting | Value |
| --- | --- |
| VPN type | IPsec |
| Key exchange | IKEv2 |
| Local peer | 192.168.50.84 |
| Remote peer | 192.168.50.159 |
| Local subnet | 192.168.2.0/24 |
| Remote subnet | 192.168.1.0/24 |
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
| Source | 192.168.1.0/24 |
| Destination | 192.168.2.0/24 |
| Purpose | Allow MainLAN to BranchLAN over IPsec |

## DNS Handoff

BranchLAN DHCP provides `192.168.1.10` as DNS.

Win11Pro-3 uses the MainLAN Domain Controller/DNS server to resolve `lab.local` across the VPN.

## Verification

- Win11Pro-3 received a `192.168.2.x` lease from pfSense #2
- Win11Pro-3 used `192.168.2.1` as its gateway and DHCP server
- Win11Pro-3 received `192.168.1.10` as its DNS server
- IPsec tunnel established with pfSense #1
- pfSense #2 reached pfSense #1 LAN at `192.168.1.1`
- pfSense #2 reached the Domain Controller at `192.168.1.10`
- Win11Pro-3 resolved `lab.local` to `192.168.1.10`
- Win11Pro-3 joined `lab.local`
- Win11Pro-3 logged in as `LAB\Alex`
- Win11Pro-3 applied the `Test-Wallpaper` GPO across the VPN

## Troubleshooting

| Issue | Fix |
| --- | --- |
| Host could not reach the pfSense #2 web GUI after LAN segment placement | Temporarily allowed WAN admin access from console using `pfSsh.php playback enableallowallwan` |
| Temporary WAN access was unsafe to leave enabled | Deleted the WAN allow rules after setup and reset firewall states |
| BranchLAN-to-Domain Controller ping initially failed | Powered on the Windows Server 2022 VM, then confirmed pfSense #2 could reach `192.168.1.10` |