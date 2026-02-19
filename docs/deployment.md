# Deployment

**VM Provisioning**
- Create three VMs in Proxmox.
- Attach all VMs to `vmbr0`.
- Assign static private IPs and record them in `docs/vm-plan.md`.

**Reverse Proxy**
- Configure Nginx to terminate TLS and route to Matrix and LiveKit.
- Keep internal upstreams on private IPs.

**Matrix Stack**
- Synapse, Postgres, and Element run on the Matrix VM.
- Use `matrix/docker-compose.yml` as the deployment base.

**LiveKit Stack**
- LiveKit and TURN run on the LiveKit VM.
- Use `livekit/docker-compose.yml` as the deployment base.

**DNS**
- Update A records when public IPs change.
- Use distinct hostnames for Matrix, Element, LiveKit, and TURN.
