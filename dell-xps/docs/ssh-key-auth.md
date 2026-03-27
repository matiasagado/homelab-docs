# SSH Key Authentication
**Date:** 2026-03-26

## Why
Eliminates password prompts when SSHing into the XPS. Faster, more secure, and cleaner for screenshares.

## Setup
Generated ED25519 key pair on Mac and copied public key to XPS:
```bash
ssh-copy-id matiasagado@100.94.36.48
```

## SSH Config on Mac
```
# ~/.ssh/config
Host dell-xps
    HostName 100.94.36.48
    User matiasagado
```

## Result
```bash
ssh dell-xps
```
Connects instantly with no password prompt via Tailscale IP from any network.
