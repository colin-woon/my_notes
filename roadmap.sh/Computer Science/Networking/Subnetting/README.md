### Subnet Mask - used to denote network addresses and host addresses, not an entity in the network


### CIDR (Classless Inter-Domain Route) represents an IP address with a slash (/) followed by a number, which defines the number of bits used for the **network** portion.
- eg: 192.168.1.0/24 (first 24 bits is used for the network)
- if its 192.162.1.0/27 (first 27 bits is used for the network, meaning the host address starts after that, and it always goes left to right)  \[8 bits]\[8 bits]\[8 bits]\[11100000] the zeros are for host addresses

### Network ID - first ID of the subnet range 
### Broadcast ID - last ID of the subnet range

# Calculating a subnet mask
205.150.65.0/26
1. we know maximum is 32 bits, and each octet is 8 bits, means 24 bits is preoccupied
	- means subnet mask should be 255.255.255.0
2. but 26 - 24 = 2, meaning from left to right, there the network address occupies 2 extra bits
	- \[24bits]\[1100000]
	- when converting binary to base 10, we go from right to left, so the 2 bits is 2^7 + 2\^6
	- 128 + 64 = 192
	- final subnet mask is 255.255.255.192 

