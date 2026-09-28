# Lab-2-WireShark-and-Network-Analysis

![Tool](https://img.shields.io/badge/Tool-Wireshark-1679A7)

Follow along as I complete this lab! 

https://www.loom.com/share/00fdabe6b66741368c5b8a03275f3c78

## Overview

---

Business Problem This Lab Solves

---

## Prerequisites

---

## Architecture 

---

## Steps

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


   

   
