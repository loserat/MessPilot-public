# Changelog

Alle nennenswerten Änderungen an MessPilot werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und das Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [Unreleased]

---

## [0.7.1] - 2026-07-11

### Added
- **Tagesdokumentation für SQL-/PDF-Nachzug**: Der Arbeitsstand vom 2026-07-11 ist jetzt als eigener Tagesbericht dokumentiert, inklusive SQL-Fortschritt, Impressum-/UI-Nachzug, VDE-Zweitkabel-Themen und PDF-/Skizzenkorrekturen.
- **SQL-Admin-Nutzung geschärft**: `System > SQL-Datenbank` wurde als aktiver Betriebs- und Resetpunkt für den PostgreSQL-Teststand weiter verfestigt.

### Changed
- **App-Version auf 0.7.1 angehoben**: `package.json`, `package-lock.json` und die sichtbaren Versionsbausteine wurden auf den neuen Patchstand für den laufenden SQL-/Export-Stabilisierungszyklus gesetzt.
- **SQL-Only-Hauptpfad weiter durchgezogen**: Sichtbare Listen und zentrale CRUD-Pfade für Fachdaten orientieren sich noch konsequenter am PostgreSQL-Stand statt an gemischten JSON-/Legacy-Zwischenständen.
- **Verbrauchsdiagramm Baustrom logisch nachgeschärft**: GUI und PDF bewerten den Verbrauchsverlauf jetzt gegen einen gleitenden Mittelwert der letzten bis zu drei Vorgängerwerte statt nur gegen den direkten Vorwert.
- **PDF-Skizzenprojektion vereinheitlicht**: Die Punktprojektion für Beleuchtungs- und ESD-Skizzen orientiert sich jetzt enger an der quadratischen GUI-Darstellung.
- **VDE-Mehrkabelworkflow nachgezogen**: Zweitkabel, Mehrzeilen-Messmatrix, Bezeichnerlogik (`W1`/`W2`) und mehrkabelige PDF-Ausgaben wurden weiter an den fachlichen Stromkreisworkflow angepasst.
- **DIN-A3-/DGUV-Header verdichtet**: Die großen PDF-Kopfbereiche wurden schrittweise komprimiert, Logo- und Metaflächen ruhiger verteilt und doppelte Auftraggeber-/Auftragnehmer-Darstellungen reduziert.

### Fixed
- **Fehlende Messpunkte im PDF-Export**: Beleuchtungs-Messpunkte fallen im PDF nicht mehr aus, wenn einzelne `pointXPosition`-Felder fehlten oder nur der aktive Punkt im Formular gespeichert wurde.
- **Impressum-Dialog nach Login**: Das globale Impressum wurde als echter zentrierter Vordergrund-Dialog vom generischen Modalverhalten entkoppelt.
- **Baustrom-PDF-Verbrauchsseite**: Die Verlaufsauswertung zeigt Referenzlinie, geglättete Skala und verständlichere Zusammenfassung statt nur roher Vorwertdifferenzen.
- **Protokoll-Archivierung**: Beim Archivieren werden nicht mehr fälschlich ganze VDE-/Wiederholungsgruppen derselben fachlichen Zuordnung mitgezogen.
- **Prüfer- und Messgerätepfade auf SQL**: Anlegen, Bearbeiten, Löschen und Quellenanzeige wurden für den laufenden PostgreSQL-Betrieb robuster gemacht.
- **VDE-Messmatrix-Trennlinien**: Unscharfe bzw. dicke senkrechte Gruppentrenner in der breiten GUI-Matrix wurden optisch bereinigt.

---

## [0.7.0] - 2026-07-10

### Added
- **Coolify-Postgres-Rollout dokumentiert**: Die Deployment- und Datenbankdokumentation beschreibt jetzt den sauberen Weg ueber eine eigene interne PostgreSQL-Ressource (`messpilot`), das Setzen von `DATABASE_URL` in der App und die anschliessenden Prisma-Testschritte.
- **SQL-Betriebsstatus dokumentiert**: Die technische Dokumentation beschreibt jetzt den aktiven PostgreSQL-/Prisma-Betrieb, Legacy-IDs fuer Frontend-Kompatibilitaet und den bereinigten SQL-Status in System- und Adminansichten.
- **SQL-Datenbank leeren im Adminbereich**: Unter `System > SQL-Datenbank` gibt es jetzt eine geschuetzte Admin-Funktion, die die fachlichen SQL-Nutzdaten gezielt leert, ohne Benutzerzugang, Sessions und Systemanker zu entfernen.

### Changed
- **SQL-Only Backendpfad hergestellt**: Repository-Layer, Healthcheck, PDF-Exportpfade und sichtbare Quell-Badges laufen jetzt ohne stillen JSON-Fallback auf dem PostgreSQL-/Prisma-Stand.
- **Protokoll-GUI auf SQL-Sicht umgestellt**: Die Messprotokoll-Liste im Frontend mischt keine lokalen Browser-Protokolle mehr mit API-Daten. Sichtbar bleiben nur noch die vom Backend gelieferten Datensaetze.
- **Relation-ID-Mapping vereinheitlicht**: SQL-Records geben in den zentralen `toRecord`-Mappings wieder fachliche IDs aus dem Payload zurueck statt interner SQL-UUIDs. Das betrifft Benutzer-/Kundenketten, Gebaeude-/Raumketten sowie Protokoll-, Mangel- und Dokumentrelationen.
- **CRUD-Aufloesung fuer Legacy-IDs vereinheitlicht**: `Gebaeude`, `Raeume`, `Verteiler` und `Protokolle` loesen `find/update/remove` robuster ueber direkte SQL-ID, Legacy-ID und fachliche Inhaltsbezuge auf.
- **Adminkonsole-Statuslogik nachgezogen**: `System > Adminkonsole` und `System > SQL-Datenbank` zeigen jetzt den aktiven PostgreSQL-Status ohne JSON-Mischbild konsistenter an.
- **Protokollanlage fuer SQL harmonisiert**: `Pruefschritte starten` und die Wiederholungspruefungs-Pfade legen neue VDE-Protokolle jetzt frueher an den echten Server-/SQL-Pfad an, statt zuerst nur auf fluechtigen Browser-Drafts zu laufen.
- **Legacy-DemoStore entschärft**: Die alte Demo-/JSON-Fixture erzeugt im PostgreSQL-Modus keine Dateien und keine Speicherseiteneffekte mehr.

### Fixed
- **VDE-Protokollworkflow**: Nach dem Anlegen eines VDE-Protokolls fuehrt `Pruefschritte starten` wieder in den eigentlichen Editor statt im Grunddatenmodus zu blockieren; redundante Footer-Navigation im Schrittbereich wurde entfernt.
- **Protokollquellen in der Liste sichtbar**: Protokolle markieren jetzt direkt in der Liste ihre Datenquelle; sichtbare Default-Badges fallen nicht mehr ungewollt auf `JSON` zurueck.
- **Protokoll-Loeschen im SQL-Hybridmodus**: Vor dem Entfernen eines Protokolls werden verknuepfte Messwerte geloescht und Mangel-/Dokumentrelationen entkoppelt; zusaetzlich wird das Zielprotokoll bei ID-Drift ueber Spiegel- und Inhaltsdaten aufgeloest.
- **Protokoll-Anlage mit lokalen Draft-IDs**: Temporaere Frontend-IDs wie `tmp-*` oder `local-*` werden beim SQL-Create nicht mehr als echte `legacyId` gespeichert.
- **Kettenbruch bei Raum/Gebaeude/Verteiler**: Fachliche Relationen wie `customerId`, `locationId`, `buildingId`, `roomId`, `distributionId` und `protocolId` bleiben fuer das Frontend stabil, obwohl SQL intern UUIDs verwendet.
- **Auth-Sessions auf SQL vorbereitet**: Das Prisma-Schema und der Auth-Service unterstuetzen jetzt SQL-Sessions als laufzeitfaehigen Pfad fuer den aktiven PostgreSQL-Betrieb.
- **Wiederholungspruefungen als SQL-Protokolle**: Aus einem bestehenden VDE-Protokoll gestartete Wiederholungspruefungen bleiben nicht mehr auf einem lokalen Draft haengen, sondern werden ueber den Serverpfad als echte SQL-Protokolle angelegt.
- **Wiederholungspruefungen in der Liste sichtbar**: Neu angelegte Wiederholungspruefungen tauchen nach dem Speichern wieder konsistent in der Protokollansicht auf.
- **Verteilerwahl in der Protokollanlage**: Die Verteilerliste im Protokoll-Wizard filtert SQL-Verteiler wieder robuster ueber Kunde, Gebaeude und Raum, auch wenn nicht jede Hilfsrelation direkt am Datensatz mitgeschrieben ist.
- **Doppelte Schrittleiste im VDE-Editor**: Die Pruefschrittnavigation wird im VDE-Workspace nicht mehr doppelt gerendert.
- **Adminkonsole-Healthcheck**: Fehlende optionale Zaehlpfade werfen die gesamte Systemansicht nicht mehr auf `Backend nicht verfügbar`.

---

## [0.6.0-beta.8] - 2026-07-04

### Added
- **Versionsbausteine erweitert**: Neue Bausteine `protocol-repeat-workflow`, `pdf-export-engine`, `role-access-control`, `measurement-device-management`, `dashboard-analytics`, `system-qr-system` und `admin-console` in `src/config/versioning.js` aufgenommen.
- **Version-Tooling in der UI**: Für die neuen Bausteine wurden passende Beschreibungen und Changelog-Texte in `public/js/app.settings.js` ergänzt, damit `Einstellungen > Version` die neue Funktionstiefe vollständig zeigt.
- **Wiederholungsprüfung und Workflow-Ziele**: Der Wiederholungs-Workflow ist in den Bausteinen als eigener Bestandteil dokumentiert, inkl. Live-Vorwertlogik und Wiederholungs-Kettenverhalten.
- **App-Beta auf 0.6.0-beta.8**: Globale Versionsnummer auf `0.6.0-beta.8` angehoben, damit das neue Modullevel im UI konsistent sichtbar ist.

### Changed
- **Bausteinstände neu bewertet**: `ui-shell`, `backend-api`, `protocol-core`, `protocol-lighting`, `protocol-esd-point-to-point`, `vde-circuit-model`, `pdf-lighting-template`, `pdf-esd-template`, `role-access-control`, `measurement-device-management`, `system-qr-system`, `admin-console` und `pdf-export-engine` auf den aktuellen Beta-Stand gebracht.
- **Dokumentationslinien vereinfacht**: Tägliche Dokumentation und zentrale Versionsseite wurden für den neuen Beta-Wert aktualisiert (README, `docs/VERSIONING.md`, `docs/daily/2026-07-04.md`, CHANGELOG-Header).
- **Komponenten-Transparenz erhöht**: In den Bausteinbeschreibungen werden jetzt explizit mehr App-Funktionen benannt (Dashboard, Mesgeräte, Rollen- und QR-Flüsse, Adminkonsole).

### Fixed
- **Versionskonsistenz**: `package.json` und `package-lock.json` auf denselben App-Tag gebracht.
- **Release-Nachvollziehbarkeit**: Neue Beta-Komponenten sind in der Komponentenliste ersichtlich und haben dedizierte Changelog-Texte für spätere Rückverfolgung.
- **Kommunikationskette**: Täglicher Fortschritt inkl. App-Beta-Wechsel jetzt sauber dokumentiert, um spätere Release-Übergabe zu erleichtern.

---

## [0.6.0-beta.7] - 2026-07-04

### Added
- **Firmaeinstellungen API**: Eigener Backend-Pfad fuer `companySettings`, damit Firmenstammdaten und Logos nicht nur lokal im Browser liegen.
- **System > Icons**: Eigener Icon- und Asset-Bereich fuer Brandmarks, animierte Logos, Loader, UI-Iconset, Sprite und iOS-App-Icons.
- **iOS-App-Icons**: Master-SVG, PNG-Groessen und Xcode-kompatibles `AppIcon.appiconset` fuer eine spaetere iOS-App vorbereitet.
- **Animierte Brand-Assets**: Logo-, Symbol-, Favicon- und Loader-Varianten im MessPilot-CI ergaenzt.
- **Globale Ladeanimationen**: Zentrale MessPilot-Ladeanimation fuer GUI-Ladevorgaenge, App-Start, PDF-Vorschau und Abmelden vorbereitet.
- **UI-Iconset**: Konsistentes MessPilot-SVG-Iconset fuer Navigation, Aktionen, System/Admin und Statusbeispiele vorbereitet.

### Changed
- **App-Version**: Beta-Version auf `0.6.0-beta.7` angehoben, weil der GUI-/CI-Designstand deutlich fortgeschritten ist.
- **Systemeinstellungen**: Mehrere Auswahlfelder wurden auf kompakte Schalter-/Segmentlogik umgestellt und visuell an den vorhandenen Theme-Switch angeglichen.
- **Bildablage fuer PDF**: Firmenlogo- und Unterschrifts-Uploads werden auf einen PDF-tauglicheren Pfad vorbereitet, statt nur als GUI-Vorschau behandelt zu werden.
- **System > Icons Performance**: Asset-Gruppen werden jetzt ueber Untertabs geladen, damit animierte SVGs und viele PNGs nicht alle gleichzeitig im DOM liegen.
- **Login-Branding**: Anmeldebereich zeigt nur noch eine zentrale Logo-/Animationsvariante statt doppelter Wellenanimation.
- **Theme-Umschaltung**: Light-/Dark-/System-Wechsel dimmt ueber langsamere UI-Transitions ohne Blitz-Overlay.
- **CI-Farben und Logos**: Light-/Dark-Logos, BETA-Platzierung, Icon-Zentrierung, Loader und App-Icon-Stil weiter an das MessPilot-CI angepasst.
- **System > Icons statt Version**: Brand-Asset-Uebersicht aus dem Versionsbereich in einen eigenen Icon-Bereich ueberfuehrt.

### Fixed
- **PDF-Export / Firmenlogo**: Hinterlegte Firmenlogos werden im PDF-Export wieder in den vorgesehenen Feldern verarbeitet; bestehende JPEG- und PNG-Daten werden akzeptiert.
- **PDF-Export / Prüfer-Unterschrift**: Hinterlegte Unterschriften aus den Prüferdaten werden im PDF-Export wieder im Unterschriftsbereich verarbeitet.
- **Wiederholungsprüfung Folgekette**: `Wiederholungsprüfung 2` zieht Vorwerte nicht mehr nur aus einem alten Snapshot, sondern löst den aktuellen Stand von `Wiederholungsprüfung 1` live auf.
- **Wiederholungsprüfung bei offenem Bearbeitungsstand**: Wird eine neue Wiederholungsprüfung aus einem gerade bearbeiteten Vorgänger gestartet, wird auch der aktuelle Arbeitsstand als Quelle berücksichtigt.
- **Zentrierter GUI-Loader**: Globale Ladeanimation sitzt nicht mehr oben im Layout, sondern fixed in der Bildschirmmitte.
- **Abmelden-Feedback**: Logout zeigt eine sofortige mittige MessPilot-Ladeanimation.
- **Theme-Dimmen**: Aufhellendes Fade-Cover entfernt, weil es beim Umschalten wie ein Blitz wirken konnte.

---

## [0.6.0-beta.6] - 2026-07-04

### Added
- **Topbar**: Einstellungen-Icon im Topbar wieder integriert, ergänzt um ein separates Benutzermenü mit Account-, Passwort- und Abmelden-Aktionen.
- **Passwortzugriff**: `master` und `admin` können im Topbar-Menu direkt zur Benutzerkonto-Ansicht wechseln.

### Changed
- **Topbar-Menüarchitektur**: Benutzer- und Einstellungen-Handling zentral auf neue Handler in `app.topbar.js` und robuste UI-Struktur in `app.auth.js` überführt; Klickpfade klar getrennt.

### Fixed
- **Topbar-Klickbarkeit**: Menü überdeckt Klickflächen nicht mehr, Theme-Wechsel und Navigation aus dem Topbar funktionieren konsistent.
- **Account-Edit-Berechtigung**: `admin`/`master` können sich in `topbar > Benutzerkonto` konsistent selbst bearbeiten (`auth.service.js`).

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
