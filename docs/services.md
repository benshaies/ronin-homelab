
# Services

Overview of the services running on Ronin, what each one does, and how it fits into the setup.

## AdGuard Home
Network-wide DNS server and ad/tracker blocker. All DNS on the network routes through this. Also handles wildcard DNS rewrites for internal domains (`*.stillbenja.dev`) and a separate rewrite for the Tailscale IP, so services resolve correctly whether I'm on the local network or connecting remotely.

## Nginx Proxy Manager
Reverse proxy that routes incoming traffic to the right service based on domain/subdomain, and handles SSL/TLS termination. Holds a wildcard Let's Encrypt certificate (via DNS challenge) for `stillbenja.dev`, so every service is served over HTTPS.

## Tailscale
VPN mesh network used for secure remote access to the server and its services without opening any ports on the router.

## Forgejo
Self-hosted Git server — lightweight GitHub/GitLab alternative. Used for private repos and version control outside of GitHub. Push mirroring to GitHub not yet set up.

## Vaultwarden
Self-hosted, lightweight Bitwarden-compatible password manager. Used as the primary password vault across devices.

## Affine
Self-hosted project and task manager. Used for tracking personal projects and to-dos.

## Scrutiny
S.M.A.R.T. monitoring dashboard (built on smartctl) for tracking drive health across the server's disks — early warning for failing drives.

## Jellyfin
Self-hosted media server for streaming personal media library.

---

### Notes
- All service data lives on the RAID1 array (`/mnt/data/service/`), not the boot SSD — a drive failure on the OS disk doesn't touch service data.
- Compose files for each stack live under `/opt/stacks/<app>/` — easy to tear down and recreate since they hold no persistent data themselves.
