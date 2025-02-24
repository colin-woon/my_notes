# IPv4
- xxx.xxx.xxx.xxx, a 32-bit binary/ 4 octets/ 4 bytes
- maximum value of 1 byte is 255 or 11111111

| Class | Address Range               | Leading Bits | Default Subnet Mask | Hosts per Network | Usage                                              |
| ----- | --------------------------- | ------------ | ------------------- | ----------------- | -------------------------------------------------- |
| A     | 1.0.0.0 - 126.255.255.255   | 0            | 255.0.0.0 (/8)      | 16 million+       | Large networks (ISPs, enterprises)                 |
| B     | 128.0.0.0 - 191.255.255.255 | 10           | 255.255.0.0 (/16)   | 65,000+           | Medium-sized networks (universities, corporations) |
| C     | 192.0.0.0 - 223.255.255.255 | 110          | 255.255.255.0 (/24) | 254               | Small networks (home, small businesses)            |
| D     | 224.0.0.0 - 239.255.255.255 | 1110         | N/A                 | N/A               | Multicasting (one-to-many communication)           |
| E     | 240.0.0.0 - 255.255.255.255 | 1111         | N/A                 | N/A               | Experimental, research, future use                 |

### Special Address Ranges

- **127.0.0.0 - 127.255.255.255** → Loopback addresses (Local testing)
- **169.254.0.0 - 169.254.255.255** → APIPA (Automatic Private IP Addressing, assigned when DHCP fails)
