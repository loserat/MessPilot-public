# MessPilot

MessPilot ist eine Web-Anwendung für strukturierte Elektro-Dokumentation, Prüfabläufe und PDF-Export im Gebäudebestand. Der aktuelle Schwerpunkt liegt auf Verteilern, Stromkreisen, VDE-/DGUV-Workflows, Beleuchtungsmessungen und ESD-Ableitmessungen.

Website: [www.messpilot.de](https://www.messpilot.de)

## Projektstatus

- Version: `0.7.1`
- Reifegrad: Beta
- Backend: `Node.js` + `Express`
- Frontend: modulares Vanilla JavaScript
- Persistenz: PostgreSQL als aktiver Hauptpfad
- Deployment: Docker / VPS / Coolify

MessPilot ist funktional nutzbar, aber noch nicht als final produktionsreif dokumentiert. Der laufende Fokus liegt auf SQL-Konsolidierung, PDF-Finalisierung und fachlicher Härtung der Prüfworkflows.

## Was MessPilot aktuell abdeckt

- Kunden-, Liegenschafts-, Gebäude- und Raumstruktur
- Verteiler- und Stromkreisverwaltung
- VDE- und DGUV-Protokollabläufe
- Wiederholungsprüfungen mit Vorwertbezug
- Beleuchtungsmessungen
- ESD Punkt-zu-Punkt-Ableitmessungen
- PDF-Vorschau und PDF-Export
- Rollen- und Rechtebasis
- Firmenlogo, Prüferdaten und Unterschrift im Export
- Dashboard-, Admin- und SQL-Statusansichten

## Kernfunktionen

### Struktur und Stammdaten

- Kunden, Standorte, Gebäude und Räume werden als technische Hierarchie verwaltet.
- Verteiler können mit Gruppen, Stromkreisen und Kabeldaten aufgebaut werden.
- Prüfer und Messgeräte sind im Systembereich pflegbar.

### Prüf- und Protokollworkflows

- VDE-/DGUV-Protokolle führen schrittweise durch Grunddaten, Stromkreise, Besichtigen, Erproben, Messen, Bewertung und Abschluss.
- Wiederholungsprüfungen übernehmen Vorwerte aus Vorgängerprotokollen.
- Mehrkabelige Stromkreise werden im VDE-Kontext als eigene Messzeilen geführt.

### PDF und Dokumentation

- PDF-Vorschau direkt in der Anwendung
- A4- und A3-Ausgaben je nach Protokolltyp
- Firmenlogo und Prüfer-Unterschrift im Export
- Mängel- und Bewertungsinformationen im Protokollkontext

### Betrieb und Administration

- PostgreSQL-/Prisma-Betrieb mit Systemstatus
- SQL-Adminansicht für technischen Überblick
- Rollenmodell für `master`, `admin`, `user`, `viewer`, `demo`

## Architektur

```text
Browser
  |
  v
Express API
  |
  +-- PostgreSQL / Prisma
  +-- Export-/PDF-Services
  +-- Rollen- und Fachlogik
```

Einige reine UI-Zustände bleiben lokal im Browser, fachliche Nutzdaten sollen jedoch aus dem SQL-Hauptpfad kommen.

## Quick Start

### Lokal mit Node.js

Voraussetzungen:

- Node.js `>= 20`
- npm
- optional PostgreSQL für den SQL-Betrieb

```bash
git clone https://github.com/loserat/messpilot.git
cd messpilot
npm install
npm start
```

Danach: `http://localhost:3100`

Testzugänge:

```text
admin / admin
demo / demo
```

### Docker

```bash
docker compose up -d --build
docker compose logs -f messpilot
docker compose down
```

Alternativer Port:

```bash
MESSPILOT_PORT=3101 docker compose up -d --build
```

## PostgreSQL-Betrieb

MessPilot läuft inzwischen primär auf PostgreSQL. Der typische lokale oder serverseitige Ablauf ist:

```bash
cp .env.example .env
npm install
npm run db:generate
npm run db:push
```

Beispiel für `DATABASE_URL`:

```text
postgresql://messpilot:<secret>@<host>:5432/messpilot?schema=public
```

Der produktive SQL-Betrieb ist aktiver Hauptpfad. Historische JSON-/Demo-Reste werden schrittweise aus produktionsnahen Fachabläufen entfernt.

## Dokumentation

- [CHANGELOG.md](CHANGELOG.md)
- [ROADMAP.md](ROADMAP.md)
- [SECURITY.md](SECURITY.md)
- [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)
- [docs/API.md](docs/API.md)
- [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)
- [docs/SYSTEM_OVERVIEW.md](docs/SYSTEM_OVERVIEW.md)
- [LICENSE](LICENSE)

## Feedback

Bitte nutze das öffentliche Repository für:

- Fehlerberichte
- Feature-Wünsche
- Fragen zur Roadmap
- Vorschläge zur Bedienung und zum Fachablauf

Sicherheitsprobleme bitte nicht öffentlich mit Details melden. Siehe dazu [SECURITY.md](SECURITY.md).

## Nächste fachliche Schwerpunkte

1. SQL-Only-Pfade weiter bereinigen
2. PDF-Templates fachlich finalisieren
3. VDE-/Wiederholungsprüfungen weiter härten
4. Export- und Auditpfade nachziehen
5. Rollen- und Betriebsmodell produktionsnäher machen

## Lizenz und Sicherheit

- Lizenz: [LICENSE](LICENSE)
- Sicherheitsmeldungen: [SECURITY.md](SECURITY.md)
