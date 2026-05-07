+++
title = "Computer Networking: A Gentle Introduction"
date = 2025-04-23
description = "A gentle beginner's guide to Computer Networks."
[taxonomies]
tags = ["networking", "devops", "guide"]
+++

Computer networking is often more complicated than expected, but just learning the basics can help many of y'all in your development journeys. Even though I do different things these days, I have a background and certificates in networking, so might as well talk about it :)

## Why Network Knowledge Matters
- Troubleshoot problems faster
- Make better architectural decisions
- Understand security implications
- Communicate effectively with network teams
- Optimize application performance

---

## The basics, and the why

There are many concepts in there, but an important part of teaching is knowing what to leave out. I could preach to you about the layers of OSI or TCP/IP models (popular topics), but I don't think you actually need to know about them.

The point of networking is to have computers be able to talk to each other. It is a desired ability for computers, otherwise they get lonely.

You can, actually, just connect an ethernet cable between two laptops, and have them communicate, send data etc. It's that simple.

_The_ protocol for network communication these days is called *Internet Protocol* (a.k.a. IP). If a physical connection is established between computers (be it a direct cable, a connection through switch, or a remoter connection through routers, or a remoter-er connection through layers of VPNs), IP addresses will act as a "logical home address" of the computers, so they know where to send the packets to. There are also MAC addresses, which are actual burned-in physical addresses of your network adapters, and are specific to your device in your local physical network. IP addresses on the other hand, are designed to be dynamic and easily changeable.

There are 4294967296 possible IP addresses in the 4th version (de-facto version still, unfortunately) of the protocol (called IPv4). Spoiler alert, there are way more connected devices than that now. Therefore it has become necessary to segregate networks into local networks and have a gateway to connect them to the world, which is usually handled by your router (will get into the devices later).

As a rule-of-thumb, any IP address that looks like:
- 10.x.x.x (a.k.a. anything that starts with 10)
- 172.16.x.x - 172.32.x.x
- 192.168.x.x (most popular in home networks)

... are defined as local IP addresses, and aren't usable in the global internet.

If you check your IP address in your device, you'll see that you have an IP address from one of those, so how come you're able to connect to internet? Well your ISP (Internet Service Provider, e.g. Vodafone) gives _your router_ a single _public_ IP address, and anything that is behind it gets routed (get it?) through it.

As a consequence of this, you aren't able to just give your public IP address to anyone and have them directly connect to you. There are ways to get around it using stuff like port forwarding if you're lucky, but probably you are not (look up CGNAT if you want to get angry).

### IPv6
To mitigate these issues, a new protocol was defined, that has 128 bits of address space instead of 32. This means every screen pixel in every iPhone in the world could have its own _public_ IP address and we'd still have more than enough addresses left over—by a margin of over 10^23 times. Therefore no advanced routing, no NAT etc. shenanigans are needed, and networking should be much simpler.

So why wasn't I talking about it? Well outside of mobile carrier networks, it still hasn't taken off unfortunately. A big reason is that we've lost the ability to just say and remember the addresses out loud. Here's what an IPv6 address looks like: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### Subnetting
Those numbers you often see after IP address spaces like (192.168.1.1**/24**) define the subnet of a specific IP address, or in other words, the range of the IP addresses this specific IP belongs to. Can also be used to define the range itself. You can read more about the math [here](https://en.wikipedia.org/wiki/Subnet).  
TL;DR: use /24.

## DHCP

So if there are millions of IP Addresses, how do you know which one you should use for your computer? Well you don't silly, the Dynamic Host Configuration Protocol does it for you. In every network, there's (usually) (hopefully) one DHCP server, that knows the particular IP subnet that's being used there. When a device joins a physical network (Ethernet cable, Wi-Fi etc.), it shouts to everyone calling "HEY Y'ALL, I'M NEW HERE, Y'ALL GOT ANY MORE OF THEM IP ADDRESSES?". It's the DHCP server's job to find an available address from the pool, and reply saying "Hey man, I got you, here's 10.0.15.28/24, does it look good to you?". Your device will agree, and voila, you have yourself an IP address now. This is also how your router gets its public IP address from your ISP.

## DNS

**DNS = Domain Name System**

DNS is every network administrator's favorite technology, and it never causes any problems whatsoever. Here's a popular haiku about it:

![DNS Haiku](dns-haiku.jpg)

Every website you visit is hosted on a server somewhere, and to get to it you need to know its IP address. Ever noticed that you don't actually need to type 151.101.65.140 to go to reddit.com? Turns out it is useful to have human-readable dynamic names for IP addresses, and that's what DNS does.

Whenever your computer would like to translate a domain name to an IP address, it will send a DNS request to your DNS server, who is supposed to reply with the address if it knows it. What happens if it doesn't? Well there's this granddaddy of all DNS servers all the way up the chain who knows where to ask for every public address ever. DNS servers are globally organized in a tree structure, so your DNS request keeps following the chain all the way up until an answer is found, or fails.

Usually the DHCP server tells you the IP of the DNS server you're supposed to use in that network, but you can also just configure it manually. You can use 8.8.8.8 (Google's DNS server) and/or 1.1.1.1 (Cloudflare) if you want the least headaches, or 9.9.9.9 (QuadDNS) if you'd like more privacy.

## Ports

This is another important concept. Turns out people might want to run more than one application on their computers (shocking, I know). So when a network packet comes in to the computer's network interface, how does it know which application is supposed to receive it?

To this effort, every network interface has a concept of 65535 ports, each of which can be used for a separate connection. One application can bind to itself many ports, but one port can be bound by only a single application process at a time.

The HTTPS protocol usually uses the port 443, for example. It doesn't have to, but that's the standard, so your browser assumes it when you type https:// in front of the url. The end result of all of this is that you can just type in reddit.com and go to reddit, instead of https://151.101.65.140:443. Most browsers will assume HTTPS instead of HTTP these days.

Other popular ports include 80 for HTTP, 22 for SSH, 3389 for RDP, 53 for DNS, and etc.

## The devices
It can be helpful to know about your network devices and what they do as well. The most common device is a router, also incorrectly called a modem a lot of the times, but you might also have heard of switches, firewalls, load balancers etc. Here's what they do:

#### Modems, cables
By itself this isn't strictly even a networking device, but the purpose of this is to convert analog signals to 1s and 0s so that they can be understood by digital devices. They're a relic from the times we used phone networks' cabling to carry computer network signals, not needed in most modern installations where the cables carry digital signals directly. Those cables are usually called Ethernet cables, but technically Ethernet is just a protocol, and they're called twisted pair cables with RJ45 terminations. Usually any cable that has CAT5e is good enough for most people, but CAT6 is recommended if you want best performance. Modern networks also may use fiber-optic cables, in which signals are transmitted as light, not electrical voltage. Much more reliable over long distances and allows for much faster speeds, but is usually more expensive.

#### Routers
These are the real heroes of the internet, as it's their job to deal with IP packets and *route* them wherever they need to go. They have special protocols between them, which means they can auto-update routing tables and the end result is that you can just connect to anywhere in the world. Internet is amazing, no?

#### Wi-Fi Access Points
These devices are fancy antennas with some smarts built into them, and they allow you to connect to a network using Wi-Fi. Enterprise ones even let you keep the same connection when you move around, they talk in-between themselves to automatically switch your active connection. Once you know about them, you start to see them everywhere :)

#### Firewalls
Again, it turns out, that there are some really nasty people in the world and they might have less-than-honorable intentions about your devices and your data. So we had to put firewalls in front of our internet-facing devices. They allow you to restrict the flow of packets in any way you'd like. Usually they're used to allow internet access outside, but prevent outside people from directly accessing your devices inside. They can be a pain, but a necessary one. They can work based on IP addresses and/or ports and/or more identifying information, so you'd check your firewall or the relevant team if you're not able to access something that you should be able to, for example.

#### Switches
These are the traffic cops of your local network. While routers connect different networks together, switches connect devices within the same network, usually by giving you a lot of ethernet ports. They're smart enough to learn which device is connected to which port and only send data where it needs to go, unlike old "hubs" that broadcast to everyone. It's always a good idea to use a switch to connect devices together whenever you have the option, instead of using Wi-Fi. Thing about Wi-Fi is that it's a shared medium, which means the air time is divided between all the devices that are connected. This means, more devices using Wi-Fi, less connection everyone gets.

#### Appendix: Naming

What people call "Modems" in their home these days are actually a combination of these five. But they're *mostly* routers, so it's more appropriate to call them that :) Or call them a Router/Modem/Access Point/Firewall/Switch combo if you want, I'm not your mom.

---

## Essential Network Diagnostic Commands
I would be sad if you didn't leave this article with some practical knowledge too. So here are some of the most used network troubleshooting commands that I hope will help you:

**ping**  
Use when you want to test if you can reach something
```sh
ping google.com
```
- Tests basic connectivity
- Measures round-trip time
- Identifies packet loss

**traceroute/tracert**  
Use when you want to trace the route of your packets to a particular destination
```sh
# On Linux/macOS
traceroute google.com

# On Windows
tracert google.com
```
- Shows network path
- Identifies where delays occur
- Highlights routing issues

**nslookup/dig**  
Use when you want to manually ask for the IP address behind a domain name
```sh
# On Linux/macOS
dig google.com

# On Windows
nslookup google.com
```
- Queries DNS servers
- Shows DNS records
- Helps debug DNS issues

**netstat/ss**  
Use when you would like to check what ports are open and/or what process is using a specific port
```sh
# On Linux
ss -tuln

# On Windows
netstat -an | findstr LISTEN
```
- Shows active connections
- Identifies listening ports
- Helps diagnose socket issues

### More advanced: Network Capture
You use these when you want to actually capture the packets going through, useful for application troubleshooting and/or hacking.

**tcpdump**
```sh
# On Linux/macOS
sudo tcpdump -i eth0 host 192.168.1.5 and port 80
```
- Captures packets for analysis
- Can filter by host, port, protocol
- Lightweight, available on most systems

**Wireshark**
- GUI-based packet analyzer
- Deep inspection capabilities
- Powerful filtering and visualization

---

### Common Networking Issues & Solutions

#### "It works on my machine"

- Check if both environments have the same network configurations
- Verify firewall rules aren't different
- Ensure DNS resolution works the same way
- Look for proxy settings that might differ

#### Connection Timeouts

- First, check if the service is actually running
- Verify the port is correct and open
- Check if a firewall is blocking the connection
- Make sure your DNS isn't lying to you

---

#### VPNs: Not Just for Netflix
Virtual Private Networks extend private networks across public ones. They're not just for watching region-locked content or downloading totally legal Linux ISO's (though I won't judge).

When you're working remotely, VPNs are often your ticket to accessing internal resources. Just be prepared for that speed hit—encryption ain't free, performance-wise.

#### Cloud Networking
These days, most developers are deploying to the cloud and the beauty of cloud networking is you can define your entire network infrastructure as code. No more begging the network team to open a port!

#### Container Networking
If you're using Docker or Kubernetes (my condolences), networking gets... interesting.

- Bridge Networks: Default for containers, creates a private network
- Host Networks: Containers share the host's network namespace
- Overlay Networks: Allow containers on different hosts to communicate
- Service Discovery: How containers find each other automatically

Remember that containers are ephemeral—they come and go—so hardcoding IP addresses is a recipe for disaster. Use DNS instead.

### Security Considerations
I'd be remiss not to mention security, since the internet is basically the wild west with better graphics. A good rule of thumb: if you wouldn't shout it across a crowded coffee shop, it shouldn't travel over the network unencrypted. But these days most of security is handled for you, so if you see the little lock icon in your browser bar, it means you're using HTTPS, and no one, including the coffee shop owner, your ISP, your government etc. can see the contents of the communication you're making with that website. What they _can_ tell is that you are accessing that website, since DNS is usually unencrypted.

### Wrapping Up
Networking can seem like dark magic sometimes, but understanding these basics will save you countless hours of frustration. Next time something's not connecting, you'll have a better idea of where to look.
Remember, the network is always guilty until proven innocent. It's the first thing to blame and often the last thing checked—but with these tools in your belt, you'll be the one saying "have you tried checking the firewall?" instead of banging your head against the keyboard.

Got questions? Google them! Or ask a GPT model if you don't care about the environment. Lastly, feel free to reach out to me for anything :)

Happy networking!
