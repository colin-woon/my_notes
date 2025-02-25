### Subnet Mask - used to denote network addresses and host addresses, not an entity in the network
### CIDR (Classless Inter-Domain Route) represents an IP address with a slash (/) followed by a number, which defines the number of bits used for the **network** portion.
- eg: 192.168.1.0/24 (first 24 bits is used for the network)
- if its 192.162.1.0/27 (first 27 bits is used for the network, meaning the host address starts after that, and it always goes left to right)  \[8 bits]\[8 bits]\[8 bits]\[11100000] the zeros are for host addresses
### Network ID - first ID of the subnet range 

### Broadcast ID - last ID of the subnet range