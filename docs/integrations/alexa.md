# Alexa-Integration

## Aufbau

Die Alexa-Handler-Lambda läuft in `eu-west-1`.

Wichtige Environment Variables:

```text
ALEXA_TOKEN_TABLE=airlytics-alexa-tokens
ALEXA_TOKEN_TABLE_REGION=eu-west-1
SENSORS_TABLE_NAME=sensors_iot
SENSORS_TABLE_REGION=eu-central-1
COGNITO_DOMAIN=https://eu-central-19gxdzpw07.auth.eu-central-1.amazoncognito.com
LWA_TOKEN_URL=https://api.amazon.com/auth/o2/token
ALEXA_EVENT_GATEWAY=https://api.eu.amazonalexa.com/v3/events
ALEXA_ENDPOINT_ID=airlytics-warning
ALEXA_EVENT_INSTANCE=airlytics.warning.level
```

Zusätzlich werden `ALEXA_CLIENT_ID` und aktuell noch `ALEXA_CLIENT_SECRET` als Environment Variables hinterlegt.

## Smart-Home-Endpoint

```text
Endpoint ID: airlytics-warning
Friendly Name: Airlytics Warnsystem
Interface: Alexa.SimpleEventSource
Instance: airlytics.warning.level
```

## Lambda-Aktionen

Für Tests und Backend-Aufrufe existieren unter anderem:

```text
send_test_event
get_warning_settings
set_warning_settings
process_sensor_value
process_measurement
```

## Eventversand

Ein erfolgreicher Aufruf des Alexa Event Gateways liefert:

```text
HTTP 204
```

## Routinen

| Event | Aktion |
|---|---|
| NORMAL | Lampe grün + optionale Ansage |
| WARNING | Lampe gelb + Warnansage |
| CRITICAL | Lampe rot + kritische Ansage |

Die Lambda unterstützt zusätzlich `ELEVATED` und `HIGH`. Diese wurden vor der Abgabe nicht mehr vollständig als eigene Routinen in der Alexa-App verfügbar gemacht.

## Sprachausgabe

Die Lambda spricht nicht direkt dynamisch über den Echo. Stattdessen löst ein Smart-Home-Event eine Alexa-Routine aus, in der eine statische Ansage hinterlegt ist.
