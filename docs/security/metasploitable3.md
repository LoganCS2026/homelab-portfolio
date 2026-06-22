# Metasploitable 3

Metasploitable 3 is the intentionally vulnerable Windows Server target for this VMware IT infrastructure homelab. It is used for controlled scanning, service discovery, and future detection practice from Kali Linux.

## Role

Metasploitable 3 is used for:

* Authorized testing against a lab-owned vulnerable system
* Vulnerability scanning practice
* Service discovery and validation
* Future security monitoring and log-correlation testing

## Platform Configuration

| Setting             | Value                                          |
| ------------------- | ---------------------------------------------- |
| Platform            | VMware Workstation Pro                         |
| Deployment method   | Vagrant with VMware Desktop provider           |
| Target system       | Metasploitable 3 win2k8                        |
| VM management       | Vagrant-managed, visible in VMware Workstation |
| Network             | VMnet8 / VMware NAT                            |
| Target IPv4 address | 192.168.80.133                                 |

## Network Placement

| System                       | Network               | IPv4 Address     | Purpose                  |
| ---------------------------- | --------------------- | ---------------- | ------------------------ |
| Metasploitable 3             | VMnet8 / VMware NAT   | 192.168.80.133   | Vulnerable target        |
| Kali Linux                   | VMnet1 / MainSite LAN | 192.168.1.103/24 | Primary lab access       |
| Kali Linux secondary adapter | VMnet8 / VMware NAT   | 192.168.80.134   | Testing access to target |

Metasploitable 3 is isolated on VMnet8. Kali Linux keeps its primary MainSite connection through VMnet1 and uses a second adapter on VMnet8 to reach the vulnerable target.

## Current State

Completed work includes:

* Installed Vagrant and required VMware provider components
* Deployed the Metasploitable 3 win2k8 target
* Added the generated VM to VMware Workstation for visibility
* Connected Metasploitable 3 to VMnet8
* Added a second Kali adapter on VMnet8 for controlled testing access
* Verified Kali-to-target reachability
* Confirmed service discovery against exposed target services
* Created a clean baseline state for future testing

## Verification

Metasploitable 3 configuration was verified by checking:

* Vagrant-managed VM state
* VMware Workstation visibility
* VMnet8 network placement
* Kali access to the VMnet8 testing subnet
* ARP reachability from Kali
* TCP reachability from Kali
* Initial service discovery against exposed target services

ICMP ping did not respond, but ARP and TCP checks confirmed the target was reachable.

## Troubleshooting Performed

During deployment, required Vagrant and VMware provider components were missing from the host system. These were installed so Vagrant could deploy the Metasploitable 3 VM through VMware Workstation.

The default Rapid7 Vagrantfile included multiple targets, so only the Windows target was selected to avoid deploying unnecessary VMs.

Metasploitable 3 did not initially appear in the normal VMware library because Vagrant created it inside its own workspace structure. The generated VM configuration was opened in VMware Workstation while keeping Vagrant as the management method.

Kali could not initially reach Metasploitable 3 because Kali was on VMnet1 while the target was on VMnet8. A second Kali network adapter was added to VMnet8, giving Kali direct access to the testing subnet.

ICMP testing failed after network placement was corrected, so reachability was confirmed through ARP and TCP service checks.

## Planned Improvements

Planned improvements for Metasploitable 3 include:

* Run controlled scans from Kali Linux
* Document discovered services and findings
* Generate security events for centralized logging
* Correlate test traffic with pfSense and endpoint logs
* Build detection and remediation notes from findings
