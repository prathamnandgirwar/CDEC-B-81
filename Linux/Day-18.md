# Basic Networking in Linux

## Overview of Networking Fundamentals
Networking is the process of connecting computers and devices to share resources and communicate.

### Key Concepts
IP Address identifies devices on a network.
Subnet Mask divides an IP address into network and host parts.
Gateway routes traffic between networks.
DNS (Domain Name System) resolves domain names to IP addresses.

## IP Address
Explanation:
Every device needs a unique number to communicate. This is called an IP address.

Demo:
ip addr

## Subnet Mask
Explanation:
Subnet mask tells which part is network and which part is device.

Demo:
ip addr show

## Gateway
Explanation:
Gateway is the exit door to the internet.

Demo:
ip route

## DNS
Explanation:
Humans remember names (google.com), computers understand IPs.

Demo:
nslookup google.com
OR
dig google.com

Explain:
Domain name → IP address

## OSI Model
The OSI (Open Systems Interconnection) Model is a conceptual framework used to understand and implement network protocols.

## Layers
- **Physical Layer**: Hardware components like cables and switches
- **Data Link Layer**: Responsible for error detection and framing (e.g., Ethernet)
- **Network Layer**: Handles routing and IP addressing (e.g., IP protocol)
- **Transport Layer**: Ensures reliable communication (e.g., TCP, UDP)
- **Session Layer**: Manages sessions between applications
- **Presentation Layer**: Formats data (e.g., encryption, compression)
- **Application Layer**: Interfaces with applications (e.g., HTTP, FTP)

## Network Types
LAN (Local Area Network):
Covers a small geographic area, such as an office.
High speed and low latency.

MAN (Metropolitan Area Network):
Covers a city or metropolitan area.
Typically used for city-wide connectivity.

WAN (Wide Area Network):
Covers large geographic areas, such as countries or continents.
Examples include the internet.

## Types of IPs
Static IP:
Permanently assigned to a device.
Commonly used for servers and network devices.

Public IP:
Exposed to the internet.
Unique across the globe.

Private IP:
Used within private networks.
Cannot be accessed directly from the internet.

## Basic Networking Commands
ping 0.0.0.0 - to check internet connectivity
dig - to check domain
curl - to download files from internet and data transfer
wget - to download files
ifconfig - to check ip address
ip addr - to check ip address
nslookup - DNS lookup
netstat - network connections

## ping – Connectivity Test
Explain:
ping checks if the other system is alive.

Demo:
ping google.com
ping 8.8.8.8

## dig – DNS Lookup
dig google.com

## curl – Data Transfer
curl https://example.com
curl -O https://example.com

## wget – Download Files
wget https://example.com

## ifconfig (Old command)
ifconfig

Explain:
Older networking tool.
Shows IP address and MAC address.

## ip addr (Modern command)
ip addr

## nslookup
nslookup google.com

Explain:
Name → IP
Used for DNS troubleshooting.

## systemctl (Service Management)
Explain:
systemctl controls services like start, stop, restart.

Demo:
systemctl status ssh

Start service:
sudo systemctl start ssh

Stop service:
sudo systemctl stop ssh

## journalctl (Logs)
Explain:
journalctl shows system logs.

Demo:
journalctl -n 10

Service logs:
journalctl -u ssh

Live logs:
journalctl -f
