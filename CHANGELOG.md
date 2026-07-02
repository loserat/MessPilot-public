# Changelog

Alle nennenswerten Änderungen an MessPilot werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und das Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [Unreleased]

Keine Eintraege seit `0.5.0`.

---

## [0.5.0] - 2026-07-02

### Added
- **System > Firma**: Firmenstammdaten inklusive Logo-Datei vorbereitet; das Logo bleibt in der Firmenansicht als eigene Vorschau sichtbar.
- **System > Adminkonsole**: Technische Systeminfo wurde zur rechten Admin-Ansicht umbenannt und zeigt Speicherstatus, Adapter, Healthcheck und Datenbereichszaehlung.
- **VDE-Wiederholungsfrist**: DIN-VDE-0100-600-Protokolle koennen ein Wiederholungsintervall von 1 bis 4 Jahren speichern; das naechste Pruefdatum wird automatisch berechnet.
- **Dashboard-Pruefliste**: Dashboard zeigt naechste VDE-Pruefungen chronologisch und bietet direkte Aktionsbuttons fuer Protokolle, Kunden, Raeume, Verteiler, Export und Adminansicht.
- **Bewertungsspruenge**: Globale VDE-Maengel und Hinweise haben jetzt ebenfalls Sprungaktionen zum passenden Protokollschritt.

### Changed
- **PDF/VDE-Export**: Finaler gemischter Seitenaufbau mit DIN A4 Deckblatt, DIN A3 Stromkreistabelle, DIN A4 Hinweisen/Maengelbericht und letzter Unterschriftseite.
- **PDF/Beleuchtung**: ASR-PDFs laufen in DIN A4 Hochformat; Messpunkte werden zuerst aufgelistet, Ergebnis folgt danach, die Raumskizze steht immer auf der letzten Seite.
- **PDF-Branding**: Footer-Logo auf das runde MessPilot-Logo umgestellt und direkt mit dem Public-GitHub-Repository verlinkt.
- **Systemnavigation**: Leere Systembereiche fuer PDF, Vorlagen und System entfernt; rechte Infokaesten in Systemansichten entfallen.
- **Kundenlisten**: Erklaertexte unter Listenueberschriften entfernt, um mehr Platz fuer Nutzdaten zu schaffen.
- **ASR-Messwerte**: Messwertliste, Eingabefluss, Enter/Button-Verhalten und automatische Bewertung wurden verdichtet.
- **Raumeditor**: Bauteile fuer Tueren/Fenster wurden weiter Richtung freier Benennung, Farbauswahl, Breitenanpassung und sauberer Listenansicht entwickelt.
- **Versionierung**: Hauptversion auf `0.5.0` angehoben; betroffene Unterversionen fuer Protokollkern, VDE, Beleuchtung, PDF, UI, Datenmodell und Backend aktualisiert.

### Fixed
- **VDE-Speichern**: Bearbeitete Messwerte werden beim erneuten Oeffnen nicht mehr durch alte Stromkreis-Snapshots ueberschrieben.
- **VDE-Status**: Abgeschlossene Protokolle werden beim erneuten Bearbeiten nicht durch reines Zuruecknavigieren automatisch auf `In Bearbeitung` zurueckgesetzt.
- **PDF-Seitenumbruch**: Beleuchtungs-Messpunkttabellen laufen nicht mehr in den Footerbereich.

---

## [0.4.0] - 2026-07-01

### Added
- **Archivierte Protokolle**: Archivierte Protokolle sind keine Untertab-Ansicht mehr, sondern werden ueber einen Pfeilbutton neben `Protokoll erstellen` als eigene Uebersicht geladen.
- **VDE-Bewertung 0.4**: Fehlende Messwerte werden erst nach aktivem Weiter-Versuch orange markiert; harte Grenzwertverletzungen bleiben sofort rot.
- **VDE-Grenzwerte**: Isolationswerte muessen strikt `> 500 MOhm` sein; Zi/Ik, ungueltige RCD-Werte, Beruehrungsspannung und negative Widerstands-/Impedanzwerte werden staerker bewertet.
- **Persistenz-Roadmap**: PostgreSQL, dauerhafter PDF-Storage, Audit-Log und Revisionsmodell als naechster technischer Fokus dokumentiert.
- **Storage-Konfiguration**: Healthcheck und Environment-Konfiguration zeigen jetzt explizit JSON/PostgreSQL- und PDF-Storage-Zielwerte.
- **Repository-Schicht**: Backend-Services nutzen einen zentralen Repository-Adapter; der aktuelle JSON-Store ist damit austauschbar fuer spaetere PostgreSQL-Anbindung.

### Changed
- **Protokollbereich**: Die Untertab-Leiste unter `Protokolle` wurde entfernt; aktive Protokolle bleiben die Standardansicht.
- **Listenansichten**: Kunden-, Objekt-, Protokoll- und Exportlisten zeigen weniger Detailspalten; Telefon, E-Mail, Hinweise, Masse und PDF-/Statusdetails bleiben in Detailansichten oder Aktionsmenues.
- **PDF/VDE-Export**: VDE-PDF-Tabellenbreiten, Kopfbereiche, Mangelhinweise und Stromkreis-Hinweise wurden weiter vereinheitlicht.
- **Raumanlage**: Raumskizze, Bauteile, Wandzuordnung und Arbeitsdialoge wurden weiter Richtung finaler Bedienlogik vorbereitet.
- **Versionierung**: App-Version und betroffene Baustein-Versionen fuer Protokollkern, VDE, Regelbasis, PDF, UI, Datenmodell und Objektstruktur auf `0.4.0` bzw. passende Teilstaende angehoben.
- **API-Dokumentation**: Healthcheck, Rollen und PDF-Archiv-Endpunkte auf den aktuellen Backend-Stand gebracht.

### Fixed
- **Protokollnavigation**: Klick auf die Hauptnavigation `Protokolle` fuehrt wieder zur aktiven Protokollliste, auch wenn zuvor archivierte Protokolle angezeigt wurden.
- **VDE-Messmatrix**: Fehlende Pflichtfelder werden nicht mehr durch reines Rendern der Schrittanzeige als validiert markiert.
- **Deployment-Sicherheit**: Hart eingetragener GitHub-Token aus `docker-compose.yml` entfernt; Tokens werden nur noch ueber Environment-Variablen gesetzt.

### Changed
- **Frontend-Struktur**: Statische Icons, API-Wrapper, Datumsformatierung, Navigation, Kundenkontext, Datenzugriff, Dashboard, Kunden-Dialoge, Verteiler-Seite, Settings-Rendering, Exportansichten und Kunden-Einstieg aus `app.js` in eigene JS-Dateien ausgelagert
- **Frontend-Struktur**: Kunden-/Objekt-Tabellen und einfache Platzhalter-/Verwaltungsseiten aus `app.js` in `app.customer-tables.js` und `app.placeholder-pages.js` ausgelagert.
- **Frontend-Struktur**: Auth/Login-Screen, Session-Menü und Rollen-Helfer aus `app.js` nach `app.auth.js` ausgelagert.
- **Versionierung**: Semantic-Versioning-Spezifikation dokumentiert und zentrale Baustein-Versionen nach `src/config/versioning.js` ausgelagert
- **Protokolllisten**: Protokollübersicht und Protokolltabellen lassen sich nach Datum, Prüfart, Prüfobjekt, Status und PDF-Status sortieren.
- **Listenaktionen**: Verteiler werden in der Liste über einen kompakten Bearbeiten-Icon-Button geöffnet.
- **Zuordnungsdialoge**: Liegenschafts- und Gebäudeanlage verwenden kompaktere Popups mit kleineren Suchlisten; Protokoll-Zuordnungskarten und Raumdialog wurden verdichtet, damit der Bildschirm weniger überladen wirkt.

### Fixed
- **VDE-PDF-Export**: Stromkreistabellen werden nicht mehr mit leeren Zeilen aufgefüllt; pro Tabellenblatt erscheinen nur vorhandene Stromkreise.
- **VDE-PDF-Export**: Deckblatt, Tabellenblätter und Mängelbericht verwenden denselben Kopf; Seitenzählung wird einheitlich unten mittig ausgegeben.
- **Projektpflege**: `package-lock.json` auf die aktuelle App-Version synchronisiert und leere Arbeitsordner entfernt.
- **Kundenlisten**: Löschaktionen für Liegenschaften, Gebäude und Räume wurden aus den Listen entfernt und in die jeweiligen Bearbeiten-Dialoge verschoben.

### Planned
- Backend Persistierung: SQLite/PostgreSQL Migration
- Erweiterte Authentifizierung: OAuth2 / LDAP Support
- Mobile-optimierte Ansichten
- Import/Export von Bestandsdaten (CSV, XLS, JSON)
- Audit-Logging für alle Änderungen
- 2FA (Two-Factor Authentication)

---

## [0.3.0] - 2026-06-29

### Added
- **VDE-Messmatrix**: Bearbeitbare Breit-Tabelle für Stromkreise mit Sammelerfassung von Schutzleiter-, Isolations-, Überstrom- und RCD-Werten
- **Bewertungsreport**: Automatische Mängel-/Hinweisliste mit Sprungaktion direkt zum betroffenen Stromkreis und Messbereich
- **VDE-Regelbasis**: Zentrale Vorbewertung `VDE-Regelbasis 0.3` fuer PE, RLO-Plausibilitaet, Isolation, RCD, TT-Plausibilitaet, Zs/Zi und Ik anhand von Schutzorgan, Charakteristik und Nennstrom
- **Workflow-Fortschritt**: Abgeschlossene Protokollschritte werden persistiert (`completedProtocolSteps`) und bei Navigation berücksichtigt
- **Systemstammdaten**: Prüfer- und Messgeräteverwaltung mit API, Kalibrierfeldern und Unterschriftsdatei-Referenz

### Improved
- **VDE-Zuordnung**: VDE/DGUV-Protokolle arbeiten im Startdialog ohne Anlagen-Auswahl; der Verteiler ist die verbindliche Quelle fuer die Stromkreisliste
- **Oberflaeche**: Grosse Seitenueberschriften weiter reduziert, Listenaktionen auf kompakte Plus-Buttons umgestellt und Login-Screen mit neuem MessPilot-Logo beruhigt
- **VDE-Validierung**: Pflichtfelder für Besichtigen/Erproben werden vollständig geprüft; unvollständige Stromkreisdaten werden klar benannt
- **Verteiler-Übernahme**: Wechsel des Verteilers aktualisiert optional die Stromkreisliste direkt im Protokollentwurf
- **Stromkreis-Duplikate**: Zielbezeichnungen werden beim Duplizieren konsistent fortlaufend nummeriert
- **Isolationslogik**: Sichtbare/erforderliche Isolationsfelder werden abhängig von Leiteranzahl und Phasenmodus dynamisch gefiltert
- **Bewertungsnavigation**: Fehler-/Hinweiszeilen springen in der VDE-Matrix direkt zur betroffenen Zelle und markieren diese rot
- **Fachliche Vorbewertung**: RLO ohne Leitungslängenmodell, K/Z-Kennlinien und selektive RCDs werden als Pruefhinweise statt als scheinbar finale Normfehler behandelt
- **VDE-Livebewertung**: niO-Messwerte werden direkt beim Eingeben in der Matrix markiert, ohne den Prüfablauf zu blockieren
- **Protokoll-Grunddaten**: Prüfer und VDE-Messgeräte werden aus Systemstammdaten ausgewählt und als Snapshot im Protokoll gespeichert

### Fixed
- **VDE-Ablauf**: Der Protokollstart blockiert nicht mehr durch eine nicht genutzte Anlagenpflicht und kann den gewaehlten Verteiler direkt laden
- **VDE-PDF-Tabelle**: Nicht erforderliche Isolationsspalten werden mit `X` markiert statt leer ausgegeben
- **Checklisten-PDF**: Status `Nicht geprüft` wird in Besichtigen/Erproben klar als gestrichener Eintrag dargestellt
- **Zuordnungswechsel**: Distributor-Auswahl in der Zuordnung triggert die korrekte Draft-Synchronisierung
- **VDE-Messwerte**: Auffällige oder falsche Messwerte bleiben gespeichert und werden nicht durch die Bewertung verworfen
- **VDE-Abschluss**: Protokolle können trotz Mängeln abgeschlossen werden; Ergebnis wird automatisch als `Bestanden`, `Nicht Bestanden` oder `Mängel` gespeichert

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
