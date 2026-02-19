# Troubleshooting

**Matrix Not Loading**
- Verify Nginx routing to the Matrix VM.
- Confirm Synapse is running and reachable on `8008/tcp`.

**LiveKit Call Issues**
- Check that TURN ports are reachable from the Internet.
- Confirm LiveKit UDP port range is open.
- Validate public IPs and DNS records.

**High CPU Usage**
- Reduce video resolution or participant count.
- Scale LiveKit VM resources.
