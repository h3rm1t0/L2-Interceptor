# L2-Interceptor 🕸️

![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![Scapy](https://img.shields.io/badge/Library-Scapy-orange.svg)
![Concept](https://img.shields.io/badge/Category-Red_Team-red.svg)

**L2-Interceptor** is a tactical Man-in-the-Middle (MITM) tool designed for localized network traffic interception. Unlike generic automated suites, this tool is built from the ground up using Python and `Scapy`, providing granular control over Layer 2 Ethernet frames and ARP protocol manipulation.

## 🎯 Project Overview

In professional Red Team engagements, network stability is paramount. Standard automation tools often leave target ARP tables corrupted if interrupted, leading to accidental Denial of Service (DoS). This project implements a robust, concurrent architecture that ensures stealthy interception followed by a mandatory "graceful teardown" to restore network integrity.

## ⚙️ Technical Architecture & Key Features

*   **Raw Packet Manipulation:** Direct construction of Ethernet and ARP frames, allowing for precise identity spoofing between a target host and the gateway.
*   **Asynchronous Concurrency (Threading):** 
    *   **Poisoning Thread:** A background *daemon thread* maintains a continuous ARP Poisoning loop to keep the victim's cache entry pointing to the attacker.
    *   **Main Thread:** Operates as a blocking *sniffer* and packet forwarder, ensuring real-time traffic routing without I/O bottlenecks.
*   **Graceful Teardown & Restoration:** Implements a native `SIGINT` (`KeyboardInterrupt`) handler. Upon termination, the tool automatically:
    1.  Broadcasts ARP restoration packets (`ff:ff:ff:ff:ff:ff`) to the victim and the router.
    2.  Disables Linux Kernel IP Forwarding.
    3.  Safely closes all active threads to prevent zombie processes.

#### ⚠️ Disclaimer

This code was developed strictly for information security research, authorized auditing, and network protocol studies. It must not be used on any network without the explicit, written consent of the network administrators. The author is not responsible for any misuse or damage caused by this tool.
pip install scapy

## 🚀 Installation & Usage

**Note:** This tool requires root privileges for raw socket manipulation and Linux Kernel modification (`/proc/sys/net/ipv4/ip_forward`).

### Prerequisites
- Python 3.x
- Scapy

### Setup
```bash
# Clone the repository
git clone [https://github.com/h3rm1t0/L2-Interceptor.git](https://github.com/h3rm1t0/L2-Interceptor.git)

# Navigate to the directory
cd L2-Interceptor

# Install dependencies (if not already installed)

# Run the tool
sudo python3 L2-Interceptor.py


