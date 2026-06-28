# MessPilot

MessPilot ist eine Web-App in aktiver Entwicklung fuer Elektro-Dokumentation,
Messprotokolle, Verteilerstrukturen, Kunden-/Objektverwaltung und PDF-Exporte.

Diese oeffentliche Repository dient als Community- und Informationsbereich fuer
Roadmap, Releases, Sicherheitsinformationen und Feedback. Der Anwendungscode
wird derzeit in einer privaten Entwicklungs-Repository gepflegt.

## Aktueller Status

- Status: Beta / aktive Entwicklung
- Fokus: Elektro-Messprotokolle, VDE-Workflows, Verteiler- und Stromkreisstruktur
- Deployment-Ziel: Docker-faehiger Betrieb auf VPS/Coolify
- Datenspeicher aktuell: JSON-Datei, spaetere Migration zu SQLite/PostgreSQL geplant

## Was MessPilot koennen soll

- Kunden, Liegenschaften, Gebaeude und Raeume strukturieren
- Verteiler und Stromkreise fachlich sauber erfassen
- Messprotokolle schrittweise ausfuellen
- VDE-/DGUV-Pruefablaeufe vorbereiten
- PDF-Vorschauen und Exporte erzeugen
- Benutzer- und Rollenverwaltung ausbauen
- spaeter stabil auf einem Server betrieben werden

## Dokumentation

| Datei | Inhalt |
| --- | --- |
| [CHANGELOG.md](CHANGELOG.md) | Release-Notizen und Aenderungen |
| [ROADMAP.md](ROADMAP.md) | Geplante Entwicklung |
| [SECURITY.md](SECURITY.md) | Sicherheits- und Meldeprozess |
| [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) | Lizenzhinweise zu Abhaengigkeiten |
| [docs/API.md](docs/API.md) | API-Uebersicht |
| [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) | Deployment-Hinweise |
| [docs/SYSTEM_OVERVIEW.md](docs/SYSTEM_OVERVIEW.md) | System- und Ablaufuebersicht |
| [LICENSE](LICENSE) | Lizenz |

## Architekturueberblick

```text
Browser
  |
  v
MessPilot API
  |
  +-- Stammdaten
  +-- Protokollentwuerfe
  +-- Messwerte
  +-- PDF-Export
  |
  v
Speicher
  +-- aktuell: JSON-Datei
  +-- geplant: SQLite/PostgreSQL
```

## Protokollablauf

```text
Zuordnung und Norm
  |
Grunddaten und Verteiler
  |
Stromkreise
  |
Besichtigen
  |
Erproben
  |
Messen
  |
Bewertung
  |
Abschluss / Export
```

## Feedback

Bitte nutze die oeffentlichen GitHub-Issues fuer:

- Fehlerberichte
- Feature-Wuensche
- Fragen zur Roadmap
- Vorschlaege zur Bedienung und zum Fachablauf

Sicherheitsprobleme bitte nicht als oeffentliches Issue mit Details melden.
Siehe dazu [SECURITY.md](SECURITY.md).

## Lizenz

MessPilot steht unter der MIT-Lizenz. Details siehe [LICENSE](LICENSE).
