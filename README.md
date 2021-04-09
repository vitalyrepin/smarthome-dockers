# About smarthome-dockers

Config files for my smart home controlled by Raspberry Pi.

Hardware components:
 - 4 Zigbee lamps (Ikea and Philips HUE)
 - [Smoke detector Honeywell](https://www.zigbee2mqtt.io/devices/JTYJ-GD-01LM_BW.html)

Software components:
 - [Zigbee2MQTT](https://www.zigbee2mqtt.io/)
 - [Eclipse Mosquitto](https://mosquitto.org/)
 - [Home Assistant](https://www.home-assistant.io/)
 
Everything runs in docker.

# What this config does?

- Lamps and smoke detector are connected to Home Assistant and can be managed from its web ui
- [Zigbee2MQTT is integrated with Home Assistant](https://www.zigbee2mqtt.io/integration/home_assistant.html)
- Two scenes are configured: *Lights in the dark* and *No lights* in the Home Assistant and the first one is activated 5 minutes before sunset and at 7 AM (only if there is dark outside, uses geo location). Light are turned off always five minutes after sunrise and 15 minutes after midnight.

Don't forget to copy `docker-smarthome.service` to `/etc/systemd/system/docker-smarthome.service` and enable docker-smarthome
systemd service:

```
systemctl enable docker-smarthome
```

These configs are supposed to be placed to `/srv/smarthome/`

# Useful commands

To check docker logs:

```
docker-compose logs -f
```

To check is [OTA update](https://www.zigbee2mqtt.io/information/ota_updates.html) available for specific lamp (see docker logs for results):

```
docker exec -it smarthome_mqtt_1 mosquitto_pub -t zigbee2mqtt/bridge/ota_update/check -m 'Lamp_3_Ikea_Kron'
```

To set smoke alarm sensitivity login to container with `/bin/sh` (`docker exec -it /bin/sh`) and:

```
docker exec -it smarthome_mqtt_1 mosquitto_pub -t zigbee2mqtt/Brandvarnare/set -m '{"sensitivity": "medium"}' 
```

(Results are in the container logs!)
