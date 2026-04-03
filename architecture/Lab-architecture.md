# Lab Architecture

## Purpose

This document describes the architecture of the Blue Team Detection Lab, including
host roles, network segmentation, sensor placement, and data flow.

The architecture was intentionally designed to reflect real-world SOC and on-prem
defensive environments where visibility is limited, tooling is constrained, and
detections must be validated across multiple telemetry sources.

---

## High-Level Design

The lab consists of two virtual machines operating within an isolated virtual network:

- **Attacker VM:** Kali Linux
- **Defender / Sensor VM:** Ubuntu Server

Both systems communicate over a **Host-Only Adapter**, ensuring:
- No internet exposure
- No external noise
- Controlled and repeatable attack traffic

---

## Network Topology

- **Network Mode:** Host-Only Adapter
- **IP Addressing:** Private RFC1918 space
- **Traffic Scope:** East–West only (attacker → defender)

This setup mirrors internal enterprise segments where attackers have already gained
a foothold and lateral movement or service abuse is the primary concern.

---

## Component Roles

### Kali Linux (Attacker)

- Simulates adversarial behavior
- Generates controlled SSH reconnaissance and authentication attempts
- Represents a compromised internal host or red team activity

### Ubuntu Server (Defender / Sensor)

Acts as both a detection sensor and a deception host:

#### Suricata (Network Layer)
- Inspects live network traffic on the primary interface
- Detects SSH scanning and brute-force patterns
- Generates structured alerts in `eve.json`

#### Cowrie (Application Layer)
- Exposes a fake SSH service on a non-standard port (2222)
- Records authentication attempts and session behavior
- Provides high-fidelity attacker intent and interaction data

---

## Data Flow

1. Attacker initiates SSH traffic from Kali
2. Traffic traverses the isolated host-only network
3. Suricata inspects packets and generates network-level alerts
4. Cowrie processes SSH connections and logs application-layer events
5. Logs are analyzed and correlated using structured JSON parsing (`jq`)

This dual-sensor visibility enables validation of alerts across independent telemetry
sources.

---

## Detection Philosophy

The architecture intentionally separates:
- **Detection (Suricata)** from
- **Behavioral observation (Cowrie)**

This mirrors real SOC designs where:
- IDS tools provide early warning
- Endpoint or service telemetry provides confirmation and context

The overlap between these layers increases confidence in detections and reduces false positives.

---

## Design Constraints

The lab was built under the following constraints:

- Limited or intermittent internet access
- No external SIEM or managed services
- Manual log analysis and correlation

These constraints were intentional and reflect operational realities in many environments.

---

## Scalability Considerations

This architecture can be extended to include:

- Additional honeypot services (HTTP, FTP)
- Automated correlation rules
- SIEM ingestion (ELK, Splunk)
- Alert enrichment and scoring
- Multiple attacker sources

The current design prioritizes clarity, signal quality, and analyst reasoning.

---

## Summary

This architecture supports realistic blue team workflows by combining:
- Network-layer detection
- Application-layer telemetry
- Controlled attack simulation
- Log-driven correlation

The focus is not on tool quantity, but on detection accuracy, validation, and operational thinking.
