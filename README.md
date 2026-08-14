# Airlytics Dokumentation

Technische Dokumentation des Airlytics IoT-Projekts.

Nach dem GitHub-Pages-Deployment erreichbar über:

https://web-services-smart-energy.github.io/airlytics-mkdocs/

## Lokal starten

```bash
pip install -r requirements.txt
mkdocs serve
```

## Produktionsbuild prüfen

```bash
mkdocs build --strict
```

## Auf GitHub Pages veröffentlichen

Vom `main`-Branch des Repositories aus:

```bash
mkdocs gh-deploy --force
```

Dadurch wird die gebaute Seite in den Branch `gh-pages` veröffentlicht.

Anschließend im GitHub-Repository unter **Settings → Pages** einstellen:

- Source: **Deploy from a branch**
- Branch: **gh-pages**
- Folder: **/(root)**
