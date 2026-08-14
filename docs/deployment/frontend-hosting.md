# Frontend Hosting

Das Vue-Frontend wird als statische Anwendung gebaut und über Amazon S3 und CloudFront ausgeliefert.

## 1. Frontend bauen

```powershell
npm run build
```

Nach einem erfolgreichen Build befindet sich die Produktionsversion im Ordner:

```text
dist/
```

## 2. S3 aktualisieren

Der Inhalt von `dist/` wird in den Airlytics-Frontend-Bucket geladen.

Aktueller Bucket:

```text
airlytics-frontend-dev-372448341428-eu-central-1-an
```

Bei einem manuellen Upload müssen insbesondere die aktuelle `index.html` und der komplette aktuelle `assets/`-Ordner hochgeladen werden.

## 3. CloudFront invalidieren

Nach dem Upload wird für die Airlytics-CloudFront-Distribution eine Invalidation erstellt:

```text
/*
```

Dadurch werden gecachte Dateien verworfen und die neue Frontend-Version ausgeliefert.

## 4. Funktionstest

Nach dem Deployment werden mindestens folgende Punkte geprüft:

1. Cognito-Login funktioniert.
2. Sensorstation wird angezeigt.
3. Messwerte werden geladen.
4. `/metrics` verwendet `user_device`.
5. Warnungen werden ohne Frontend-eigene PM-Grenzwertlogik dargestellt.
