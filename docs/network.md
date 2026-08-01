# Network — Ronin Homelab

## Overview
- Brief description of the network topology
- Diagram (optional — even ASCII or a linked image works)

## Hardware
- Router/modem (make/model, firmware)
- Switch(es)
- Server (Ronin) — NIC details, connection type (wired/wireless)

## IP Addressing
- Subnet (e.g. 192.168.1.0/24)
- Router/gateway IP
- Ronin's static IP
- DHCP range vs static reservations
- VLAN setup (if any)

## DNS — AdGuard Home
- Wildcard rewrite config (*.ronin.home → Ronin's IP)
- Upstream DNS servers used
- Any blocklists enabled
- Clients that use AdGuard as their resolver

## Reverse Proxy — Nginx Proxy Manager
- List of proxy hosts (subdomain → internal service:port)
  - e.g. jellyfin.ronin.home → localhost:32400
- SSL/cert setup (self-signed, Let's Encrypt, etc.)
- Access lists / auth if used

## Port Forwarding
- Any ports forwarded on the router, and why
- Security notes (what's exposed externally vs. LAN-only)

## Remote Access
- VPN setup (if any — Tailscale, WireGuard, etc.)
- How you access services when away from home

## Firewall Rules
- Any custom rules on router/server
- Docker network isolation notes

## Troubleshooting / Known Issues
- Common problems and fixes
- Things to check first when something breaks

## TODO
- Planned changes (e.g. VLAN segmentation, external portfolio site exposure)
