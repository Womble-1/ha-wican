# Active Context

## Current Focus
Implemented Toyota Land Cruiser 200 (VDJ200R) / Techstream parameter definitions, aliases, and odometer conversion fix:
1. `custom_components/wican/data/params.json`:
   - Updated `ODOMETER_MI` to `"class": "none"` so Home Assistant does not automatically convert miles to kilometers on Metric HA instances.
   - Added `ODOMETER_KM` with `"class": "distance"` and `"unit": "km"`.
   - Added 37 canonical Toyota parameters (`ENGINE_SPEED`, `ENGINE_SPEED_CAN`, `BATTERY_VOLTAGE`, `MAP`, `FUEL_INPUT_LEVEL`, `FUEL_INPUT_LEVEL_CAN`, `AT_OIL_TEMPERATURE_1`, `AT_OIL_TEMPERATURE_2`, `PARTIC_FILTER_DIFF_PRESS_1`, `PARTIC_FILTER_DIFF_PRESS_2`, `DIFF_PRESS_SENSOR_CORR`, `DIFF_PRESS_SENSOR_CORR_2`, `PM_ACCUMULATION_RATIO`, `PM_ACCUMULATION_RATIO_2`, `EXHAUST_FUEL_ADDITION_FB`, `EXHAUST_FUEL_ADDITION_FB_2`, `DPNR_DPF_STATUS_REJU_PM`, `TARGET_COMMON_RAIL_PRESSURE`, `COMMON_RAIL_PRESSURE`, `FUEL_TEMPERATURE`, `EXHAUST_TEMPERATURE_B1S1..B2S3`, `TARGET_BOOSTER_PRESSURE`, `TARGET_VN_TURBO_POSITION.._2`, `ACTUAL_VN_TURBO_POSITION.._2`, `TARGET_EGR_VALVE_POS.._2`, `ACTUAL_EGR_VALVE_POS.._2`, `ACTUAL_THROTTLE_POSITION.._2`). Total parameters in `params.json`: 397.
2. `custom_components/wican/param_loader.py`:
   - Changed merge order in `_async_apply_stored()` and `async_sync()` to `{**result.data, **_PARAMS, **_load_params()}` so local definitions take precedence over remote GitHub fetches.
   - Added icons for Toyota parameters to `PARAM_NAME_ICONS`.
   - Added aliases for all Techstream and legacy PID names to `_PID_ALIASES`.
3. `custom_components/wican/sensor.py`:
   - Updated `_normalize_device_class()` so that explicit `"none"` device class from config returns `None` immediately without falling back to `params.json`.
4. `custom_components/wican/api.py`:
   - Handled `HTTP 400` (Bad Request) alongside `HTTP 404` in `async_export_log_rows()` so `/api/logger/export` falls back cleanly when the SD card params stream is not formatted as jsonl or csv.
5. `tests/test_param_loader.py`:
   - Added `TestToyotaParameters` verifying unit, device class, icon lookups, and odometer behavior (76 tests passing).
