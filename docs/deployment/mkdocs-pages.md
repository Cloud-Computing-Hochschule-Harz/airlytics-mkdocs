# MkDocs auf GitHub Pages

Die technische Airlytics-Dokumentation wird als eigene GitHub Project Page veröffentlicht.

## Repository

```text
Web-Services-Smart-Energy/airlytics-mkdocs
```

## Zieladresse

```text
https://web-services-smart-energy.github.io/airlytics-mkdocs/
```

## Lokale Vorschau

```bash
pip install -r requirements.txt
mkdocs serve
```

## Build prüfen

```bash
mkdocs build --strict
```

## Deployment

Vom Hauptbranch des Repositorys:

```bash
mkdocs gh-deploy --force
```

MkDocs baut die Dokumentation und veröffentlicht den erzeugten Stand standardmäßig auf dem Branch `gh-pages`.

## GitHub Pages aktivieren

Im Repository:

1. **Settings** öffnen.
2. **Pages** öffnen.
3. Unter **Build and deployment** als Source **Deploy from a branch** wählen.
4. Branch **gh-pages** auswählen.
5. Ordner **/(root)** auswählen.
6. Speichern.

Danach ist die Seite unter der oben angegebenen Project-Page-URL erreichbar.

## Aktualisierung

Nach Änderungen an der Dokumentation:

```bash
mkdocs build --strict
mkdocs gh-deploy --force
```

Die Markdown-Quelldateien bleiben im `main`-Branch. Der erzeugte HTML-Stand liegt ausschließlich im `gh-pages`-Branch.
