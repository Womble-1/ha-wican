# System Patterns

## Architecture & Naming Conventions
- Base branch: `meatpi-multi-device`
- Entity prefix: `MeatPi*` (`MeatPiDataUpdateCoordinator`, `MeatPiSensorEntity`, `MeatPiPidSensorEntity`, `MeatPiSensorEntityDescription`).
- Data flow:
  1. Webhook receives payload with `autopid_data`.
  2. `coordinator.handle_webhook_data(data)` normalizes and stores data in coordinator data cache.
  3. Dispatcher signals new PID keys.
  4. `_async_process_pid_update()` creates `MeatPiPidSensorEntity` instances and calls `async_add_entities()`.
  5. `MeatPiPidSensorEntity.async_added_to_hass()` seeds native value from coordinator data (or restored state), which sets `_numeric_seen` and enables `state_class = SensorStateClass.MEASUREMENT`.
  6. Parameter definitions in `param_loader.py` look up PID key (normalized / alias) in `_PARAMS` (from `data/params.json` merged with GitHub-synced params).
