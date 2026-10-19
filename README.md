# Wazuh SIEM Monitoring & Detection Engineering Lab

## Overview

A hands-on Security Operations Center (SOC) project demonstrating
centralized Windows security monitoring, custom detection engineering,
controlled authentication attack simulation, and alert investigation
using Wazuh SIEM.

## Lab Architecture

- Hypervisor: Oracle VirtualBox
- SIEM Server: Ubuntu Server 24.04 LTS
- SIEM Platform: Wazuh 4.14.9
- Monitored Endpoint: Windows 11 Pro
- Wazuh Agent: 4.14.9
- Lab Network: Isolated VirtualBox internal network
- SIEM Server IP: 192.168.57.60
- Windows Endpoint IP: 192.168.57.101

### Monitoring Pipeline

Windows Security Event Log
    -> Wazuh Agent
    -> Wazuh Manager
    -> Custom Detection Rules
    -> Security Alerts
    -> SOC Investigation

## Detection Engineering

Three custom detection rules were implemented and validated.

| Rule ID | Detection | Severity |
|---------|-----------|----------|
| 100100 | Windows failed logon (Event ID 4625) | 8 |
| 100101 | Five failed logons for the same username within 60 seconds | 10 |
| 100102 | Successful network logon (Event ID 4624, Type 3) | 5 |

Custom rules are available in `rules/local_rules.xml`.

## Attack Simulation

Six failed network authentication attempts were generated
against a nonexistent Windows account using the Windows
LogonUser API through PowerShell.

Wazuh detected the individual authentication failures and
generated a severity-10 correlation alert.

The simulation was performed exclusively in an authorized
laboratory environment.

## Investigation Results

- Detection: Repeated failed authentication
- Windows Event ID: 4625
- Logon Type: 3 (Network)
- Status: 0xc000006d
- Substatus: 0xc0000064
- Root Cause: Authorized authentication simulation
- Outcome: True positive detection of simulated activity
- Confirmed Compromise: None

The complete investigation is documented in
`docs/incident-investigation.md`.

## Repository Structure

```text
wazuh-siem-monitoring/
├── README.md
├── rules/
│   └── local_rules.xml
├── evidence/
│   ├── authentication_attack_alerts.jsonl
│   └── successful_logon_alerts.jsonl
└── docs/
    └── incident-investigation.md
```

## Skills Demonstrated

- SIEM deployment and configuration
- Windows endpoint monitoring
- Windows Security Event Log analysis
- Custom Wazuh detection engineering
- Authentication failure correlation
- Controlled security testing
- Alert triage and investigation
- SOC incident documentation

## Security and Scope

All tests were conducted on personally controlled,
isolated virtual machines for educational and
defensive security purposes.
