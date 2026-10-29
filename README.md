# 🦈 Lab 2: Network Traffic Analysis with Wireshark

![Tool](https://img.shields.io/badge/Tool-Wireshark-1679A7)

## 🎥 Walkthrough

See network traffic in action and discover how to analyze packets to uncover what’s really happening on a network!

[Loom Video: WireShark Network Analysis Lab](https://www.loom.com/share/00fdabe6b66741368c5b8a03275f3c78)

## 📋 Overview

Network traffic carries critical enterprise activity, including DNS queries, authentication requests, file transfers, and application communications. When connectivity issues, performance degradation, or security alerts occur, packet-level analysis helps administrators and cybersecurity analysts investigate network behavior and identify potential causes.

This lab uses Wireshark to capture, filter, and analyze network traffic at the packet level. Key activities include examining DNS queries and responses, analyzing the TCP three-way handshake (SYN, SYN-ACK, ACK), reconstructing application conversations using Follow TCP Stream, and comparing HTTP and HTTPS traffic to understand how encryption protects data in transit. In a controlled training environment, I examined unencrypted HTTP traffic to demonstrate how sensitive information, including credentials, can be exposed when transmitted without encryption.

The lab also explores how packet analysis supports network troubleshooting and security investigations. Examples include investigating unexpected DNS queries, analyzing unanswered TCP connection attempts, and inspecting reconstructed TCP streams for potentially exposed data. These indicators require further investigation and must be evaluated in context rather than treated as definitive evidence of malicious activity.

The skills developed through this project provide a practical foundation for Security Operations Center (SOC) monitoring, incident response, network troubleshooting, and cloud network diagnostics.

---

## 🎯 Business Context

Organizations depend on reliable and secure network communications to support authentication, business applications, cloud services, and data exchange. When connectivity failures, performance degradation, or suspicious activity occur, IT and security teams need visibility into network traffic to identify root causes, investigate potential threats, and minimize operational disruption.

This lab simulates real-world network troubleshooting and security investigations using Wireshark. By capturing and analyzing packets, inspecting DNS queries, tracing TCP connections, and comparing encrypted and unencrypted traffic, the lab demonstrates how packet-level visibility helps diagnose communication issues, identify potentially exposed sensitive data, and investigate suspicious network behavior.

The ability to distinguish normal traffic patterns from unusual activity supports efficient troubleshooting, incident response, and informed security decisions. These capabilities help organizations reduce downtime, investigate security incidents, and improve the protection of data transmitted across enterprise and cloud networks.

---

## 🧩 Architecture

<img width="1024" height="587" alt="Wireshark Lab Architecture" src="https://github.com/user-attachments/assets/84dfbfdb-e465-4ceb-b676-9b92f0eb1768" />

>Shows the overall process of capturing network traffic and understanding how devices communicate, including how DNS requests and responses work, how TCP connections are established, and how HTTP data is put back together to show web communication.

---

## 🛠️ Technology Stack

| Category | Technology | Purpose in This Project |
|---|---|---|
| **Network Analysis** | Wireshark | Packet capture, protocol analysis, and network traffic inspection. |
| | Wireshark Display Filters | Filtering traffic by protocol, IP address, TCP port, and connection behavior. |
| | Follow TCP Stream | Reconstructing application-level conversations between network endpoints. |
| **Networking Protocols** | TCP/IP | Analyzing connection establishment, packet exchanges, and communication failures. |
| | DNS | Examining domain name queries and responses. |
| | HTTP and HTTPS | Comparing unencrypted and encrypted web traffic. |
| | TLS | Understanding encryption and data protection during network communications. |
| **Analysis and Troubleshooting** | Packet Capture (PCAP/PCAPNG) | Saving and reviewing network traffic for investigation. |
| | TCP Three-Way Handshake | Examining SYN, SYN-ACK, and ACK packets. |
| | Traffic Pattern Analysis | Investigating unusual DNS activity, unanswered TCP connection attempts, and potentially exposed sensitive data. |
| **Security Applications** | Network Troubleshooting | Investigating connectivity and communication issues. |
| | Security Monitoring | Identifying traffic patterns that may warrant further investigation. |
| | Incident Response Fundamentals | Using packet-level evidence to support security investigations. |

---



---

## 🛠️ Technology Stack

| Category | Technology | Purpose in This Project |
|---|---|---|
| **Network Analysis** | Wireshark | Packet capture, protocol analysis, and network traffic inspection. |
| | Wireshark Display Filters | Filtering traffic by protocol, IP address, TCP port, and connection behavior. |
| | Follow TCP Stream | Reconstructing application-level conversations between network endpoints. |
| **Networking Protocols** | TCP/IP | Analyzing connection establishment, packet exchanges, and communication failures. |
| | DNS | Examining domain name queries and responses. |
| | HTTP and HTTPS | Comparing unencrypted and encrypted web traffic. |
| | TLS | Understanding encryption and data protection during network communications. |
| **Analysis and Troubleshooting** | Packet Capture (PCAP/PCAPNG) | Saving and reviewing network traffic for investigation. |
| | TCP Three-Way Handshake | Examining SYN, SYN-ACK, and ACK packets. |
| | Traffic Pattern Analysis | Investigating unusual DNS activity, unanswered TCP connection attempts, and potentially exposed sensitive data. |
| **Security Applications** | Network Troubleshooting | Investigating connectivity and communication issues. |
| | Security Monitoring | Identifying traffic patterns that may warrant further investigation. |
| | Incident Response Fundamentals | Using packet-level evidence to support security investigations. |

---

## ✅ Prerequisites

> **Only capture traffic on networks you own or have permission to monitor.** For this lab, your own home network or machine is fine.

<details>
<summary><b> Step 1: Install Wireshark</b></summary>
<br>

Download the installer for your operating system from [wireshark.org/download.html](https://www.wireshark.org/download.html).

| OS | Download | Notes |
|---|---|---|
| Windows | Windows x64 Installer (.exe) | Accept all defaults. **Install Npcap when prompted.** This is required to capture packets |
| macOS | macOS Arm or Intel (.dmg) | Run the installer. If prompted about **ChmodBPF**, allow it. This gives Wireshark permission to access network interfaces |
| Linux | Use your package manager | `sudo apt install wireshark` (Ubuntu/Debian). Add yourself to the `wireshark` group to capture without root |

```bash
# Linux only: add yourself to the wireshark group (log out and back in after)
sudo usermod -aG wireshark $USER

# Verify Wireshark is installed
wireshark --version
```

On Linux, when the installer asks "Should non-superusers be able to capture packets?", choose **Yes**.

**Check it worked:** Wireshark opens and the welcome screen lists your network interfaces. If the list is empty, the capture driver (Npcap, ChmodBPF, or group membership) was not set up correctly. Re-run the installer or log out and back in.

<img width="1063" height="839" alt="Wireshark Download Page" src="https://github.com/user-attachments/assets/35cd0153-892e-42a6-aadb-14bbaafcd5ea" />

<img width="1032" height="839" alt="Install Wireshark" src="https://github.com/user-attachments/assets/522d9010-c7d3-4435-bd50-0f0f81500b6a" />


</details>

<details>
<summary><b> Step 2: Your First Capture</b></summary>
    
<br>

This step gets you comfortable with the Wireshark interface before doing anything complex.

1. Open Wireshark.
2. On the welcome screen, you’ll see a list of network interfaces, each with a live traffic graph showing network activity in real time.
3. Double-click your active interface (Ethernet or Wi-Fi). Pick the one with the most activity in the wave graph.
4. Wireshark starts capturing immediately. Packets appear in the list in real time.
5. Open a browser and navigate to any website.
6. After 30 seconds, click the red square **Stop** button in the toolbar.

You now have a live packet capture. Each row is one packet, with its time, source, destination, protocol, and a short summary. Click any row and the panes below show the packet broken down layer by layer, plus the raw bytes.

**Optional:** save the capture with **File > Save As** (for example `first-capture.pcapng`) so you can reopen it later without recapturing.

You are ready for the main lab.

<img width="1130" height="685" alt="Wireshark Interface" src="https://github.com/user-attachments/assets/57ff8064-5ab9-41e1-81d0-94cd506f5f7c" />


</details>

---
## 🛠️ Steps

<details>
<summary><b>Step 1: Essential Display Filters</b></summary>

<br>

Type filters into the filter bar at the top of the Wireshark window and press Enter. The packet list updates instantly to show only matching traffic. This is one of the most important skills in the lab.

**Display filters vs Capture filters**

Wireshark has two types of filters. **Capture filters** are applied before capturing and limit what gets recorded. **Display filters** are applied after capturing and limit what you see without discarding anything.

For this lab, always use display filters. They let you look at the same capture through different lenses without having to re-capture. You apply a `dns` filter, look at DNS traffic, then remove it and apply a `tcp` filter to look at something else. The full capture is always there underneath.

| Filter | What it shows | When to use it |
|---|---|---|
| `dns` | All DNS queries and responses | Troubleshooting name resolution, identifying unusual domain lookups |
| `http` | Unencrypted HTTP traffic only | Finding cleartext data, debugging web applications without HTTPS |
| `tcp` | All TCP traffic | Starting point for connectivity investigations |
| `tcp.flags.syn == 1` | TCP SYN packets only (connection attempts) | Seeing which hosts are trying to connect to what |
| `tcp.flags.reset == 1` | TCP RST packets (connection resets) | Finding refused or forcibly closed connections |
| `icmp` | All ICMP traffic including ping | Verifying basic reachability between hosts |
| `ip.addr == 192.168.1.1` | All traffic to or from a specific IP | Isolating traffic for a single host in a busy capture |
| `ip.src == 10.0.0.5` | Traffic from a specific source IP only | Isolating outbound traffic from one host |
| `tcp.port == 443` | All HTTPS traffic | Identifying encrypted web traffic by port |
| `http.request` | HTTP GET and POST requests only | Finding web requests, useful for spotting data exfiltration |

</details>

<details>
<summary><b>Step 2: Guided Exercises</b></summary>

<br>

Work through each exercise in order. Each one builds on the previous and teaches a specific skill you will use in real-world network analysis.

<details>
<summary><b>Exercise A: Capture a DNS Lookup</b></summary>

<br>

**Before you start: what is `nslookup` and where do you run it?**

`nslookup` is a built-in command-line tool that manually performs a DNS lookup. You give it a domain name and it tells you the IP address that DNS returns for it. It lets you trigger a DNS query on demand, which is exactly what you need to generate DNS traffic that Wireshark can capture.

You run `nslookup` on your local machine, **not** inside Wireshark. Wireshark does not have a terminal. It is purely a packet capture and analysis tool. The workflow is:

1. Start a capture in Wireshark.
2. Switch to a separate terminal window on your machine and run the command.
3. Come back to Wireshark and stop the capture.

Wireshark will have recorded the DNS traffic that `nslookup` generated.

**How to open your terminal**

- **Windows:** press the Windows key, type `cmd`, press Enter. This opens Command Prompt.
- **Mac:** press Cmd + Space, type `Terminal`, press Enter.
- **Linux:** right-click the desktop and select Open Terminal, or press Ctrl + Alt + T.

**What is a DNS A record?**

DNS has different record types for different purposes. An **A record** (Address record) maps a domain name to an IPv4 address. It is the most common type. When you type `google.com` into a browser, your computer makes a DNS query asking for the A record for `google.com`, and the response contains the IPv4 address to connect to.

Other record types exist: AAAA records map to IPv6 addresses, MX records identify mail servers, CNAME records are aliases. In this exercise you will see A record queries and responses in Wireshark. The packet shows the record type as a number: type 1 is an A record.

**Steps**

1. In Wireshark, start a capture on your active interface. Click the blue shark fin icon or double-click your interface name.
2. Leave Wireshark running and open a separate terminal window on your local machine (see above for how to open it).
3. In the terminal, type the following command and press Enter:
   ```
   nslookup google.com
   ```
4. The terminal shows the IP address(es) returned for `google.com`. This confirms the DNS lookup worked.
5. Switch back to Wireshark and click the red square **Stop** button.
6. In the Wireshark filter bar at the top, type `dns` and press Enter. The packet list now shows only DNS traffic.
7. Find the query packet for `google.com`. Look in the Info column for "Standard query A google.com". This is your machine asking for the A record.
8. Find the response packet. Look for "Standard query response A google.com". This packet contains the IP address the DNS server returned.
9. Click the DNS response packet to select it. In the bottom half of the Wireshark window (the packet detail pane), click the arrow next to "Domain Name System (response)" to expand it. Look inside for the **Answers** section. You will see the A record with the IP address Google returned. Confirm it matches what your terminal showed when you ran `nslookup`.

**What you just saw:** your machine sent a DNS query asking for the A record for `google.com`. The DNS server replied with an IP address. Your browser then used that IP address to make the actual connection. This invisible lookup happens before every website visit, API call, and email your machine sends.

In the real world, seeing unexpected DNS queries in a capture, such as queries to unusual domains, is often the first sign of malware calling home to a command and control server.

</details>

<details>
<summary><b>Exercise B: Watch the TCP Three-Way Handshake</b></summary>

<br>

1. Start a capture on your active interface.
2. Open a browser and navigate to `http://example.com`. Use HTTP, not HTTPS, because it makes the handshake easier to see.
3. Stop the capture.
4. Run `nslookup example.com` first to get the IP address, then apply the filter: `tcp and ip.addr == [that IP]`
5. Find three packets in order: **SYN → SYN-ACK → ACK**

| Packet | Flags | What it means |
|---|---|---|
| 1st packet | SYN | Your machine: "I want to connect. Here is my sequence number." |
| 2nd packet | SYN, ACK | The server: "I got your request. Here is my sequence number. Connection accepted." |
| 3rd packet | ACK | Your machine: "Got it. Connection is now open. Ready to send data." |

If you see a SYN but no SYN-ACK following it, the connection was refused or the server is unreachable. If you see a RST (reset) packet, the connection was forcibly closed. These two patterns are the most common things network engineers look for when diagnosing connectivity problems.

</details>

<details>
<summary><b>Exercise C: Spot Cleartext Credentials (HTTP)</b></summary>

<br>

> **Educational exercise only.** Only capture on networks and against systems you own or have explicit permission to analyse. Never use this technique against systems you do not own.

1. Set up a test HTTP login form on your local machine, or use a test site that runs over HTTP (not HTTPS).
2. Start a capture.
3. Submit a login form over HTTP with a test username and password.
4. Stop the capture.
5. Apply the filter: `http.request.method == POST`
6. Click the POST packet and look in the packet detail pane. Find the **HTML Form URL Encoded** layer.
7. You will see the username and password in plaintext.

This is why every login form must use HTTPS. Without TLS encryption, anyone on the network path between you and the server (your ISP, a coffee shop router, anyone performing a man-in-the-middle attack) can read your credentials exactly as you typed them. Wireshark is how security teams prove this vulnerability exists and demonstrate it to developers who resist adding HTTPS.

</details>

<details>
<summary><b>Exercise D: Follow a Full TCP Stream</b></summary>

<br>

1. Capture any HTTP traffic by navigating to an HTTP website.
2. Find any HTTP packet in the capture list.
3. Right-click it, then choose **Follow → TCP Stream**.
4. Wireshark reassembles all the packets from that connection into a readable conversation.
5. Red text is your browser's request. Blue text is the server's response.

This is how incident responders reconstruct what happened during a network event. Individual packets are fragments. The stream view shows the complete conversation, which is what you need to understand what data was transferred, what commands were sent, and what the server responded with.

</details>

</details>

<details>
<summary><b>Step 3: Save and Export Captures</b></summary>

<br>

Always save interesting captures. They are evidence of your skills and they are your portfolio entries for this lab.

```text
# Save a capture for later analysis
File → Save As → choose .pcapng format

# Export only the packets matching your current filter
Apply your display filter first
File → Export Specified Packets → Displayed

# Re-open a saved capture
File → Open → select your .pcapng file
```

```bash
# Command-line capture with tshark (included with Wireshark, useful for remote servers)
tshark -i eth0 -w capture.pcapng -c 1000
# -i: interface name   -w: output file   -c: stop after this many packets
```

</details>

## ✅ Validation & Troubleshooting

| Skill | How to verify |
|---|---|
| DNS capture | Apply the `dns` filter and identify a query packet and its response packet. They should have matching transaction IDs |
| TCP handshake | Find three sequential packets with SYN, SYN-ACK, and ACK flags. Explain what each one means without referring to notes |
| Display filters | Filter by IP address, port, and protocol from memory. You should not need to look these up |
| Stream reconstruction | Follow a TCP stream and read the full HTTP request and response as a conversation |
| File management | Save a capture, close Wireshark, reopen it, and load the file. Confirm all packets are there |

---

## 📖 Key Terms

Based on the provided Wireshark lab documentation, here is a curated table of the **Top 10 Most Important Terms and Concepts** essential for network analysis and troubleshooting:

| Rank & Term | Category | Why It Is Crucial |
| --- | --- | --- |
| **1. Packet** | Core Concept | The foundational unit of data captured and inspected by Wireshark, consisting of a header and payload.|
| **2. TCP Three-Way Handshake** | Core Concept | The fundamental connection establishment process (SYN, SYN-ACK, ACK) vital for diagnosing network connectivity and refusal patterns.|
| **3. Display Filter** | Key Term | An essential tool applied after a capture to narrow down and isolate specific traffic without discarding raw data. |
| **4. Promiscuous Mode** | Core Concept | The NIC setting that enables Wireshark to capture network traffic passing across the segment beyond just local machine traffic. |
| **5. TCP Stream** | Key Term | Reassembles all individual packets belonging to a single connection into an end-to-end conversation for easy investigation. |
| **6. Cleartext vs. TLS (Encryption)** | Concept / Term | Explains the security risk of unencrypted HTTP traffic versus secure HTTPS/TLS sessions, demonstrated through captured credentials.|
| **7. DNS (Domain Name System)** | Core Concept | The critical translation layer mapping domain names to IP addresses; if broken, all external application and web traffic fails. |
| **8. Payload** | Core Term | The actual user data carried inside a packet, critical for inspecting application layers or discovering exposed cleartext passwords. |
| **9. Port** | Key Term | Numerical identifiers (like port 53 for DNS or 80 for HTTP) that map traffic to specific network services. |
| **10. Capture Filter** | Key Term | A pre-capture filter used to limit what data gets recorded to disk, optimizing performance and storage. |


---

## 🛠️ Key Skills Demonstrated

**Live Network Traffic Capture:** Setting up and operating Wireshark across local interfaces using capture engines (WinPcap/Npcap) to record raw data packets passing through network interfaces.   

**Advanced Display Filtering:** Writing and applying precise display filters (dns, http, tcp, ip.addr, http.request.method) to isolate specific protocols, IP addresses, ports, or traffic patterns out of thousands of packets.  

**Network Protocol & DNS Analysis:** Executing and investigating DNS queries and responses (nslookup), recognizing A record translations, and tracking name resolution dependencies across network workflows.  

**TCP Handshake & Connectivity Diagnostics:** Analyzing connection establishment phases by identifying sequential TCP flags (SYN, SYN-ACK, ACK), and diagnosing connection failures or resets (RST).  

**Application Layer & Payload Inspection:** Examining packet payloads and HTTP POST requests to uncover security vulnerabilities, such as identifying exposed cleartext credentials and understanding why TLS/HTTPS encryption is mandatory.   

**TCP Stream Reassembly:** Using Wireshark's "Follow TCP Stream" feature to stitch individual fragmented packets back together into complete, readable client-server conversations for incident investigation.   

**Capture Management & CLI Tools:** Saving, exporting specified packets, reopening .pcapng evidence files, and utilizing command-line tools (tshark) for remote server capture workflows.   


## 💡 Key Takeaway

- **Every connection starts with DNS.** Seeing the query and response before each website visit made it clear why broken DNS looks like "the internet is down." It is also where unusual domain lookups would show up first in a real investigation.
- **The TCP handshake is a diagnostic tool.** A SYN with no SYN-ACK points to a refused connection or an unreachable server, and a RST means the connection was forcibly closed. Knowing these patterns turns a vague "it won't connect" into a specific question.
- **HTTP exposes everything.** Finding a test username and password in plaintext in a POST request showed why HTTPS is required on any login form. It is one thing to be told this and another to read the credentials yourself.
- **Following a stream makes packets readable.** Individual packets are fragments. Follow TCP Stream turns them into a conversation, which is how you would reconstruct what actually happened during an incident.
- **Only capture what you own or have permission to monitor.** The credential exercise worked because it ran against my own test system.
   

   
