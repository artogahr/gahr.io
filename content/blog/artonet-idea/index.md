+++
title = "Artonet - a simple & fast Mesh VPN solution"
date = 2023-01-21
description = "A WireGuard-based mesh VPN I designed for simple, private peer networks."
[taxonomies]
tags = ["networking", "wireguard", "rust", "projects"]
+++

This post describes an idea for a Mesh VPN (also called an Overlay VPN Network) application. Hopefully want to do as my Master's Thesis project.

# What is it?

Artonet allows you to set up a virtual local network between your devices, without obstructing internet access. This network and all the traffic going between the devices is encrypted of course.

The end result is that, you and your peers can communicate to each other as if in the same local network. This can be useful if you're trying some technology with your peers, or if you're gaming with your friends. This also allows you to share the services you run with other people, without needing to open a public port to the internet.

*Aug 2023 Update:*
Since I've thought of this idea many similar projects have also surfaced to my attention, one of the ones I like is [Netbird](https://github.com/netbirdio/netbird).

## Key features:

- Uses Wireguard protocol at kernel level - which means it's faster than traditional VPN technologies
- Joining is simple - you only need to point the client to the control server and enter the login password
- You can set up a local DHCP and DNS server per network on the control server
- You can do split tunnelling - You can either have all nodes go to internet through one node, or have the Artonet network only be used for inter-node communication
- Simple - Trivially easy to set up and connect to.
- Fast - Written with Rust, using speed as the first order of concern.

## Comparison to competitors

There are various solutions offering the same or enhanced featureset, the main thing separating Artonet from them is ease of setup, open-source + simplistic nature, and deliberate lack of features.

Some solutions like [Tailscale](https://tailscale.com/) combine the speed of Wireguard with excellent featureset within a professionally developed product, however might be too expensive for a casual user trying to set up a network with their peers. Other solutions like [Zerotier](https://www.zerotier.com/) or [Hamachi](https://vpn.net/) are also good, but they use outdated technology, are not open source, too pricy, or a combination of these.

Tailscale, along with similar competitors also use complicated authorization techniques. While this is good for security, users may prefer a more simplistic UX for simple / not as important projects. Tailscale assumes the position of "Not providing any auth at all", and leaves it to other Auth providers, thus making truly private and self-contained networks impossible.

In Artonet, by default, there are no accounts nor auth providers. Users simply ask to join a specific network ID from a control server, and provide the password and/or keyfile for it.

## What's the Research angle?

The things to be researched in this project / thesis are as follows:

1. **WireGuard: Next Generation Kernel Network Tunnel**: It's not a simple protocol, and will require advanced research into [its code](https://www.wireguard.com/repositories/) and [published papers](https://www.wireguard.com/papers/wireguard.pdf). Within this research, I would learn about traffic routing, encryption, kernel space programming etc.
2. **Routing**: In order for our application to differentiate itself, it needs to be easy to set up, while providing stable and fast performance. To do this, advanced network routing protocols will need to be researched and implemented.
3. **OS Level implementation**: In order to make this code cross-compatible, I would need to research different operating system's networking architectures and learn to implement this program's features on them.
