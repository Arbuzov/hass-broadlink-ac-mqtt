<!-- https://developers.home-assistant.io/docs/add-ons/presentation#keeping-a-changelog -->

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