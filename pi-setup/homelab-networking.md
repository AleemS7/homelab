# Homelab Networking

This file outlines the core networking components of my homelab, including how I configured IP addresses, bridged connections, and DNS settings to ensure seamless communication between my Raspberry Pi, Windows Server VM, and external resources (like Azure). I also plan to expand this environment to test multi-cloud scenarios (AWS, OpenShift) and container orchestration.

## Objectives

1. **Establish a Stable Local Network**  
   - Assign static or reserved IPs to critical devices (Pi-hole, Windows VM).
2. **Bridged Networking**  
   - Use VMware Workstation in bridged mode so the Windows VM appears on the same subnet as my Pi and router.
3. **DNS and Routing**  
   - Integrate Pi-hole as a DNS server for ad-blocking.  
   - Confirm router or manual DNS settings point to the Pi’s IP.
4. **Hybrid Connectivity**  
   - Enable the Pi and Windows VM to reach external services (Azure VM, WSL environment).

## Steps & Highlights

- **VMware Network Editor**  
  I set my Windows VM to “Bridged” so it would get an IP from the same subnet as the Pi:

  ![VMware Virtual Network Editor](/images/21.png)

- **Avoiding APIPA**  
  At times, the Windows VM defaulted to `169.254.x.x`:

  ![APIPA / General Failure](/images/20.png)

  To fix this, I ensured the VM’s adapter was truly bridged and sometimes assigned a static IP if DHCP didn’t work.

- **Testing Connectivity**  
  Once bridging worked, I could ping the VM from the Pi and vice versa:

  ![Pi pinging 192.168.1.254](/images/22.png)

  ![Windows pinging 192.168.1.64](/images/23.png)

## Challenges & Troubleshooting

- **Router Limitations**  
  Couldn’t set Pi-hole DNS globally; used per-device config.  
- **Wi-Fi vs. Ethernet**  
  If the Pi or VM was on Wi-Fi, bridging can behave differently than wired.  
- **MAC & IP Reservations**  
  For the Pi, I used DHCP reservation to keep the same IP. For the Windows VM, bridging let me get an IP from the router.

## Lessons Learned

1. **Consistent IPs**: Static or reserved IPs prevent conflicts.  
2. **Bridged Networking**: Properly bridging the VM adapter simulates a real LAN environment.  
3. **DNS Workarounds**: Manual device-level DNS can circumvent router restrictions.  
4. **Layered Troubleshooting**: Checking DHCP, VM adapter settings, and OS firewall is essential.

## Next Steps

- **Multi-Cloud**: Extend beyond Azure to AWS and OpenShift.  
- **Advanced VLANs**: Potentially segment the network.  
- **Automation**: Use scripts to manage IP assignments and firewall rules.
