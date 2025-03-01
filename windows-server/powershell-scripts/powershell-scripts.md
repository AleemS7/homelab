# PowerShell Scripts

This document gathers various PowerShell commands and scripts used in my homelab—particularly for **OpenSSH installation**, **firewall rules**, and other configurations on Windows Server.

> **Note**: Some commands may differ depending on your Windows version. If you encounter parameter issues (e.g., `-Port` vs. `-LocalPort`), adjust accordingly.

---

## 1. Built-In OpenSSH Installation (Windows Server 2019/2022)

Use this script if your Windows Server supports the built-in OpenSSH feature (and you have enough system resources):

```powershell
# Built-In OpenSSH Installation

# Installs the OpenSSH server capability on Windows Server (if available).
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Start and configure the sshd service to run at boot.
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'

# (Optional) Verify sshd status
Get-Service sshd
