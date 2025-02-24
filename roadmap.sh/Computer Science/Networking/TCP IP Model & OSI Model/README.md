These models define now data is transmitted over networks

| Feature     | TCP/IP Model                          | OSI Model                                  |
|------------|--------------------------------------|-------------------------------------------|
| Layers     | 4                                    | 7                                         |
| Usage      | Practical, internet-based           | Theoretical, for understanding networking |
| Protocols  | TCP, IP, UDP, HTTP, FTP, etc.       | Conceptual framework, less focus on specific protocols |
| Flexibility| More flexible, adapted for real-world applications | More structured but complex |

# OSI (Open Systems Interconnection)
- Used mainly for understanding how networks function and troubleshooting.
- **Layers:**
    1. **Physical** – Cables, signals, and hardware.
    2. **Data Link** – MAC addresses, error detection (Ethernet, Wi-Fi).
    3. **Network** – Routing and IP addressing.
    4. **Transport** – Reliable data transmission (TCP, UDP).
    5. **Session** – Establishing and managing sessions between devices.
    6. **Presentation** – Encryption, compression, and format conversion.
    7. **Application** – Interfaces with user applications (HTTP, DNS, SMTP).
- Client side goes from 7-1 then 1-7 to the server and vice versa

# TCP/IP (Transmission Control Protocol/Internet Protocol)
- Designed for **practical implementation** and focuses on reliable communication.
- **Layers:**
	1. **Network Interface (Link) Layer** – Handles physical hardware and data transmission.
	2. **Internet Layer** – Routes packets using IP addresses (IP, ICMP, ARP).
	3. **Transport Layer** – Ensures reliable data transfer (TCP for reliability, UDP for speed).
	4. **Application Layer** – User-facing protocols like HTTP, FTP, and SMTP.

### **Key Takeaway**

- **TCP/IP is the actual model used in networking today.**
- **OSI helps understand and troubleshoot networking concepts.**
- TCP/IP maps onto OSI roughly as:
    - **Application (TCP/IP) → Application, Presentation, Session (OSI)**
    - **Transport (TCP/IP) → Transport (OSI)**
    - **Internet (TCP/IP) → Network (OSI)**
    - **Network Interface (TCP/IP) → Data Link, Physical (OSI)**