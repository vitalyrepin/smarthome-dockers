# smarthome-dockers
Mosquitto + zegbee2mqtt + Home Assistant on Raspberry pi

docker exec -it smarthome_mqtt_1 mosquitto_pub -t zigbee2mqtt/bridge/ota_update/check -m 'Lamp_3_Ikea_Kron'

 mosquitto_pub -t zigbee2mqtt/bridge/ota_update/check -m 'Lamp_3_Ikea_Kron'

/etc/systemd/system/docker-smarthome.service

systemctl enable docker-smarthome

