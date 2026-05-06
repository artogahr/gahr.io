+++
title = "Computer Networking: A Gentle Introduction"
date = 2025-04-23
description = "A practical overview of networking fundamentals for developers and sysadmins."
[taxonomies]
tags = ["networking", "devops", "guide"]
+++

## Why Network Knowledge Matters

- Troubleshoot problems faster
- Make better architectural decisions
- Understand security implications
- Communicate effectively with network teams
- Optimize application performance

---

## The Basics and the Why

The fundamental purpose of networking is enabling computers to communicate with each other. You can directly connect two laptops via ethernet cable for data exchange—it's that straightforward.

**Internet Protocol (IP)** serves as the standard for network communication today. When a physical connection exists between computers, IP addresses function as "logical home addresses" so packets reach their destinations. MAC addresses represent the actual burned-in physical addresses of network adapters, while IP addresses are dynamic and changeable.

IPv4 supports 4,294,967,296 possible addresses—insufficient for today's device density. Networks are therefore segregated into local networks with gateway routers connecting them globally.

**Local IP address ranges** (non-routable on the public internet):
- 10.x.x.x
- 172.16.x.x – 172.32.x.x
- 192.168.x.x (most common in home networks)

Your ISP provides your router a single public IP address; devices behind it route through it to access the internet.

### IPv6

This newer protocol uses 128-bit addresses instead of 32, providing vastly more addresses. However, adoption remains limited outside mobile networks. An example IPv6 address: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### Subnetting

The numbers following IP addresses (e.g., `/24`) define the subnet—the range of IP addresses that specific IP belongs to. As a practical rule: "use /24."

---

## DHCP

The Dynamic Host Configuration Protocol automatically assigns IP addresses. When a device joins a network, it broadcasts a request; the DHCP server replies with an available address from its pool.

---

## DNS

**DNS = Domain Name System**

DNS translates human-readable domain names to IP addresses. When your computer needs to access a website, it sends a DNS request to your configured DNS server, which follows a hierarchical chain until finding the answer.

**Common public DNS servers:**
- 8.8.8.8 (Google)
- 1.1.1.1 (Cloudflare)
- 9.9.9.9 (Quad9)

---

## Ports

Each network interface supports 65,535 ports, allowing multiple applications on one computer. One application can bind to many ports, but each port accommodates only one process.

**Standard port assignments:**
- 443 (HTTPS)
- 80 (HTTP)
- 22 (SSH)
- 3389 (RDP)
- 53 (DNS)

---

## Network Devices

#### Modems & Cables
Convert analog signals to digital data. Modern installations use Ethernet cables with CAT5e (adequate for most users) or CAT6 (recommended for best performance). Fiber-optic cables transmit signals as light, offering greater reliability over distance and faster speeds.

#### Routers
Route IP packets to their destinations using specialized protocols that auto-update routing tables, enabling global connectivity.

#### Wi-Fi Access Points
Wireless antennas allowing network access via Wi-Fi; enterprise versions maintain connections when moving between access points.

#### Firewalls
Restrict packet flow to protect devices from unauthorized external access based on IP addresses, ports, and other identifying information.

#### Switches
Direct traffic within local networks by learning which devices connect to which ports, only sending data where needed.

---

## Essential Network Diagnostic Commands

### ping
Tests basic connectivity and measures round-trip time.
```
ping google.com
```

### traceroute/tracert
Shows the network path to a destination.
```
# Linux/macOS
traceroute google.com

# Windows
tracert google.com
```

### nslookup/dig
Manually queries DNS servers for domain-to-IP translations.
```
# Linux/macOS
dig google.com

# Windows
nslookup google.com
```

### netstat/ss
Checks open ports and identifies processes using specific ports.
```
# Linux
ss -tuln

# Windows
netstat -an | findstr LISTEN
```

### Advanced: Network Capture

**tcpdump** (Linux/macOS)
```
sudo tcpdump -i eth0 host 192.168.1.5 and port 80
```

**Wireshark**  
GUI-based packet analyzer with deep inspection and powerful filtering capabilities.

---

## Common Networking Issues & Solutions

### "It works on my machine"
- Verify matching network configurations
- Check firewall rules
- Confirm DNS resolution consistency
- Identify differing proxy settings

### Connection Timeouts
- Verify the service runs
- Confirm correct and open ports
- Check firewall blocking
- Validate DNS accuracy

---

## Additional Topics

### VPNs
Virtual Private Networks extend private networks across public ones. They encrypt traffic but incur performance costs.

### Cloud Networking
Cloud infrastructure allows defining networks as code, eliminating manual configuration requests.

### Container Networking
Docker and Kubernetes containers use:
- **Bridge Networks:** Create private container networks
- **Host Networks:** Share the host's network namespace
- **Overlay Networks:** Enable communication across hosts
- **Service Discovery:** Automatic container location

Containers being ephemeral requires DNS rather than hardcoded IP addresses.

### Security Considerations

"If you wouldn't shout it across a crowded coffee shop, it shouldn't travel over the network unencrypted." HTTPS provides encryption—visible via the browser lock icon—preventing ISPs, governments, and third parties from viewing communication contents. However, DNS queries typically remain unencrypted, revealing which sites you visit.

---

## Conclusion

Understanding networking fundamentals prevents countless hours of frustration. When troubleshooting connections, firewalls and network configuration should be checked systematically. These concepts and tools provide the foundation for diagnosing most connectivity issues effectively.
