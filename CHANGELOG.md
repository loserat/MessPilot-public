# Changelog

Alle nennenswerten Änderungen an MessPilot werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und das Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [Unreleased]

Noch keine dokumentierten Änderungen.

## [0.7.7] - 2026-07-17

### Added
- **Website-Admin-Besuche SQL-persistent vorbereitet**: Website- und Loginseiten-Zugriffe koennen jetzt ueber `WebsiteVisit` in PostgreSQL gespeichert werden. Erfasst werden Zeitpunkt, Pfad, Methode, IP, Browser, Betriebssystem, Referrer und kompakter User-Agent.
- **Website-Einstellungen SQL-persistent vorbereitet**: Einstellungen der Website-Admin-GUI koennen jetzt ueber `WebsiteSetting` in PostgreSQL gespeichert werden. Die bestehende JSON-Datei bleibt als lokaler Fallback erhalten.
- **Login-Auswertung im Website-Admin erweitert**: App-Loginereignisse aus dem Audit-Log liefern fuer die Website-Admin-GUI jetzt neben IP auch Browser und Betriebssystem, sofern diese Informationen im Login-Payload vorhanden sind.
- **SEO-Vorbereitung dokumentiert**: Die Website ist auf minimale, rechtlich neutrale SEO-Optimierung ausgelegt: klare Seitentitel, Meta-Beschreibungen, strukturierte Daten, Website-Check und fachlich neutrale Begriffe statt Keyword-Ueberladung.
- **Verteiler v2 als separater Konzepteditor vorbereitet**: Unter `Kunden > Verteiler` gibt es den neuen Untertab `Verteiler v2`. Der Editor liegt in `public/js/app.distributors-v2.js` und bleibt bewusst getrennt vom bestehenden Verteilereditor.
- **Read-only Flow-Adapter fuer Verteilerlayouts**: Bestehende `layout.rows` werden in ein internes Flow-Modell mit Nodes, Kanten, Viewport, Quellversion und Template-Referenz uebersetzt. Unklare Abgaenge werden als `Abgang unklar` markiert, ohne CEE-/Schuko-/Klemmenabgaenge zu raten.
- **Node-RED-artiger Canvas-Prototyp fuer Verteiler v2**: Der V2-Editor besitzt Baustein-Palette, freien Canvas mit Raster, Pan, Zoom, Mini-Map, Eigenschaftenpanel und Baum-Synchronisierung. Nodes koennen lokal verschoben und per Palette als Entwurf erzeugt werden.
- **Lokale Entwurfsverbindungen im Canvas**: OUT-Ports koennen lokal per Drag auf IN-Ports verbunden werden. Vorschaukanten, Zielhervorhebung und UI-Schutzregeln verhindern Selbstanschluss, Duplikate, Gegenrichtung, Zyklen und Power-PE-Mischverbindungen.
- **Dauerhafte Flow-v2-Speicherung vorbereitet**: Der Verteiler-v2-Editor kann Positionen, Entwurfsnodes, Entwurfskanten, Source-/Draft-Kanten und Canvas-Viewport jetzt manuell als `payload.flowV2` im bestehenden Verteiler-Datensatz speichern.
- **Mehrfachauswahl im Verteiler-v2-Canvas**: Nodes koennen per Mausrahmen oder mit `Shift`/`Cmd`/`Strg` mehrfach markiert und gemeinsam verschoben werden.

### Fixed
- **Website-Admin-Daten ueberstehen Redeploy besser**: Neue Besucher- und Website-Einstellungsdaten sind nicht mehr nur an den Node-Prozess gebunden, sobald die neuen Prisma-Tabellen per `db:push` in der Datenbank vorhanden sind.
- **App-Login-Aufrufe werden im Website-Tracking beruecksichtigt**: Neben Website-Seiten werden auch `/login` und `/app` als relevante Zugriffspfade fuer Besucherstatistiken erfasst.
- **Footer-Dialoge mit X-Button**: Impressum, Datenschutz und AGB nutzen auf der Website jetzt einen kompakten X-Button statt eines Textlinks zum Schließen.
- **Verteiler-v2-Portdarstellung korrigiert**: IN-/OUT-Anschluesse werden im Canvas jetzt als runde Portpunkte direkt am Node-Rand dargestellt statt als pillenfoermige Labels.
- **Verteiler-v2-Kantenfuehrung verbessert**: Power- und PE-Verbindungen werden defensiver orthogonal geroutet, damit Linien beim Verschieben der Nodes nicht mehr durch Karteninhalte laufen.
- **Website-Topbar seitenübergreifend vereinheitlicht**: Die zentrale Website-CSS setzt Radius, Flächen, Buttonzustände und Box-Sizing für die Topbar jetzt unabhängig von seitenlokalen Variablen. Dadurch verändert sich die Navigation beim Wechsel auf den Blog nicht mehr sichtbar.
- **Statistik-Topbar korrekt lizenzierbar**: `Statistiken` verschwindet jetzt direkt aus der Topbar, wenn die Premiumfunktion `premiumStatisticsEnabled` deaktiviert wird.
- **Statistik-Untertab entfernt**: Die Statistikseite zeigt keinen generischen Untertab `Übersicht` mehr, weil sie als eigene Topbar-Seite funktioniert.
- **Direktzugriff auf deaktivierte Premiumroute abgesichert**: Ein direkter Hash-Aufruf von `#statistiken` wird bei deaktivierter Statistik-Premiumfunktion wieder auf eine erlaubte Route zurückgeführt.
- **Alter Verteilereditor bleibt von Flow-v2 getrennt**: Speicherpfade des bestehenden Verteilereditors erhalten `flowV2`, ohne `payload.layout` oder `layout.rows` zu überschreiben.

### Changed
- **Version auf 0.7.7 angehoben**: `package.json`, `package-lock.json`, README, Changelog, Website-Blog und Tagesdokumentation bilden den neuen Beta-Zwischenstand ab.
- **Docker-/SQL-Hinweise fuer Website-Admin geschaerft**: Fuer produktive Website-Admin-Statistiken muessen nach Deployment und Schema-Aenderungen `npm run db:generate` und `npm run db:push` ausgefuehrt werden.
- **Verteiler-v2-Canvas lesbarer gemacht**: Standard-Zoom liegt bei `90%`, `Alles einpassen` richtet den Canvas auf alle sichtbaren Nodes aus, Palette und Baumansicht sind einklappbar, Ports wurden auf `IN`/`OUT` plus separaten PE-Port reduziert und Kanten laufen orthogonal mit kleinen Rundungen.
- **Verteiler-v2-Arbeitsbereich vergroessert**: Der freie Canvas bietet jetzt mehr Platz fuer groessere Verteileraufbauten und zeigt bei Mehrfachauswahl eine eigene Inspector-Zusammenfassung.
- **Fachliche Darstellung im Verteiler-v2-Prototyp geschaerft**: Normale `circuit`-Zeilen erzeugen nicht mehr automatisch Klemmen. Ohne expliziten `outputType` erscheint `Abgang unklar · <Stromkreis>`. PE bleibt als gruen gestrichelter separater Konzeptpfad und wird nicht ueber RCD oder LS gefuehrt.
- **Verteiler-v2-Speicherstatus ergänzt**: Der Editor zeigt `Gespeichert`, `Ungespeicherte Änderungen` oder `Speichern fehlgeschlagen`, warnt vor dem Verlassen bei ungespeicherten Änderungen und bietet `Änderungen verwerfen` sowie `Flow zurücksetzen`.
- **Flow-v2-Fallback abgesichert**: Gespeicherte Flow-v2-Daten werden beim Öffnen bevorzugt geladen; fehlen sie oder sind sie ungültig, wird die Ansicht weiterhin sicher aus `layout.rows` erzeugt.
- **Website-Design stärker an Blog-Optik angeglichen**: Die zentrale Website-CSS übernimmt die ruhigere Blog-Palette, weichere Schatten, dezente Kartenflächen, einheitlichere Pills und einen harmonisierten Footer für Home, Blog, Preise, FAQ und vorbereitete Zusatzseiten.
- **Blog-Changelog ausführlicher aufgebaut**: Der öffentliche Blog zeigt den `0.7.x`-Stand jetzt nicht mehr als kompakte Kurzfassung, sondern nach Unterversionen von `0.7.6` bis `0.7.0` mit konkreten Änderungen und Bugfixes.
- **Normbezüge auf der Website neutraler formuliert**: Website-Texte vermeiden produktähnliche Aussagen wie VDE-zertifiziert oder VDE-autorisiert. DIN-VDE-Normbezug wird nur als fachlicher Bezug innerhalb der Prüfdokumentation beschrieben.
- **Preisseite bis zum Final Release entschärft**: Preise bleiben unkenntlich, Zusatzleistungen zeigen keinen verkaufsbetonten Preisblock, und der Betriebshinweis stellt Self-Hosting als bevorzugte, datensouveräne Variante dar.
- **FAQ um Betriebs- und Normhinweise ergänzt**: Die FAQ beschreibt Self-Hosting, optionales späteres Hosting und die rechtlich neutrale Einordnung von Normbezügen klarer.
- **Home-Seite der Website final reduziert**: Die Startseite wurde auf maximal fünf klare Bereiche zurückgebaut: Hero, drei Kernbereiche, einfacher Prüfablauf, Zielgruppe und Abschluss. Dadurch wirkt die Website weniger wie eine überladene SaaS-Landingpage und stärker wie eine ruhige Produktvorstellung.
- **Website-Home semantisch geschärft**: Texte, Buttons, Überschriftenhierarchie und Demo-/Roadmap-Verweise wurden für bessere Lesbarkeit, Barrierefreiheit und mobile Nutzung neu strukturiert.
- **Public-README aktualisiert**: Das README beschreibt jetzt Version `0.7.6`, Website-/App-Routen, SQL-Hauptpfad, BSV-Vorbereitung, Statistik-/Premiumbereiche und den aktuellen Beta-Stand.
- **Website optisch ruhiger ans CI gezogen**: Alle Website-Seiten erhalten einen gemeinsamen, gedämpften MessPilot-Farb-Layer mit Blau-, Grün- und Goldakzenten, hochwertigeren Kartenflächen und weniger harten Abschnittskanten.
- **Website-Hintergrund an App-Wellen angeglichen**: Die Website nutzt jetzt eine feste SVG-Wellenebene mit durchgehenden roten, goldenen und blauen Linien wie in der App-Optik. Bei reduzierter Bewegung wird die Animation deaktiviert.
- **Home-Hero reduziert**: Der experimentelle Protokoll-Preview-Slider wurde wieder entfernt. Die Startseite nutzt wieder einen ruhigeren, einspaltigen Hero ohne rechten Beispielblock.
- **Browser-Titel der Website gekürzt**: Die Titel in den Browser-Tabs wurden auf kurze Namen wie `MessPilot`, `MessPilot Blog` und `MessPilot Roadmap` reduziert.
- **Demo-Link hervorgehoben**: Der Website-Topbar-Link heißt jetzt `Demo-Login` und pulsiert langsam grün.
- **Footer reduziert**: Der separate Link `Kontakt` wurde aus dem Website-Footer entfernt, weil die Kontaktdaten bereits im Impressum stehen.
- **GitHub-Footerlink direkt geöffnet**: Der GitHub-Eintrag im Website-Footer öffnet jetzt direkt das Public Repository in einem neuen Tab statt ein Info-Popup.
- **Website-Navigation reduziert**: Der Menüpunkt `Funktionen` wurde aus der Website-Topbar entfernt, bis die Funktionsseite neu sauber konzipiert ist.
- **Funktionsseite komplett neu aufgebaut**: Die Seite `Funktionen` wurde als cleanere Produktseite mit Hero, ruhigen Scroll-Abschnitten, Datenfluss, Prüfablauf, Wiederholungsprüfung, Export-Erklärung und echten Demo-PDFs aus `public/demo/pdf` neu strukturiert.
- **Landingpage inhaltlich geschärft**: Die Startseite beschreibt MessPilot jetzt klarer als Prüfsoftware für strukturierte Elektroprüfungen, Wiederholungsprüfungen, PDF-Ausgabe und vorbereitete BSV-Produktdatenbank, ohne zusätzliche Inhaltsbuttons oder überladene Marketingblöcke.
- **Website mobil beruhigt**: Die Website-Topbar scrollt auf kleinen Displays mit und nimmt nicht mehr dauerhaft Platz weg. Der überladene Detail-Testblock auf der Funktionsseite wurde entfernt, damit die Seite auf Mobile, Tablet und Laptop klarer wirkt.
- **Landingpage auf Root-Pfad gelegt**: `messpilot.de/` zeigt jetzt die Website/Landingpage statt direkt die App. Die MessPilot-App ist ueber `/login` und `/app` erreichbar; alte `/preview`-Routen bleiben als Kompatibilitaet erhalten.
- **Settings-Dateien entlastet**: Der BSV-/Baustromverteiler-Renderer wurde aus `app.settings.js` in `app.settings-temporary-power.js` ausgelagert. Das verbessert Nachverfolgbarkeit, reduziert die Größe der zentralen Settings-Datei und bereitet weitere modulare Refactorings vor.
- **Statistik-Renderer ausgelagert**: Der Premium-Statistikbereich wurde aus `app.settings.js` in `app.settings-statistics.js` verschoben. Damit sind BSV und Statistik als eigenständige Settings-Module getrennt und die zentrale Settings-Datei weiter entlastet.
- **Log-Renderer ausgelagert**: Der System-Logs-/Audit-Trail-Bereich wurde aus `app.settings.js` in `app.settings-logs.js` verschoben. Dadurch sind Logliste, Detaildialog, PDF-Payload und Log-Löschdialog als eigenes Modul nachvollziehbar.
- **Version-Renderer ausgelagert**: Der System-Versionstab wurde aus `app.settings.js` in `app.settings-version.js` verschoben. Die große Versionsansicht mit Bausteinen und Detaildialog ist damit ebenfalls ein eigenständiges Settings-Modul.
- **Audit-Direktsprung ausgelagert**: Der Sprung aus `System > Logs` zum betroffenen Protokollfeld wurde aus `app.js` in `app.audit-jump.js` verschoben. Damit wird der App-Orchestrator kleiner, ohne Protokollfachlogik anzufassen.
- **Bild-/JPEG-Helfer ausgelagert**: Datei- und Bildkonvertierungslogik wurde aus `app.js` in `app.image-utils.js` verschoben. Logo-, Zertifikat- und Signatur-Uploads nutzen damit ein eigenes Frontend-Modul.
- **QR-Formular-Helfer ausgelagert**: Das Sammeln und Speichern der QR-Formulareinstellungen wurde aus `app.js` in `app.qr-form.js` verschoben und liegt damit näher am QR-Modul.
- **Navigation-Helfer ausgelagert**: Reine Tab-/String-Helfer wie `tabId`, `moduleTabId` und `moduleTabLabel` wurden aus `app.js` in `app.navigation-utils.js` verschoben und stehen frueher in der Script-Reihenfolge bereit.

## [0.7.6] - 2026-07-13

### Changed
- **Interner Updatepfad zurückgestellt**: `System > Version` zeigt weiter Versionsstand, GitHub-Status und Changelog, blendet aber den experimentellen `Update ausführen`-Button sowie die GitHub-/Coolify-Debugkonfiguration aus. Deployments laufen vorerst über Push auf `main` und Coolify-Autodeploy.
- **Baustromverteiler-Premiumbereich vorbereitet**: `System > Baustromverteiler` ist als lila Premium-/Lizenzbereich für Admin/Systemadmin vorbereitet und nutzt jetzt eine SQL-basierte MERZ-Vorlagenstruktur mit Produktschlüssel, Baumknoten, Steckvorrichtungen, Schutzorganen und Zusatzkennzeichen.
- **BSV-Vorlagenansicht erweitert**: Die Baustromverteiler-Ansicht zeigt mehr MERZ-Startvorlagen, eine kompaktere Baumstruktur und einen klar lila markierten Premium-Tab `BSV`; der Kopfchip `Premium vorbereitet` wurde entfernt.
- **BSV-Liste auf Tabellenstruktur umgebaut**: `System > BSV` nutzt jetzt eine echte Listen-/Tabellenansicht mit eingeblendeter Baumstruktur direkt unter dem ausgewählten MERZ-Datensatz; der Hauptordner im Baum heißt einheitlich `Merz Verteilerschränke`.
- **BSV als Produktdatenbank verfeinert**: Die BSV-Seite nutzt nun ein Master-Detail-Layout mit linker MERZ-Produktauswahl, rechter Produktkarte, technischen Kennzahlen und kompakter Baumstruktur für die spätere Protokollübernahme.
- **BSV-Produktdatenbank auf Explorer-Baum umgestellt**: Die BSV-Ansicht zeigt Hersteller, Produktfamilien, Produkttypen und Produktschlüssel jetzt als eingeklappte Explorer-Struktur. MERZ und WALTHER-WERKE sind vorbereitet; Detaildaten öffnen erst nach Klick auf einen konkreten Baustromverteiler.
- **BSV-Details an Verteiler-Stromkreise angenähert**: Die Detailansicht zeigt vorbereitete Abgänge jetzt stromkreisnah als Baum mit Root, Schutzgruppe und fortlaufenden `W`-Stromkreisen, inklusive Bezeichnung, Schutz, Phasen und Leitung. Das bereitet die spätere Übernahme in `Kunden > Verteiler` und Protokoll-Stromkreismessungen vor.
- **Unvollständige BSV-Vorlagen ausgeblendet**: Die sichtbare Produktliste zeigt vorerst nur Vorlagen mit belastbarer technischer Struktur, damit keine halbfertigen Daten als übernahmefähig wirken. Weitere Typen bleiben für spätere Nachpflege vorbereitet.
- **MERZ-Tabellendatenbestand eingebunden**: Der vorbereitete MERZ-Katalogauszug mit 233 Typenschlüsseln wurde als separate Datenquelle unter `src/data` eingebunden und wird serverseitig in BSV-Seeds mit Bestellnummer, Baureihe, Nennstrom, kVA, Steckdosen, Zähler-/Wandlerkennzeichen, Klemmen, Schutzdaten und Katalogmetadaten übersetzt.
- **Statistiken in die Topbar verschoben**: `System > Statistiken` wurde als eigene lila Premium-Topbar-Seite `Statistiken` ausgelagert und bleibt weiterhin nur für Admin/Systemadmin bei aktiver Premiumfreischaltung sichtbar.
- **VDE-Bewertung optisch aufgeräumt**: Der Bewertungsschritt nutzt kompaktere Karten für Ergebnis, nächsten Prüftermin und Prüfplakette; die Plakettenfunktion erscheint nicht mehr als native Checkbox-Leiste.
- **PDF-Ergebnislogik vereinheitlicht**: Beleuchtungs- und ESD-PDFs bevorzugen im Kopfbereich das fachliche Prüfergebnis statt nur den allgemeinen Protokollstatus.

### Fixed
- **Prüfplakette im VDE-PDF abgesichert**: Der PDF-Export gibt `Prüf-Plakette: Angebracht` nur noch aus, wenn das Prüfergebnis tatsächlich `Bestanden` ist.
- **BSV-Detailpopup aus Panel-Kontext gelöst**: Die Detailansicht wird als Vordergrunddialog vorbereitet, damit sie nicht mehr in Karten-/Panelbereichen abgeschnitten wirkt.

## [0.7.5] - 2026-07-12

### Added
- **Lizenzierbare Premiumbereiche vorbereitet**: `System > Lizenz` enthält jetzt testbare Freischaltungen für `System > Statistiken` und `System > Firma > Kalkulation`, damit beide Bereiche später sauber an ein Lizenzmodul gekoppelt werden können.
- **Passwortregel als Adminoption ergänzt**: Unter `System > Konsole` gibt es eine globale Option, ob einfache Passwörter erlaubt bleiben oder eine strenge Regel mit Großbuchstaben, Kleinbuchstaben, Zahl und Mindestlänge erzwungen wird.

### Changed
- **System-Untertabs verständlicher benannt**: `Einstellungen` heißt sichtbar jetzt `GUI`, `VDE Berechnungen` heißt `VDE-Sollwerte`, `Adminkonsole` heißt `Konsole`, `SQL-Datenbank` heißt `Datenbank`, `QR-Code` heißt `QR` und `Messgeräte` heißt `Geräte`.
- **Admin- und Premium-Tabs visuell getrennt**: Admin-/Systembereiche bleiben orange, `System > Statistiken` wird als Premium-/Auswertungsbereich lila zwischen normalen und Admin-Tabs einsortiert.
- **System-Konsolenansicht verdichtet**: Die obere Statusleiste in `System > Konsole` nutzt kompakte Status-Chips mit einheitlichen Farben für Backend, SQL und Prisma statt großer gemischter Statuskarten.
- **System-Aktionsbuttons vereinheitlicht**: Aktualisieren- und Löschen-Aktionen in Systembereichen werden als icon-only Buttons dargestellt, darunter `Status aktualisieren`, `Logs aktualisieren`, `Logs löschen` und `SQL-Daten leeren`.
- **SQL-/Datenbankübersicht aktualisiert**: Die Datenbankansicht zeigt den aktuellen SQL-only Betrieb klarer, inklusive JSON-Bootstrap-Status, Systemzugang, Reset-Hinweis und zusätzlicher SQL-Bereiche wie Sessions, Messwerte, Prüfer, Messgeräte und Audit-Logs.

### Fixed
- **Gepinnte Liegenschaften in Protokollen robuster gefiltert**: Die Protokollanlage vergleicht Kunden-/Liegenschaftsbezüge jetzt SQL-/Legacy-ID-tolerant, sodass gepinnte Kunden und Liegenschaften im Wizard zuverlässiger zur richtigen Kundenzuordnung passen.
- **Gepinnte Liegenschaft priorisiert**: Die Liegenschaftsauswahl im Protokoll-Wizard sortiert die gepinnte Liegenschaft nach oben, statt sie zwischen fremden oder falsch gematchten Einträgen untergehen zu lassen.
- **Globale Passwortoption persistiert korrekt**: Die neue Passwort-Komplexitätsoption wird serverseitig als Firmeneinstellung gespeichert und beim Anlegen oder Ändern von Benutzern im Auth-Service berücksichtigt.

## [0.7.4] - 2026-07-12

### Added
- **Status-Icons im PDF fachlich vereinheitlicht**: Die Ergebnisdarstellung im PDF verwendet jetzt dieselbe Iconsprache wie `System > Icons`, statt frei nachgezeichnete Ersatzsymbole zu zeigen.
- **Rollen-Normalisierung für Admin/Master erweitert**: Rolle-Erkennung berücksichtigt jetzt Alias-Schlüssel (`role`, `roleLabel`, `userRole`, `payload.userRole`, `roleName`, `capabilities`) aus Session und User-Payload, damit Master/Admin nicht ungewollt im Standard-Nutzerpfad landen.

### Changed
- **Versionsstand angehoben**: `package.json`, `package-lock.json`, Tagesdokumentation, Website-Blog und die sichtbaren Versionsbausteine wurden auf `0.7.4` angehoben.
- **VDE-Abschlussfluss weiter verdichtet**: Die Prüfschrittfolge endet klarer in einer Vorschau-/Abschlusslogik, damit Bewertung und PDF-Sicht im Ablauf enger zusammenliegen.
- **PDF-Ergebnisdarstellung ruhiger positioniert**: Das Statussymbol sitzt im VDE-Export jetzt direkt in der Prüfergebnis-Zeile und wirkt dadurch nicht mehr wie ein doppelter zweiter Statusblock.
- **Verteiler-Komponenteneditor weiter gestrafft**: Die rechte Bearbeitungsseite unter `Kunden > Verteiler` wurde für Schmelzsicherungen, RCD-Gruppen und Stromkreise erneut kompakter gezogen.
- **System-Logs-Interaktion vereinfacht**: Die Refresh-Aktion im Logs-Toolbar verwendet nun ein icon-only-Design und nutzt das zentrale Iconset der App.
- **System-UnderTabs konsistenter gerendert**: Untertabs in System-Bereichen greifen jetzt auf die zentrale Icon-Registry zurück und laden ihre Symbole stabiler ohne visuelle Neuausrichtung bei jedem Tabwechsel.
- **System > Statistiken nach Jahresjahr filterbar**: Die Statistikseite erhielt einen Jahr-Wechselschalter, mit dem sich Kennzahlen gezielt je Kalenderjahr untersuchen lassen.
- **Benutzerverwaltung klarer getrennt**: Standard-Kernbenutzer (`master`, `admin`) werden in der GUI nicht mehr als löschbare Benutzer angeboten; normale SQL-Benutzer bleiben für Master löschbar.

### Fixed
- **PDF-Statussymbole im Export korrigiert**: Statt generischer Kästen oder unpassender Ersatzmarken werden wieder klare `OK`-, `Warnung`- und `Fehler`-Symbole in der MessPilot-Iconlogik dargestellt.
- **VDE-Prüfergebnis im PDF nicht mehr doppelt**: Die separate Statusbox unterhalb des Ergebnisses entfällt; Icon und Text bilden wieder eine gemeinsame Aussage in derselben Ergebniszelle.
- **Prüfplakettenpfad bis zum Export stabilisiert**: Die Bewertungslogik und der PDF-Pfad bleiben konsistenter zusammen, sodass Prüfstatus und Plakettenhinweis nicht mehr gegeneinander laufen.
- **Audit-Direktsprung robuster auf Protokollkontext**: Der Log-Detailsprung findet das Ziel jetzt auch bei fehlender ID über alternative Payload-Felder (`protocolId`, `measurementId`) sicherer.
- **Audit-Log-Detailinhalt vollständig erhalten**: Die Kompaktierung von Änderungspayloads wurde so angepasst, dass bei vielen Feldänderungen nicht durch harte Trunkierung Daten verlieren.
- **Admin-/Master-Berechtigungen in API/Session robuster erkannt**: Berechtigungskern liest Rollen jetzt aus mehreren Session- und Payload-Feldern, wodurch Statistikansicht und Benutzerverwaltung für berechtigte Rollen wieder zuverlässig erreichbar sind.
- **Benutzer löschen als Master stabilisiert**: Der Löschpfad bereinigt Session-/Audit-Abhängigkeiten vor dem Entfernen und fällt bei blockierenden SQL-Constraints auf einen ausgeblendeten `deleted`-Status zurück, statt mit internem Serverfehler abzubrechen.
- **Kernbenutzer-Schutz korrigiert**: `master` und der Standard-`admin` werden nicht mehr scheinbar löschbar dargestellt, weil diese Startkonten durch die Core-User-Sicherung ohnehin automatisch wiederhergestellt werden.
- **VDE-PDF-Ausgabe gegen unbestimmte Layoutwerte abgesichert**: Interner Exportfehler durch nicht initialisierte Werte (`signatureTop`, `vdeRowHeight`) ist entschärft; der Export nutzt stabile Fallbacks.
- **SQL-Readiness-Checks validiert**: `npm run smoke` und `npm run smoke:sql` laufen erfolgreich gegen PostgreSQL (Live/Dev), inklusive 19 Tabellen und Kern-CRUD-Checks; der SQL-Operativbetrieb ist damit dokumentiert freigegeben.
- **Jahreswechsel in der Statistik stabil gehalten**: Der Statistikrender nutzt einen gemeinsamen Jahreszustand, sodass der Wechsel von `‹` / `›` nachvollziehbar bleibt und den bestehenden Layoutzustand nicht resettiert.
- **Schrittnavigation bei 9 Schritten optimiert**: Die Protokoll-Workflow-Navigation nutzt bei langen 9-Schritt-Folgen nun den kompakten Dichte-Modus, damit der Abstand zwischen letztem Schritt „Vorschau“ und dem Abschluss-`✓` wieder korrekt eng bleibt.

## [0.7.3] - 2026-07-12

### Added
- **Log-Details mit Direktsprung erweitert**: In `System > Logs` besitzt jede fachliche Änderungszeile jetzt einen Sprung-Button, der direkt in das betroffene Protokoll, den passenden Prüfschritt und den geänderten Wert führt.
- **Log-PDF aus dem Detailfenster**: Der aktuell geöffnete Logeintrag kann direkt aus `System > Logs` als sauber aufgebautes PDF erzeugt und in einer Vorschau geöffnet werden.

### Changed
- **Versionsstand angehoben**: `package.json`, `package-lock.json` und die sichtbaren Versionsbausteine wurden auf `0.7.3` angehoben.
- **Adminkonsole strukturiert verdichtet**: `System > Adminkonsole` zeigt Backend-, Adapter-, SQL-, Prisma- und Speicherstatus jetzt in kompakteren Betriebs- und Datenstandkarten statt in einer langen Mischansicht.
- **SQL-Datenbankseite klarer getrennt**: `System > SQL-Datenbank` trennt Verbindung, Bereichsübersicht und Wartung deutlicher, damit Betriebsdaten und riskantere Eingriffe wie `SQL-Daten leeren` visuell besser voneinander abgegrenzt sind.
- **System-Logs Übersicht beruhigt**: Die Logliste gruppiert schnelle fachliche Protokolländerungen wieder kompakter, statt jeden direkt aufeinander folgenden Autosave ungefiltert als volle Einzelzeile stehen zu lassen.
- **Login- und App-Start entlastet**: Der Bootstrappfad lädt Kerndaten nach erfolgreichem Login jetzt schlanker und in einem ruhigeren Übergang; schwere Admin-/Log-Pfade blockieren den Einstieg nicht mehr direkt.
- **System-Logs konsequent lazy geladen**: Logs werden nicht mehr bereits beim normalen Login oder beim allgemeinen Öffnen von `Einstellungen` mitgeladen, sondern erst beim echten Wechsel nach `System > Logs`.
- **Verteiler-Eigenschaftseditor kompakter aufgebaut**: Der rechte Editor unter `Kunden > Verteiler` wurde für Stromkreise, Schmelzsicherungen und RCD-Gruppen auf ein ruhigeres, platzsparenderes Formularschema mit kompakteren Auswahlfeldern umgestellt.
- **Leitungskennzeichnung fachlich nachgezogen**: Leitungen im Verteilerbaum und in den Editoren werden jetzt fortlaufend je Stromkreis als `W1`, `W2`, `W3` usw. geführt; bei Doppelkabeln wird sauber auf `Wn-1` und `Wn-2` erweitert.

### Fixed
- **Logliste nicht mehr überladen**: Die Gruppierungslogik für `measurements.update` orientiert sich wieder am echten Action-Key und erzeugt dadurch eine deutlich kleinere, fachlich lesbarere Übersicht.
- **Log-Performance in der Übersicht**: Die teure Feldänderungsanalyse läuft nicht mehr bereits in der Listen-Gruppierung, wodurch `System > Logs` die GUI nicht mehr unnötig ausbremst.
- **Login-Flackern beim Übergang**: Nach Klick auf `Anmelden` fällt die GUI nicht mehr sichtbar kurz in den Login-Zustand zurück, bevor die eigentliche App erscheint.
- **Log-PDF-Vorschau trotz Pop-up-Schutz**: Die PDF-Vorschau öffnet ihr Ziel-Tab direkt aus dem Benutzerklick heraus und wird danach erst mit dem erzeugten Dokument befüllt, statt vom Browser als verspätetes Pop-up blockiert zu werden.
- **Admin-Start ohne Log-Ballast**: `System > Logs` verursacht keine unnötige Last mehr im normalen Login-/Startpfad und bremst dadurch den ersten GUI-Aufbau nicht mehr aus.
- **VDE-Prüfplakette erreicht den PDF-Export wieder korrekt**: Die Formularübernahme behandelt Checkbox plus Hidden-Fallback jetzt robust, sodass `Angebracht` nicht mehr still auf `Nicht angebracht` zurückfällt.
- **Falsche Aktionen in Verteiler-Komponentenansichten entfernt**: Schmelzsicherungen und RCD-Gruppen verwenden nicht länger das Stromkreis-Aktionsgerüst mit unpassenden Kopier- oder Auswahlblöcken.

### Added
- **Lizenzserver-Testdaten im UI:** Die Seite `System > Lizenz` enthält jetzt editierbare Felder für Lizenzserver-Status (`status`, `message`, `checkedAt`, `tenant`, `expiresAt`, `features`) und speichert diese im serverseitigen `company-settings` Datensatz.
- **Serverpersistenz für Lizenzstatus:** Neue Firmeneinstellungsfelder wurden in `src/services/companySettings.service.js` für die zulässige Persistenz auf dem SQL-Pfad ergänzt.
- **Website-Admin-Dashboard ausgebaut:** Die Preview-Website besitzt jetzt eine eigenständige Admin-GUI mit strukturierten Bereichen für `Übersicht`, `Besucher`, `Logins` und `Website`, inklusive Besucher-/Login-Charts sowie zusätzlicher Donut-Auswertungen für Browser, Betriebssystem, Tages- und Wochenverteilung.
- **Öffentliche Website in Seitenstruktur ausgebaut:** `Home`, `Funktionen`, `Blog`, `Roadmap` sowie eigene Preview-Adminseiten wurden als zusammenhängende Website-Struktur aufgebaut.
- **Website-Footer mit Rechtsmodals und GitHub-Link erweitert:** Impressum, Datenschutz, AGB, Kontakt und GitHub laufen jetzt über einheitliche Footer-Dialoge; GitHub besitzt zusätzlich ein Footer-Icon.

### Changed
- **Lizenzformular auf Datenmodell erweitert:** Die bestehenden Lizenzformulare lesen die neuen Felder aus dem aktuellen Einstellungshintergrund und aktualisieren die Statusanzeige im `Lizenzstand` sofort nach dem Speichern.
- **Testorientierter Austausch vorbereitet:** Die Struktur ist vorbereitet, um den späteren `GM-Core`-Validierungsfluss direkt im Lizenzbereich ohne Architekturwechsel abzubilden.
- **Website-Admin-Login und Navigation verdichtet:** Die Admin-Loginseite der Website läuft jetzt ohne Topbar als kompakte Login-Maske; die Admin-GUI selbst nutzt eine reduzierte Icon-Topbar mit schlanker Logout-Aktion und kompakten Überblicks-Chips statt überladener Kopftexte.
- **Landingpages visuell vereinheitlicht:** `Home`, `Funktionen`, `Blog` und `Roadmap` wurden im Stil ruhiger gezogen, inhaltlich präzisiert und in Hero-, Karten- und Footerlogik enger angeglichen.
- **Roadmap wieder aktiviert und bereinigt:** Der Navigationspunkt `Roadmap` ist wieder aktiv; die Seite wurde an die übrigen Landingpages angenähert und um den zuvor störenden Kernfokus-Block bereinigt.
- **Seitentitel- und Theme-Verhalten der Website stabilisiert:** Die Preview-Einstellungen überschreiben Seitentitel nicht mehr auf reines `MessPilot`; Light/Dark wechselt weicher über Fades.
- **Website mobilfähig gemacht:** Topbar, Navigation, Footer, Modal-Fenster, Hero-Blöcke und Inhaltskarten reagieren jetzt auf kleinere Viewports deutlich sauberer und nutzen auf Smartphones eine eigene kompaktere Anordnung.
- **Website-Blog an Changelog gekoppelt:** Der öffentliche Blogeintrag für `0.7.3` spiegelt jetzt den offiziellen Changelog enger, damit Release-Kommunikation und interne Änderungsdokumentation nicht auseinanderlaufen.

---

## [0.7.2] - 2026-07-11

### Changed
- **Versionsstand angehoben**: `package.json`, `package-lock.json` und sichtbare Versionsbausteine wurden auf `0.7.2` angehoben.
- **Fokussierte Versionsdokumentation**: Der Tagesstand für den SQL-/PDF-/Workflow-Stabilisierungszyklus wurde als neuer Patch-Stand dokumentiert und für den weiteren Abgleich genutzt.
- **ToDo-Ranking für den nächsten Zyklus ergänzt**: Offene fachliche Themen wurden in einen klaren nächsten Arbeitspaketplan überführt.

### Open
- **Offene Themen bleiben fachlich priorisiert**: SQL-Finalisierung bei Restpfaden, VDE-Zweitkabel-Endto-End, Export-/Footer-Stabilisierung und Rollen-/Session-Feinschliff laufen weiterhin als nächster Block.

---

## [0.7.1] - 2026-07-11

### Added
- **Tagesdokumentation für SQL-/PDF-Nachzug**: Der Arbeitsstand vom 2026-07-11 ist jetzt als eigener Tagesbericht dokumentiert, inklusive SQL-Fortschritt, Impressum-/UI-Nachzug, VDE-Zweitkabel-Themen und PDF-/Skizzenkorrekturen.
- **SQL-Admin-Nutzung geschärft**: `System > SQL-Datenbank` wurde als aktiver Betriebs- und Resetpunkt für den PostgreSQL-Teststand weiter verfestigt.
- **Lizenz-Freischaltungen vorbereitet**: `System > Lizenz` steuert jetzt testweise `PDF-Wasserzeichen`, `Firmenlogo in PDF-Kopf` und `Unterschriftfeld bei Prüfern` als sichtbare Feature-Gates.

### Changed
- **App-Version auf 0.7.1 angehoben**: `package.json`, `package-lock.json` und die sichtbaren Versionsbausteine wurden auf den neuen Patchstand für den laufenden SQL-/Export-Stabilisierungszyklus gesetzt.
- **SQL-Only-Hauptpfad weiter durchgezogen**: Sichtbare Listen und zentrale CRUD-Pfade für Fachdaten orientieren sich noch konsequenter am PostgreSQL-Stand statt an gemischten JSON-/Legacy-Zwischenständen.
- **Globale und lokale Einstellungen getrennt**: Persönliche Browser-/UI-Präferenzen bleiben lokal, während `PDF-Wasserzeichen` und `PDF nach Abschluss erzeugen` jetzt über die serverseitigen Firmen-/SQL-Einstellungen laufen.
- **Verbrauchsdiagramm Baustrom logisch nachgeschärft**: GUI und PDF bewerten den Verbrauchsverlauf jetzt gegen einen gleitenden Mittelwert der letzten bis zu drei Vorgängerwerte statt nur gegen den direkten Vorwert.
- **PDF-Skizzenprojektion vereinheitlicht**: Die Punktprojektion für Beleuchtungs- und ESD-Skizzen orientiert sich jetzt enger an der quadratischen GUI-Darstellung.
- **VDE-Mehrkabelworkflow nachgezogen**: Zweitkabel, Mehrzeilen-Messmatrix, Bezeichnerlogik (`W1`/`W2`) und mehrkabelige PDF-Ausgaben wurden weiter an den fachlichen Stromkreisworkflow angepasst.
- **DIN-A3-/DGUV-Header verdichtet**: Die großen PDF-Kopfbereiche wurden schrittweise komprimiert, Logo- und Metaflächen ruhiger verteilt und doppelte Auftraggeber-/Auftragnehmer-Darstellungen reduziert.
- **Adminbereiche nachgeschärft**: `System > Lizenz`, `Adminkonsole` und `SQL-Datenbank` wurden klarer als eigenständige Admin-/Betriebsansichten strukturiert.
- **Lizenz-, Firmen- und Prüferoberflächen verdichtet**: `System > Lizenz` wirkt kompakter und finaler; `System > Firma` wurde in klarere Tabs inklusive eigenem `Logo`-Bereich gegliedert, und der `Prüfer > Unterschrift`-Tab wurde optisch an denselben Upload-/Vorschau-Stil angepasst.
- **Feature-Gates bis in die PDF-Ausgabe gezogen**: Firmenlogo und Prüfer-Signatur werden nicht mehr nur GUI-seitig ein-/ausgeblendet, sondern auch im PDF-Modell, in Headern, Abschlussbereichen und einfachen Listenexporten an den Freigabestatus gekoppelt.

### Fixed
- **Fehlende Messpunkte im PDF-Export**: Beleuchtungs-Messpunkte fallen im PDF nicht mehr aus, wenn einzelne `pointXPosition`-Felder fehlten oder im Formular nur der aktive Punkt Positionsdaten geliefert hat.
- **Impressum-Dialog nach Login**: Das globale Impressum wurde vom generischen Modalverhalten entkoppelt und als echter zentrierter Vordergrund-Dialog stabilisiert.
- **Baustrom-PDF-Verbrauchsseite**: Referenzlinie, Achsenskalierung und Zusammenfassung sind nachvollziehbarer und zeigen nicht mehr nur rohe Vorwertdifferenzen.
- **Protokoll-Archivierung**: Beim Archivieren und Entarchivieren werden nicht mehr fälschlich ganze VDE-/Wiederholungsgruppen derselben fachlichen Zuordnung mitgezogen.
- **Prüfer- und Messgerätepfade auf SQL**: Anlegen, Bearbeiten, Löschen und Quellenanzeige wurden für den laufenden PostgreSQL-Betrieb robuster gemacht.
- **VDE-Messmatrix-Trennlinien**: Unscharfe bzw. dicke senkrechte Gruppentrenner in der breiten GUI-Matrix wurden optisch bereinigt.
- **VDE-Mehrkabeldarstellung**: Zweitkabel werden in GUI und PDF konsistenter als eigene Leitungszeilen geführt, statt in der Darstellung zu verschwinden oder unklar zusammenzulaufen.
- **A3-PDF-Kopfbereiche**: Doppelte Auftraggeber-/Auftragnehmer-Wiederholungen sowie übergroße Leerflächen im DIN-A3-/DGUV-Header wurden reduziert.
- **Lokale Refresh-Session stabilisiert**: Die Cookie-Logik behandelt lokale HTTP-Sitzungen nicht mehr unnötig als `Secure`-Only-Fall, sodass Refreshs lokal nicht sofort wieder ausloggen.
- **Firmeneinstellungen nicht mehr als stiller Browser-Cache**: Global relevante Firmen-/Systemschalter hängen nicht mehr an einem lokalen Firmen-`localStorage`-Puffer, sondern werden klarer über den Serverzustand geführt.
- **SQL-Health-Sicht ergänzt**: `Firmeneinstellungen` erscheinen jetzt als eigener SQL-Bereich in Health-/Adminübersichten und machen die globale Einstellungsschicht sichtbarer.
- **Generische CRUD-Fabrik auf SQL-Niveau**: Der verbleibende generische CRUD-Service arbeitet jetzt ebenfalls asynchron und passt damit sauberer zu den aktiven PostgreSQL-/Prisma-Repositories.
- **Lizenzlogik in PDF-Hinweisen konsistent gemacht**: Abschlussseiten sprechen bei gesperrter Signaturfunktion nicht mehr irreführend von einer Unterschrift, sondern neutral von Freigabe; ebenso wurden feste Logo-Platzhalter im gesperrten Zustand entschärft.

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
