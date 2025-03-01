# My Homelab

## Current State

- **Raspberry Pi (Ubuntu) + Pi-hole** for DNS ad-blocking  
- **Local Windows Server VM** for on-prem Windows administration (OpenSSH, firewall rules)  
- **Azure VM** integration for hybrid connectivity, remote management, and networking tests  
- **Bridged Networking** to simulate a realistic LAN environment  
- **Packet Captures** (tcpdump, Wireshark) to troubleshoot and analyze traffic

## Future Vision

This homelab is **just the beginning** of a larger, fully automated environment where I can **experiment**, **learn**, and **test** cutting-edge technologies. Expect frequent changes and updates. My ultimate goal is to integrate:

- **Multi-Pi Cluster**: Scale out Pi-based nodes for distributed workloads  
- **Kubernetes & GitOps**: Automate deployments (e.g., with ArgoCD, Helm, or K3s)  
- **Multi-Cloud**: Extend beyond Azure into AWS or OpenShift for containerized services  
- **Advanced Networking**: Implement VLANs, VPN (WireGuard, Tailscale), and robust security policies  
- **Monitoring & Alerting**: Use tools like Prometheus, Grafana, and Loki for real-time observability  
- **Continuous Improvement**: Explore ephemeral PXE booting, container registries, single sign-on, and more

## Roadmap & Documentation

1. **Homelab Networking**  
   - [homelab-networking.md](/pi-setup/homelab-networking.md): Bridged adapters, static IPs, DHCP reservations, and more  
2. **Pi-hole Setup**  
   - [pihole-install.md](/pi-setup/pihole-install.md): Steps to install Pi-hole on Raspberry Pi, plus DNS tips  
3. **OpenSSH on Windows**  
   - [openssh-config.md](/windows-server/openssh-config.md): How I enabled SSH on a Windows Server VM  
4. **Azure Integration**  
   - [azure-networking.md](/azure-setup/azure-networking.md): Managing NSGs, WSL DNS fixes, and hybrid connectivity  
5. **Packet Captures**  
   - [packet-captures/README.md](packet-captures/README.md): Why and how I capture `.pcap` files to troubleshoot  
6. **PowerShell Scripts**  
   - [powershell-scripts.md](/windows-server/powershell-scripts/powershell-scripts.md): Central place for Windows firewall rules, OpenSSH installs, etc.

As I **expand** this homelab, I’ll add new documentation, scripts, and hardware details.

## Contributions
 
Feel free to fork this project or reference any configurations for your own learning. If you have suggestions, PRs are welcome—just note this is a personal playground, so I may pivot directions rapidly.

---
