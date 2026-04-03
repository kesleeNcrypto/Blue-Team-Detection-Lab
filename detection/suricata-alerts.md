# Suricata Alerts

## Purpose
This file documents how Suricata was used in the lab to detect network-based attacker activity.

## Detection Source
- Tool: Suricata
- Log format: EVE JSON
- Role: Network intrusion detection

## Observed Activity
- SSH scan activity
- Suspicious connection attempts
- Traffic generated from the Kali attacker system

## Example Detection Logic
Suricata inspected live traffic on the monitored interface and generated alerts based on enabled IDS signatures.

## Output
Relevant alerts were written to structured JSON logs for review and correlation.

## Security Value
Suricata provided network-layer visibility and helped validate malicious behavior before deeper application-level review.
