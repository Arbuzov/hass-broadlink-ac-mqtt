<!-- https://developers.home-assistant.io/docs/add-ons/presentation#keeping-a-changelog -->

## 0.7.0

- Consume `Arbuzov/broadlink_ac_mqtt@1.2.4` directly instead of patching 1.2.3 at build time: both downstream patches (`skip-unreachable-devices`, `mqtt-callback-guard`) are now upstream, so `patches/` and the `patch -p1` chain are gone
- Pick up the rest of 1.2.4 on top of those patches: an unnamed AC no longer aborts auto-discovery for every device, ambient temperature above 31°C no longer wraps and now keeps its tenths, a swing position the AC reports but the mode table does not name no longer makes Home Assistant drop the entity, the retired `action_topic` that made HA 2025+ reject the entity is gone, the last-will/goodbye message is actually waited on rather than assumed sent, and the MQTT network thread is stopped where it was started
- Take the broker from the Supervisor when `mqtt.host` is left empty: host, port, username and password all come from the MQTT service (`mqtt:want`), so nothing has to be typed in twice and there is no hostname left to get wrong. A host that is filled in still wins, so an external broker keeps working
- Fix the default MQTT host, which no install could ever have connected to: it was `addon_core_mosquitto`, the Docker container name, which the Supervisor DNS does not resolve (`[Errno -5] Name has no usable address`). The default is now empty, i.e. "ask the Supervisor"
- Drop the `koos` / `koos_se_password` placeholder credentials from the defaults; they are empty now, and empty means the Supervisor supplies them
- Existing Home Assistant entities survive the upgrade: the discovery topic and `unique_id` are still the device MAC, and every command and state topic is unchanged
- Install the upstream `requirements.txt` rather than a hand-kept package list, so the add-on inherits its pins — notably `paho-mqtt>=2.1,<3`, which stops an unattended jump to a future paho 3.x
- Install to `/usr/share/broadlink_ac_mqtt` instead of a version-named directory, so an upstream bump no longer has to be mirrored in the service script, and pin the download to the upstream commit rather than the tag, so one add-on version can only ever mean one set of sources
- Fix the `mac` placeholder in the default configuration: it was 14 hex characters, and every real MAC is 12
- Drop the C build toolchain from the image: every requirement resolves to a musllinux wheel on both architectures, so nothing was ever compiled. The add-on image goes from ~393 MB to ~150 MB
- Keep an upper bound on `cryptography`, which upstream floats unbounded: the AES code still names the `backend` argument that has been deprecated since cryptography 3.1, so an unbounded major could break a rebuild of an unchanged add-on version
- **Existing installs keep their saved options.** To move onto the Supervisor's broker, clear `mqtt.host`, `mqtt.user` and `mqtt.passwd` in the add-on configuration; to stay on a broker of your own, set `mqtt.host` to a name that resolves (`core-mosquitto` for the Mosquitto add-on)

## 0.6.10

- Stop an MQTT command from killing the paho network thread: any exception raised while handling a message is now logged instead of escaping into the client loop (previously it silently ended all MQTT traffic until an add-on restart)
- Fix `AttributeError: 'AcToMqtt' object has no attribute 'device_objects'` when a retained/queued command arrived between the MQTT connect and the first poll cycle
- Ignore commands addressed to devices that were skipped as unreachable at startup, instead of raising `KeyError`
- Match devices by MAC case-insensitively, so a MAC written in upper case in the add-on options no longer leaves that AC deaf to commands (state reporting always used the lower-case form the device reports)

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
