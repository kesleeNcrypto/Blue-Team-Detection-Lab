# Detection Mapping: SSH Brute-Force

## Incident Summary

A controlled SSH brute-force simulation was launched from Kali Linux against the Cowrie SSH honeypot on port 2222.

The activity was observed across multiple telemetry layers:

- **Suricata** detected network-level scanning and brute-force behavior
- **Cowrie** recorded connection attempts and failed authentication activity
- **Wazuh** aggregated and normalized alerts for security monitoring
- **jq** was used to manually inspect and correlate structured log data

This scenario demonstrates how a single attack can be validated across network, application, and SIEM layers.

---

## Detection to Framework Mapping

| Detection / Signal | Source | Framework Mapping | Relevance | Suggested Response |
|---|---|---|---|---|
| SSH scan / service probing | Suricata | **MITRE ATT&CK:** T1046 Network Service Discovery | Adversary identifies reachable services before access attempts | Alert analyst, validate target exposure, review source IP activity |
| Repeated SSH authentication attempts | Cowrie | **MITRE ATT&CK:** T1110 Brute Force / T1110.001 Password Guessing | Repeated failed login attempts indicate credential attack behavior | Investigate source, monitor session behavior, document pattern |
| SSH remote access targeting | Cowrie / Suricata | **MITRE ATT&CK:** T1021.004 Remote Services: SSH | Confirms focus on SSH as attack path | Review SSH exposure, restrict access, harden authentication |
| Multi-source alert correlation | Wazuh | **NIST CSF:** DE.AE Security Continuous Monitoring / Event Analysis | Improves confidence by correlating multiple telemetry sources | Escalate confirmed malicious activity for triage |
| Deception-based attacker observation | Cowrie | **MITRE D3FEND:** Decoy Systems / Deception | Captures attacker interaction without exposing production systems | Preserve logs, analyze behavior, refine detections |
| Suspicious login abuse pattern | Cowrie / Wazuh | **MITRE F3:** Credential Abuse / Account Takeover scenario alignment | Maps brute-force activity to fraud and abuse use cases | Flag account abuse risk, enrich detections for repeated login anomalies |
| Continuous log monitoring | Wazuh / Splunk | **NCPS 2021:** Monitoring, logging, incident detection alignment | Supports centralized visibility and response readiness | Retain evidence, support incident reporting and review |

---

## Evidence Sources

### Suricata
- `eve.json`
- Alert signatures related to SSH scanning or brute-force behavior
- Source IP and timestamp used for correlation

### Cowrie
- Session and authentication logs
- Failed login attempts
- Username and password attempt visibility
- Session metadata for attacker behavior analysis

### Wazuh
- Aggregated security alerts
- Correlated events across monitored sources
- SIEM-style visibility for triage and validation

### jq Analysis
- Structured parsing of JSON logs
- Manual verification of timestamps and source IP alignment
- Cross-layer confirmation of the same activity

---

## Correlation Logic

The attack was validated through:

- **source IP matching**
- **timestamp proximity**
- **shared attack context across tools**

This confirmed that the same SSH brute-force activity was independently observed at different layers of the detection pipeline.

---

## Architecture Alignment

| Tool | Role in Detection Pipeline | Compliance / Detection Value |
|---|---|---|
| Kali Linux | Attack simulation source | Generates controlled adversary activity for validation |
| Suricata | Network-layer detection | Detects scanning and suspicious SSH traffic |
| Cowrie | Application-layer deception | Captures attacker interaction and failed login attempts |
| Wazuh | Aggregation and alert correlation | Supports centralized monitoring and triage |
| Splunk | Enterprise visibility layer | Extends SIEM use case and searchable alert analysis |
| jq | Manual log inspection | Validates raw telemetry without relying only on dashboards |

---

## Response Workflow

1. Detect suspicious SSH activity in **Suricata**
2. Review corresponding session behavior in **Cowrie**
3. Confirm related alerts in **Wazuh**
4. Validate timestamps and source IPs using raw logs
5. Classify activity as brute-force / credential abuse
6. Document attack pattern and framework mappings
7. Update detection content or response logic if needed

---

## Detection Engineering Insight

This scenario highlights an important SOC principle:

**A single alert is not enough. Confirmed detection quality comes from correlated telemetry.**

In this lab:

- **Suricata** provided network evidence
- **Cowrie** provided attacker interaction context
- **Wazuh** improved operational visibility
- **jq** supported raw-log validation

That combination produces a stronger signal than relying on any one tool alone.

---

## Why This Mapping Matters

This mapping shows that the lab is not only detecting attacks, but also:

- aligning detections to recognized security frameworks
- translating attack behavior into incident handling context
- demonstrating how practical SOC telemetry supports compliance goals
- positioning the project for enterprise, public-sector, and regulated security discussions
