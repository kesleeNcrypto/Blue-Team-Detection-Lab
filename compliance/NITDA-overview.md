# NITDA Directive — Technical Response

## Overview

Recent cybersecurity directives from NITDA require Ministries, Departments, and Agencies (MDAs) to strengthen their security posture through improved monitoring, detection, and incident response capabilities.

This document outlines how this lab simulates those requirements using a practical SOC detection pipeline.

---

## Core Requirements from NITDA

- Centralized log monitoring  
- Continuous threat detection  
- Access control hardening  
- Incident detection and response capability  
- Alignment with NCPS 2021  

---

## Lab Implementation Mapping

| NITDA Requirement | Implementation in This Lab |
|------------------|---------------------------|
| Centralized monitoring | Wazuh + Splunk log aggregation |
| Threat detection | Suricata IDS + Cowrie honeypot |
| Incident detection | SIEM alerts and correlation |
| Response capability | Documented workflows + alert triage |
| Framework alignment | MITRE ATT&CK + NIST CSF + NCPS |

---

## Detection Pipeline Alignment

This lab simulates a real SOC pipeline:

1. Attack simulation (Kali Linux)  
2. Network detection (Suricata)  
3. Application telemetry (Cowrie)  
4. Log aggregation (Wazuh)  
5. SIEM visibility (Splunk)  
6. Alert analysis and correlation  

---

## Gap Analysis (Current vs Next Phase)

| Area | Current Status | Next Step |
|------|---------------|-----------|
| Network detection | Implemented (Suricata) | Expand custom detection rules |
| Application monitoring | Implemented (Cowrie) | Add more attack scenarios |
| SIEM correlation | Active (Wazuh/Splunk) | Improve alert tuning |
| Automated response | In progress (n8n) | Complete response workflows |
| Threat intelligence | Planned | Integrate threat feeds |
| Compliance reporting | In progress | Generate structured reports |

---

## Key Insight

Security directives define *what must be done*.

Detection engineering defines *how it is actually implemented*.

This lab focuses on bridging that gap by translating policy requirements into observable detection and response behavior.
