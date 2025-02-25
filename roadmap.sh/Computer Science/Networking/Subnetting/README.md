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
	- when converting binary to base 10, we go from right to left, so the 2 bits is 2^7 + 2\^6, since rightmost will start at 2^0 (\[00000001], 1\*2^0)
	- 128 + 64 = 192
	- final subnet mask is 255.255.255.192 

# Calculating Network Address
IP Address: 205.150.65.0/26
Subnet Mask: 255.255.255.192
1. To find network address manually, you need to convert the IP Address and the Subnet Mask to binary, then do an AND operation with the bits
2. Or you can use a binary calculator and find the AND operation with the decimals
3. Say if the ip address is 0, it will always result in 0 for AND, cause 0 + 1 is still 0

# Calculating number of Subnets & Hosts
`# of subnets = 2^n`     `# of hosts = 2^r-2`
`n = extra bits from CIDR range, its either 8, 16, 24`
`r = remaining bits in an octet after deducting the subnet bits`
1. Using the previous example, 26 - 24 is 2 bits, so:
	- number of subnets = 2^2 = 4
2. in 8 bits, 2 bits is reserve for the subnets, so remaining is 6 bits
	- number of hosts = 2^6 - 2 = 64 - 2 = 62

# Calculating Broadcast Address
1. Determine the Network Address = 205.150.65.0
2. Determine the Host Address range = 62
	- 1st Host Address = 205.150.65.1
	- Last Host Address = 205.150.65.62
3. Finally, Broadcast Address is = 205.150.65.63

#### Next network address will start from .64, there will be a total of 4 subnets as calculated


# Creating Subnets
### Problem: Create 10 subnets
Ori IP Address: 205.150.65.0/24
Ori Subnet Mask: 255.255.255.0

1. using formula 2^n to find total subnets, compare it with the \<number of subnets required>
	- nearest possible value to accommodate 10 subnets is 2^4 = 16, 2^3 = 8 is not enough
	- convert and find the new subnet mask
New IP Address:  205.150.65.0/24
New Subnet Mask: 255.255.255.
