# 🦈 Lab 2: Network Traffic Analysis with Wireshark

![Tool](https://img.shields.io/badge/Tool-Wireshark-1679A7)

## 🎥 Walkthrough

Follow along as I complete this lab! 

https://www.loom.com/share/00fdabe6b66741368c5b8a03275f3c78

## 📋 Overview

Network traffic carries critical enterprise activity, including authentication requests, database queries, file transfers, and API communications. When connectivity issues, performance degradation, or security alerts occur, packet-level analysis provides visibility into network communications and helps identify the underlying cause.

This lab uses Wireshark to capture and analyze network traffic at the packet level. Analysis includes examining DNS queries and responses, tracing the TCP three-way handshake (SYN → SYN-ACK → ACK), reconstructing application conversations using Follow TCP Stream, and comparing HTTP and HTTPS traffic to understand the role of encryption in protecting data in transit. An HTTP capture demonstrated how credentials transmitted without encryption can be exposed in plaintext, highlighting the importance of TLS-protected authentication.

Understanding normal network behavior establishes a baseline for identifying suspicious activity and diagnosing connectivity problems. Examples include unexpected DNS queries that may indicate malware command-and-control activity, unanswered TCP SYN packets that may suggest connectivity issues or packet filtering, and reconstructed TCP streams that reveal the contents of unencrypted application traffic.

These packet analysis skills provide a practical foundation for Security Operations Center (SOC) monitoring, incident response, network troubleshooting, and cloud network diagnostics.

---

## 🎯 Business Context

Organizations depend on reliable and secure network communications to support authentication, business applications, cloud services, and data exchange. When connectivity failures, performance issues, or suspicious activity occur, IT and security teams need visibility into network traffic to identify root causes, investigate potential threats, and minimize operational disruption.

This lab simulates real-world network troubleshooting and security investigation using Wireshark. By capturing and analyzing packets, inspecting DNS queries, tracing TCP connections, and comparing encrypted and unencrypted traffic, the investigation demonstrates how packet-level visibility helps diagnose communication failures, identify potentially exposed sensitive data, and recognize suspicious network behavior.

Developing the ability to distinguish normal from abnormal traffic supports faster troubleshooting, more effective incident response, and better-informed security decisions. These capabilities help organizations reduce downtime, investigate security events, and strengthen the protection of data transmitted across enterprise and cloud networks.
---

## ✅ Prerequisites

---

## 🧩 Architecture

---

## 🛠️ Steps

1. Get Wireshark

Wireshark is completely free and open source. Go to wireshark.org/download.html and download the installer for your operating system. No account , no trial, or no license required.

| OS | Download | Notes |
|---|---|---|
| Windows | Windows x64 Installer (.exe) | Accept all defaults. Install Npcap when prompted — this is required to capture packets |
| macOS | macOS Arm or Intel (.dmg) | Run the installer. If prompted about ChmodBPF — allow it. This gives Wireshark permission to access network interfaces |
| Linux | Use your package manager | `sudo apt install wireshark` (Ubuntu/Debian). Add yourself to the `wireshark` group to capture without root |

    - # Linux only — add yourself to the wireshark group (log out and back in after)
    - sudo usermod -aG wireshark $USER

    - # Verify Wireshark is installed
    - wireshark --version

---

2. Your First Capture

* This step gets you comfortable with the Wireshark interface before doing anything complex.

- Open Wireshark

- On the welcome screen you will see a list of network interfaces with wavy lines showing live traffic activity

- Double-click your active interface — Ethernet or Wi-Fi, pick the one with the most activity shown in the wave graph
  
- Wireshark starts capturing immediately — packets start appearing in the list in real time

- Open a browser and navigate to any website
  
- After 30 seconds, click the red square Stop button in the toolbar

---

3. Essential Display Filters

--- 

4. Guided Exercise

   a. Capture a DNS Lookup

   b. Watch the TCP Three-Way Handshake

   c. Spot Cleartext Credentials (HTTP)

   d. Follow a Full TCP Stream

      + Capture any HTTP traffic by navigating to an HTTP website

      + Find any HTTP packet in the capture list

      + Right-click it → Follow → TCP Stream
   
      + Wireshark reassembles all the packets from that connection into a readable conversation
   
      + Red text is your browser's request. Blue text is the server's response


   

   
