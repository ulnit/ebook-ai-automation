# Chapter 2: Hardware That Pays for Itself

## Shopping List (Total: ~$60)

| Item | Cost | Why |
|------|------|-----|
| Raspberry Pi 4 (4GB) | $35 | Enough RAM for LLM API calls + Python |
| 32GB SD Card | $8 | OS + scripts + data |
| Power Supply | $10 | Stable power = stable income |
| Ethernet Cable | $5 | Wired > WiFi for reliability |

## OS Setup

```bash
# Flash Raspberry Pi OS Lite (64-bit)
# Enable SSH
# Set static IP
# Install essentials
sudo apt update && sudo apt install python3 git curl -y
```

## Why ARM64 on Pi?

The Raspberry Pi's ARM64 architecture matters. Some Docker images are x86-only. Some npm packages need native compilation. This book covers all the workarounds — from stdlib-only Python scripts to cross-compilation tricks.