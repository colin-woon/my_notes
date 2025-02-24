# IPv4
- xxx.xxx.xxx.xxx, a 32-bit binary/ 4 octets/ 4 bytes
- maximum value of 1 byte is 255 or 11111111
- an IP address consist of 2 parts
	- Network IDs (used for identifying the network, subnet mask)
	- Host IDs (used for identifying the network device)

# Private IPs (only for LANs)
- 10.0.0.0
- 172.16.0.0
- 192.168.0.0

# Public IPs

| Class | Address Range               | Leading Bits | Default Subnet Mask | Hosts per Network | Usage                                              |
| ----- | --------------------------- | ------------ | ------------------- | ----------------- | -------------------------------------------------- |
| A     | 1.0.0.0 - 126.255.255.255   | 0            | 255.0.0.0 (/8)      | 16 million+       | Large networks (ISPs, enterprises)                 |
| B     | 128.0.0.0 - 191.255.255.255 | 10           | 255.255.0.0 (/16)   | 65,000+           | Medium-sized networks (universities, corporations) |
| C     | 192.0.0.0 - 223.255.255.255 | 110          | 255.255.255.0 (/24) | 254               | Small networks (home, small businesses)            |
| D     | 224.0.0.0 - 239.255.255.255 | 1110         | N/A                 | N/A               | Multicasting (one-to-many communication)           |
| E     | 240.0.0.0 - 255.255.255.255 | 1111         | N/A                 | N/A               | Experimental, research, future use                 |
- Host per network depends on default subnet masks,
eg: 255.0.0.0 = 2^24
that consists of 3 2^8
2^24 - 2 (network & broadcast address) = host per network

- Leading Bits in the 1st octet determine its class, will also determine the number of networks
	- class A *0*1111111 NHHH 2^7 = 126 
	- class B *10*111111 NNHH 2^6 * 2^8 = 16 384 
	- class C *110*11111 NNNH 2^5 * 2^8 * 2^8 = 2 million
	- N - octet for network
	- H - octet for hosts

### Special Address Ranges
- **127.0.0.0 - 127.255.255.255** → Loopback addresses (Local testing) (LOCALHOST 127.0.0.0)
- **169.254.0.0 - 169.254.255.255** → APIPA (Automatic Private IP Addressing, assigned when DHCP fails)

# 2^Host_bits - 2
- 0 network IP
- 255 broadcast IP
