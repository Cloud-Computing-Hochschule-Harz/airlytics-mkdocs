# Tests und Fehlersuche

## Abschluss-Systemcheck

Ein CloudShell-Skript prüfte read-only:

- alle DynamoDB-Tabellen aktiv
- Sensor-Metadaten vorhanden
- globale Config und User-Warnsettings vorhanden
- aktuelle Messwerte vorhanden
- alle zentralen Lambda-Funktionen aktiv
- benötigte Environment Variables vorhanden
- direkter Test von `GetMetricsIoT` erfolgreich
- Alexa-Handler erreichbar

Ergebnis:

```text
Erfolgreich: 48
Fehler:      0
```

## Letzten Messwert prüfen

```bash
aws dynamodb query \
  --region eu-central-1 \
  --table-name data_iot \
  --key-condition-expression "user_device = :ud" \
  --expression-attribute-values '{
    ":ud": {
      "S": "<USER-ID>#hs2-raspi-combined-01"
    }
  }' \
  --no-scan-index-forward \
  --limit 3
```

## Alexa-Testevent

```json
{
  "action": "send_test_event",
  "user_id": "<USER-ID>",
  "event_id": "CRITICAL"
}
```

Erwartung:

```json
{
  "status": "success",
  "event": "CRITICAL",
  "alexa_http_status": 204
}
```

## Automatische Klassifikation

Beispiel HIGH:

```json
{
  "action": "process_measurement",
  "user_id": "<USER-ID>",
  "device_id": "test-manual",
  "pm25": 22,
  "pm10": 20
}
```

Erwartete Gesamtstufe: `HIGH`.

## WHO-Test

Für den Rolling-24h-Test wurden synthetische Daten angelegt. PM2.5 = 18 und PM10 = 55 führten erwartungsgemäß zu `EXCEEDED`.
