### Alert Logging and Scan Detection Results

Snort 3 was configured to write alerts to `/var/log/snort/alert_fast.txt`.

During a controlled Nmap TCP SYN scan from Kali Linux (`192.168.56.20`) to the Ubuntu IDS (`192.168.56.10`), the custom repeated-SYN detection rule (SID `1000003`) generated multiple alerts.

This demonstrates successful custom rule-based detection and persistent alert logging in the isolated VirtualBox lab.

**Built-in port-scan inspector:** To be documented separately after confirming whether a native inspector alert was recorded.

**Evidence:** `screenshots/05-snort-logs.png` and `logs/sample-alerts.txt`.
## Test Results

The Snort 3 IDS was tested in an isolated VirtualBox lab using Kali Linux as the traffic-generation machine and Ubuntu Server as the IDS sensor.

| Test | Rule SID | Observed alerts | Result |
|---|---|---:|---|
| ICMP echo requests | 1000001 | 8 | Passed |
| TCP SYN attempts to SSH | 1000002 | 2 | Passed |
| Repeated TCP SYN activity | 1000003 | 158 | Passed |
| Built-in port-scan inspector | GID 122 | 0 matching events found | Further verification required |

### Findings

- Snort successfully detected ICMP echo requests and TCP SYN traffic.
- The custom repeated-SYN rule generated multiple alerts during the controlled Nmap scan.
- Alerts were saved to `/var/log/snort/alert_fast.txt`.
- The built-in port-scan inspector did not produce a matching event in the inspected log. Its configuration and detection behavior require further verification.

### Lab Safety

All scan tests were performed against the project's own Ubuntu VM on a private VirtualBox host-only network.

### Evidence

- `screenshots/05-snort-logs.png`
- `rules/local.rules`
- `logs/sample-alerts.txt`

