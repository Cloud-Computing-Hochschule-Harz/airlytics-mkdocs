# Sicherheit und offene Punkte

## Bereits umgesetzt

- MQTT/TLS mit X.509-Zertifikaten
- Cognito-Authentifizierung für Frontend/API
- Benutzertrennung über Cognito `sub`
- Sensor-Metadaten werden serverseitig ergänzt
- Tabellen, ARNs, Regionen und externe URLs weitgehend über Environment Variables
- `.env`-Dateien gehören nicht ins Repository
- Delete-/Update-Lambdas prüfen Benutzerzuordnung und Item-Typ

## Bekannter offener Punkt: Alexa Client Secret

Aktuell liegt `ALEXA_CLIENT_SECRET` noch als Lambda-Environment-Variable vor.

Für einen produktiven Ausbau sollte dieser Wert in AWS Secrets Manager oder einer vergleichbaren Secret-Verwaltung abgelegt und nur zur Laufzeit gelesen werden.

Dieser Umbau wurde bewusst nach hinten priorisiert, um die funktionale Fertigstellung des Projekts vor der Abgabe nicht zu gefährden.

## Weitere mögliche Verbesserungen

- IAM-Rechte weiter nach Least-Privilege reduzieren
- vollständige fünfstufige Alexa-Routinen
- WHO-Jahresmittelwerte
- automatisierte Integrationstests
- Monitoring und Alarme für Lambda-Fehler
- saubere Trennung von Dev- und Prod-Ressourcen
