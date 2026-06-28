# Changelog

Alle nennenswerten Änderungen an MessPilot werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und das Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [Unreleased]

### Planned
- Backend Persistierung: SQLite/PostgreSQL Migration
- Erweiterte Authentifizierung: OAuth2 / LDAP Support
- Mobile-optimierte Ansichten
- Import/Export von Bestandsdaten (CSV, XLS, JSON)

---

## [0.2.0] - 2026-06-28

### Added
- **Verteiler-Modul**: Hierarchische Verwaltung von Schutzvorrichtungen (Schmelz → RCD → Stromkreise) mit Drag-and-Drop
- **Protokoll-Workflows**: VDE-Integration, Messgruppen-Tabs (Schutzleiter, Isolation, Schleife/Netz, RCD)
- **Raum-Editor**: SVG-basiertes Sketch-Tool mit Gitter-Snap und Raum-Templates
- **PDF-Export**: GitHub-Logo und Beleuchtungs-PDF Seite 1+2 Layout
- **Versioning-Service**: Git-basierte Versions-Erkennung mit Caching
- **Kontext-Pinning**: Persistierung von Liegenschaft/Gebäude-Kontext über Sessions

### Improved
- Dashboard UI: Kompaktere Raum-Dialog Darstellung
- Messpunkt-Parser: Robustheit und Fehlerbehandlung
- VDE-Workflow: Zusammenfassung von Grunddaten & Verteiler-Schritt
- Authentifizierung: UI-Überarbeitung mit Session-Management

### Internal
- Modulare Frontend-Architektur vorbereitet für künftige Splits
- Code-Commenting: Section Headers für bessere Navigierbarkeit
- Daily-Dokumentation: Detaillierte Progress Logs (docs/daily/)

### Fixed
- Auth-Flow: Session-Persistence über Seitenneulade
- API Response Format: Standardisierte Fehlerbehandlung
- Storage: JSON-Backup bei fehlerhaften Writes

---

## [0.1.0] - 2026-06-01

### Added
- Initial Release
- Basis-CRUD für Kunden, Liegenschaften, Gebäude, Räume, Systeme
- Demo-Datensatz mit 30+ Datensätzen
- REST API mit standardisierten Endpoints
- Docker-basiertes Deployment
- JSON-File-basierte Datenspeicherung
- Rollenbasierte Zugriffskontrolle (Admin, User, Viewer)
- Basis-PDF-Export für Inspektionen

---

## Versioning

Versionen werden in `src/services/githubVersion.service.js` automatisch über Git-Tags oder Fallback auf `package.json` ermittelt.

- **Snapshot-Versionen**: Commits werden mit Short-SHA gekennzeichnet (z.B. `0.2.0-abc1234`)
- **Release-Versionen**: Git-Tags folgen SemVer Format `v0.2.0`

---

## Beitragen

Melden Sie Bugs, Wünsche und Verbesserungen bitte unter:
https://github.com/loserat/MessPilot-public/issues

Für Sicherheitsprobleme siehe `SECURITY.md`.
