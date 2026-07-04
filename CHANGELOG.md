# Changelog

Alle nennenswerten Änderungen an MessPilot werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und das Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [Unreleased]

---

## [0.6.0-beta.5] - 2026-07-04

### Added
- **System > QR-Code**: Neuer QR-Code-Bereich fuer Systemlinks mit Vorschau, Vergroesserung, SVG-Download und optionalem Logo in der Mitte.
- **Brand-Assets**: Lokale MessPilot-CI-Assets fuer Favicon, Symbol, Icon und Wortmarke in Light-/Dark-Varianten vorbereitet.
- **System > Plugins**: Fluke-App-Kandidat `zach-edf/fluke-app` als spaeter zu pruefende Messgeraete-Anbindung dokumentiert.

### Changed
- **Frontend-Refactor**: `app.js` weiter entlastet; Topbar, Dialog-Schliessen, Navigation/Tab-Wechsel, Kundenaktionen, Settings-Aktionen, Verteileraktionen, Protokollaktionen, Protokollschritte, Messpunktlogik und VDE-Stromkreisaktionen liegen jetzt in eigenen bzw. fachlich passenden Modulen.
- **PDF-Service-Refactor**: Wiederverwendbare PDF-Basisfunktionen, Dokument-/Zeichenhelfer, Geometrie, Messdatenaufbereitung, VDE-Daten und Lighting-/ESD-Layout aus `pdf.service.js` in kleinere Service-Module ausgelagert.
- **Brand-Hintergrund**: GUI- und Login-Wellen nutzen die CI-Farben zentral, sind in Light und Dark kraeftiger sichtbar und bleiben ueber die Systemeinstellungen steuerbar.
- **Logo/CI**: Topbar, Login, QR-Code und lokale Assets nutzen die neue runde Wellenmarke statt des alten Messkurvenzeichens.
- **Asset-Auslieferung**: CSS- und JS-Asset-Versionen wurden erneut erhoeht, damit Browser/Coolify den Beta-Bugfix-Stand sicher neu laden.
- **Technische Dokumentation**: Modulgrenzen, PDF-Service-Aufbau und Refactor-Zwischenstand in `docs/TECHNICAL.md` nachgezogen.

### Fixed
- **Archivierung von Wiederholungspruefungen**: Hauptpruefung und alle zugehoerigen Wiederholungspruefungen werden beim Archivieren und Wiederherstellen als zusammenhaengende Pruefgruppe behandelt.
- **QR-Code-Scanbarkeit**: Logo-Aussparung, Modulrundung und QR-Version wurden so angepasst, dass iPhone-Scanner den Code zuverlaessiger erkennen.
- **Login-Anzeige**: App-Topbar bleibt beim Laden des Anmeldebildschirms ausgeblendet; GitHub-Link und Theme-Schalter sind stabil positioniert.

---

## [0.6.0-beta.4] - 2026-07-04

### Added
- **System > Messgeräte**: Messgeräte können optional einem Prüfer zugeordnet werden; Liste, Details und Bearbeiten-Dialog zeigen die Zuordnung.
- **System > Benutzer**: Benutzerliste ist jetzt nach Name, Benutzer/E-Mail, Rolle, Prüfer und Status sortierbar.
- **Dashboard**: Fällige und abgelaufene Messgeräte-Kalibrierungen werden als eigene Übersicht angezeigt.
- **System > Messgeräte**: Messgeräteliste kann über ein rechtes Exportmenü als CSV oder JSON heruntergeladen werden.
- **Dashboard > Nächste Prüfungen**: Wiederholungsprüfungen können direkt aus dem Dashboard als neues VDE-Protokoll gestartet werden; alte Messwerte werden als schreibgeschützte Vorwerte übernommen und neue Messwerte vorbelegt.

### Changed
- **Topbar-Benutzermenü**: Das Menü wird als eigener Body-Layer gerendert, damit Einstellungen, Abmelden und Light/System/Dark unabhängig von Dashboard- oder Tabellenflächen klickbar bleiben.
- **Untertab-Leisten**: System- und Kunden-Untertabs nutzen schwebende Pills ohne durchgehenden Hintergrundbalken.
- **Asset-Auslieferung**: Stylesheet sowie zentrale App-/Auth-Skripte erhalten eine Asset-Version, damit Browser/Docker nach UI-Fixes nicht am alten Stand hängen bleiben.
- **System > Benutzer**: Rollen-, Prüfer- und Statuszuweisungen werden nicht mehr als Dropdowns direkt in der Liste angezeigt, sondern im Anlegen-/Bearbeiten-Dialog gepflegt.
- **Wiederholungsprüfung**: Norm-Bezug wurde für `DGUV V3`-Wiederholungsprüfungen auf `DIN VDE 0105-100` vereinheitlicht (Setup, Protokollanzeige, PDF-Header/Norm-Checkbox).

### Fixed
- **Topbar-Menü**: Klicks auf Einstellungen, Abmelden und Theme-Auswahl werden nicht mehr von darunterliegenden Listen oder Dashboard-Tabellen abgefangen.
- **Login-Footer**: GitHub-Link auf dem Anmeldebildschirm sitzt wieder bündig unten links zur Versionsanzeige.

---

## [0.6.0-beta.3] - 2026-07-03

### Added
- **Benutzer bearbeiten**: Master und Admins erhalten in der Benutzerliste wieder einen Bearbeiten-Dialog fuer Name, Benutzer/E-Mail, Rolle, Status, Pruefer-Zuordnung und optionales neues Passwort.
- **Admin-Demo-Start**: Login ist fuer den Beta-Test mit `admin / admin` vorbelegt; `master / master` bleibt als geschuetztes Master-Konto enthalten.
- **System > Plugins**: Platzhalterbereich fuer spaetere Messgeraete-Plugins wie Fluke, Megger oder weitere Schnittstellen vorbereitet.

### Changed
- **Rollenmodell**: Rollen auf `master`, `admin`, `user`, `viewer` und `demo` vereinheitlicht; alte Systemadmin-/Gast-Begriffe werden intern migriert.
- **Benutzerrechte**: `admin` darf normale Benutzer verwalten, `master` verwaltet zusaetzlich geschuetzte Admin-/Master-Konten.
- **Protokoll-Menues**: Protokollanlage-Menue schliesst per Klick ausserhalb, blendet bei Inaktivitaet ab und nutzt eine passendere Archiv-Navigation.
- **Systemeinstellungen**: Tab `System` wurde zu `Einstellungen`, Versionen stehen wieder in einem eigenen Tab; PDF-Wasserzeichen, Theme und weitere Schalter sind kompakter angeordnet.

### Fixed
- **Benutzerverwaltung**: Bearbeiten-Button und Dialog fehlen nicht mehr fuer berechtigte Master-/Admin-Sitzungen.
- **Zuordnungsdialoge**: Gepinnte Kontexte und freie Auswahl bleiben konsistenter, damit neue Protokolle nicht durch alte Pin-Zustaende blockiert werden.
- **Topbar-Kontext**: Entpinnen von Kunden/Raeumen synchronisiert die Anzeige in der Topbar sauberer.

---

## [0.6.0-beta.2] - 2026-07-03

### Added
- **System > System**: Versionsbereich zeigt jetzt einen direkten Changelog-Link zum Public Repository.
- **Adminkonsole**: Admins sehen App-Version, Versionsquelle, Commit und Changelog-Link direkt in den technischen Systemdaten.
- **Kundenanlage**: Kundendialog enthaelt jetzt Liegenschafts-Tabs; mindestens eine Liegenschaft ist beim Speichern Pflicht, weitere Liegenschaften koennen ueber `+` direkt im Kunden angelegt werden.

### Changed
- **Systemnavigation**: `Themes` und `Version` wurden in den zentralen Tab `System` zusammengefuehrt; alte lokale Tab-Zustaende werden weiter auf `System` umgeleitet.
- **Systemversionen**: Baustein-/Unterversionen werden als responsive Kacheln statt als breite Tabelle dargestellt.
- **Topbar**: Das separate Zahnrad fuer Einstellungen wurde entfernt, weil der Systemzugang ueber das Benutzermenue erfolgt.
- **Dashboard**: Die Schnellzugriff-Kacheln wurden entfernt; Dashboard fokussiert jetzt auf Statuszahlen, naechste Pruefungen, aktuelle Arbeit und Arbeitsfokus.
- **Kundenbereich**: Der Untertab `Liegenschaften` wurde entfernt; Liegenschaften werden im Kundenstamm als Baum unter dem jeweiligen Kunden und im Kundendialog gepflegt.

---

## [0.6.0-beta.1] - 2026-07-03

### Added
- **Login-Version**: Der Anmeldebildschirm zeigt die aktuelle App-Version dezent am unteren Bildschirmrand; die Versionsinfo wird bereits vor dem Login geladen.
- **Beta-Kennung**: Login-Hintergrund und Topbar-Branding weisen sichtbar, aber dezent auf den Beta-Status hin.
- **ESD-Ableitmessung**: Neue Protokollbasis fuer ESD Punkt-zu-Punkt-Messungen mit Raumbezug, Norm-/Grenzwertschritt, Potentialausgleich-Bauteilen, farbigem Bezug, Messpunktraster, automatischer Bewertung und PDF-Vorbereitung.
- **ESD-Versionierung**: Eigene Bausteinversionen fuer `protocol-esd-point-to-point` und `pdf-esd-template` angelegt.
- **ESD-Dokumentation**: Pruefschritte, Datenregeln, Bewertung und offene fachliche Punkte in `docs/ESD_PROTOCOL.md` dokumentiert.

### Changed
- **Theme-System**: Darstellung auf ein zentrales `Light / System / Dark`-Modell reduziert; alte Theme-Presets und Demo-Presets entfernt.
- **UI-Farben**: Light- und Dark-Theme auf eine ruhigere, Apple-naehere Farbpalette umgestellt; primaere GUI-Aktionen verwenden kein Gruen mehr, sondern den blauen Systemakzent.
- **Login-Screen**: Header im Anmeldezustand ausgeblendet, Hintergrund fuellt den kompletten Viewport, Loginfenster kompakter gestaltet und Logo in den Login-Kopf verschoben.
- **Login-Hintergrund**: Interaktive Code-Partikel durch einen ruhigen Oszilloskop-/Messkurven-Hintergrund ersetzt; grosser dezenter `MessPilot`-Schriftzug liegt oberhalb des Loginfensters.
- **Formularfelder**: Browseruebergreifende Feldradien zentralisiert, damit Chrome und Safari naeher beieinander liegen.
- **ESD-Messschritt**: Raumdaten, Raster, erfasste Messpunkte und Stepper aus der ASR-Messung uebernommen.
- **ESD-Bezug**: Messwerte werden jetzt direkt in den Bauteil-/Potentialausgleich-Karten angezeigt; die separate Bezug-Spalte der Messpunktliste entfaellt.
- **PDF-Branding**: Alle PDF-Seiten erhalten ein dezentes MessPilot-Wellen-Wasserzeichen als Vektor-Overlay.

### Fixed
- **ESD-Messwerte**: Bewertung und Fortschritt verlangen jetzt genau einen Messwert je Messpunkt statt mindestens einen Wert je Bezug.
- **ESD-Bauteile**: Farbauswahl, Default-Farbe, Drag-Position und Loeschen von Potentialausgleich-Bauteilen stabilisiert.
- **Protokoll-Loeschen**: Loeschdialog erwartet bei technischen lokalen IDs nicht mehr die lange `local-...` Kennung, sondern einen kurzen Bestaetigungstext.

---

## [0.5.4] - 2026-07-03

### Fixed
- **Protokollabschluss**: Klick auf den Haken am Ende des VDE-/Protokollablaufs speichert und springt danach wieder in die aktive Protokollliste.

---

## [0.5.3] - 2026-07-03

### Fixed
- **VDE-Protokollspeicherung**: Server-Speicherung ist im Protokollablauf jetzt verbindlich; API-Fehler werden sichtbar im Protokollhinweis angezeigt statt still auf lokalen Browser-Speicher auszuweichen.
- **VDE-Zwischenschritte**: Schrittwechsel, Zurueck/Weiter, Abschluss, Listenwechsel und Editor-Schliessen brechen bei fehlgeschlagenem Server-Save ab, damit keine Messwerte unbemerkt verloren gehen.
- **Messprotokoll-API**: Speichern nutzt den gemeinsamen API-Wrapper mit HTTP-Statuspruefung und sauberer Fehlermeldung.

---

## [0.5.2] - 2026-07-02

### Added
- **Online-Beispieldaten**: Frische Stores enthalten jetzt ein bestandenes DIN-VDE-0100-600-Demoprotokoll und ein bestandenes ASR-Beleuchtungsprotokoll inklusive Messwerten fuer Listen-, Bearbeiten- und PDF-Tests.

---

## [0.5.1] - 2026-07-02

### Fixed
- **VDE-Online-Speichern**: API-Payload-Limit auf `5mb` angehoben, damit groessere VDE-Protokolle mit Stromkreis- und Messwertmatrix serverseitig gespeichert werden.
- **Protokollnavigation**: Interne Routenbuttons speichern den aktiven Protokollentwurf jetzt vor dem Wechsel der Ansicht.

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
