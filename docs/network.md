# Network — Ronin Homelab

## Overview
- Ubuntu Server Running on HP Z420
- Most configuration done through SSH (Port 22) from main PC
- Simple networking services such as Adguard Home and Nginx Proxy Manager running

## Hardware
- Original ISP Modem/Router & WAP
- Server (Ronin) — Connected through Ethernet
- **NIC**: 82579LM Gigabit Network Connect (Intel)
- **Capacity**: 1Gbit/s
- **Usual Speed**: 1Gbit/s

## IP Addressing
- Subnet: 192.168.40.x
- Router/gateway IP: 192.168.40.1
- Ronin's static IP: 192.168.40.169
- No VLAN setup

## DNS — AdGuard Home
- 2 seperate DNS rewrites to make access easier\
      *.ronin.home -> 191.168.40.169\
      *.ronin.home -> 100.89.91.10 (Remote Tailscale Access IP)
- Upstream DNS: https://dns10.quad9.net/dns-query
- **BlockLists**: Adguard DNS Filter, HaGeZi's Normal Blocklist, OISD Blocklist Big

## Reverse Proxy — Nginx Proxy Manager
- Proxy manager running to make access easier
- 
**List of Proxy Hosts** PORTS ONLY (All running under 192.126.40.169)
- adguard.ronin.home : Port 90
- dockge.ronin.home : Port 5001
- forgejo.ronin.home : Port 3000
- jellyfin.ronin.home : Port 8096
- npm.ronin.home : Port 81
- plex.ronin.home : Port 32400
- qbittorrent.ronin.home : Port 8080
- vikunja.ronin.home : Port 3456

## Port Forwarding
- No Ports forwarded currently
- All access to services internally is done through SSH and WebUI with log in details
- All remote access is done through Tailscale through preauthorized devices
- Currently no need for Port Forwarding

## Remote Access
- TailScale installed and running
- Added to device list allowing remote access

**TailScale Setup**
- Changed Global Nameserver as local server static IP
- Turned on Override DNS servers
- Configured Adguard to rewrite *.ronin.home to tailscale IP when called

This configuration allows seamless, easy and secure remote access while still allowing easy access to services with proper domains such as "http://adguard.ronin.home"

## Firewall Rules
- No firewall rules on server 

## Troubleshooting and Network Challenges
**Problem #1**\
Router and WiFi was advertising IPv6 router address as DNS alongside my servers IPv4 address for DNS. My network only allows for custom IPv4 addresses through the application, with no way to set static IPv6 addresses and disable IPv6. This led to all devices on my network automatically using the IPv6 as DNS skipping by my Adguard configuration\
**Solution**\
I found I was able to set a static IPv6 DNS address through the Admin WebUI. However I was unable to make my servers IPv6 static. Thus I used the local link address of my server and changed the ipv6 DNS of my network to the local link address of my server. Effectively sending all network traffic through my server and thus through Adguard Home.

**Problem #2**\
Tailscale creates its own internal IP for my server so my domains like jellyfin.ronin.home do not work while using a VPN remotely.\
**Solution**\
Turn on IP forwarding -> Told tailscale to advertise my home subnet -> approve subnet in admin console -> Pointed tailscale DNS name server to Adguard / Server IP Address

## TODO
- Configure and enable SSH cert for all service domains
- Build own router using mini pc and most likely PfSense
- Setup and configure DHCP and port forwarding on custom router
- Configure and add a switch, configure VLANS and seperate server from other devices
- Add server and WAP to switch 
