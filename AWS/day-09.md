# 📘 Basics of Networking & CIDR Calculation

---

# 🌐 1. Basics of Networking

## 🔹 What is Networking?

**Networking** is the process of connecting two or more devices so they can communicate and share data with each other.

Examples of network devices:

* Computer
* Laptop
* Mobile
* Server
* Router
* Switch
* Printer

### Simple Example

```text
Laptop
   │
   ↓
Wi-Fi Router
   │
   ├── Mobile
   ├── Laptop
   └── Server
```

---

# 🆔 2. What is a MAC Address?

**MAC (Media Access Control) Address** is a unique hardware address assigned to a network interface.

It works at **Layer 2 (Data Link Layer)** of the OSI model.

Example:

```text
00:1A:2B:3C:4D:5E
```

### Important Points

* MAC address identifies a network interface.
* Usually represented in hexadecimal.
* Used for communication within a local network.
* A device can have different MAC addresses for different network interfaces.

Example:

```text
Laptop
 ├── Wi-Fi → MAC Address
 └── Ethernet → MAC Address
```

---

# 🌍 3. What is an IP Address?

An **IP (Internet Protocol) address** is a logical address assigned to a device or network interface so that it can communicate over an IP network.

Example:

```text
192.168.1.10
```

IP addresses are mainly used to identify:

* Network
* Host/device

---

# 🔢 4. Types of IP Addresses

There are two major versions of IP:

```text
IPv4
IPv6
```

---

# 4.1 IPv4

**IPv4 (Internet Protocol Version 4)** is the most commonly encountered IP addressing format.

IPv4 uses **32 bits**.

It is divided into **4 octets**, with each octet containing 8 bits.

```text
32 bits
   ↓
8 bits | 8 bits | 8 bits | 8 bits
```

Example:

```text
192.168.1.10
```

Each octet can have a value from:

```text
0 – 255
```

### Example

```text
192    .    168    .    1    .    10
 ↑          ↑          ↑         ↑
Octet      Octet      Octet     Octet
```

---

# 4.2 IPv6

**IPv6 (Internet Protocol Version 6)** was developed to provide a much larger address space than IPv4.

IPv6 uses **128 bits**.

Example:

```text
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

IPv6 is written using hexadecimal numbers separated by `:`.

### IPv4 vs IPv6

| Feature              | IPv4           | IPv6          |
| -------------------- | -------------- | ------------- |
| Address Size         | 32 bits        | 128 bits      |
| Format               | Decimal        | Hexadecimal   |
| Example              | `192.168.1.10` | `2001:db8::1` |
| Address Availability | Limited        | Very large    |
| Separator            | `.`            | `:`           |

---

# 🏠 5. Public IP Address

A **Public IP** is an IP address that can be used for communication over the public internet.

Example:

```text
8.8.8.8
```

Public IP addresses must be globally unique.

Examples of where public IPs can be used:

* Web servers
* Load balancers
* Internet-facing applications
* AWS EC2 instances

---

# 🔒 6. Private IP Address

A **Private IP** is used inside a private/internal network.

Private IP addresses are not directly routable over the public internet.

### Private IPv4 Ranges

```text
10.0.0.0/8
```

```text
172.16.0.0/12
```

```text
192.168.0.0/16
```

### Examples

```text
10.0.0.10
172.16.1.20
192.168.1.10
```

Private IPs are commonly used in:

* Home networks
* Office networks
* AWS VPC
* Azure VNet
* Internal application networks

---

# 🖥️ 7. What is a Host?

A **host** is a device or system connected to a network that has an IP address.

Examples:

* Laptop
* Computer
* EC2 instance
* Server
* Printer
* Mobile phone

Example:

```text
Network: 192.168.1.0/24

Hosts:

192.168.1.10
192.168.1.11
192.168.1.12
```

Here, each device using one of these IP addresses can be considered a host.

---

# 🌐 8. What is a Network?

A **network** is a group of IP addresses that belong to the same logical network.

Example:

```text
192.168.1.0/24
```

This represents a network.

Hosts can exist inside this network:

```text
192.168.1.1
192.168.1.2
192.168.1.3
...
192.168.1.254
```

### Simple Concept

```text
Network
   │
   ├── Host 1
   ├── Host 2
   ├── Host 3
   └── Host 4
```

---

# 🧩 9. Network Portion vs Host Portion

An IP address can be divided into:

```text
Network Portion + Host Portion
```

For example:

```text
192.168.1.10/24
```

The `/24` means:

```text
Network Bits = 24
Host Bits    = 8
```

Therefore:

```text
192.168.1 | 10
   Network | Host
```

---

# 🔢 10. What is CIDR?

**CIDR** stands for:

> **Classless Inter-Domain Routing**

CIDR is a method used to represent IP networks using a **prefix length**.

CIDR notation looks like:

```text
IP Address / Prefix Length
```

Example:

```text
192.168.1.0/24
```

Here:

```text
192.168.1.0 → Network Address
/24          → Prefix Length
```

---

# 🧠 11. What Does `/24` Mean?

IPv4 contains:

```text
32 bits
```

If we have:

```text
/24
```

it means:

```text
24 bits → Network
8 bits  → Host
```

Because:

```text
32 - 24 = 8
```

Therefore:

```text
Network Bits = 24
Host Bits = 8
```

---

# 📊 12. CIDR Examples

| CIDR  | Network Bits | Host Bits | Total IPs | Usable Hosts* |
| ----- | -----------: | --------: | --------: | ------------: |
| `/24` |           24 |         8 |       256 |           254 |
| `/25` |           25 |         7 |       128 |           126 |
| `/26` |           26 |         6 |        64 |            62 |
| `/27` |           27 |         5 |        32 |            30 |
| `/28` |           28 |         4 |        16 |            14 |
| `/29` |           29 |         3 |         8 |             6 |
| `/30` |           30 |         2 |         4 |             2 |

> *The usable-host calculation shown here is the traditional IPv4 calculation of total addresses minus network and broadcast addresses. AWS VPC subnets reserve additional IPv4 addresses, so AWS usable IP counts differ.

---

# 🧮 13. Host Calculation Formula

The basic formula for total IPv4 addresses is:

```text
Total IPs = 2^(32 - Prefix Length)
```

Traditional usable-host calculation:

```text
Usable Hosts = Total IPs - 2
```

### Example: `/24`

```text
2^(32 - 24)
= 2^8
= 256
```

Traditional usable hosts:

```text
256 - 2
= 254
```

---

# 📌 14. IPv4 Binary Structure

IPv4 contains 32 bits:

```text
8 bits     8 bits     8 bits     8 bits
   ↓          ↓          ↓          ↓
11111111 . 11111111 . 11111111 . 00000000
```

The bit values of one octet are:

```text
128 64 32 16 8 4 2 1
```

Example:

```text
192
```

Binary:

```text
11000000
```

Because:

```text
128 + 64 = 192
```

---

# 🧮 15. CIDR Calculation Example – `/24`

### IP Address

```text
172.68.1.0/24
```

### Binary Subnet Mask

```text
11111111.11111111.11111111.00000000
```

### Subnet Mask

```text
255.255.255.0
```

### Network Bits

```text
24
```

### Host Bits

```text
32 - 24 = 8
```

### Total IPs

```text
2^8 = 256
```

### Traditional Usable Hosts

```text
256 - 2 = 254
```

### Network Address

```text
172.68.1.0
```

### Broadcast Address

```text
172.68.1.255
```

### Host Range

```text
172.68.1.1
      ↓
172.68.1.254
```

---

# 🧠 16. Magic Number

The **Magic Number** is a subnetting shortcut used to quickly calculate network ranges.

### Formula

```text
Magic Number = 256 - Subnet Mask Value
```

For `/26`:

```text
Subnet Mask = 255.255.255.192
```

Therefore:

```text
256 - 192 = 64
```

Magic Number:

```text
64
```

---

# 🧮 17. CIDR Calculation Example – `/26`

### IP Address

```text
172.68.1.0/26
```

### Binary Subnet Mask

```text
11111111.11111111.11111111.11000000
```

### Subnet Mask

```text
255.255.255.192
```

### Network Bits

```text
26
```

### Host Bits

```text
32 - 26 = 6
```

### Total IPs

```text
2^6 = 64
```

### Traditional Usable Hosts

```text
64 - 2 = 62
```

### Magic Number

```text
256 - 192 = 64
```

---

# 📊 18. Network Ranges for `/26`

A `/26` network creates four ranges within the `/24` block:

| Network Address | Usable Host Range             | Broadcast      |
| --------------- | ----------------------------- | -------------- |
| `172.68.1.0`    | `172.68.1.1 – 172.68.1.62`    | `172.68.1.63`  |
| `172.68.1.64`   | `172.68.1.65 – 172.68.1.126`  | `172.68.1.127` |
| `172.68.1.128`  | `172.68.1.129 – 172.68.1.190` | `172.68.1.191` |
| `172.68.1.192`  | `172.68.1.193 – 172.68.1.254` | `172.68.1.255` |

---

# 🔀 19. What is Subnetting?

**Subnetting** is the process of dividing one larger network into multiple smaller networks.

Example:

```text
192.168.1.0/24
```

can be divided into four `/26` networks:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

### Why do we use Subnetting?

* Better IP address management
* Network segmentation
* Security
* Reduced broadcast domain
* Separating different workloads

---

# ☁️ 20. CIDR in AWS VPC

CIDR is very important when creating an AWS VPC.

Example:

```text
VPC CIDR:
192.168.0.0/16
```

We can create smaller subnets inside it:

```text
Public Subnet:
192.168.1.0/24

Private Subnet:
192.168.2.0/24
```

Architecture:

```text
VPC
192.168.0.0/16
       │
       ├── Public Subnet
       │   192.168.1.0/24
       │
       └── Private Subnet
           192.168.2.0/24
```

The subnet CIDR must be within the VPC CIDR and should not overlap with another subnet in the same VPC.

---

# 🧠 21. Important Networking Terms

| Term              | Meaning                                                         |
| ----------------- | --------------------------------------------------------------- |
| MAC Address       | Hardware/network-interface address                              |
| IP Address        | Logical network address                                         |
| IPv4              | 32-bit IP addressing system                                     |
| IPv6              | 128-bit IP addressing system                                    |
| Public IP         | IP used for public internet communication                       |
| Private IP        | IP used inside private networks                                 |
| Network           | Logical group/range of IP addresses                             |
| Host              | Device/system connected to a network                            |
| CIDR              | Notation used to represent IP network ranges                    |
| Subnet            | Smaller network created from a larger network                   |
| Subnet Mask       | Determines network and host portions                            |
| Network Address   | Identifies the network                                          |
| Broadcast Address | Used to communicate with all hosts in a traditional IPv4 subnet |

---

# 🔑 One-Line Summary

```text
MAC Address → Identifies Network Interface
       ↓
IP Address → Identifies Logical Network Location
       ↓
Network + Host
       ↓
CIDR → Defines Network Size
       ↓
Subnetting → Divides Network into Smaller Networks
```

