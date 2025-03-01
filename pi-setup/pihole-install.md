# Pi-hole Installation

This document explains how I installed and configured [Pi-hole](https://pi-hole.net/) on my Raspberry Pi. The goal was to create a **DNS sinkhole** that blocks ads and trackers at the network level, while also teaching me about DNS, DHCP, and local network troubleshooting.

## Objectives

1. **Ad & Tracker Blocking**  
   - Reduce ads across devices on my LAN by directing DNS queries through Pi-hole.
2. **Local DNS Server**  
   - Serve as a primary DNS for the homelab, ensuring consistent name resolution.
3. **Learning Opportunity**  
   - Explore how DNS queries flow, troubleshoot network issues, and gain practical sysadmin experience.

## Installation Steps

1. **Reserve IP for Pi-hole**  
   In my router’s DHCP settings, I assigned a **static IP** or “DHCP reservation” to the Pi:

   ![IP Allocation for Pi-hole](/images/1.png)

2. **Run Pi-hole Installer**  
   After flashing Ubuntu onto the Pi and updating packages, I used Pi-hole’s official install script. At the end, Pi-hole displays the final IP and admin password:

   ![Pi-hole Installation Complete](/images/2.png)

3. **Access the Dashboard**  
   Once installed, Pi-hole provides a web interface (default: `http://<Pi-IP>/admin`):

   ![Pi-hole Dashboard (initial)](/images/3.png)

   Over time, queries and block rates appear here:

   ![Pi-hole Dashboard with Queries](/images/8.png)

4. **Router DNS Challenges**  
   My AT&T router wouldn’t let me globally set the Pi-hole IP as DNS, displaying a “Page not found” error:

   ![AT&T Router Limitation](/images/4.png)

   So I manually configured DNS on individual devices instead.

5. **Testing & Validation**  
   - On Windows, I set **Preferred DNS** to Pi-hole’s IP:

     ![Windows DNS Settings](/images/5.png)

   - Flushed DNS cache:

     ![ipconfig /flushdns](/images/6.png)

   - Verified ad-blocking with `nslookup`:

     ![nslookup flurry.com => 0.0.0.0](/images/7.png)

## Challenges & Troubleshooting

- **Static IP**  
  Pi-hole strongly recommends a static IP. During setup, Pi-hole even warns:

  ![Pi-hole Static IP Needed](/images/10.png)

- **Router Limitations**  
  Couldn’t globally set Pi-hole as DNS, so each client was manually pointed to `192.168.1.x`.

## Lessons Learned

1. **DNS Fundamentals**: Understood how DNS requests are routed and how Pi-hole can intercept them.  
2. **Network Workarounds**: Learned to bypass router restrictions by pointing individual devices to Pi-hole.  
3. **Logging & Analysis**: Gained insight into which domains are being queried, improving security awareness.  
4. **Customization**: Explored whitelisting and blacklisting specific domains to fine-tune blocking.

## Next Steps

- **DHCP Server Option**: Potentially enable Pi-hole’s built-in DHCP server for full LAN control.  
- **Integration with Other Services**: Combine Pi-hole logs with a centralized logging solution.  
- **Multi-Subnet Setup**: Experiment with VLANs or multiple subnets, ensuring Pi-hole can handle DNS across them.
