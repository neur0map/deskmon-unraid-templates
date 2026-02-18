# deskmon-unraid-templates

unRAID Community Applications template for [deskmon-agent](https://github.com/neur0map/deskmon-agent).

## What is deskmon-agent?

A lightweight system monitoring agent that streams live server stats to the [Deskmon](https://github.com/neur0map/deskmon) macOS menu bar app. CPU, memory, disk, network, Docker containers — all visible from your Mac's menu bar.

No cloud. No accounts. No telemetry. Connects via SSH tunnel over your local network.

## Installation

1. Install the **Community Applications** plugin on your unRAID server (if not already installed)
2. Search for **deskmon-agent** in the Apps tab
3. Click **Install**
4. Click **Apply** (defaults are correct for most setups)
5. Install the [Deskmon macOS app](https://github.com/neur0map/deskmon/releases), add your server IP and SSH credentials

## What the container accesses

| Mount | Mode | Why |
|-------|------|-----|
| `/` -> `/hostfs` | Read-only | Disk usage for all drives (array, cache, parity) |
| `/sys` -> `/host/sys` | Read-only | CPU temperature sensors |
| `/var/run/docker.sock` | Read-write | Container stats and start/stop/restart |
| `/etc/deskmon` | Read-write | Config file persistence |

The `--pid=host` flag is used to see host processes (CPU/memory per process). The `--network=host` flag is used for accurate network speed reporting.

The agent binds to `127.0.0.1:7654` (localhost only) and is not reachable from the network. The macOS app connects through an SSH tunnel.

## Links

- [deskmon-agent source](https://github.com/neur0map/deskmon-agent)
- [Deskmon macOS app](https://github.com/neur0map/deskmon)
- [Support thread](https://forums.unraid.net/topic/197287-deskmon-agent-lightweight-system-monitoring-agent-for-linux-servers-for-native-macos-deskmon-app/)
