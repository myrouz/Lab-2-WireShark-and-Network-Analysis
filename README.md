# 🦈 Lab 2: Network Traffic Analysis with Wireshark

![Tool](https://img.shields.io/badge/Tool-Wireshark-1679A7)

## 🎥 Walkthrough

Follow along as I complete this lab! 

https://www.loom.com/share/00fdabe6b66741368c5b8a03275f3c78

## 📋 Overview

Networks carry everything an organization produces: logins, database queries, file transfers, API calls. When something goes wrong, whether it's an unreachable service, slow performance, or a security alert, the network is almost always involved, and the only way to know what is happening is to look at the packets.

This lab uses Wireshark to capture live traffic and decode it at the packet level. I analyzed DNS queries and responses, followed the TCP three-way handshake (SYN → SYN-ACK → ACK), reconstructed a full conversation with Follow TCP Stream, and compared HTTP and HTTPS traffic to see why encryption matters. In the HTTP capture, credentials were readable in plaintext, which is the clearest demonstration of why every login form needs TLS.

Knowing what normal traffic looks like is the baseline for spotting abnormal traffic: an unexpected DNS lookup that could be malware calling home, a SYN with no reply that points to a refused connection, or a stream that shows exactly what data left the network. That makes this lab a foundation for SOC analysis, incident response, and cloud network troubleshooting.

---

## 🎯 Business Context

Every piece of data an organization produces crosses the network, and when something breaks, the network is almost always involved. Packet analysis is how teams prove what is actually happening instead of guessing.

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


   

   
