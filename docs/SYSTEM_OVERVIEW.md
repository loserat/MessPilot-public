# MessPilot-Systemübersicht

Stand: 2026-09-08 · Version 0.7.9 · Beta. Diese Übersicht beschreibt den aktuellen
App-Quellcode; sie bestätigt keine produktive Installation oder fachliche Freigabe.

## Bausteine und Datenfluss

```text
Browser der Mitarbeiter
  │ Anmeldung, Kunden, technische Objekte, Prüfprotokolle
  ▼
MessPilot-App / Express-API
  ├─ PostgreSQL / Prisma: Konten, Sitzungen und fachliche Daten
  ├─ PDF-Erzeugung: Vorschau, Download und Dateiablage
  └─ Rollen, Validierung und Audit

Separates Projekt: öffentliche Website / Shop / zukünftiger Lizenzserver
  ▲
  └─ geplante ausgehende Lizenz-API-Verbindung des App-Backends
```

PostgreSQL ist der einzige aktive fachliche Datenpfad. Es gibt keinen automatischen
JSON-Demo-Fallback. Browserzustände wie Theme, Navigation und noch nicht gespeicherte
Formulareingaben sind keine dauerhafte SQL-Speicherung.

Die Installation ist für einen Betrieb mit mehreren Benutzern vorgesehen.
Mehrere unabhängig getrennte Firmen auf derselben Installation sind nicht abgenommen.
Die externe Lizenzplattform ist geplant; im App-Code besteht noch die alte
GM-Core-Anbindung mit offenen Prüf- und Durchsetzungslücken.

## Fachliche Struktur

```text
Kunde → Liegenschaft → Gebäude → Räume / technische Anlagen / Verteiler
Verteiler → Schutzstruktur → Stromkreise → Leitungen
Prüfprotokoll → Zuordnung + Stammdaten-Snapshot + Prüf- und Messwerte
             → Bewertung / Dokumentationsstatus → PDF und Mängel
```

Protokolle übernehmen den jeweils benötigten Stammdatenstand als Snapshot.
Das ist eine im Protokoll gespeicherte Kopie; Messwerte gehören zum Prüfprotokoll.
Eine vollständige unveränderliche Historie sämtlicher Profile und PDFs ist noch offen.

## Prüfablauf

1. Kunde und technisches Objekt zuordnen, Prüfart wählen.
2. Grunddaten und benötigte Struktur erfassen.
3. Prüfschritte und Messwerte der gewählten Prüfart dokumentieren.
4. Ergebnis bzw. Dokumentationsstatus prüfen und ausdrücklich abschließen.
5. PDF ansehen/exportieren; Folgeprüfung bei Bedarf aus dem bestehenden Kontext starten.

Die Schritte unterscheiden sich für VDE/DGUV/Baustrom, Beleuchtung, ESD und
Anlagen-Inbetriebnahmen. Der Server kontrolliert beim Abschluss erforderliche
Daten und Zuordnungen. Dies ist keine vollständige normative Messwertfreigabe.

Abgeschlossene Protokolle sind schreibgeschützt. Änderungen erfordern bestätigtes
Wiederöffnen, passende Rechte und eine aktuelle Version. Widersprüchliche oder
konkurrierende Schreibzugriffe können mit HTTP 409 abgelehnt werden.

## Betrieb und Grenzen

`/` und `/login` öffnen die Anmeldung, `/app` liefert die App-Oberfläche.
Öffentliche Website und Shop werden außerhalb dieses Repositories entwickelt.
Verbliebene ältere Preview-APIs sind eine gesonderte Aufräumaufgabe.

Die App benötigt PostgreSQL sowie dauerhafte Dateiablage für gespeicherte PDFs.
Schemaänderungen werden versioniert migriert; ein neues App-Image allein aktualisiert
keine Bestandsdatenbank. Es gibt keine automatisch erzeugten Standardkonten.

Fachliche Endabnahme, Backup/Restore der konkreten Installation, sichere
Lizenzdurchsetzung und vollständige Browser-/Berechtigungsprüfung bleiben offen.
Einzelne bestandene Tests bedeuten keine allgemeine Produktionsfreigabe.

Weitere Informationen: [API](API.md) und [Deployment](DEPLOYMENT.md).
