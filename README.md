# Network Intrusion Detection System (NIDS) Using Snort 3

## Overview

A hands-on cybersecurity lab implementing a Network Intrusion Detection System (NIDS) with Snort 3, Ubuntu Server, Kali Linux, and Nmap in Oracle VirtualBox.

The project demonstrates custom rule development, packet inspection, controlled network testing, alert generation, and security event logging.

## Lab Architecture

| Component | Configuration |
|---|---|
| Host OS | Windows 11 |
| Virtualization | Oracle VirtualBox |
| IDS | Ubuntu Server 26.04 |
| IDS engine | Snort 3 |
| Testing machine | Kali Linux |
| Traffic generation | Nmap and ping |
| Ubuntu lab IP | 192.168.56.10 |
| Kali lab IP | 192.168.56.20 |
| Network | VirtualBox host-only |

The lab uses a private host-only network for testing. NAT is used for software updates and package downloads.

## Detection Rules

Three custom Snort rules were implemented:

- **SID 1000001 — ICMP detection:** Detects ICMP echo requests to the IDS.
- **SID 1000002 — TCP SYN detection:** Detects TCP SYN packets targeting SSH port 22.
- **SID 1000003 — Repeated TCP SYN detection:** Uses a detection filter to identify bursts of matching connection attempts from a source.

The Snort built-in `port_scan` inspector was also configured for testing.

## Testing Results

The following alert counts were observed in the saved Snort alert log during the lab tests:

| Test | SID | Observed alert count |
|---|---|---:|
| ICMP echo requests | 1000001 | 8 |
| TCP SYN attempts to SSH | 1000002 | 2 |
| Repeated TCP SYN attempts | 1000003 | 158 |

These are alert counts, not counts of unique attacks. The repeated-SYN rule can generate multiple alerts during one scan.

No matching GID 122 built-in port-scan alerts were found in the log checked during this test. The inspector's detection behavior remains a possible future improvement.

## Alert Logging

Snort alerts were saved to:

`/var/log/snort/alert_fast.txt`

Representative logs are included in the `logs/` directory after review and sanitization.

## Skills Demonstrated

- Linux server administration
- VirtualBox network configuration
- Snort 3 installation and configuration
- Custom IDS rule development
- TCP/IP traffic analysis
- Nmap-based testing in an isolated lab
- Security alert logging and troubleshooting
- Technical documentation

## Future Improvements

- Tune and validate built-in port-scan detection
- Add JSON alert logging
- Analyze packet captures using Wireshark
- Build an alert dashboard
- Automate setup and repeatable testing

## References

- [Snort 3 Documentation](https://docs.snort.org/)
- [Kali Linux](https://www.kali.org/)
- [Nmap Documentation](https://nmap.org/book/)
- [Oracle VirtualBox](https://www.virtualbox.org/)

