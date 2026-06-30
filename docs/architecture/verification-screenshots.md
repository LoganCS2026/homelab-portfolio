# Verification Screenshots

Selected screenshots used to verify network segmentation, DHCP behavior, VPN connectivity, domain access, Group Policy, and isolated testing.

## VMware Virtual Networks

<img src="../assets/screenshots/vmware-virtual-networks.png" alt="VMware Virtual Network Editor showing VMnet0, VMnet1, and VMnet8" width="850">

VMnet0 provides bridged WAN access, VMnet1 is MainLAN with VMware DHCP disabled, and VMnet8 is the isolated testing network.

## Main Site DHCP

<img src="../assets/screenshots/pfsense-main-site-dhcp.png" alt="pfSense Main Site DHCP lease for Win11Pro-1" width="850">

pfSense #1 issued a `192.168.1.x` DHCP lease on MainLAN.

## Branch Site DHCP

<img src="../assets/screenshots/pfsense-branch-site-dhcp.png" alt="pfSense Branch Site DHCP lease for Win11Pro-3" width="850">

pfSense #2 issued a `192.168.2.x` DHCP lease on BranchLAN.

## Branch Workstation IP Configuration

<img src="../assets/screenshots/win11-branch-ipconfig.png" alt="Win11Pro-3 ipconfig output showing BranchLAN IP, gateway, DHCP, and DNS settings" width="850">

Win11Pro-3 received BranchLAN addressing with `192.168.2.1` as its gateway and `192.168.1.10` as its DNS server.

## IPsec Tunnel Status

<img src="../assets/screenshots/pfsense-ipsec-status.png" alt="pfSense IPsec status showing established tunnel and installed Phase 2" width="850">

pfSense shows the BranchLAN-to-MainLAN IPsec tunnel as established with Phase 2 installed.

## Branch DNS Validation

<img src="../assets/screenshots/win11-branch-dns-validation.png" alt="Win11Pro-3 nslookup and ping validation for lab.local and 192.168.1.10" width="850">

Win11Pro-3 resolved `lab.local` to `192.168.1.10` and reached the Domain Controller across the VPN.

## Branch Domain Validation

<img src="../assets/screenshots/win11-branch-domain-validation.png" alt="Win11Pro-3 whoami, user domain, and computer name validation" width="850">

Win11Pro-3 authenticated as `lab\alex` on the `LAB` domain.

## Branch Group Policy Result

<img src="../assets/screenshots/win11-branch-gpresult.png" alt="Win11Pro-3 gpresult output showing Test-Wallpaper applied" width="850">

`gpresult /r` confirmed the `Test-Wallpaper` GPO applied to `LAB\Alex` on Win11Pro-3.

## Branch Domain Controller Discovery

<img src="../assets/screenshots/win11-branch-nltest-logonserver.png" alt="Win11Pro-3 nltest and logonserver output showing Domain Controller discovery" width="850">

Win11Pro-3 located `WIN-JEEASK82S6D.lab.local` and confirmed `\\WIN-JEEASK82S6D` as the logon server.

## Ubuntu Server Network Verification

<img src="../assets/screenshots/ubuntu-network-verification.png" alt="Ubuntu Server network verification commands" width="850">

Ubuntu Server confirmed MainLAN addressing, gateway reachability, internet access, and DNS resolution.

## Kali to Metasploitable 3 Reachability

<img src="../assets/screenshots/kali-metasploitable-reachability.png" alt="Kali Linux reachability and Nmap scan against Metasploitable 3" width="850">

Kali confirmed ARP reachability and TCP service discovery against Metasploitable 3 on VMnet8.