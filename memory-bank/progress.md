# Progress

## Status
- All changes from the patch specification implemented.
- Added Toyota Land Cruiser 200 (VDJ200R) canonical parameters (397 total in `params.json`).
- Fixed `Odometer_mi` metric auto-conversion in Home Assistant (`class: "none"`).
- Added `ODOMETER_KM` (`unit: "km"`, `class: "distance"`).
- Fixed merge order in `param_loader.py` so bundled `params.json` overrides take precedence over GitHub fetches.
- Fixed `api.py` `async_export_log_rows()` to handle `HTTP 400` gracefully.
- All unit tests added and passing (76 in `test_param_loader.py`).

## Completed
- [x] Check / finish dependency installation.
- [x] Implement changes in `custom_components/wican/coordinator.py`.
- [x] Implement changes in `custom_components/wican/sensor.py`.
- [x] Implement changes in `custom_components/wican/data/params.json`.
- [x] Implement changes in `custom_components/wican/param_loader.py`.
- [x] Add unit tests in `tests/test_pid_sensor_config.py`.
- [x] Add unit tests in `tests/test_param_loader.py`.
- [x] Add unit tests in `tests/test_coordinator.py`.
- [x] Run full test suite and ensure all tests pass without regressions.
