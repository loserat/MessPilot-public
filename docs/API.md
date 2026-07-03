# API-Dokumentation

Die API ist aktuell eine Demo-API mit JSON-Datei-Persistenz. Sie bereitet die spaetere Fach-App vor, ersetzt aber noch keine relationale Datenbank.

Basis-URL lokal:

```text
http://localhost:3100/api
```

## Healthcheck

```http
GET /api/health
```

Beispielantwort:

```json
{
  "success": true,
  "data": {
    "app": "MessPilot",
    "status": "ok",
    "mode": "demo",
    "storage": {
      "mode": "json",
      "database": "jsonFile",
      "databaseUrlConfigured": false,
      "databaseUrlMasked": "",
      "databaseHost": "",
      "databaseName": "",
      "dataStorage": "storage/demoStore.json",
      "pdfStorage": {
        "mode": "local",
        "path": "storage/pdfs"
      },
      "persistentStorageRequired": true,
      "activeRepository": "json"
    },
    "timestamp": "2026-06-15T19:37:31.926Z",
    "counts": {
      "customers": 5,
      "locations": 6,
      "buildings": 4,
      "rooms": 4,
      "systems": 4,
      "distributions": 4,
      "inspections": 4,
      "measurements": 4,
      "defects": 5,
      "inspectors": 2,
      "testDevices": 2
    }
  },
  "message": "Backend erreichbar"
}
```

Die Datenbank-URL wird nie im Klartext ausgeliefert. Fuer den Systembereich wird nur eine maskierte Darstellung und der technische Status gemeldet.

## Einheitliche Antworten

Erfolg:

```json
{
  "success": true,
  "data": [],
  "message": "Kunden geladen"
}
```

Fehler:

```json
{
  "success": false,
  "error": {
    "message": "Pflichtfeld fehlt: name",
    "code": "VALIDATION_ERROR"
  }
}
```

## Authentifizierung

Alle Fachendpunkte ausser `/api/health` und `/api/auth/*` erwarten eine gueltige MessPilot-Session. Die Session wird als HTTP-only Cookie gespeichert.

Startkonto im lokalen Seed:

```text
Benutzer: admin
Passwort: admin
Rolle: admin
```

Geschuetztes Master-Konto: `master / master`. Lokale Standardkonten folgen dem Schema Benutzer=Passwort=Rolle: `master`, `admin`, `user`, `viewer`, `demo`.

### Session pruefen

```http
GET /api/auth/me
```

### Login

```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "master",
  "password": "master"
}
```

### Logout

```http
POST /api/auth/logout
```

### Benutzer

```http
GET  /api/users
GET  /api/users/:id
POST /api/users
PUT  /api/users/:id
```

`GET`, `POST` und `PUT` fuer Benutzer benoetigen `master` oder `admin`. Admins koennen normale Benutzer pflegen; geschuetzte `master`- und `admin`-Konten duerfen nur von `master` geaendert werden. Benutzer werden nicht geloescht, sondern ueber `status: "disabled"` deaktiviert.

Rollen:

- `master`
- `admin`
- `user`
- `viewer`
- `demo`
- `demo`

Aktives Rollenmodell:

- `master`: Benutzer, Rollen, Lizenz, Datenbank, Updates und Systemstatus verwalten.
- `admin`: Kunden-/Objektstruktur, Messgeraete, Pruefer und fachliche Einstellungen verwalten.
- `user`: fachliche Bearbeitung ohne Systemverwaltung.
- `viewer`: nur lesen und exportierte/erzeugte Dokumente ansehen.
- `demo`: Demo-/Gastzugang ohne Schreibrechte.

`master` und `admin` sind geschuetzte Kernrollen und duerfen nicht deaktiviert oder in andere Rollen umgewandelt werden.

### Lizenz und Feature-Gates

Noch kein aktiver Endpunkt. Geplantes Ziel:

- `GET /api/system/license` fuer Status, Edition, Limits und Installations-ID
- `PUT /api/system/license` fuer Lizenzschluessel durch `master`
- serverseitige Pruefung vor Kundenanlage, PDF-Export und editionabhaengigen Funktionen

Beispiele fuer spaetere Gates:

- ohne Lizenz maximal 2 Kunden
- PDF-Wasserzeichen nur mit passender Lizenz entfernen
- erweiterte Rollen/Rechte und Branding nur mit passender Edition

### Prüfer

```http
GET    /api/inspectors
GET    /api/inspectors/:id
POST   /api/inspectors
PUT    /api/inspectors/:id
DELETE /api/inspectors/:id
```

Wichtige Felder:

- `name`
- `role`
- `certificateNumber`
- `phone`
- `email`
- `signatureFileName`
- `status`
- `note`

### Messgeräte

```http
GET    /api/test-devices
GET    /api/test-devices/:id
POST   /api/test-devices
PUT    /api/test-devices/:id
DELETE /api/test-devices/:id
```

Messgeraete koennen optional ueber `inspectorId` einem Pruefer zugeordnet werden. Die Zuordnung ist nicht exklusiv; ein Pruefer darf mehrere Messgeraete verantworten.

Wichtige Felder:

- `name`
- `deviceType`
- `manufacturer`
- `model`
- `serialNumber`
- `calibrationDate`
- `calibrationDue`
- `status`
- `note`

## CRUD-Endpunkte

Alle folgenden Fachbereiche benoetigen Login. Die meisten Bereiche unterstuetzen aktuell:

- `GET /`
- `GET /:id`
- `POST /`
- `PUT /:id`
- `DELETE /:id`

### Kunden

```http
GET    /api/customers
GET    /api/customers/:id
POST   /api/customers
PUT    /api/customers/:id
```

Pflichtfeld bei `POST`: `name`

Kunden koennen nicht geloescht werden. Ein DELETE-Versuch wird serverseitig abgewiesen.

### Standorte

```http
GET    /api/locations
GET    /api/locations/:id
POST   /api/locations
PUT    /api/locations/:id
DELETE /api/locations/:id
```

Pflichtfelder bei `POST`: `customerId`, `name`

### Gebaeude

```http
GET    /api/buildings
GET    /api/buildings/:id
POST   /api/buildings
PUT    /api/buildings/:id
DELETE /api/buildings/:id
```

Pflichtfelder bei `POST`: `locationId`, `name`

### Anlagen

```http
GET    /api/systems
GET    /api/systems/:id
POST   /api/systems
PUT    /api/systems/:id
DELETE /api/systems/:id
```

Pflichtfelder bei `POST`: `buildingId`, `name`

### Verteilungen

```http
GET    /api/distributions
GET    /api/distributions/:id
POST   /api/distributions
PUT    /api/distributions/:id
DELETE /api/distributions/:id
```

Pflichtfelder bei `POST`: `systemId`, `name`

### Pruefungen

```http
GET    /api/inspections
GET    /api/inspections/:id
POST   /api/inspections
PUT    /api/inspections/:id
DELETE /api/inspections/:id
```

Pflichtfelder bei `POST`: `distributionId`, `type`, `date`

### Messprotokolle

```http
GET    /api/measurements
GET    /api/measurements/:id
POST   /api/measurements
PUT    /api/measurements/:id
DELETE /api/measurements/:id
```

Pflichtfelder bei `POST`: `date`, `measurementType`, `objectLabel`

Der aktuelle Frontend-Workflow speichert Entwuerfe ueber diesen Endpunkt. Fuer die Zuordnung werden zusaetzlich `customerId`, `locationId`, `buildingId` und `roomId` mitgefuehrt.

Beleuchtungsmessungen koennen ausserdem uebergeben:

- `tester`
- `standardPreset`
- `workArea`
- `targetLux`
- `uniformity`
- `maxMinRatio`
- `measuringPlane`
- `grid`
- `edgeOffset`
- `rating`
- `note`
- `measurementValues`

Wichtiges aktuelles Verhalten:

- Das Frontend vergibt fuer aktive Entwuerfe eine stabile `protocolId`.
- Nach dem ersten Speichern wird diese ID weiterverwendet.
- Weitere Speicherungen sollen per Aktualisierung denselben Datensatz fortschreiben.
- Die Demo-API ist noch kein finales Datenmodell und erzwingt noch keine fachliche Eindeutigkeit auf Serverebene.

Beispiel:

```bash
curl -X POST http://localhost:3100/api/measurements \
  -H "Content-Type: application/json" \
  -d '{"date":"2026-06-18","measurementType":"Beleuchtungsmessung ASR 3.4","objectLabel":"EG-001 · Technikraum","customerId":"customer-1","locationId":"location-1","status":"Entwurf"}'
```

### Export

```http
GET /api/export/measurements/:id/pdf
POST /api/export/measurements/:id/archive
POST /api/export/measurements/:id/unarchive
```

Erzeugt serverseitig ein PDF fuer ein gespeichertes Messprotokoll. Standard ist eine Inline-Ausgabe fuer Browser-Vorschau.

Optionale Query-Parameter:

- `?preview=1`: Vorschau erzeugen, ohne den PDF-Status des Protokolls zu veraendern.
- `?download=1`: PDF als Download ausliefern und den Exportstatus als erzeugt markieren.

Archivieren erzeugt/markiert den PDF-Stand serverseitig und setzt den PDF-Status auf `Erzeugt`. Zurueckholen setzt den PDF-Status wieder auf `Nicht erzeugt`, damit das Protokoll wieder in der aktiven Liste bearbeitet werden kann.

Der aktuelle PDF-Export enthaelt:

- Protokollkopf mit Pruefart und Status
- Kunde, Liegenschaft, Gebaeude und Raum
- Pruefdatum, Pruefer und Bearbeitungsstatus
- Norm-/Grunddaten fuer Beleuchtungsmessungen
- Raum-, Raster- und Randabstandsangaben
- Messwerte, falls im Protokoll gespeichert
- Bewertung und Hinweisbereich

Beispiel:

```bash
curl -I http://localhost:3100/api/export/measurements/mea_demo_001/pdf?preview=1
curl -o messprotokoll.pdf http://localhost:3100/api/export/measurements/mea_demo_001/pdf?download=1
```

### Maengel

```http
GET    /api/defects
GET    /api/defects/:id
POST   /api/defects
PUT    /api/defects/:id
DELETE /api/defects/:id
```

Pflichtfelder bei `POST`: `title`, `status` sowie `inspectionId` oder `distributionId`

### Dokumente

```http
GET    /api/documents
GET    /api/documents/:id
POST   /api/documents
PUT    /api/documents/:id
DELETE /api/documents/:id
```

Pflichtfelder bei `POST`: `name`, `type`

Hinweis: Es gibt noch keine Datei-Uploads. Die erste PDF-Erzeugung laeuft ueber den Export-Endpunkt.

### Benutzer

Benutzer sind im Abschnitt Authentifizierung dokumentiert. Es gibt keinen DELETE-Endpunkt.

## Testbeispiele

Healthcheck:

```bash
curl http://localhost:3100/api/health
```

Kunden laden:

```bash
curl -c /tmp/messpilot.cookies \
  -H "Content-Type: application/json" \
  -d '{"email":"master","password":"master"}' \
  http://localhost:3100/api/auth/login

curl -b /tmp/messpilot.cookies http://localhost:3100/api/customers
```

Demo-Kunden anlegen:

```bash
curl -b /tmp/messpilot.cookies -X POST http://localhost:3100/api/customers \
  -H "Content-Type: application/json" \
  -d '{"name":"Demo GmbH","status":"aktiv"}'
```

Die Kundennummer wird automatisch fortlaufend durch den Server vergeben, zum Beispiel `KD-0006`. Manuell übergebene `customerNumber`-Werte werden bei Anlage und Aktualisierung ignoriert.

Die Kundenart wird automatisch aus der USt-ID abgeleitet: ohne `taxId` wird der Kunde als `Privatkunde` geführt, mit `taxId` als `Gewerbe`.

Validierung testen:

```bash
curl -b /tmp/messpilot.cookies -X POST http://localhost:3100/api/customers \
  -H "Content-Type: application/json" \
  -d '{}'
```

## Aktuelle Grenzen

- Daten werden aktuell in `storage/demoStore.json` gespeichert.
- `storage/` wird nicht versioniert und ist lokale Laufzeitpersistenz.
- Der Healthcheck meldet die konfigurierte Storage-Art ueber `storage.mode`.
- Der Healthcheck meldet den tatsaechlich aktiven Repository-Adapter ueber `storage.activeRepository`.
- PostgreSQL ist als Zielarchitektur vorbereitet, aber noch nicht als Laufzeit-Backend aktiv.
- Keine Relationenpruefung zwischen IDs.
- Authentifizierung und Rollen sind ein erster JSON-/Cookie-Startpunkt, aber noch nicht produktiv gehaertet.
- Keine Uploads.
- Keine E-Mail-Funktionen.
- PDF-Export ist als erste Vorschau vorhanden, aber noch nicht final freigegeben.
- Keine normativ freigegebenen Berechnungen.
