# ZeroClaw Assistant Integration for Home Assistant

A custom integration that connects Home Assistant to [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw), a Rust-based AI agent runtime. Use ZeroClaw as a conversation agent in HA Assist, monitor its status through entities, and send messages via services.

## Prerequisites

This integration requires the **ZeroClaw addon** to be installed and running. Install it from the [`slayer/zeroclaw-homeassistant`](https://github.com/slayer/zeroclaw-homeassistant) repository. See that repo's README for addon installation instructions.

## Installation

### Option A: HACS (recommended)

1. Open HACS in Home Assistant
2. Click the three-dot menu in the top right and select **Custom repositories**
3. Add `https://github.com/slayer/zeroclaw-homeassistant-integration` with category **Integration**
4. Search for **ZeroClaw Assistant** and install it
5. Restart Home Assistant

### Option B: Manual

1. Copy the `custom_components/zeroclaw/` directory into your Home Assistant `config/custom_components/` directory
2. Restart Home Assistant

## Configuration

1. Go to **Settings** > **Devices & Services** > **Add Integration**
2. Search for **ZeroClaw**
3. If the ZeroClaw addon is running locally, it will be auto-detected
4. For a remote ZeroClaw instance: enter the host, port, and pairing code (found in the addon logs)

## What You Get

### Conversation Agent

ZeroClaw registers as a conversation agent in Home Assistant Assist. You can select it under **Settings** > **Voice Assistants** as your conversation agent.

### Entities

| Entity | Type | Description |
|--------|------|-------------|
| ZeroClaw Connected | Binary sensor | Whether the integration can reach the ZeroClaw instance |
| ZeroClaw Status | Sensor | Current status reported by ZeroClaw (e.g., `running`, `pairing`) |
| ZeroClaw Active Model | Sensor | The AI model currently in use |

### Services

**`zeroclaw.send_message`** -- Send a message to ZeroClaw and get a response.

```yaml
service: zeroclaw.send_message
data:
  message: "Turn on the living room lights"
```

## Troubleshooting

**"Cannot connect"** -- Verify the ZeroClaw addon is running and reachable. If running remotely, confirm the host and port are correct and that no firewall is blocking the connection.

**"Invalid pairing code"** -- Pairing codes are single-use and time-limited. Check the ZeroClaw addon logs for a fresh pairing code and try again.
