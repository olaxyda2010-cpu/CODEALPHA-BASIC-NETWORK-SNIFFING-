# PYTHON NETWORK SNIFFER PROJECT 

## 1. Project Title

**Development and Implementation of a Python Network Packet Sniffer Using Scapy**

---

## 2. Introduction

Network traffic consists of packets transmitted between devices, applications, and servers. These packets contain information required for communication across a network using protocols such as TCP, UDP, ICMP, IP, and DNS.

For this project, a Python-based network packet sniffer was developed using the **Scapy** library. The purpose of the project was to capture network packets, analyze their structure, identify communication protocols, and display useful information about the captured traffic.

The project was conducted in an authorized cybersecurity laboratory environment.

---

## 3. Project Objectives

The main objectives of the project were to:

- Build a network packet sniffer using Python.
- Capture network traffic using the Scapy library.
- Analyze the structure of captured packets.
- Identify common network protocols.
- Display source and destination IP addresses.
- Identify TCP and UDP source and destination ports.
- Analyze ICMP traffic.
- Examine packet information and payload-related metadata.
- Understand how data flows through a network.
- Learn the relationship between different network protocol layers.
- Generate controlled network traffic.
- Verify that the packet sniffer correctly identifies different types of traffic.
- Implement protocol filtering.
- Count captured packets by protocol.

---

## 4. Technologies and Tools Used

| Tool / Technology | Purpose |
|---|---|
| Python 3 | Programming language |
| Scapy | Packet capture and packet analysis |
| Kali Linux | Cybersecurity laboratory environment |
| Terminal | Executing commands and running the program |
| ICMP | Testing network connectivity |
| DNS | Domain name resolution |
| UDP | Transport protocol commonly used by DNS |
| TCP | Reliable transport protocol |
| `ping` | Generating ICMP test traffic |
| `nslookup` | Generating DNS traffic |
| `ip addr` | Identifying network interfaces |

---

## 5. Project Environment

The project was implemented on **Kali Linux** in an authorized laboratory environment.
<img width="1073" height="437" alt="image" src="https://github.com/user-attachments/assets/9b22efa8-6b5d-4952-8ba4-030743d3453e" />


The network interface was identified using:

```bash
ip addr
```
The available interfaces could also be displayed through the program:
```bash
python3 network_sniffer.py --interfaces
```
## 6. Installation

Scapy was installed using:
```bash
sudo apt update
sudo apt install python3-scapy -y
```

The installation was verified using:
```bash
python3 -c "from scapy.all import sniff; print('Scapy is working')"
```
<img width="1086" height="516" alt="image" src="https://github.com/user-attachments/assets/877b9831-4434-4678-ae48-a395c2ccdde6" />

## 7. Program Design

The Python program was designed around several major functions.

Packet Capture

Scapy's sniff() function was used to capture packets:
```bash


sniff(
    iface=interface,
    prn=analyze_packet,
    count=count,
    store=False
)
```
The captured packet is passed to the analyze_packet() function.


Packet Analysis

The program checks whether the packet contains an IP layer:
```bash

if IP not in packet:
    return
```

It then extracts information such as:
```bash

source_ip = packet[IP].src
destination_ip = packet[IP].dst
packet_length = len(packet)
```

Protocol Detection

The program identifies TCP, UDP and ICMP packets:
```bash

if TCP in packet:
    protocol = "TCP"

elif UDP in packet:
    protocol = "UDP"

elif ICMP in packet:
    protocol = "ICMP"
```


Payload Analysis

Where a raw payload is present, the program displays a hexadecimal and ASCII preview:
```bash

if Raw in packet:

    payload = bytes(packet[Raw].load)
```
8. Packet Information Captured

The sniffer was designed to display information including:

Timestamp

Protocol

Source IP address

Destination IP address

Source port

Destination port

TCP flags

Packet length

Payload length

Packet layers

Payload preview

An example of the captured output was:
```bash


Protocol:      ICMP
Source IP:     10.0.2.5
Destination IP:192.232.216.135
Packet Length: 98 bytes
Payload Length:56 bytes
```

## 9. Testing Methodology

To test the packet sniffer, the following command was executed:
```bash

ping -c 4 networkwalks.com
```
The -c 4 option instructed the system to send four ICMP Echo Requests.

Before the ICMP traffic could be generated, the computer needed to determine the IP address of networkwalks.com.

This caused DNS traffic to be generated, which was also captured by the Python sniffer.

## 10. DNS Traffic Analysis

The first significant traffic observed was DNS.

The sniffer captured:
```bash


Protocol:      UDP
Source IP:     10.0.2.5
Destination IP:8.8.8.8
Source Port:   40030
Destination Port: 53
Layers:        Ether / IP / UDP / DNS Qry
```

This represented a DNS query from the Kali machine to Google's public DNS server at:
```bash

8.8.8.8
```
The query requested the IP address associated with:
```bash

networkwalks.com
```

The DNS server returned:

```bash
192.232.216.135
```
Therefore, the hostname was resolved as:
```bash

networkwalks.com
        ↓
192.232.216.135
```
## 11. UDP Analysis

The DNS traffic demonstrated the use of UDP.

The captured packet contained:
```bash

Source IP:        10.0.2.5
Destination IP:   8.8.8.8
Source Port:      40030
Destination Port: 53
Protocol:         UDP
```

Port 53 is the standard port associated with DNS.

The response travelled in the opposite direction:
```bash

8.8.8.8:53
      ↓
10.0.2.5:40030
```
This demonstrated the two-way communication between the client and DNS server.

## 12. ICMP Analysis

After DNS resolution, the system knew that:
```bash


networkwalks.com = 192.232.216.135
```

The ping command then generated ICMP traffic.

The sniffer captured:
```bash

Protocol:      ICMP
Source IP:     10.0.2.5
Destination IP:192.232.216.135
Packet Length: 98 bytes
Payload Length:56 bytes
```
The packet layers were displayed as:
```
Ether / IP / ICMP / Raw
```
The first ICMP packet was an:
```bash

echo-request
```
The remote server responded with:
```
echo-reply
```
The communication therefore followed this pattern:
```bash


10.0.2.5
   |
   | ICMP Echo Request
   ↓
192.232.216.135
   |
   | ICMP Echo Reply
   ↓
10.0.2.5
```
## 13. Four-Packet Ping Analysis

Because the command was:
```bash

ping -c 4 networkwalks.com
```

four ICMP requests were generated.

The sniffer observed the corresponding requests and replies.

Request 1
```bash

10.0.2.5 → 192.232.216.135
ICMP Echo Request
```
Reply 1
```bash

192.232.216.135 → 10.0.2.5
ICMP Echo Reply
```
Request 2
```
10.0.2.5 → 192.232.216.135
ICMP Echo Request
```
Reply 2
```bash

192.232.216.135 → 10.0.2.5
ICMP Echo Reply
```
Request 3
```bash

10.0.2.5 → 192.232.216.135
ICMP Echo Request
```
Reply 3
```bash

192.232.216.135 → 10.0.2.5
ICMP Echo Reply
```
Request 4
```bash

10.0.2.5 → 192.232.216.135
ICMP Echo Request
```
Reply 4
```bash

192.232.216.135 → 10.0.2.5
ICMP Echo Reply
```
This demonstrated successful two-way ICMP communication.

## 14. Packet Payload Analysis

The ICMP packets contained a 56-byte payload.

The program displayed the payload in hexadecimal format:
```bash

09 99 c0 6a 00 00 00 00 7e 2e 0c 00
00 00 00 00 00 10 11 12 13 14 15 16
17 18 19 1a 1b 1c 1d 1e 1f 20 21 22
23 24 25 26 27 28 29 2a 2b 2c 2d
2e 2f 30 31 32 33 34 35 36 37
```
The program also produced an ASCII representation:
```bash

...j....~....................... !"#$%&'()*+,-./01234567
```
This demonstrated that network packet payloads are fundamentally byte data and are not necessarily readable text.

## 15. Packet Layer Analysis

One of the important observations from the project was the layered structure of network packets.

For ICMP traffic, the program displayed: 

```bash

Ether
  ↓
IP
  ↓
ICMP
  ↓
Raw
```

For DNS traffic:
```bash


Ether
  ↓
IP
  ↓
UDP
  ↓
DNS
```
This demonstrates the concept of protocol encapsulation.

Each layer provides information or functionality required by the communication process.

## 16. Traffic Flow Observed

The complete traffic flow observed during the test was:

User executes:
```bash

ping -c 4 networkwalks.com
              |
              v
       DNS Resolution
              |
              v
10.0.2.5 → 8.8.8.8
              |
              | DNS Query
              v
8.8.8.8 → 10.0.2.5
              |
              | DNS Response
              v
networkwalks.com
       |
       v
192.232.216.135
       |
       v
ICMP Echo Request
       |
       v
192.232.216.135
       |
       v
ICMP Echo Reply
       |
       v
10.0.2.5
```
This was useful for demonstrating how an apparently simple command such as ping networkwalks.com involves multiple network protocols.

## 17. Traffic Statistics

The program was also designed to maintain counters for different protocol types:
```bash

Total Packets
TCP Packets
UDP Packets
ICMP Packets
Other Packets
```
The counters are updated whenever a packet is successfully identified.

Example:
```bash

statistics["tcp"] += 1
statistics["udp"] += 1
statistics["icmp"] += 1
```
When packet capture is stopped with:
```bash

CTRL+C
```
the program displays a traffic summary.

## 18. Challenges Encountered

Several technical concepts were encountered during development.

18.1 Understanding Network Interfaces

The packet sniffer must capture traffic from the correct network interface.

The interface was identified using:
```bash

ip addr
```
18.2 Administrative Privileges

Packet capture requires appropriate privileges on Linux.

The program was therefore executed using:
```bash

sudo python3 network_sniffer.py
```
18.3 Understanding Protocol Layers

The captured traffic demonstrated that a packet can contain multiple protocol layers.

For example:
```bash

Ether / IP / UDP / DNS
```
Initially, this output may appear complex, but it represents the encapsulation of different network protocols.

18.4 Payload Interpretation

Raw packet data is represented as bytes. It is therefore not always possible or appropriate to interpret the payload as readable text.

The program handles this by displaying hexadecimal and sanitized ASCII representations.

18.5 DNS Traffic

The testing process demonstrated that DNS traffic can occur before the actual ICMP traffic. This helped demonstrate the relationship between hostname resolution and network communication.

## 19. Security and Ethical Considerations

The packet sniffer was developed strictly for authorized network monitoring and cybersecurity education.

Packet capture can expose sensitive information depending on the network and protocols being monitored. Therefore, packet sniffing should only be performed on:

Systems owned by the user

Personal laboratory environments

Virtual machines

Networks where explicit authorization has been granted

The project does not implement:

Password harvesting

Credential theft

Authentication bypass

Session hijacking

Packet injection

Traffic manipulation

Decryption of protected communications

The purpose of the project is network visibility, protocol learning and defensive cybersecurity education.

## 20. Results

The project successfully demonstrated the ability to:

Capture live network packets.

Identify IP traffic.

Identify UDP traffic.

Identify ICMP traffic.

Extract source and destination IP addresses.

Extract UDP source and destination ports.

Identify DNS queries and responses through Scapy's packet layers.

Display packet lengths.

Analyze ICMP payloads.

Display packet protocol layers.

Demonstrate DNS resolution.

Demonstrate ICMP Echo Request and Echo Reply communication.

Maintain traffic statistics.

The test using:
```bash

ping -c 4 networkwalks.com
```
successfully demonstrated the complete sequence of:
```bash

DNS Query
     ↓
DNS Response
     ↓
IP Resolution
     ↓
ICMP Echo Request
     ↓
ICMP Echo Reply
```
## 21. Learning Outcomes

Through this project, I developed a better understanding of:


How network packets are transmitted.

How IP addresses identify network endpoints.

How ports identify network services and applications.

The difference between TCP, UDP and ICMP.

How DNS resolves domain names to IP addresses.

How protocols are encapsulated within network packets.

How Scapy can be used for packet analysis.

How Python can automate network monitoring tasks.

How packet payloads are represented as bytes.

How network traffic can be analyzed for cybersecurity purposes.

22. Future Improvements

The project can be extended with additional functionality, including:

TCP connection analysis.

More detailed DNS analysis.

Protocol filtering.

Packet filtering by IP address.

Packet filtering by port.

Exporting captured traffic to a file.

CSV logging.

PCAP file generation.

Real-time traffic statistics.

Graphical user interface.

Traffic visualization.

Detection of unusual traffic patterns.

Integration with defensive security monitoring tools.

A future version could also provide a command such as:
```bash
sudo python3 network_sniffer.py -i eth0 --protocol TCP
```
to capture only a specific protocol.

23. Conclusion

The Python Network Sniffer project successfully demonstrated how Python and Scapy can be used to capture and analyze network traffic.

During testing, the command:
```bash

ping -c 4 networkwalks.com
```
generated multiple types of traffic. The sniffer first observed DNS queries and responses using UDP and then captured ICMP Echo Requests and Echo Replies between the local machine and the resolved server IP address.

The project provided practical experience with packet structures, network protocols, IP addressing, ports, payloads and protocol encapsulation. It also demonstrated how network traffic can be observed and analyzed using Python in a controlled cybersecurity laboratory.

Overall, the project provides a foundation for more advanced network monitoring, traffic analysis and defensive cybersecurity projects.

24. Project Evidence

Test Command
```bash

ping -c 4 networkwalks.com
```
DNS Query Observed
```bash

10.0.2.5:40030 → 8.8.8.8:53
```
DNS Query: networkwalks.com

DNS Response Observed
```bash

8.8.8.8:53 → 10.0.2.5:40030
DNS Answer: 192.232.216.135
```
ICMP Request Observed
```bash
10.0.2.5 → 192.232.216.135
```
ICMP Echo Request

ICMP Response Observed
```bash

192.232.216.135 → 10.0.2.5
ICMP Echo Reply
```
Packet Structure
```bash

Ether / IP / UDP / DNS
Ether / IP / ICMP / Raw
```
Final Project
```bash

Python Network Packet Sniffer
        |
        +-- Packet Capture
        +-- Protocol Detection
        +-- IP Analysis
        +-- Port Analysis
        +-- Payload Analysis
        +-- Packet Layer Analysis
        +-- Traffic Statistics


```
<img width="1071" height="714" alt="image" src="https://github.com/user-attachments/assets/fb9b1784-b55d-4946-9cc5-3be294d6c184" />
<img width="1078" height="705" alt="image" src="https://github.com/user-attachments/assets/ca8cd313-63a2-4880-a736-6ca2e8efd660" />

<img width="863" height="633" alt="image" src="https://github.com/user-attachments/assets/bdd80123-ccce-41d7-a001-d8f37b27de01" />
<img width="941" height="715" alt="image" src="https://github.com/user-attachments/assets/735547fe-9b17-418a-89d1-9575710556b3" />
<img width="1099" height="686" alt="image" src="https://github.com/user-attachments/assets/d6ef5b57-3a42-40d0-abc5-7d708fa0894f" />
<img width="1098" height="714" alt="image" src="https://github.com/user-attachments/assets/2fe62efb-f4fc-4397-b35a-effe78a79abd" />


