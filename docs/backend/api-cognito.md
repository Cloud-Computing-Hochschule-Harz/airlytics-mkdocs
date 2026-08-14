# API und Cognito

## Authentifizierung

Das Frontend verwendet Amazon Cognito über OIDC. Die API liest die Cognito-User-ID aus:

```text
requestContext.authorizer.claims.sub
```

Damit werden Benutzerzugriffe auf eigene Sensoren und Konfigurationen beschränkt.

## Benutzer-/Geräteschlüssel

Für Messwerte wird folgende Kombination verwendet:

```text
user_device = <cognito-sub>#<device-id>
```

Das Frontend erzeugt diesen Wert aus dem aktuell angemeldeten Benutzer und der ausgewählten Sensorstation.

## GetMetricsIoT

Beispiel:

```text
GET /metrics?user_device=<user>#<device>&limit=500
```

Optionale Parameter:

```text
from=<ISO timestamp>
to=<ISO timestamp>
limit=<number>
```

Die Lambda prüft, ob die Cognito-User-ID zum angefragten `user_device` gehört.

## Alexa Cognito App Client

Für Alexa Account Linking existiert ein separater Cognito App Client mit Authorization Code Grant und den Scopes:

```text
openid
email
profile
```

Alexa Redirect URLs:

```text
https://pitangui.amazon.com/api/skill/link/M1C5KGTR0RPYH
https://layla.amazon.com/api/skill/link/M1C5KGTR0RPYH
https://alexa.amazon.co.jp/api/skill/link/M1C5KGTR0RPYH
```
