# Lokale Entwicklung und Konfiguration

## Voraussetzungen

- Node.js / npm
- Zugriff auf die für die Entwicklungsumgebung vorgesehenen Cognito- und API-Werte

## Environment Variables

Das Frontend verwendet Vite-Environment-Variablen:

```env
VITE_API_BASE_URL=...
VITE_COGNITO_AUTHORITY=...
VITE_COGNITO_CLIENT_ID=...
VITE_COGNITO_REDIRECT_URI=...
VITE_COGNITO_LOGOUT_URI=...
VITE_COGNITO_DOMAIN=...
VITE_DEFAULT_SENSOR_NAME=BME680+SDS011
VITE_REFRESH_INTERVAL_MS=30000
```

`.env` und `.env.*` werden nicht versioniert. Für Dokumentationszwecke kann eine `.env.example` ohne geheime Werte verwendet werden.

## Installation

```bash
npm install
```

## Entwicklungsserver

```bash
npm run dev
```

## Produktionsbuild

```bash
npm run build
```

Der Produktionsbuild wird in `dist/` erzeugt. Vor einem Deployment sollte der TypeScript-/Vite-Build ohne Fehler durchlaufen.

## Metrics-Aufruf

Der aktuelle Benutzer wird über Cognito ermittelt. Für den Messwertabruf wird daraus gemeinsam mit der Geräte-ID der Schlüssel gebildet:

```text
user_device=<cognito-sub>#<device-id>
```

Beispielrequest:

```text
/metrics?user_device=<cognito-sub>%23hs2-raspi-combined-01
```

`%23` ist die URL-kodierte Darstellung von `#`.
