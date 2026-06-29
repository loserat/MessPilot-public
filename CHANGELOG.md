# Changelog

Alle nennenswerten Änderungen an MessPilot werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und das Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [Unreleased]

### Added
- **VDE-Messmatrix**: Bearbeitbare Breit-Tabelle für Stromkreise mit Sammelerfassung von Schutzleiter-, Isolations-, Überstrom- und RCD-Werten
- **Bewertungsreport**: Automatische Mängel-/Hinweisliste mit Sprungaktion direkt zum betroffenen Stromkreis und Messbereich
- **VDE-Regelbasis**: Erste zentrale Vorbewertung fuer RLO, Isolation, RCD, Zs/Zi und Ik anhand von Schutzorgan, Charakteristik und Nennstrom
- **Workflow-Fortschritt**: Abgeschlossene Protokollschritte werden persistiert (`completedProtocolSteps`) und bei Navigation berücksichtigt

### Improved
- **VDE-Validierung**: Pflichtfelder für Besichtigen/Erproben werden vollständig geprüft; unvollständige Stromkreisdaten werden klar benannt
- **Verteiler-Übernahme**: Wechsel des Verteilers aktualisiert optional die Stromkreisliste direkt im Protokollentwurf
- **Stromkreis-Duplikate**: Zielbezeichnungen werden beim Duplizieren konsistent fortlaufend nummeriert
- **Isolationslogik**: Sichtbare/erforderliche Isolationsfelder werden abhängig von Leiteranzahl und Phasenmodus dynamisch gefiltert
- **Bewertungsnavigation**: Fehler-/Hinweiszeilen springen in der VDE-Matrix direkt zur betroffenen Zelle und markieren diese rot

### Fixed
- **VDE-PDF-Tabelle**: Nicht erforderliche Isolationsspalten werden mit `X` markiert statt leer ausgegeben
- **Checklisten-PDF**: Status `Nicht geprüft` wird in Besichtigen/Erproben klar als gestrichener Eintrag dargestellt
- **Zuordnungswechsel**: Distributor-Auswahl in der Zuordnung triggert die korrekte Draft-Synchronisierung
- **VDE-Messwerte**: Auffällige oder falsche Messwerte bleiben gespeichert und werden nicht durch die Bewertung verworfen

### Planned
- Backend Persistierung: SQLite/PostgreSQL Migration
- Erweiterte Authentifizierung: OAuth2 / LDAP Support
- Mobile-optimierte Ansichten
- Import/Export von Bestandsdaten (CSV, XLS, JSON)
- Audit-Logging für alle Änderungen
- 2FA (Two-Factor Authentication)

---

## [0.2.0] - 2026-06-28

### Added
- **Verteiler-Modul**: Hierarchische Verwaltung von Schutzvorrichtungen (Schmelz → RCD → Stromkreise) mit Drag-and-Drop
- **Protokoll-Workflows**: VDE-Integration, Messgruppen-Tabs (Schutzleiter, Isolation, Schleife/Netz, RCD)
- **Raum-Editor**: SVG-basiertes Sketch-Tool mit Gitter-Snap und Raum-Templates
- **PDF-Export**: GitHub-Logo und Beleuchtungs-PDF Layout Seite 1 + 2
- **Versioning-Service**: Git-basierte Versions-Erkennung mit Caching
- **Kontext-Pinning**: Persistierung von Liegenschaft/Gebäude-Kontext über Sessions
- **GitHub Actions Sync**: Automatische Synchronisation von Dokumentation zur Public-Repo

### Improved
- Dashboard UI: Kompaktere Raum-Dialog Darstellung
- Messpunkt-Parser: Robustheit und Fehlerbehandlung
- VDE-Workflow: Zusammenfassung von Grunddaten & Verteiler-Schritt
- Authentifizierung: UI-Überarbeitung mit Session-Management
- Code-Kommentierung: Section Headers für bessere Navigierbarkeit

### Fixed
- Auth-Flow: Session-Persistence über Seitenneulade
- API Response Format: Standardisierte Fehlerbehandlung
- Storage: JSON-Backup bei fehlerhaften Writes
- Sync-Workflow: Token-Authentifizierung für Cross-Repo-Zugriff

### Known Issues
- Auth-System ist noch nicht produktionsreif (kein CSRF-Schutz, kein Audit-Log)
- Datenspeicher ist JSON-basiert (kein SQL-Backend)
- PDF-Export ist noch auf Beleuchtungs-Standard begrenzt
- Keine Mandantenfähigkeit

---

## [0.1.0] - 2026-06-01

### Added
- Initial Release
- Basis-CRUD für Kunden, Liegenschaften, Gebäude, Räume, Systeme
- Demo-Datensatz mit 30+ Datensätzen
- REST API mit standardisierten Endpoints
- Docker-basiertes Deployment
- JSON-File-basierte Datenspeicherung
- Rollenbasierte Zugriffskontrolle (Admin, User, Viewer, SystemAdmin)
- Basis-PDF-Export für Inspektionen
- Benutzer-Management mit Login/Logout
- System-Einstellungen mit Theme-Wechsel

---

## Versioning

Versionen werden in `src/services/githubVersion.service.js` automatisch über Git-Tags oder Fallback auf `package.json` ermittelt.

- **Snapshot-Versionen**: Commits werden mit Short-SHA gekennzeichnet (z.B. `0.2.0-abc1234`)
- **Release-Versionen**: Git-Tags folgen SemVer Format `v0.2.0`

---

## Beitragen

Melden Sie Bugs, Wünsche und Verbesserungen bitte unter:
👉 https://github.com/loserat/MessPilot-public/issues

Für Sicherheitsprobleme siehe `SECURITY.md`.

---

**Danke dass Sie MessPilot verwenden!** 🚀
