# Azure Networking

This document covers my experience integrating Azure into my homelab environment. The goal was to explore hybrid connectivity between a local Raspberry Pi (with Pi-hole), a Windows Server VM, and an Azure VM—focusing on **network configuration**, **DNS resolution**, and **firewall rules**.

## Objectives

1. **Set up a small Azure VM** to test hybrid scenarios.  
2. **Connect** from my local machines to the Azure VM via SSH or RDP.  
3. **Troubleshoot** DNS and networking issues in WSL (`az login` failures).  
4. **Capture and analyze** traffic flows between on-prem and the cloud.

## Steps & Highlights

1. **Creating the VM in Azure**  
   ![Azure Create VM settings](/images/19.png)

   I chose **B1s** for cost efficiency, set Region to `East US 2`, and used Windows Server 2022.

2. **Finding the Public IP**  
   ![az vm show public IP](/images/20.png)

   This IP let me RDP or SSH (if I installed OpenSSH) into the VM.

3. **WSL DNS Issues**  
   Initially, `az login` failed with “temporary failure in name resolution”:

   ![WSL DNS error / resolv.conf fix](/images/9.png)

   I had to override `/etc/resolv.conf`:

   ![WSL resolv.conf override](/images/17.png)

   After pointing to a public DNS (like `8.8.8.8`), `az login` worked.

## Challenges & Troubleshooting

- **NSG vs. Windows Firewall**  
  Needed to allow inbound RDP or SSH in both the **Network Security Group** and the VM’s firewall.  
- **Minimal VM Size**  
  B1s can be laggy for Windows; sometimes I used Linux or upscaled to B2s.  
- **Public IP Exposure**  
  Real IP is shown in some screenshots. If still active, consider obfuscating it.

## Lessons Learned

1. **Layered Security**: Azure NSG + OS firewall must align.  
2. **DNS Configuration**: Even small missteps in WSL or local DNS can break cloud connectivity.  
3. **Resource Constraints**: Tiny VMs can hamper Windows performance.  
4. **Real-World Troubleshooting**: This hybrid setup mirrors production issues.

---
