# AWS IoT und Verarbeitung

## MQTT

Der Raspberry Pi verbindet sich per TLS mit AWS IoT Core und veröffentlicht auf:

```text
iot/data
```

Die Authentifizierung erfolgt mit einem gerätespezifischen X.509-Zertifikat.

## IoT Thing

Beim Anlegen eines Sensors wird ein AWS-IoT-Thing erzeugt. Das Namensschema lautet:

```text
<user-id>-<device-id>
```

Beispiel:

```text
53349842-...-hs2-raspi-combined-01
```

## IoT Policy

Der Name der Policy wird in `NewSensorIoT` über folgende Environment Variable bezogen:

```text
IOT_POLICY_NAME=raspi-policy
```

## iotProcessor

Wichtige Environment Variables:

```text
DATA_TABLE_NAME=data_iot
SENSORS_TABLE_NAME=sensors_iot
ALEXA_LAMBDA_ARN=arn:aws:lambda:eu-west-1:372448341428:function:airlytics-alexa-handler
ALEXA_LAMBDA_REGION=eu-west-1
```

### Aufgaben

1. `device_id` aus MQTT-Event lesen
2. Sensor-Metadaten in `sensors_iot` finden
3. `user_id`, `room` und `sensor` ergänzen
4. UTC-`sort_key` erzeugen
5. Messwert in `data_iot` speichern
6. Alexa Handler asynchron mit `process_measurement` aufrufen

Ein Fehler beim Alexa-Aufruf verhindert die Messwertspeicherung nicht.
