# Investigation: Detection Analysis & Log Correlation

## Objective

This document demonstrates how malicious SSH activity was detected, validated, and correlated across both network-layer and application-layer telemetry using Suricata and Cowrie.

The objective was to validate detection accuracy by confirming that multiple independent sensors observed the same adversarial behavior.

---

## Environment Context

- **Attacker:** Kali Linux  
- **Defender / Victim :** Ubuntu Server  
- **Network Mode:** Host-Only Adapter (isolated)  
- **IDS:** Suricata  
- **Honeypot:** Cowrie (SSH on port 2222)

All activity occurred in a controlled, non-internet-facing environment to preserve signal clarity.

---

## Attack Execution Summary

The attacker initiated SSH-based reconnaissance and authentication attempts against the Cowrie service.

Example attack command executed from Kali Linux:

```bash
ssh -p 2222 root@192.168.56.101
```

This simulates a common real-world scenario involving enumeration of non-standard SSH ports and credential guessing against exposed services.


## Network-Layer Detection (Suricata)

Suricata monitored live traffic on the primary interface and generated alerts related to SSH activity.


### Alert Extraction

Alerts were extracted directly from Suricata’s structured JSON output:

```bash
sudo jq 'select(.alert != null)' /var/log/suricata/eve.json
```


### Observed Indicators

* SSH connection attempts targeting port 2222
* Source IP consistent with the Kali attacker
* Timestamps aligned with attack execution

These alerts confirmed network-level visibility of the attack.

---
## Application-Layer Telemetry (Cowrie)

Cowrie captured detailed session-level telemetry from the same attacker.

### Failed Authentication Events

```bash
jq 'select(.eventid=="cowrie.login.failed")' var/log/cowrie/cowrie.json
```

Captured fields included:

* `src_ip`
* `username`
* `password`
* `timestamp`
* `session`

### Command Interaction Events

```bash
jq 'select(.eventid=="cowrie.command.input")' var/log/cowrie/cowrie.json
```

These events demonstrate attacker interaction within the honeypot environment.

---
## Cross-Layer Correlation

Correlation was performed manually to validate detection accuracy.

### Correlation Keys Used

* Source IP address
* Timestamp proximity
* Target service (SSH / port 2222)

### Result

Both Suricata and Cowrie independently observed:

* The same source IP
* The same time window
* The same SSH activity

This confirmed that network alerts were true positives and that application-layer telemetry validated the IDS signal.

---

## Detection Logic Validation

This lab demonstrates a core SOC principle:

> **One alert is a signal. Multiple corroborating alerts are evidence.**

Suricata provided early network detection, while Cowrie delivered high-fidelity behavioral context.

---

## MITRE ATT&CK Mapping

Observed activity mapped to the following techniques:

* **T1110** — Brute Force
* **T1021.004** — Remote Services: SSH

---

## Analyst Takeaways

* Structured logs (`eve.json`, Cowrie JSON) enable powerful analysis without a SIEM
* `jq` is sufficient for early-stage detection engineering and alert triage
* Cross-layer correlation reduces false positives and increases analyst confidence
* Honeypots provide attacker intent, not just alert volume

---

## Future Enhancements

Planned improvements include:

* Automated correlation rules
* SIEM ingestion (ELK / Splunk)
* Alert enrichment and scoring
* Additional honeypot services

---

## Why This Matters

This analysis mirrors real SOC workflows including alert review, validation, context enrichment, and behavioral analysis.

The focus is on operational decision-making rather than tool output alone.

---

## Redaction Note

All IP addresses, usernames, and credentials shown are from a controlled lab environment and do not represent real systems or users.


