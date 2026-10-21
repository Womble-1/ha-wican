# Product Context

## Why this project exists
The WiCAN Home Assistant integration connects WiCAN and WiCAN-PRO OBD-II CAN bus adapters (by MeatPi) with Home Assistant. The adapter reads telemetry and CAN/OBD-II PIDs from vehicles and posts them to Home Assistant over webhooks or MQTT.

## Problems Solved
- WiCAN devices push `autopid_data` via webhooks. When new PIDs are pushed, they should be discovered dynamically and created with accurate units, icons, device classes, and state classes (e.g. `SensorStateClass.MEASUREMENT`).
- When string-encoded numbers arrive from the firmware (e.g., with whitespace `" 114 "` or signs `"+10"` or decimals `" 13.61 "`), they must be converted to `int` or `float` rather than being treated as string states.
- On first discovery via webhook, newly created PID sensors previously remained `"unknown"` until the next webhook update arrived because the entity was added after coordinator notification.
- Parameter metadata fallback must resolve standard OBD-II and vehicle PIDs even if not configured explicitly in device config.
- Synced parameter updates from GitHub must not wipe bundled parameter definitions.
