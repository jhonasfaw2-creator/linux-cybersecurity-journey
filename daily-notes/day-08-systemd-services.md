# Day 8 — Linux Services and systemd

## Objective
Understand how Linux manages background services using systemd.

## Key Concepts
- **Service:** A program running in the background.
- **systemd:** Manages system services.
- **systemctl:** Command used to control services.
- **start:** Starts a service.
- **stop:** Stops a service.
- **restart:** Restarts a service.
- **enable:** Starts a service automatically at boot.
- **disable:** Prevents automatic startup.

## Important Commands

```bash
systemctl --version
systemctl list-units --type=service
systemctl --failed
systemctl status NetworkManager
systemctl is-active NetworkManager
systemctl is-enabled NetworkManager
journalctl -n 20
```

## Security Importance
Monitoring services helps identify unnecessary, unexpected, or suspicious background processes.

## What I Learned
I learned how Linux manages services, checks their status, and monitors service activity using systemd and systemctl.
