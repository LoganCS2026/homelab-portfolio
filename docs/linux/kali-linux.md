# Kali Linux

Kali Linux is the testing workstation for lab-owned targets.

## Network Placement

| Adapter | Network | Addressing | Purpose |
| --- | --- | --- | --- |
| Adapter 1 | VMnet1 | 192.168.1.103 | MainLAN access |
| Adapter 2 | VMnet8 | 192.168.80.134 | Isolated testing access |

## Target Access

| Target | Network | IP |
| --- | --- | --- |
| Metasploitable 3 | VMnet8 | 192.168.80.133 |

Kali reaches Metasploitable 3 through VMnet8 without placing the vulnerable target on MainLAN or BranchLAN.

## Verification

- Confirmed Kali has interfaces on VMnet1 and VMnet8
- Confirmed ARP reachability to Metasploitable 3
- Confirmed TCP service discovery with Nmap
- Confirmed ICMP failure did not prevent TCP validation

## Nmap Findings

Nmap confirmed multiple exposed services on Metasploitable 3, including:

- SSH
- IIS 7.5
- GlassFish 4.0
- Additional filtered or exposed Windows services

## Notes

ICMP ping failed because the target blocks or filters ICMP. Reachability was validated through ARP and TCP service discovery instead.