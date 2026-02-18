# Architecture Overview

```mermaid
flowchart TB
  Internet[(Internet)]
  subgraph PublicIPs[Dynamic Public IPs]
    NGINX_PUB[Public IP A\nNginx VM]
    LIVEKIT_PUB[Public IP B\nLiveKit+TURN VM]
  end

  subgraph Proxmox[Proxmox Host]
    direction TB
    BRIDGE[vmbr0\nBridge 10.0.0.0/24]

    NGINX_VM[reverse-proxy VM\nNginx]
    MATRIX_VM[matrix VM\nSynapse + Postgres + Element]
    LIVEKIT_VM[livekit VM\nLiveKit + TURN]
  end

  Internet --> NGINX_PUB --> NGINX_VM
  Internet --> LIVEKIT_PUB --> LIVEKIT_VM

  NGINX_VM --> BRIDGE
  MATRIX_VM --> BRIDGE
  LIVEKIT_VM --> BRIDGE

  NGINX_VM -->|HTTPS| MATRIX_VM
  NGINX_VM -->|HTTPS/WSS| LIVEKIT_VM
  LIVEKIT_VM -->|TURN/ICE| Internet
```

Notes:
- Public IPs are temporary and may change.
- Synapse, Postgres, and Element are co-located in the Matrix VM.
- No LiveKit recordings; only message logs are retained.
