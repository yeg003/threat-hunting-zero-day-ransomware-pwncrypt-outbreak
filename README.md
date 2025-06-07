# Threat Hunt: PwnCrypt Ransomware Simulation

This repository documents a simulated threat hunt on a Windows endpoint (`yc-vm-mde`) that was targeted by a staged PowerShell-based ransomware named `PwnCrypt`.

## Scenario Summary
A malicious script (`pwncrypt.ps1`) was downloaded and executed using PowerShell with the intent to encrypt files using AES-256 and rename them with a `.pwncrypt` extension.

However, no files were encrypted. The hunt was able to confirm delivery and execution, but no data loss occurred.

## MITRE ATT&CK Coverage

| Tactic              | Technique                                | ID         |
|---------------------|-------------------------------------------|------------|
| Execution           | PowerShell Execution                      | T1059.001  |
| Ingress Tool Transfer | Download via Invoke-WebRequest        | T1105      |
| Defense Evasion     | ExecutionPolicy Bypass                    | T1562.001  |
| Impact (attempted)  | File Encryption for Impact                | T1486 (not observed) |

## Timeline

![Timeline](pwncrypt_timeline.png)

## Report

See [`pwncrypt_threat_hunt_report.md`](./pwncrypt_threat_hunt_report.md) for the full analysis, IOCs, timeline, and recommendations.

## Outcome

The incident was contained. The script was executed but encryption failed or was prevented. Recommended follow-up actions were implemented.

---

## Tools Used

- Microsoft Defender for Endpoint (Advanced Hunting)
- Kusto Query Language (KQL)
- Python (for report/chart generation)
- GitHub (for documentation and portfolio)
