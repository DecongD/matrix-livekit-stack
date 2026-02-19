# VM And Network Plan

This document captures a practical baseline for a single-host Proxmox deployment using `vmbr0` on `10.0.0.0/24` with dynamic public IPs.

**Assumptions**
- One Proxmox host with a Linux bridge: `vmbr0`.
- Internal subnet: `10.0.0.0/24`.
- Two dynamic public IPs assigned by ISP.
- Reverse proxy is Nginx.
- No LiveKit recordings; only message logs are retained on the Matrix VM.

**VM Inventory**
1. `vm-reverse-proxy`
   - Purpose: Nginx reverse proxy and TLS termination.
   - Public IP: Dynamic Public IP A.
   - Private IP: `10.0.0.10`.
   - Suggested size: 2 vCPU, 2-4 GB RAM, 20-30 GB disk.
2. `vm-matrix`
   - Purpose: Synapse + Postgres + Element.
   - Public IP: None.
   - Private IP: `10.0.0.20`.
   - Suggested size: 4 vCPU, 8-16 GB RAM, 100+ GB disk (log growth).
3. `vm-livekit`
   - Purpose: LiveKit + TURN.
   - Public IP: Dynamic Public IP B.
   - Private IP: `10.0.0.30`.
   - Suggested size: 4 vCPU, 8-16 GB RAM, 50+ GB disk.
   - 1080p note: keep at least 4 vCPU and 8 GB RAM; scale up if sessions grow.

**DNS Plan**
- `matrix.example.com` -> Public IP A
- `element.example.com` -> Public IP A
- `livekit.example.com` -> Public IP A for HTTPS/WSS routing
- `turn.example.com` -> Public IP B for TURN/ICE

**Firewall Plan**
- Proxmox host: allow only management access from trusted IPs.
- `vm-reverse-proxy` inbound:
  - `80/tcp`, `443/tcp` from Internet.
- `vm-matrix` inbound:
  - `8008/tcp` from `vm-reverse-proxy` only.
  - `5432/tcp` local only (Postgres).
- `vm-livekit` inbound:
  - `443/tcp` from `vm-reverse-proxy` for HTTPS/WSS.
  - `3478/udp`, `3478/tcp` from Internet for TURN.
  - `50000-60000/udp` from Internet for media (adjust to LiveKit config).

**Operational Notes**
- Public IPs change: update DNS A records when they rotate.
- Keep logs on `vm-matrix` only. No recording storage.
- Consider snapshots before major upgrades.
 - 1080p video requires stable uplink bandwidth and open UDP media ports.
