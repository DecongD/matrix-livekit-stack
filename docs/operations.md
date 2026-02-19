# Operations

**Routine Tasks**
- Monitor disk usage on the Matrix VM because logs grow over time.
- Check LiveKit CPU and bandwidth usage during screen-sharing sessions.
- Update DNS records after public IP rotation.

**Backup**
- Back up the Matrix Postgres database.
- Back up Synapse configuration and media store as needed.
- No recording storage is used for LiveKit.

**Update Workflow**
- Update containers in a maintenance window.
- Snapshot VMs before major upgrades.
- Validate service health after restart.
