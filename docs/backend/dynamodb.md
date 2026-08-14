# DynamoDB

## `sensors_iot`

Die Tabelle enthält mehrere Item-Typen.

### Sensor

```json
{
  "user_id": "<cognito-sub>",
  "device_id": "hs2-raspi-combined-01",
  "room": "labor",
  "sensor": "BME680+SDS011",
  "type": "sensor"
}
```

### Globale Grenzwerte

Schlüssel:

```text
user_id   = config#global
device_id = thresholds
```

Wichtige Werte:

```text
pm25_limit_24h = 15
pm25_limit_year = 5
pm10_limit_24h = 45
pm10_limit_year = 15

pm25_elevated_default = 10
pm25_warning_default = 15
pm25_high_default = 20
pm25_critical_default = 25

pm10_elevated_default = 30
pm10_warning_default = 45
pm10_high_default = 60
pm10_critical_default = 75

hysteresis_default = 2
cooldown_seconds_default = 300
```

### User-Warneinstellungen

Schlüssel:

```text
user_id   = <cognito-sub>
device_id = warning-settings
```

Die Alexa-Lambda kann ältere Settings automatisch um fehlende Stufen ergänzen.

### Raumkonfiguration

Namensschema:

```text
user_id   = <cognito-sub>#config#<room>
device_id = setting
type      = config
```

## `data_iot`

Partition Key:

```text
user_device = <user-id>#<device-id>
```

Sort Key:

```text
sort_key = UTC ISO-8601 timestamp
```

Beispiel:

```json
{
  "user_device": "<user>#hs2-raspi-combined-01",
  "sort_key": "2026-08-14T20:12:09.277144+00:00",
  "temperature": 28.69,
  "humidity": 37.39,
  "pressure": 989.72,
  "voc": 43989,
  "pm25": 7.0,
  "pm10": 9.5,
  "room": "labor",
  "sensor": "BME680+SDS011"
}
```

## `airlytics-alexa-tokens`

Region:

```text
eu-west-1
```

Die Tabelle speichert die für Alexa Events benötigten Autorisierungstoken.
