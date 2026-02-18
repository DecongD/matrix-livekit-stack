# Network Flow

```mermaid
sequenceDiagram
  autonumber
  participant U as User Client
  participant N as Nginx (Public IP A)
  participant M as Matrix VM (10.0.0.x)
  participant L as LiveKit VM (Public IP B / 10.0.0.y)

  U->>N: HTTPS (Matrix API, Element)
  N->>M: HTTP/HTTPS (Synapse, Element)
  M-->>N: Responses
  N-->>U: Responses

  U->>N: HTTPS/WSS (LiveKit signaling)
  N->>L: HTTPS/WSS (LiveKit)
  L-->>N: Responses
  N-->>U: Responses

  U->>L: UDP/TCP (ICE, TURN)
  L-->>U: Media relay
```

Notes:
- Media traffic prefers direct UDP to LiveKit/turn.
- Nginx handles TLS termination and routes internal traffic.
- Temporary public IPs should be updated in DNS when they change.
