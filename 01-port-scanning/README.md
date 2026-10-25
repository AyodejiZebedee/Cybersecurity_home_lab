## 🌐 Project 1 : Target System Infrastructure Analysis

### Objective
To analyze the security posture, exposed services, and attack surface of a live target system utilizing specific IP-based reconnaissance.

### Methodology & Tools
* **Platform:** Kali Linux 2025.4 
* **Tool:** Nmap (Network Mapper) v7.99
* **Target System IP:** `198.167.98.45`

### Technical Execution
The following command was executed to actively probe the target system's communication channels:
```bash
nmap -v -oN target_ip_results.txt 198.167.98.45
```

### Data Collection & Technical Analysis

The scan successfully mapped the host infrastructure and fingerprinted three critical open ports:

| Port / Protocol | State | Default Service | Practical Security Analysis & Risk Assessment |
| :--- | :--- | :--- | :--- |
| **22 / TCP** | `open` | SSH (Secure Shell) | **Remote System Access:** Provides command-line terminal management. Because this channel is exposed externally, it is highly vulnerable to brute-force credential attacks. Hardening via public-key authentication and rate-limiting is strongly recommended. |
| **80 / TCP** | `open` | HTTP (Web Server) | **Unencrypted Legacy Web Gateway:** Serves standard web traffic. Any data transmitted over this connection travels in cleartext. Best security practices mandate redirecting all incoming traffic on this port automatically to HTTPS. |
| **443 / TCP** | `open` | HTTPS (Secure Web Server) | **Encrypted Modern Web Gateway:** Indicates the server supports SSL/TLS encryption. This ensures data transport integrity and confidentiality, preventing local data sniffing or MiTM (Man-in-the-Middle) payload interception. |

### Architectural Conclusion
The discovered port combination indicates this host is structured as a **secure public-facing web server environment** that allows remote developer/administrator access. 

While the inclusion of **HTTPS (Port 443)** 
