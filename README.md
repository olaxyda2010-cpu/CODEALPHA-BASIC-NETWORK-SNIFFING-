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

The network interface was identified using:

```bash
ip addr
