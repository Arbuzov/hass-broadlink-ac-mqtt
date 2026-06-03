<!-- https://developers.home-assistant.io/docs/add-ons/presentation#keeping-a-changelog -->

## 0.6.9

- Patch upstream startup handling so an unreachable configured AC is retried five times, skipped, and does not prevent other configured ACs from starting
- Avoid a tight daemon loop when no configured ACs are reachable after startup retries

## 0.6.8

- Bump upstream to `Arbuzov/broadlink_ac_mqtt@1.2.3`, which restores the Linux config-path fallback that 1.2.2 had regressed (the broken Windows-style fallback caused `FileNotFoundError: '/usr/share/broadlink_ac_mqtt-1.2.2\\settings\\config.yml'` on add-on startup)

## 0.6.7

- Swap `pycryptodome` for `cryptography>=42` to match upstream `Arbuzov/broadlink_ac_mqtt@1.2.2`, fixing `ModuleNotFoundError: No module named 'cryptography'` at startup
- Install `libffi-dev` and `openssl-dev` so the `cryptography` wheel/build succeeds on Alpine

## 0.6.6

- Switched upstream source from the archived `liaan/broadlink_ac_mqtt@1.2.1b` to the maintained `Arbuzov/broadlink_ac_mqtt@1.2.2` fork
- Dropped the in-Dockerfile `sed` patches (the fork already ships the `import parser` and console-log-level fixes)
- Added `service.log_level` and `service.log_level_console` configuration options to control log verbosity via the add-on UI
- Add-on now forwards these to the `LOG_LEVEL` / `LOG_LEVEL_CONSOLE` environment variables consumed by `monitor.py`
- `service.debug` is preserved as a shortcut for `log_level: DEBUG` and still wins when both are set

## 0.6.5

- Updated Home Assistant base images to Python 3.13 / Alpine 3.22
- Replaced deprecated `pycrypto` with `pycryptodome`
- Updated GitHub Actions output syntax to `$GITHUB_OUTPUT`
- Normalized add-on option booleans to lowercase YAML values
- Aligned listed architectures with currently supported targets (`aarch64`, `amd64`)

## 0.6.4

- Added `service.debug` configuration option to enable verbose debug logging
- When debug mode is active, all DEBUG-level messages (device polls, MQTT events, stack traces) are forwarded to the Home Assistant Supervisor log
- Added add-on README with full configuration reference and debug usage instructions

## 0.6.3

- Cosmetic changes at readme
- CHANGELOG added to the project
- vscode tools added to simplify the development

## 0.6.2

- Initial release
