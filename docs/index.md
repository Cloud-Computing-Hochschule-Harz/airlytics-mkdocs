# Airlytics – Technische Dokumentation

Airlytics ist ein IoT-System zur Überwachung der Raumluftqualität. Ein Raspberry Pi 3B+ erfasst Daten mit **BME680** und **SDS011**, sendet diese per MQTT an AWS und stellt die Daten über ein Vue-Frontend bereit. Zusätzlich existiert eine Alexa-Integration für visuelle und sprachliche Warnungen.

## Hauptfunktionen

- Erfassung von Temperatur, Luftfeuchtigkeit, Luftdruck, VOC, PM2.5 und PM10
- MQTT/TLS-Kommunikation über AWS IoT Core
- serverseitige Aufbereitung und Speicherung in DynamoDB
- Benutzertrennung über Amazon Cognito
- Web-Frontend mit Vue 3 und TypeScript
- Echtzeit-Warnstufen
- gleitende WHO-24h-Auswertung
- Alexa-Smart-Home-Events für eine Kasa-Lampe
- automatischer Sensorstart über systemd

## Regionen

| Bestandteil | Region |
|---|---|
| Hauptbackend / IoT / DynamoDB | `eu-central-1` |
| Alexa Handler / Token-Tabelle | `eu-west-1` |

## Wichtige Ressourcen

| Ressource | Name |
|---|---|
| Sensor-/Config-Tabelle | `sensors_iot` |
| Messwerttabelle | `data_iot` |
| Alexa Token-Tabelle | `airlytics-alexa-tokens` |
| Alexa Endpoint ID | `airlytics-warning` |
| Alexa Event Instance | `airlytics.warning.level` |

## Dokumentationsaufteilung

Diese MkDocs-Dokumentation enthält die technische Detailbeschreibung. Für die Abgabe existiert separat eine kompakte Typst-Dokumentation.

## Technische Dokumentation

Diese Website ist die ausführliche technische Dokumentation des Projekts. Die kompakte Projektdokumentation für die Abgabe wird separat in Typst gepflegt.
