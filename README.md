# Homelab (Ronin)

Old Desktop computer running Ubuntu server with services running underneath docker as containers in a RAID 1 configuration. Built to develop hands on skills and learn. 

## Overview
 - **Host OS**: Ubuntu Server 24.04.4 LTS (Noble Numbat)
 - **Hardware**: HP Z420 Workstation - Intel Xeon E5-1620 - Quadro K2000 [DOCS](docs/hardware.md)
 - **Virtualization/Containers**: Docker + Docker Compose
 - **Network**: Home network routed through server, DNS rewrites, Proxy Server [DOCS](docs/network.md)
 - **Purpose**: Self host important services, control personal data, self hosting, pratice networking, monitoring and managing a server

## Architecture

# Services
**Adguard** | Port 90 Web Client | DNS Rewrite, Home Adblocking
**Forgejo** | Port 3000 | Self Hosted Git
**Nginx-Proxy-Manager** | Port 81 Web Client | Reverse Proxy for services
**QBittorrent** | Port 8080 | Torrenting Software
**TailScale** | Remote Access to services
**Vikunja** | Port 3456 | Self Hosted Project Management
**Plex Media Server** | Port 32400 | Self hosted media

## Docs
- [Network](docs/network.md)
- [Hardware](docs/hardware.md)
- [Services](docs/services.md)

## Lessons Learned

- **DNS port conflict (AdGuard Home)** — AdGuard couldn't bind to port 53 because Ubuntu's `systemd-resolved` was already using it. Found the conflict with `sudo lsof -i :53`, fixed it by disabling the stub listener in `/etc/systemd/resolved.conf`. Learned to check what's already listening before assuming a container's broken.

- **Router advertising IPv6 DNS alongside server's IPv4** — even after setting the server as DNS for the WiFi network, devices kept resolving through the router's auto-advertised IPv6 address (Router Advertisement), bypassing the server entirely. Fixed by assigning the server's IPv6 link-local address as a static DNS entry on the WiFi network, since a static global IPv6 wasn't available. Learned IPv6 can silently override IPv4 DNS settings — check both stacks when DNS misbehaves.

## Roadmap
- Secure web connections with HTTPS and SSL certs inside Nginx proxy manager
- BitWarden for securely storing passwords
- Push mirroring with Forgejo to GitHub
- Continue experimenting








