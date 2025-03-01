# OpenSSH Configuration on Windows Server

This document outlines how I set up and troubleshot OpenSSH on my Windows Server VM, enabling **remote SSH access** from my Raspberry Pi (and other machines).

## Objectives

1. **Enable Secure Remote Access**  
   - Install OpenSSH Server so I can SSH into Windows, similar to a Linux host.
2. **Firewall Coordination**  
   - Open port 22 in the Windows Firewall and ensure no conflicts with hypervisor or router.
3. **Troubleshoot Common Issues**  
   - Address “Connection refused,” local security policy blocks, and built-in Administrator restrictions.

## Installation Steps

1. **Install OpenSSH**  
   - Attempted the built-in feature:

     ![Add Roles and Features Wizard (OpenSSH attempt)](/images/11.png)

   - If memory errors occurred, I switched to the GitHub approach.

2. **Check the sshd Service**  
   ![Get-Service sshd => Running](/images/21.png)

3. **Create Firewall Rule**  
   ![New-NetFirewallRule -Name OpenSSH](/images/22.png)

4. **Testing & Python Setup**  
   - Verified Python installation:

     ![python --version => 3.13.2](/images/24.png)

   - Created a simple Python server on Windows:

     ![server.py listening on 0.0.0.0:5000](/images/25.png)

## Challenges & Troubleshooting

- **Parameter Not Found**  
  ![Port param error](/images/14.png)

  On some Windows builds, `-LocalPort` must be used instead of `-Port`.
- **Connection Refused**  
  ![SSH Connection Refused from Pi](/images/30.png)

  Typically caused by missing firewall rules or local security policy blocking Administrator.

## Lessons Learned

1. **Layered Security**: Windows Firewall, local security policies, and Azure NSG rules must all align.  
2. **Fallback Installation**: The GitHub approach can save the day if the built-in feature fails.  
3. **Policy Awareness**: Built-in Administrator may be blocked from remote login by default.  
4. **Resource Planning**: Small VM sizes can hamper Windows feature installations.

## Next Steps

- **User Management**: Create dedicated service accounts for SSH.  
- **Key-Based Auth**: Replace password logins with public/private key pairs.  
- **Automation**: Script the entire setup with PowerShell for repeatability.
