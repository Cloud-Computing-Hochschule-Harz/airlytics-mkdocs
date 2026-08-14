# Architektur

## Gesamtübersicht

```mermaid
flowchart LR
    A[Raspberry Pi 3B+\nBME680 + SDS011] -->|MQTT/TLS| B[AWS IoT Core]
    B --> C[iotProcessor Lambda]
    C --> D[(data_iot)]
    E[(sensors_iot)] --> C
    D --> F[API Lambdas]
    E --> F
    F --> G[API Gateway]
    G --> H[Vue 3 Frontend]
    I[Amazon Cognito] --> G
    C --> J[Alexa Handler\neu-west-1]
    J --> K[Alexa Event Gateway]
    K --> L[Alexa Routinen]
    L --> M[Kasa Lampe / Echo]
```

## Verantwortlichkeiten

### Raspberry Pi

- liest Sensorwerte
- kennt keine Cognito-User-ID
- sendet nur Geräte-ID, Typ und Messwerte
- startet automatisch per systemd

### AWS IoT Core

- MQTT-Endpunkt
- TLS-Zertifikatsprüfung
- Übergabe an Lambda über IoT-Regel

### `iotProcessor`

- ordnet Messung einem Benutzer zu
- ergänzt Raum und Sensorbezeichnung
- erstellt UTC-Zeitstempel
- speichert in `data_iot`
- triggert Alexa-Auswertung asynchron

### API-Lambdas

- CRUD für Sensoren und Raumkonfigurationen
- Laden historischer Messdaten
- Echtzeit- und WHO-Auswertung
- Cognito-basierte Benutzertrennung

### Frontend

- Login
- Sensorverwaltung
- Visualisierung
- Warnanzeige
- Diagramme

### Alexa

- erhält SimpleEventSource-Events
- Routinen setzen Lampenfarbe und optional Sprachausgabe
