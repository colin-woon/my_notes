# Networking Basics

- IP Address - logical address to locate your machine in a network
- All network devices will need 3 things
	- IP
	- Subnet
	- Gateway (IP address of the router)
## Local Area Network (LAN)
- Switch - It connects multiple devices (computers, printers, etc.) and ensures that data gets sent directly to the right device instead of being broadcasted to everyone.
#### Subnet
- defines the range of your LAN
- if devices share the same subnet, they are in the same LAN
- eg:
	A - 192.168.10.20
	B - 192.168.9.72
	Their subnet is 255.255.0.0
	Anything with 255 means its the identifier, and the 0 indicates it can be any value, so in this scenario, 192.168 is the identifier

## Router
- forwards data packets between **different networks**
- to **communicate outside the LAN, it must go through the router**
- has 4 core functionalities as a gateway device
	- **Network Address Translation (NAT)**
		- (LAN > WAN) translates a network device's IP address to a different one to communicate on another network
	- **Firewall**
		-  (WAN x> LAN) set of passive rules to protect local network from unauthorized access
		- **Port Forwarding**
			- (WAN > LAN) only allows external network communication through a certain port
		- **Demilitarized Zone (DMZ)**
			- (WAN <> DMZ) allows direct access to anyone outside of any network 