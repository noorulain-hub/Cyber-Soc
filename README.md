
# CyberHawk SOC — Custom Detection Rules

## Project Overview

CyberHawk SOC is an AI-Augmented Security Operations Center project built using Wazuh SIEM. It monitors Windows and Linux endpoints, collects security events, and detects suspicious activities through custom detection rules.

This repository contains five custom Wazuh detection rules developed and tested for Windows security monitoring.

## Environment

- SIEM Platform: Wazuh 4.14.9
- Manager OS: Ubuntu 24.04.5 LTS
- Windows Endpoint: Windows 11
- Windows Agent: CyberHawk-Win11
- Agent ID: 001
- Manager IP: 192.168.179.134
- Windows Endpoint IP: 192.168.179.135

## Custom Detection Rules

| Rule ID | Detection | Event / Parent Rule |
|---|---|---|
| 100100 | Encoded PowerShell Detection | PowerShell Script Block |
| 100101 | Scheduled Task Creation | Parent Rule 60228 |
| 100102 | Windows Local Account Creation | Event ID 4720 |
| 100103 | Windows Local Account Deletion | Event ID 4726 |
| 100104 | Windows Failed Login Detection | Event ID 4625 |

## MITRE ATT&CK Mapping

| Rule ID | Technique ID | Technique |
|---|---|---|
| 100100 | T1059.001 | PowerShell |
| 100101 | T1053 | Scheduled Task/Job |
| 100102 | T1136.001 | Local Account |
| 100103 | T1531 | Account Access Removal |
| 100104 | T1110 | Brute Force |

## Rule Validation

All five custom rules were added to the Wazuh local rules configuration file:

`/var/ossec/etc/rules/local_rules.xml`

The configuration was validated using:

`sudo /var/ossec/bin/wazuh-analysisd -t`

The Wazuh manager was restarted after adding the rules.

The custom failed-login rule (100104) was successfully tested using a controlled failed login attempt on the Windows 11 endpoint. Wazuh detected Windows Security Event ID 4625 and generated a level 10 alert.

## Repository Structure

```text
CyberHawk-SOC/
├── README.md
└── rules/
    └── local_rules.xml
```

## Purpose

The purpose of these detection rules is to improve Windows endpoint monitoring, identify suspicious account and authentication activities, and support threat detection using MITRE ATT&CK techniques.

## Disclaimer

These rules were developed and tested in an authorized educational cybersecurity lab environment.

