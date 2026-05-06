+++
title = "Artonet - a simple & fast Mesh VPN solution"
date = 2023-01-21
description = "A WireGuard-based mesh VPN I designed for simple, private peer networks."
[taxonomies]
tags = ["networking", "wireguard", "rust", "projects"]
+++

*Update (August 2023): Since writing this, similar projects have emerged, including [Netbird](https://github.com/netbirdio/netbird).*

---

## What is it?

Artonet creates a virtual local network between your devices without obstructing internet access. All traffic between nodes is encrypted, and peers can communicate as if they're on the same local network.

Use cases: collaborative tech projects, gaming with friends, sharing self-hosted services without exposing public ports.

## Key Features

- Built on WireGuard at the kernel level—faster than traditional VPN technologies
- Simple joining process: connect to the control server, provide credentials, done
- Supports local DHCP and DNS configuration per network on the control server
- Split tunneling: route all traffic through one node, or keep inter-node communication isolated
- No account system by default—users request access with a password or keyfile
- Built with Rust

## Why Not Just Use Tailscale/Zerotier/Hamachi?

**Tailscale** is actually great—it combines WireGuard's speed with solid features. But it can get expensive for casual peer networks, and it relies on their infrastructure.

**Zerotier** and **Hamachi** use older VPN technology, aren't open source, and have various pricing and reliability issues.

Artonet's goal is simplicity, open-source availability, and intentional minimalism. Truly private, self-contained networks with no external authentication dependencies.

## Research Areas

Building this properly requires going deep on three things:

1. **WireGuard Protocol** — encryption, traffic routing, kernel space programming
2. **Routing** — designing protocols that are stable, fast, and easy to set up
3. **OS-Level Implementation** — cross-platform compatibility across different architectures
