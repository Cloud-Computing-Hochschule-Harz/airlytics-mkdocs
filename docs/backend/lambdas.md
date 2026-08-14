# Lambda-Funktionen

## Übersicht

| Lambda | Aufgabe |
|---|---|
| `iotProcessor` | MQTT-Messwerte aufbereiten, speichern und Alexa triggern |
| `GetMetricsIoT` | Messwerte, Warnungen und WHO-24h liefern |
| `GetSensorIoT` | Sensoren eines Benutzers laden |
| `NewSensorIoT` | Sensor, IoT Thing und Zertifikat erstellen |
| `UpdateSensorIoT` | Raum und Sensorbezeichnung aktualisieren |
| `DeleteSensorsIoT` | Thing, Zertifikate, Messwerte und Sensor-Item löschen |
| `GetConfigIoT` | Raumkonfigurationen laden |
| `NewConfigIoT` | Raumkonfiguration anlegen |
| `UpdateConfigIoT` | Raumkonfiguration aktualisieren |
| `DeleteConfigIoT` | Raumkonfiguration löschen |
| `airlytics-alexa-handler` | Alexa Discovery, Token, Events und Warnlogik |

## Environment Variables

### `GetMetricsIoT`

```text
DATA_TABLE_NAME=data_iot
CONFIG_TABLE_NAME=sensors_iot
```

### Sensor-Lambdas

`GetSensorIoT`:

```text
SENSORS_TABLE_NAME=sensors_iot
```

`NewSensorIoT`:

```text
SENSORS_TABLE_NAME=sensors_iot
IOT_POLICY_NAME=raspi-policy
ROOT_CA_URL=https://www.amazontrust.com/repository/AmazonRootCA1.pem
```

`UpdateSensorIoT`:

```text
SENSORS_TABLE_NAME=sensors_iot
```

`DeleteSensorsIoT`:

```text
SENSORS_TABLE_NAME=sensors_iot
DATA_TABLE_NAME=data_iot
```

### Config-Lambdas

Alle vier Config-Lambdas verwenden:

```text
SENSORS_TABLE_NAME=sensors_iot
```

## Designentscheidungen

- Werte wie `setting`, `config`, `sensor`, `NORMAL`, `WARNING` und `CRITICAL` sind Datenmodell- bzw. Protokollwerte und bleiben bewusst im Code.
- Tabellen, Regionen, ARNs und externe URLs werden soweit möglich über Environment Variables konfiguriert.
- Der Alexa Client Secret ist aktuell noch eine Environment Variable und soll später in Secrets Manager verschoben werden.
