# Project Brief: Fix MeatPi/WiCAN PID Numeric State Typing, First-Push PID State Race & Missing OBD-II / Vehicle PID Metadata (`meatpi-multi-device`)

## Objective
Fix four root causes on the `meatpi-multi-device` branch of `ha-wican`:
1. First-webhook discovery race in `MeatPiPidSensorEntity.async_added_to_hass()` where newly discovered PIDs start as "unknown" without numeric state typing / state class.
2. Incomplete string-to-number normalization in `MeatPiDataUpdateCoordinator._normalize_string_value()` failing on whitespace-padded strings and signed numbers.
3. Broken and missing PID definitions and aliases in `custom_components/wican/param_loader.py` and `custom_components/wican/data/params.json` (such as `ENGINE_LOAD`, `BARO_PRES`, `CTRL_MOD_V`, `DIST_MIL`, `TIMING_ADV`, `AMBIENT_TMP`, `DPF_SOOT_BANK1`, `DPF_REGEN_ACTIVE`, `IntakeManiAbsPress`, etc.).
4. `_ParamsManager` wiping bundled `params.json` definitions when syncing from GitHub in `_async_apply_stored()` and `async_sync()`.

## Scope
- Modify `custom_components/wican/coordinator.py`
- Modify `custom_components/wican/sensor.py`
- Modify `custom_components/wican/data/params.json`
- Modify `custom_components/wican/param_loader.py`
- Add unit tests in `tests/test_pid_sensor_config.py`, `tests/test_param_loader.py`, `tests/test_coordinator.py`
- Ensure entire test suite passes without regressions.
