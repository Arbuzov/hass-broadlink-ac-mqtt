# AC MQTT proxy for Home Assistant — Add-on

This add-on embeds the [liaan/broadlink_ac_mqtt](https://github.com/liaan/broadlink_ac_mqtt) project into Home Assistant.

## Configuration

| Option | Default | Description |
|--------|---------|-------------|
| `service.daemon_mode` | `true` | Run the service as a daemon (keep looping) |
| `service.update_interval` | `10` | How often (in seconds) to poll each device |
| `service.self_discovery` | `false` | Automatically discover devices on the network |
| `service.bind_to_ip` | `false` | Bind discovery to a specific IP address |
| `service.debug` | `false` | Enable verbose debug logging to help diagnose issues |
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
2. Set `service.debug` to `true`.
3. Restart the add-on.
4. Go to **Supervisor → Add-on → Broadlink AC MQTT → Log** to see verbose output.

In debug mode the add-on logs every device poll, every MQTT publish/subscribe event, and detailed error stack traces — all visible in the Home Assistant Supervisor log.

Disable debug mode once the issue has been diagnosed to keep logs concise.
