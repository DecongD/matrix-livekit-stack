# Security

**Network Segmentation**
- Only the reverse proxy and LiveKit VMs expose public services.
- Matrix VM is private and only accepts traffic from the reverse proxy.

**Firewall Baseline**
- Nginx VM: `80/tcp`, `443/tcp` from Internet.
- Matrix VM: `8008/tcp` from reverse proxy; Postgres local only.
- LiveKit VM: `443/tcp` from reverse proxy; TURN and media ports from Internet.

**Secrets**
- Do not commit secrets to the repository.
- Store secrets in `.env` or a secrets manager and keep them local.
