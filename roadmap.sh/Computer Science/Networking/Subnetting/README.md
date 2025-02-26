# Subnetting Notes

## Subnet Mask
A subnet mask is used to denote network addresses and host addresses. It is not an entity in the network but a way to segment IP addresses.

## CIDR (Classless Inter-Domain Routing)
CIDR represents an IP address with a slash (`/`) followed by a number, which defines the number of bits used for the **network** portion.

### Examples:
- `192.168.1.0/24` → First 24 bits are used for the network.
- `192.168.1.0/27` → First 27 bits are used for the network, meaning the host address starts after that.
  - **Binary representation:** `[8 bits][8 bits][8 bits][11100000]` → The zeros are for host addresses.

## Key Terms:
- **Network ID**: First address of the subnet range.
- **Broadcast ID**: Last address of the subnet range.

---

## Calculating a Subnet Mask
Example: `205.150.65.0/26`

1. The maximum bits are `32`, and each octet is `8` bits.
   - `24 bits` are preoccupied → Base subnet mask: `255.255.255.0`
2. Since `26 - 24 = 2`, the network address occupies 2 extra bits.
   - **Binary representation:** `[24 bits][1100000]`
   - Convert extra bits to base 10: `2^7 + 2^6 = 128 + 64 = 192`
   - **Final Subnet Mask:** `255.255.255.192`

---

## Calculating the Network Address
Given:
- **IP Address:** `205.150.65.0/26`
- **Subnet Mask:** `255.255.255.192`

### Steps:
1. Convert IP Address and Subnet Mask to binary.
2. Perform an **AND operation** between them.
3. The result is the **Network Address**.

Alternatively, use a binary calculator to perform the AND operation directly.

---

## Calculating the Number of Subnets & Hosts
### Formulas:
- `# of subnets = 2^n`
- `# of hosts = 2^r - 2`
  - `n = extra bits from CIDR range (8, 16, 24, etc.)`
  - `r = remaining bits in an octet after deducting the subnet bits`

### Example (`/26` CIDR):
1. `26 - 24 = 2` bits → `2^2 = 4` subnets.
2. Remaining bits in the last octet: `8 - 2 = 6`.
   - `2^6 - 2 = 64 - 2 = 62` hosts.

---

## Calculating the Broadcast Address
### Steps:
1. **Determine the Network Address:** `205.150.65.0`
2. **Determine the Host Address range:** `62`
   - First Host Address: `205.150.65.1`
   - Last Host Address: `205.150.65.62`
3. **Broadcast Address:** `205.150.65.63`

🔹 **Next network address starts from `205.150.65.64`.** There are **4 total subnets** as calculated.

---

## Creating Subnets
### Problem: Create 10 subnets
Given:
- **Original IP Address:** `205.150.65.0/24`
- **Original Subnet Mask:** `255.255.255.0`

### Steps:
1. Use `2^n` to find total subnets:
   - **10 subnets required** → Closest power of `2` is `2^4 = 16` (since `2^3 = 8` is too small).
   - **Need 4 extra bits** → `24 + 4 = 28`.
2. Convert to find the new subnet mask.
   - **New CIDR:** `/28`
   - **New Subnet Mask:** `255.255.255.240`
   - **Network Address:** `205.150.65.0`
   - **Number of Hosts:** `2^4 - 2 = 14`
   - **Host Range:** `205.150.65.1 - 205.150.65.14`
   - **Broadcast Address:** `205.150.65.15`

🔹 **Each subnet now has 16 IP addresses (14 usable hosts).**
