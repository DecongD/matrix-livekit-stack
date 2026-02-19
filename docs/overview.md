# Project Overview

This repository defines a Proxmox-hosted Matrix + LiveKit stack with Nginx as the reverse proxy. It is developed on macOS and deployed to Linux (Proxmox). No secrets are committed.

**Goals**
- Self-host Matrix (Synapse), Element, and LiveKit.
- Provide persistent voice and video rooms with 1080p capability.
- Keep the deployment simple and maintainable for a small user base (5-10 people).

**High-Level Components**
- Proxmox host with a single `vmbr0` bridge on `10.0.0.0/24`.
- Nginx reverse proxy on a public IP.
- Matrix VM hosting Synapse, Postgres, and Element.
- LiveKit VM hosting LiveKit and TURN on a public IP.

**Key Constraints**
- Public IPs are dynamic and may change.
- TURN must be reliable for NAT traversal.
- No LiveKit recordings; only message logs are retained on the Matrix VM.
