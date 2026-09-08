# MessPilot

MessPilot ist eine Web-Anwendung zur strukturierten Erfassung, Verwaltung und Dokumentation elektrotechnischer Prüfungen. Die Anwendung verbindet Kunden, Liegenschaften, Anlagen, Verteiler, Messwerte, Wiederholungsprüfungen und PDF-Ausgaben in einem nachvollziehbaren Prüfablauf.

Website/Beta: [www.MessPilot.de](https://www.MessPilot.de)

## Projektstatus

- Version im App-Checkout: `0.7.9`
- Dokumentationsstand: `2026-09-08`
- Reifegrad: Beta
- Backend: `Node.js` + `Express`
- Frontend: modulares Vanilla JavaScript
- Datenhaltung: PostgreSQL/Prisma als aktiver Hauptpfad
- Deployment: Docker / VPS / Coolify

MessPilot ist funktional nutzbar, aber noch nicht final produktionsreif. Der aktuelle Fokus liegt auf stabilen SQL-Datenflüssen, geführten Prüfabläufen, PDF-Qualität, Rollenmodell, Audit-Logs und einer vorbereiteten Baustromverteiler-Produktdatenbank.

## Was MessPilot aktuell abdeckt

- Kunden, Liegenschaften, Gebäude, Räume und technische Anlagen
- Verteiler- und Stromkreisverwaltung mit mehradrigen Leitungen
- VDE-, DGUV-, Beleuchtungs- und ESD-Prüfabläufe
- Wiederholungsprüfungen mit Vorwertübernahme
- PDF-Vorschau und PDF-Export mit Firmenlogo, Signatur und Prüfergebnis
- Mängel-, Bewertungs- und Prüfplakettenlogik
- Prüfer- und Messgeräteverwaltung
- Rollenmodell mit Systemadmin, Admin, Prüfer, Viewer und Demo
- SQL-Status, Datenbankübersicht, Systemkonsole und Audit-Logs
- Premium-vorbereitete Bereiche wie Statistiken, Kalkulation und BSV-Datenbank
- Öffentliche Website, Shop und zukünftiger Lizenzserver entstehen in einem separaten Projekt.

## Kernbereiche

### Prüfen

MessPilot führt durch vorbereitete Prüfschritte, Messwerttabellen, Vorwertübernahme und Bewertung. Mehrkabelstrukturen werden als eigene Messzeilen geführt, damit Stromkreis, Leitung und Wert nachvollziehbar bleiben.

### Verwalten

Kunden, Standorte, Gebäude, Räume, Anlagen, Verteiler, Prüfer und Messgeräte werden zentral verwaltet. Die Datenhaltung ist auf PostgreSQL ausgelegt, damit App, Listen, Exporte und Statistiken denselben Datenstand verwenden.

### Dokumentieren

PDF-Ausgaben werden aus dem jeweiligen Prüfkontext erzeugt. Firmenlogo, Prüferdaten, Unterschrift, Ergebnisstatus, Mängel und Prüfplakette werden soweit vorhanden in den Export übernommen.

### Auswerten

Systemstatistiken und Kalkulationsdaten sind als Premiumfunktion vorbereitet. Dazu gehören unter anderem Prüfartenanteile, Durchfallquoten, Jahresfilter und kaufmännische Auswertungen nach Protokollart.

### Baustromverteiler-Datenbank

`System > BSV` bereitet eine Produktdatenbank für Baustromverteiler vor. MERZ- und WALTHER-WERKE-Strukturen werden als Explorer-Baum geführt. Sichtbar bleiben vorerst nur ausreichend gepflegte Datensätze, damit spätere Übernahmen in Verteiler, Stromkreise und Prüfabläufe belastbar bleiben.

### Verteiler v2

`Kunden > Verteiler > Verteiler v2` ist als experimenteller Flow-/Konzepteditor vorbereitet. Bestehende Verteilerlayouts bleiben unverändert; lokale Flow-v2-Daten werden getrennt vom klassischen Layout geführt. Der Bereich dient der fachlichen Weiterentwicklung des Stromkreiseditors und ist noch kein finaler produktiver Editor.

## Routen der installierten App

- `/` und `/login` öffnen die MessPilot-Anmeldung.
- `/app` liefert die App-Oberfläche.
- Frühere Websitepfade wie `/preview`, `/blog.html`, `/preise.html` und `/faq.html`
  leiten auf `/login` um. Alte Preview-APIs sind eine gesonderte Aufräumaufgabe.

## Architektur

```text
Browser
  |
  v
Express API
  |
  +-- PostgreSQL / Prisma
  +-- PDF-/Export-Services
  +-- Rollen-, Audit- und Fachlogik
```

Reine UI-Zustände wie Theme-Auswahl können lokal im Browser liegen. Fachliche Nutzdaten laufen über den SQL-Hauptpfad.

## Installation und Updates

Diese öffentliche Ablage enthält ausgewählte Dokumentation und Community-Unterlagen,
keinen vollständigen App-Quellcode und kein hier zugesagtes fertiges Installationspaket.
Ein Klon dieses Repositorys allein kann die App daher nicht bauen oder starten.

Für die Einrichtung wird der vollständige App-Checkout benötigt. Voraussetzungen:
Node.js ab 20 oder Docker/Compose, PostgreSQL mit passendem Schema und persistenter
Dateispeicher. PostgreSQL ist erforderlich; es gibt keinen JSON-Demo-Fallback.
Die App läuft standardmäßig auf Port 3100. Bei direktem Node-Start muss `DATABASE_URL`
in der Prozessumgebung stehen; `npm start` lädt `.env` nicht automatisch.

Es werden keine Standardkonten erzeugt. Das erste Systemkonto wird bei leerer
Benutzertabelle ausdrücklich mit selbst gewähltem Passwort eingerichtet.

**Vor einem Bestandsupdate:** Der neue Backendstand benötigt die versionierte
Kundennummernmigration. Datenbank und Dateien sichern, Wiederherstellung separat
prüfen und Schema kontrolliert migrieren. Ein Docker-Neubau allein reicht nicht.
Die [Deployment-Anleitung](docs/DEPLOYMENT.md) trennt Neuinstallation und Bestandsupdate.

`npm run release:check` prüft im vollständigen App-Repository Build, Regressionen
und Repository-Verkabelung. Das ist keine Browser-/SQL-Endabnahme.
`npm run smoke:sql` schreibt Testdaten und gehört ausschließlich in eine isolierte
Testdatenbank. Produktions-, Sicherheits- und fachliche Freigabe bleiben offen.

Die externe Website mit Shop soll künftig Lizenzverkauf und Lizenzverwaltung
übernehmen. Die vorhandene GM-Core-Anbindung im App-Code ist noch nicht umgestellt
und nicht als fertige Lizenzdurchsetzung abgenommen.

## Dokumentation

- [CHANGELOG](CHANGELOG.md)
- [Roadmap](ROADMAP.md)
- [Deployment](docs/DEPLOYMENT.md)
- [API](docs/API.md)
- [System Overview](docs/SYSTEM_OVERVIEW.md)
- [Security](SECURITY.md)
- [Third Party Notices](THIRD_PARTY_NOTICES.md)
- [License](LICENSE)

## Nächste fachliche Schwerpunkte

1. PDF-Templates fachlich weiter finalisieren
2. BSV-Datenbank weiter vervollständigen und später in Verteiler/Stromkreise übernehmen
3. Verteiler-v2-Konzepteditor fachlich weiterentwickeln
4. Audit- und Betriebsansichten weiter vereinheitlichen
5. Rollen-, Lizenz- und Premiumfunktionen produktionsnäher härten

## Lizenz und Sicherheit

- Lizenz: [LICENSE](LICENSE)
- Sicherheitsmeldungen: [SECURITY.md](SECURITY.md)
