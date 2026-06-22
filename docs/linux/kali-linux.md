# Kali Linux

Kali Linux is the controlled security assessment workstation for this VMware IT infrastructure homelab. It is used for authorized lab testing, packet capture, and future security monitoring practice.

## Role

Kali Linux is used for:

* Authorized scanning and vulnerability validation against lab-owned targets
* Packet capture and traffic analysis
* Future SIEM and log-correlation testing

## VMware Configuration

| Setting           | Value                      |
| ----------------- | -------------------------- |
| Platform          | VMware Workstation Pro     |
| Operating system  | Kali Linux Rolling         |
| Deployment method | Official Kali VMware image |
| VM name           | Kali                       |
| CPU               | 2 vCPU                     |
| Memory            | 4 GB                       |
| Disk              | Prebuilt Kali VMware disk  |
| Primary network   | VMnet1 / MainSite LAN      |

## Network Placement

| Setting                 | Value            |
| ----------------------- | ---------------- |
| Primary network segment | VMnet1           |
| MainSite subnet         | 192.168.1.0/24   |
| Gateway                 | 192.168.1.1      |
| DHCP authority          | pfSense #1       |
| Primary IPv4 address    | 192.168.1.103/24 |

Kali Linux is connected to the MainSite LAN behind pfSense #1. This keeps security testing activity inside the controlled homelab network.

## Current State

Completed work includes:

* Deployed Kali Linux from the official VMware image
* Connected Kali to the MainSite VMnet1 network
* Adjusted VM hardware resources
* Completed system updates
* Resolved package, display, and cursor issues
* Replaced default Kali credentials
* Created a clean baseline state for future testing

## Verification

Kali Linux configuration was verified by checking:

* Correct VMnet1 placement and DHCP assignment
* Gateway, DNS, and internet connectivity
* open-vm-tools and VMware guest integration
* Functional graphical desktop and cursor behavior

## Troubleshooting Performed

During setup, the official Kali VMware image was opened through its extracted `.vmx` file instead of the New Virtual Machine Wizard because it was a prebuilt VM, not an installer ISO.

Package update failures were resolved by clearing corrupted cached package data, refreshing the package index, and repairing the broken package state.

A cursor/display issue was resolved by upgrading the VM hardware compatibility to Workstation 17.5 or later and recovering the graphical desktop session.

Default Kali credentials were replaced after setup. Passwords and private account details are intentionally omitted from this public documentation.

## Planned Improvements

Planned improvements for Kali Linux include:

* Run authorized scans against lab-owned targets
* Capture and review test traffic
* Generate controlled security events for centralized logging
* Correlate test traffic with pfSense and endpoint logs
* Document detection results after monitoring is configured
