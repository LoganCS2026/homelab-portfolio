# Network Design

Small multi-site VMware lab with MainLAN, BranchLAN, IPsec VPN, isolated testing, and bridged WAN access.

<img src="../assets/network-topology.png" alt="Network topology" width="850">

## Network Segments

| Segment | Purpose | Subnet |
| --- | --- | --- |
| VMnet0 | Bridged WAN access through the physical network | Home network |
| VMnet1 | MainLAN | 192.168.1.0/24 |
| BranchLAN | Branch office LAN | 192.168.2.0/24 |
| VMnet8 | Isolated testing network | 192.168.80.0/24 |

## Main Site

| Setting | Value |
| --- | --- |
| Router | pfSense #1 |
| LAN IP | 192.168.1.1/24 |
| DHCP scope | 192.168.1.100-192.168.1.199 |
| Domain | lab.local |
| Domain Controller / DNS | 192.168.1.10 |
| Linux infrastructure server | 192.168.1.20 |
| VMware network | VMnet1 |
| VMware DHCP | Disabled |

Windows Server 2022 provides Active Directory and DNS for `lab.local`.

## Branch Site

| Setting | Value |
| --- | --- |
| Router | pfSense #2 |
| LAN IP | 192.168.2.1/24 |
| DHCP scope | 192.168.2.100-192.168.2.199 |
| DHCP DNS server | 192.168.1.10 |
| VMware network | BranchLAN |
| VMware network type | LAN segment |

BranchLAN simulates a separate office network connected to MainLAN through IPsec VPN.

## Site-to-Site VPN

| Setting | Value |
| --- | --- |
| VPN type | pfSense IPsec |
| Key exchange | IKEv2 |
| MainLAN subnet | 192.168.1.0/24 |
| BranchLAN subnet | 192.168.2.0/24 |
| Main Site peer | 192.168.50.159 |
| Branch Site peer | 192.168.50.84 |
| Encryption | AES-256 |
| Hash | SHA256 |
| DH / PFS group | Group 14 |
| NAT/BINAT | None |

BranchLAN reaches the Domain Controller/DNS server at `192.168.1.10` across the VPN.

## Testing Network

| Setting | Value |
| --- | --- |
| VMware network | VMnet8 |
| Subnet | 192.168.80.0/24 |
| Kali VMnet8 address | 192.168.80.134 |
| Metasploitable 3 address | 192.168.80.133 |

Kali uses a second adapter on VMnet8 to test against Metasploitable 3 without placing the vulnerable target on MainLAN or BranchLAN.

## Systems

| System | Network | Addressing | Role |
| --- | --- | --- | --- |
| pfSense #1 | VMnet1 / VMnet0 | 192.168.1.1 | Main Site gateway and IPsec peer |
| pfSense #2 | BranchLAN / VMnet0 | 192.168.2.1 | Branch gateway and IPsec peer |
| Windows Server 2022 | VMnet1 | 192.168.1.10 | Domain Controller and DNS |
| Ubuntu Server | VMnet1 | 192.168.1.20 | Linux infrastructure |
| Win11Pro-1 | VMnet1 | DHCP | Domain-joined workstation |
| Win11Pro-2 | VMnet1 | DHCP | Domain-joined workstation |
| Win11Pro-3 | BranchLAN | DHCP | Domain-joined branch workstation |
| Kali Linux | VMnet1 + VMnet8 | DHCP / 192.168.80.134 | Testing workstation |
| Metasploitable 3 | VMnet8 | 192.168.80.133 | Vulnerable target |

## Design Decisions

- VMnet1 DHCP is disabled in VMware so pfSense #1 is the only DHCP authority.
- Windows Server uses a static IP so AD and DNS are stable.
- Ubuntu uses a static IP so Docker and logging services can be added later.
- BranchLAN uses a VMware LAN segment to simulate a separate site.
- BranchLAN clients use the MainLAN Domain Controller for DNS across the VPN.
- Separate Active Directory sites and subnets are not configured yet. Current domain tests use `Default-First-Site-Name`.