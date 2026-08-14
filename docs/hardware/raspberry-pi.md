# Raspberry Pi

## Hardware

- Raspberry Pi 3B+
- BME680
- SDS011

Der BME680 wird per I²C angesprochen, der SDS011 über eine serielle USB-Schnittstelle.

## Gesendeter MQTT-Payload

Der Raspberry Pi sendet bewusst nur die Messdaten und minimale Geräteinformationen:

```json
{
  "device_id": "hs2-raspi-combined-01",
  "type": "sensor",
  "temperature": 28.71,
  "humidity": 38.27,
  "pressure": 989.72,
  "voc": 40841.0,
  "pm25": 6.5,
  "pm10": 8.4
}
```

Benutzer-ID, Raum und Sensorbezeichnung werden serverseitig ergänzt.

## Konfiguration

Die Betriebsparameter liegen in einer externen `config.json`.

Beispiel:

```json
{
  "device_id": "hs2-raspi-combined-01",
  "type": "sensor",
  "aws_iot": {
    "endpoint": "a2bwq26jbhr7m-ats.iot.eu-central-1.amazonaws.com",
    "topic": "iot/data",
    "cert_path": "certs/hs2-raspi-combined-01-certificate.pem.crt",
    "key_path": "certs/hs2-raspi-combined-01-private.pem.key",
    "root_ca_path": "certs/AmazonRootCA1.pem",
    "clean_session": false,
    "keep_alive_seconds": 30
  },
  "bme680": {
    "enabled": true,
    "i2c_address": "0x77"
  },
  "sds011": {
    "enabled": true,
    "serial_port": "/dev/ttyUSB0",
    "baudrate": 9600,
    "timeout": 2
  },
  "publish_interval_seconds": 30,
  "change_threshold_percent": 1.0,
  "force_publish_interval_seconds": 900
}
```

## Autostart

Der Sensorprozess läuft als systemd-Service:

```text
/etc/systemd/system/airlytics-sensor.service
```

Aktivierung:

```bash
sudo systemctl enable airlytics-sensor.service
sudo systemctl start airlytics-sensor.service
```

Status prüfen:

```bash
sudo systemctl status airlytics-sensor.service
```

Dadurch startet Airlytics automatisch nach dem Booten des Raspberry Pi.
