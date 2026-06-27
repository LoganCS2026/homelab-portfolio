# Verification Screenshots

Selected screenshots used to verify network segmentation, DHCP behavior, host addressing, and isolated testing.

## VMware Virtual Networks

<img src="../assets/screenshots/vmware-virtual-networks.png" alt="VMware Virtual Network Editor showing VMnet0, VMnet1, and VMnet8" width="850">

VMnet0 provides bridged WAN access, VMnet1 is the Main Site LAN with VMware DHCP disabled, and VMnet8 is the isolated testing network.

## Main Site DHCP

<img src="../assets/screenshots/pfsense-main-site-dhcp.png" alt="pfSense Main Site DHCP lease for Win11Pro-1" width="850">

pfSense #1 issued a `192.168.1.x` DHCP lease on the Main Site LAN.

## Branch Site DHCP

<img src="../assets/screenshots/pfsense-branch-site-dhcp.png" alt="pfSense Branch Site DHCP lease for Win11Pro-3" width="850">

pfSense #2 issued a `192.168.2.x` DHCP lease on BranchLAN.

## Branch Workstation IP Configuration

<img src="../assets/screenshots/win11-branch-ipconfig.png" alt="Win11Pro-3 ipconfig output showing BranchLAN network settings" width="850">

Win11Pro-3 received BranchLAN addressing with `192.168.2.1` as its gateway and DHCP server.

## Ubuntu Server Network Verification

<img src="../assets/screenshots/ubuntu-network-verification.png" alt="Ubuntu Server network verification commands" width="850">

Ubuntu Server confirmed Main Site addressing, gateway reachability, internet access, and DNS resolution.

## Kali to Metasploitable 3 Reachability

<img src="../assets/screenshots/kali-metasploitable-reachability.png" alt="Kali Linux reachability and Nmap scan against Metasploitable 3" width="850">

Kali confirmed ARP reachability and TCP service discovery against Metasploitable 3 on VMnet8.