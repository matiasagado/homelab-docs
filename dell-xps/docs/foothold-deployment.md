# Foothold First Deployment
**Date:** 2026-03-26

## What
First deployment of the Foothold application to the XPS homelab server. Node.js + Express backend serving a REST endpoint, deployed and verified over Tailscale.

## Stack
- Node.js v20.20.0
- Express
- Ubuntu 24.04.4 LTS
- Tailscale for remote access

## Workflow
Code written on Mac, pushed to GitHub, pulled and run on XPS:
```bash
git clone https://github.com/matiasagado/foothold.git
cd foothold
git checkout feat/initialize-project
npm install
node index.js
```

## Verification
```bash
curl http://100.94.36.48:3000
# Hello Foothold. Lets build.
```

## Result
REST endpoint live on XPS server, accessible from Mac via Tailscale IP. First end to end deployment verified — Mac to GitHub to XPS.
