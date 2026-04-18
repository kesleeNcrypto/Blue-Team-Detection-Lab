# Compliance Mapping

This section extends the Blue Team Detection Lab with a compliance and detection-engineering layer.

It connects observed attack activity in the lab to:

- **NIST CSF**
- **MITRE ATT&CK**
- **MITRE D3FEND**
- **MITRE F3**
- **NCPS 2021**

## Purpose

The goal is to show how practical detections can be mapped beyond alerts alone and tied to:

- security monitoring requirements
- adversary behavior
- defensive countermeasures
- fraud and abuse scenarios
- incident response workflows

## Included Mappings

### Detections
- [`ssh-bruteforce-mapping.md`](./detections/ssh-bruteforce-mapping.md)

## What This Adds to the Lab

- Compliance-aware detection engineering
- Clear mapping from attack activity to security frameworks
- Higher-fidelity documentation for SOC, detection, and governance use cases
- Stronger alignment with enterprise, public-sector, and regulated environments

## Scope

This compliance layer is based on real telemetry produced by the lab, including:

- **Suricata** network alerts
- **Cowrie** honeypot session logs
- **Wazuh** alert aggregation and correlation
- **Splunk** enterprise visibility
- **jq**-based log validation and manual analysis

## Notes

This extension is intentionally practical. It documents controls and mappings that are directly supported by the lab rather than making unsupported compliance claims.
