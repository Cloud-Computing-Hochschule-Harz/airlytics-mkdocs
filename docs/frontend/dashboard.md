# Frontend

## Stack

- Vue 3
- TypeScript
- Vite
- OIDC Client
- Deployment über S3 und CloudFront

## Environment Variables

Deployment-spezifische Werte liegen in Vite-Variablen.

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

`.env` und `.env.*` sollen nicht versioniert werden. Eine `.env.example` kann ohne Secrets ins Repository.

## Messwertabruf

Das Frontend fragt das Backend mit `user_device` ab:

```text
/metrics?user_device=<cognito-sub>%23<device-id>
```

Die `%23`-Kodierung entspricht dem Zeichen `#`.

## Grenzwertlogik

Das Frontend enthält keine eigene PM2.5-/PM10-Warnlogik. Die Warnungen werden vom Backend geliefert. Dadurch gibt es keine doppelte, möglicherweise widersprüchliche fachliche Logik.

## Build

```bash
npm install
npm run build
```

Der Produktionsbuild liegt anschließend in `dist/`.

## Deployment

Der Inhalt von `dist/` wird in den S3-Frontend-Bucket hochgeladen. Anschließend wird der CloudFront-Cache mit dem Pfad `/*` invalidiert.
