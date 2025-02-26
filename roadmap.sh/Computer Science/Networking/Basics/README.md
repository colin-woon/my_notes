# Networking Basics

# IP Address

A logical address used to locate your machine in a network.

# Network Device Requirements

All network devices need three essential components:

- **IP Address**
- **Subnet Mask**
- **Gateway** (IP address of the router)

# Local Area Network (LAN)
A **LAN** connects multiple devices within a limited area.

# Switch
A switch connects multiple devices (computers, printers, etc.) and ensures that data is sent directly to the intended recipient instead of being broadcasted to all devices.

# Subnet
Defines the range of your LAN. If devices share the same subnet, they are in the same LAN.

#### Example:

- Device A: `192.168.10.20`
- Device B: `192.168.9.72`
- Subnet Mask: `255.255.0.0`

Explanation:

- Any segment with `255` represents the network identifier.
- Any segment with `0` allows for any value, meaning in this case, `192.168` is the shared network identifier.

# Router
A router forwards data packets between **different networks**.
### Core Functionalities
To communicate outside the LAN, data must go through the router. It provides four core functionalities:
#### **Network Address Translation (NAT)**
- Converts a local device's IP address to a different one to communicate on another network (LAN → WAN).
#### **Firewall**
- Implements a set of passive rules to protect the local network from unauthorized access (WAN ✗→ LAN).
#### **Port Forwarding**
- Allows external network communication through a specific port (WAN → LAN).
#### **Demilitarized Zone (DMZ)**
- Allows direct access to a specified device from outside any network (WAN ⇄ DMZ).