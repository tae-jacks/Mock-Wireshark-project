# Mock-Wireshark-project

## Help Desk Ticket: Intermittent Web Access Due to TCP Retransmissions

**Reported By**: N.HALL (HR Dept)  
**Date/Time**: 2025-10-16 14:32 EDT  
**System**: Desktop - Win11, IP: 192.***.*.*

---

### 🐞 Issue Description
User reports slow web browsing and frequent timeouts when accessing internal and external websites.

---

### 🔍 Steps Taken
- Captured traffic using Wireshark
- Ran `ping` and `tracert` to www.speedtest.net
- Reviewed NIC settings and link speed

---

### 📊 Findings
- Wireshark shows multiple TCP retransmissions and duplicate ACKs between 192.168.1.4 and 192.168.1.1
- I/O graph confirms burst of retransmissions around 75s mark
- NIC was set to auto-negotiation; router supports 1 Gbps full duplex

---

### 🛠️ Remediation
- Manually set NIC to 1 Gbps Full Duplex
- Verified improved performance via ping (0% loss, avg 85ms)
- Issue resolved

---

### 📎 Attachments
- Wireshark screenshots (TCP handshake, retransmissions)
![alt text](<handshake complete.png>)
- This screenshot shows a SYN-ACK from 45.33.32.156 to193.168.1.***. It shows confirmed successful TCP handshake Initiation.

---

![alt text](<unusual ports.png>)
Observed traffic on non-standard ports:443,37070,37071,37072,37075,22. 
Ports appear to be ephemeral and used for outboud TCP connections
There are no known services mapped to these ports.
Recommend monitoring for anomalies, brute force attacks, and malware. 

---

![alt text](<Failed connections.png>)
No SYN-ACK received 
Multiple retransmissions observed
Possible honeypot, firewall deception, or SSH filtering
verified with 'nmap -sV, manual SSH attempt, and packet inspection

---

![alt text](<to and from ip 45.33.32.156.png>)

Identifying whether 45.33.32.156 was attempting to initiate TCP connections or receiving them, and to analyze the success or failure of those attempts.

---

- I/O graph PDF
![alt text](<Screenshot 2025-10-16 193116.png>)
Indicated there was a huge spike of packets that lasted roughly 10 seconds
The huge influx of packets may indicate different types of retransmission, congestion, and/or scans

---

- Ping/tracert output
![alt text](<Screenshot 2025-10-15 085129-1.png>)
Tracert showed the packet path to ip address 45.33.32.156
ping tested connectivity  to host and how log on average would take to connect to said host.

---

- NIC setting Speed & Duplex changed from auto to 1 Gbps and said host was ran again the ping stable and the amount of retransmissions in wireshark decreased in total.

---

**Status**: ✅ Resolved  
**Technician**: Octavius (SOC Analyst Candidate)