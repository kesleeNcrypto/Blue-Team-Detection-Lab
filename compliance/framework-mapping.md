# Framework Mapping — Detection Pipeline Alignment

## Overview

This document maps the Blue Team Detection Lab to key cybersecurity frameworks to demonstrate how real-world detection pipelines align with:

- **NIST Cybersecurity Framework (CSF)**
- **MITRE ATT&CK**
- **MITRE D3FEND**
- **MITRE F3 (Fraud Framework)**
- **Nigeria Cybersecurity Policy & Strategy (NCPS 2021)**

The goal is to bridge:

**Attack Activity → Detection → Correlation → Response → Compliance**

---

## 1. NIST CSF Mapping

| Function | Category | Implementation in Lab |
|----------|----------|----------------------|
| Identify | Asset Management | Defined lab assets (Kali, Ubuntu, services) |
| Protect | Access Control | SSH exposure via controlled honeypot |
| Detect | DE.CM (Monitoring) | Suricata IDS network monitoring |
| Detect | DE.AE (Analysis) | Wazuh alert correlation |
| Respond | RS.AN (Analysis) | Log investigation using jq |
| Respond | RS.RP (Response Planning) | Documented response workflows |

---

## 2. MITRE ATT&CK Mapping

| Technique ID | Technique | Lab Simulation |
|--------------|----------|----------------|
| T1046 | Network Service Discovery | Nmap scanning |
| T1110 | Brute Force | SSH brute-force attempts |
| T1110.001 | Password Guessing | Repeated login attempts |
| T1021.004 | Remote Services (SSH) | Targeting Cowrie SSH service |
| T1078 | Valid Accounts | Credential abuse simulation |

---

## 3. MITRE D3FEND Mapping

| Defensive Technique | Implementation |
|--------------------|---------------|
| Decoy Systems | Cowrie SSH honeypot |
| Network Traffic Analysis | Suricata IDS |
| Intrusion Detection | Signature-based alerting |
| Event Correlation | Wazuh SIEM aggregation |

---

## 4. MITRE F3 (Fraud Mapping)

| Fraud Scenario | Lab Representation |
|---------------|-------------------|
| Account Takeover | SSH brute-force attempts |
| Credential Abuse | Repeated login failures |
| Suspicious Access | Unknown IP login attempts |
| Behavior Monitoring | Session tracking via Cowrie |

---

## 5. NCPS 2021 Mapping

| Requirement | Lab Implementation |
|-------------|-------------------|
| Continuous Monitoring | Suricata + Wazuh |
| Log Management | Centralized logging (Wazuh / Splunk) |
| Incident Detection | Alert generation and correlation |
| Threat Visibility | Multi-layer telemetry (network + application) |
| Response Capability | Documented SOC workflow |

---

## Detection Pipeline Summary

This lab demonstrates a complete detection pipeline:

1. Attack generation (Kali Linux)
2. Network detection (Suricata)
3. Application telemetry (Cowrie)
4. Log aggregation (Wazuh)
5. SIEM visibility (Splunk)
6. Alert analysis and correlation

---

## Key Insight

Frameworks define structure.

Detection pipelines create visibility.

Effective security comes from aligning both.

This lab demonstrates how detection engineering enables organizations to move from compliance requirements to operational security capability.
