# VM Layout

```mermaid
flowchart LR
  subgraph Proxmox[Proxmox Host]
    direction TB
    BR[vmbr0\n10.0.0.0/24]

    VM1[reverse-proxy VM\nNginx\nPublic IP A - dynamic]
    VM2[matrix VM\nSynapse + Postgres + Element\nPrivate IP]
    VM3[livekit VM\nLiveKit + TURN\nPublic IP B - dynamic]

    VM1 --- BR
    VM2 --- BR
    VM3 --- BR
  end
```

Notes:
- Keep Nginx and LiveKit on public IPs for reliability.
- Matrix VM remains private; traffic enters via Nginx.
- Message logs live in the Matrix VM; no recording storage is provisioned.
