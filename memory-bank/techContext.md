# Tech Context

## Technologies
- Python 3.12 / Home Assistant Core
- Pytest, pytest-homeassistant-custom-component, pytest-asyncio
- Custom Component: `custom_components/wican`

## Constraints & Requirements
- Preserve existing 337 entries in `params.json`, add 22 canonical entries.
- Preserve bundled params when merging GitHub sync updates.
- Adhere to Home Assistant state machine constraints (e.g. 255 character limit, numeric state conversions, state_class rules).
