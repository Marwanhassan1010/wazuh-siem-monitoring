# SOC Incident Investigation Report

## Incident Summary

- Incident type: Repeated failed Windows network authentication
- Classification: Authorized lab simulation
- Detection date: 2026-10-19
- Detection time: 03:31:07 UTC
- Endpoint: win11-soc-endpoint
- Windows hostname: DESKTOP-AN090O8
- Target username: WazuhTestNonexistent
- Wazuh correlation rule: 100101
- Alert severity: 10

## Investigation Evidence

Six failed authentication attempts were deliberately generated
using the Windows LogonUser API through PowerShell.

Wazuh generated six alerts between 03:30:59 and 03:31:09 UTC.

- Rule 100100: Individual failed authentication
- Rule 100101: Five matching failures within 60 seconds
- Windows Event ID: 4625
- Event channel: Security
- Logon type: 3 (Network)
- Authentication status: 0xc000006d
- Authentication substatus: 0xc0000064
- Initiating process: powershell.exe
- Correlation event record ID: 23855

The status indicates an authentication failure.
The substatus indicates that the specified account does not exist.

The source IP was not populated in the investigated alert.

## Analyst Assessment

The observed behavior is consistent with repeated unsuccessful
authentication attempts against a single account.

In this case, the activity was an authorized security test
performed within an isolated Windows laboratory environment.

The test did not produce a successful authentication.

## Disposition

- Finding: True positive detection of simulated activity
- Malicious incident: No
- Confirmed compromise: No
- Containment required: No
- Recommended production response: Validate the source,
  investigate related authentication activity, and escalate
  if the attempts are unauthorized.

## Supporting Evidence

- evidence/authentication_attack_alerts.jsonl
- evidence/successful_logon_alerts.jsonl
- rules/local_rules.xml
