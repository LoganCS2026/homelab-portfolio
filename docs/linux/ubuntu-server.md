# Ubuntu Server

Ubuntu Server is the Main Site Linux infrastructure server. It is static-addressed for future Docker services and centralized logging.

## Configuration

| Setting | Value |
| --- | --- |
| Network | VMnet1 / Main Site LAN |
| Interface | ens33 |
| IP address | 192.168.1.20/24 |
| Gateway | 192.168.1.1 |
| Initial DNS | 192.168.1.1 |
| Future lab DNS | 192.168.1.10 |

## Implemented

- Connected Ubuntu Server to VMnet1
- Identified the network interface as `ens33`
- Configured static addressing with netplan
- Verified gateway reachability
- Verified internet reachability
- Verified DNS resolution

## Verification

| Check | Result |
| --- | --- |
| `ip addr` | Confirmed `192.168.1.20/24` on `ens33` |
| `ip route` | Confirmed default route through `192.168.1.1` |
| Gateway ping | Confirmed reachability to pfSense #1 |
| Internet ping | Confirmed external reachability |
| DNS lookup | Confirmed name resolution |

## Next Integration

- Docker-based internal services
- Centralized logging
- pfSense log collection
- Windows event log collection
- Internal web services for lab testing