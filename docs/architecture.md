# Architecture

**Topology**
- Single Proxmox host.
- Three VMs: reverse proxy, Matrix, and LiveKit.
- `vmbr0` bridge on `10.0.0.0/24`.
- Two public IPs: one for Nginx and one for LiveKit/TURN.

**Traffic Flow**
- Matrix and Element traffic enters via Nginx, then routes to the Matrix VM.
- LiveKit signaling enters via Nginx, then routes to the LiveKit VM.
- LiveKit media flows directly to the LiveKit VM via UDP/TCP (TURN/ICE).

**Why Two Public IPs**
- LiveKit media reliability is best with a direct public IP for TURN and ICE.
- Nginx remains the single ingress for HTTPS/WSS routing.
