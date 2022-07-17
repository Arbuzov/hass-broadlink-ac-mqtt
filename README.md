# Home Assistant broadlink MQTT addon repository

This addon embedds [liaan/broadlink_ac_mqtt](https://github.com/liaan/broadlink_ac_mqtt) project into Home assistant addons. I do not plan to add any new features into the parent application, but I am open if someone propose another project as parent.

[![Open your Home Assistant instance and show the add add-on repository dialog with a specific repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Farbuzov%2Fhass-broadlink-ac-mqtt)

To make your devices working you must:

* Install this addon
* Install [Mosquitto broker](https://github.com/home-assistant/addons/tree/master/mosquitto) or something like this to manage MQTT
* Get IP and MAC addresses of your devices
* Connect this addon to the Mosquitto
* Setup your [device topics](https://community.home-assistant.io/t/broadlink-ac-integration-ac-freedom-aux-dunham-rcool-akai-rinnai-kenwood-tornado-ballu/342789)

## Add-ons

This repository contains the following add-ons

### [Broadlink to MQTT add-on](./broadlink-ac-mqtt)

![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg

### Known problems

* Devices may not be discovered. Could be fixed by setting self_discovery: False at the service section.