# Metasploitable 3

Metasploitable 3 is the vulnerable Windows Server target. It is used for controlled scanning, service discovery, and detection practice from Kali Linux.

## Role

* Authorized testing against a lab-owned vulnerable system
* Vulnerability scanning
* Service discovery and validation
* Security monitoring and log-correlation testing

## Platform Configuration

| Setting | Value |
| --- | --- |
| Platform | VMware Workstation Pro |
| Deployment method | Vagrant with VMware Desktop provider |
| Target system | Metasploitable 3 win2k8 |
| VM management | Vagrant-managed, visible in VMware Workstation |
| Network | VMnet8 / VMware NAT |

## Network Placement

| System | Network | Purpose |
| --- | --- | --- |
| Metasploitable 3 | VMnet8 / VMware NAT | Vulnerable target |
| Kali Linux | VMnet1 / Main Site LAN | Primary lab access |
| Kali Linux secondary adapter | VMnet8 / VMware NAT | Testing access to target |

Metasploitable 3 is isolated on VMnet8. Kali uses a second VMnet8 adapter to reach the target while keeping its primary Main Site connection.

## Current State

* Installed Vagrant and required VMware provider components
* Deployed the Metasploitable 3 win2k8 target
* Added the generated VM to VMware Workstation for visibility
* Connected Metasploitable 3 to VMnet8
* Added a second Kali adapter on VMnet8
* Verified Kali-to-target reachability
* Confirmed service discovery against exposed target services
* Baseline state created for later testing

## Verification

* Vagrant-managed VM state
* VMware Workstation visibility
* VMnet8 network placement
* Kali access to the VMnet8 testing subnet
* ARP reachability from Kali
* TCP reachability from Kali
* Initial service discovery against exposed target services

ICMP did not respond, but ARP and TCP checks confirmed the target was reachable.

## Troubleshooting Performed

Required Vagrant and VMware provider components were missing from the host system. These were installed so Vagrant could deploy the Metasploitable 3 VM through VMware Workstation.

The default Rapid7 Vagrantfile included multiple targets, so only the Windows target was selected.

Metasploitable 3 did not initially appear in the normal VMware library because Vagrant created it inside its workspace structure. The generated VM configuration was opened in VMware Workstation while keeping Vagrant management intact.

Kali could not initially reach Metasploitable 3 because Kali was on VMnet1 while the target was on VMnet8. A second Kali network adapter was added to VMnet8.

ICMP testing failed after network placement was corrected, so reachability was confirmed through ARP and TCP service checks.

## Planned Improvements

* Run controlled scans from Kali Linux
* Document discovered services and findings
* Generate security events for centralized logging
* Correlate test traffic with pfSense and endpoint logs
* Build detection and remediation notes from findings