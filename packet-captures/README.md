# Packet Captures

This directory contains `.pcap` files and documentation related to capturing and analyzing network traffic in my homelab. The primary goal is to troubleshoot connectivity, verify DNS/SSH traffic, and simulate real-world TSE scenarios.

## Why Packet Captures?

1. **Troubleshooting**: Identify dropped packets, firewall misconfigurations, or DNS issues.  
2. **Learning**: Gain familiarity with tools like tcpdump, Wireshark, and tshark.  
3. **Validation**: Confirm that SSH connections, Pi-hole DNS queries, and Azure communications work as intended.

## Tools & Setup

- **tcpdump** for capturing traffic on Linux-based systems (e.g., the Pi).  
- **tshark** or Wireshark for reading `.pcap` files in detail.

## Screenshots & Examples

1. **Capturing Traffic**  
   ![tcpdump capturing host 192.168.1.149 => traffic.pcap](/images/33.png)

2. **Analyzing with tshark**  
   ![tshark reading traffic.pcap (raw)](/images/34.png)

   ![tshark fields ip.src ip.dst tcp.port](/images/35.png)

3. **Python Server & Client**  
   - On Windows, I ran `server.py`:

     ![server.py listening on 0.0.0.0:5000](/images/30.png)

   - On the Pi, `client.py` sends messages:

     ![client.py example](/images/32.png)

## Challenges & Troubleshooting

- **Interface Selection**: Switching from `eth0` to `wlan0` if the wired interface wasn’t active.  
- **Filtering**: Using specific host or port filters to avoid massive capture files.  
- **Permissions**: Required elevated privileges for capturing traffic.  
- **File Transfer**: Copied `.pcap` files to a local PC for Wireshark analysis.

## Lessons Learned

1. **Interface Identification**: Knowing which interface is active is critical.  
2. **Targeted Captures**: Host/port filters reduce noise.  
3. **Security Awareness**: `.pcap` files can contain sensitive data—sanitize before sharing.  
4. **Real-World TSE Experience**: Packet-level analysis is invaluable for diagnosing issues.

## Next Steps

- **Advanced Analysis**: Explore deeper protocol decoders in Wireshark for HTTP, DNS, TLS, etc.  
- **Central Logging**: Potentially forward packet logs or events to a SIEM.  
- **Automation**: Develop scripts to automate captures under specific conditions (e.g., ping failures).
