# Cowrie Logs

## Purpose
This file documents how Cowrie was used in the lab to capture attacker interaction at the application layer.

## Detection Source
- Tool: Cowrie
- Role: SSH honeypot
- Port: 2222

## Observed Activity
- SSH connection attempts
- Failed login attempts
- Username and password trial activity
- Source IP capture
- Session metadata

## Logging Value
Cowrie provided direct visibility into attacker behavior and complemented Suricata's network-level detections.

## Correlation Use
Cowrie logs were compared with Suricata alerts using:
- Source IP address
- Timestamp proximity

## Security Value
Cowrie made it possible to observe adversary behavior beyond simple network alerts, improving investigation depth and realism.
