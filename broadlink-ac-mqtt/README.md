# AC MQTT proxy for Home Assistant — Add-on

This add-on embeds the [Arbuzov/broadlink_ac_mqtt](https://github.com/Arbuzov/broadlink_ac_mqtt) project into Home Assistant — a maintained fork of the archived [liaan/broadlink_ac_mqtt](https://github.com/liaan/broadlink_ac_mqtt).

## Configuration

| Option | Default | Description |
|--------|---------|-------------|
| `service.daemon_mode` | `true` | Run the service as a daemon (keep looping) |
| `service.update_interval` | `10` | How often (in seconds) to poll each device |
| `service.self_discovery` | `false` | Automatically discover devices on the network |
| `service.bind_to_ip` | `false` | Bind discovery to a specific IP address |
| `service.debug` | `false` | Enable verbose debug logging (shortcut for `log_level: DEBUG`; overrides `log_level` when set) |
| `service.log_level` | `INFO` | Root log level written to the log file. One of `DEBUG`, `INFO`, `WARNING`, `ERROR`, `CRITICAL` |
| `service.log_level_console` | `INFO` | Log level shown in the Supervisor log. Use `DEBUG` to surface DEBUG messages in the UI |
| `mqtt.host` | `addon_core_mosquitto` | MQTT broker hostname |
| `mqtt.port` | `1883` | MQTT broker port |
| `mqtt.client_id` | `ac_to_mqtt` | MQTT client identifier |
| `mqtt.user` | — | MQTT username |
| `mqtt.passwd` | — | MQTT password |
| `mqtt.topic_prefix` | `/aircon` | Prefix for all MQTT topics |
| `mqtt.auto_discovery_topic` | `homeassistant` | Topic for HA MQTT auto-discovery |
| `mqtt.auto_discovery_topic_retain` | `false` | Retain auto-discovery messages |
| `mqtt.discovery` | `false` | Publish MQTT auto-discovery config |

## Enabling Debug Mode

If the add-on freezes or behaves unexpectedly, enable debug logging to collect more diagnostics:

1. Open the add-on configuration in Home Assistant.
2. Set `service.debug` to `true`, **or** set `service.log_level` to `DEBUG`.
3. To see DEBUG messages in the Supervisor log (and not just in the log file), also set `service.log_level_console` to `DEBUG`.
4. Restart the add-on.
5. Go to **Supervisor → Add-on → Broadlink AC MQTT → Log** to see verbose output.

In debug mode the add-on logs every device poll, every MQTT publish/subscribe event, and detailed error stack traces — all visible in the Home Assistant Supervisor log.

Disable debug mode once the issue has been diagnosed to keep logs concise.

### Log level precedence

`debug: true` &nbsp;>&nbsp; `log_level` &nbsp;>&nbsp; default (`INFO`). `log_level_console` only affects what reaches the Supervisor log; the log file still follows `log_level`.
