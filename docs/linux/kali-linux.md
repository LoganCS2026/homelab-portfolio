# Kali Linux

Kali Linux is the security assessment workstation. It is used for authorized lab testing, packet capture, and security monitoring validation.

## Role

* Authorized scanning and vulnerability validation against lab-owned targets
* Packet capture and traffic analysis
* Security event generation for centralized logging
* Detection testing after monitoring is configured

## VMware Configuration

| Setting | Value |
| --- | --- |
| Platform | VMware Workstation Pro |
| Operating system | Kali Linux Rolling |
| Deployment method | Official Kali VMware image |
| VM name | Kali |
| CPU | 2 vCPU |
| Memory | 4 GB |
| Disk | Prebuilt Kali VMware disk |
| Primary network | VMnet1 / Main Site LAN |

## Network Placement

| Setting | Value |
| --- | --- |
| Primary network segment | VMnet1 |
| Main Site subnet | 192.168.1.0/24 |
| Gateway | 192.168.1.1 |
| DHCP authority | pfSense #1 |

## Current State

* Deployed Kali Linux from the official VMware image
* Connected Kali to VMnet1
* Adjusted VM hardware resources
* Completed system updates
* Resolved package, display, and cursor issues
* Replaced default Kali credentials
* Baseline state created for later testing

## Verification

* VMnet1 placement and DHCP assignment
* Gateway, DNS, and internet connectivity
* open-vm-tools and VMware guest integration
* Functional graphical desktop and cursor behavior

## Troubleshooting Performed

The official Kali VMware image was opened through its extracted `.vmx` file because it was a prebuilt VM, not an installer ISO.

Package update failures were resolved by clearing corrupted cached package data, refreshing the package index, and repairing the broken package state.

A cursor/display issue was resolved by upgrading VM hardware compatibility to Workstation 17.5 or later and recovering the graphical desktop session.

## Planned Improvements

* Run authorized scans against lab-owned targets
* Capture and review test traffic
* Generate controlled security events for centralized logging
* Correlate test traffic with pfSense and endpoint logs
* Document detection results after monitoring is configured