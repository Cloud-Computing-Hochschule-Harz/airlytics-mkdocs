# Warnlogik und WHO

## Echtzeitstufen

Die Alexa-Lambda verwendet fünf interne Zustände.

| Status | PM2.5 µg/m³ | PM10 µg/m³ |
|---|---:|---:|
| NORMAL | `< 10` | `< 30` |
| ELEVATED | `10 – < 15` | `30 – < 45` |
| WARNING | `15 – < 20` | `45 – < 60` |
| HIGH | `20 – < 25` | `60 – < 75` |
| CRITICAL | `>= 25` | `>= 75` |

Die Gesamtstufe entspricht der höheren Stufe aus PM2.5 und PM10.

## Hysterese

Beim Absinken einer Stufe wird eine Hysterese angewendet. Standardwert:

```text
2 µg/m³
```

Dadurch wird bei Messwerten nahe einer Grenze ein häufiges Umschalten vermieden.

## Cooldown

Standard:

```text
300 Sekunden
```

Events können nach Ablauf erneut gesendet werden, auch wenn der Zustand gleich geblieben ist. Das dient der Synchronisierung externer Aktoren.

## WHO-Grenzwerte

Die WHO-Werte werden nicht als unmittelbare Momentan-Schwellen interpretiert.

| Wert | PM2.5 | PM10 |
|---|---:|---:|
| 24h | 15 µg/m³ | 45 µg/m³ |
| Jahr | 5 µg/m³ | 15 µg/m³ |

## Rolling 24h

`GetMetricsIoT` lädt Messwerte der letzten 24 Stunden und berechnet getrennte Mittelwerte für PM2.5 und PM10.

```json
{
  "period_hours": 24,
  "sample_count": 91,
  "pm25": {
    "average": 5.06,
    "limit": 15,
    "exceeded": false
  },
  "pm10": {
    "average": 7.18,
    "limit": 45,
    "exceeded": false
  },
  "status": "OK"
}
```

Mögliche Statuswerte: `OK`, `EXCEEDED`, `NO_DATA`.

Die Jahresmittel-Auswertung ist noch nicht implementiert.
