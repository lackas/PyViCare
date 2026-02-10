# PyViCare Local Development

## Deprecated API Paths

Do NOT use these deprecated Viessmann API paths:

| Deprecated | Use Instead |
|------------|-------------|
| `heating.buffer.*` | `heating.bufferCylinder.*` |

Some devices expose both paths with identical values, but `heating.buffer.*` is deprecated.

## Pre-commit Checks

Run these before committing:

```bash
.venv/bin/pylint PyViCare/*.py tests/*.py
.venv/bin/ruff check .
.venv/bin/pytest tests/
```

Or run all CI checks:

```bash
.venv/bin/pylint PyViCare/*.py tests/*.py && .venv/bin/ruff check . && .venv/bin/pytest tests/
```

**Important:** ruff and pylint check different things. Pylint does deeper static analysis
(e.g., checking if methods exist on classes). Always run both - ruff passing doesn't mean
pylint will pass.

## Ideas (low priority)

### RoomControl / Zigbee TRV support

PyViCare skips `deviceType: roomControl` devices (line 55 in PyViCare.py). The `Smart_RoomControl`
is a virtual zigbee coordinator with 457 features covering 24 rooms (rooms.0-23), including:
- Room sensors, humidity, algorithms
- TRV control, child lock, open window detection

The Vitocal 300G test data (Trebron24, PR #645) has Zigbee TRVs. We use Homematic thermostats
instead, so not directly useful to us, but could be explored if time permits.
