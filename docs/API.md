# MessPilot API

Stand: 2026-09-06. Die installierbare App nutzt Express und PostgreSQL über Prisma.
Dies ist eine Dokumentation des aktuellen Beta-Stands, keine allgemeine Produktionsfreigabe.
Die externe Website und ihr Shop-/Lizenzserver werden in einem anderen Projekt entwickelt.

Basis lokal: `http://localhost:3100/api`. Bestehende Adressen bleiben erhalten.
Die Anwendung ist derzeit für einen Betrieb je Installation ausgelegt, nicht für
mehrere voneinander unabhängige Firmen auf derselben Installation.

## Antwortformat und Fehler

Erfolg: `{ "success": true, "data": ..., "message": "..." }`.

Fehler, beispielsweise ein ungültiger Kundenname:

```json
{
  "success": false,
  "error": {
    "message": "Bitte die markierten Pflichtfelder prüfen.",
    "code": "VALIDATION_ERROR",
    "details": {
      "fields": { "name": "Bitte einen nicht leeren Text angeben." }
    }
  }
}
```

`error.details` ist optional und additiv. Aktuell werden freigegebene Feldfehler
(`body`, `name`, `customerId`) und Zähler von Löschabhängigkeiten ausgegeben.
Interne Datenbankdetails werden nicht in dieses Feld übernommen; unerwartete
Serverfehler haben eine allgemeine Fehlermeldung.

| HTTP | Bedeutung |
| --- | --- |
| 400 | Ungültige Eingaben |
| 401 | Keine gültige Anmeldung |
| 403 | Keine Berechtigung für Aktion oder Kundendaten |
| 404 | Datensatz nicht gefunden |
| 409 | Abhängigkeit, Eindeutigkeits- oder Protokollversionskonflikt |
| 500 / 503 | Server- oder Verfügbarkeitsfehler; kein bestätigter Erfolg |

## Anmeldung und Sitzungen

- `GET /api/auth/me`: aktuellen Benutzer oder `data.user: null` abfragen.
- `POST /api/auth/login`: eigenes Konto mit `email` und `password` anmelden.
- `POST /api/auth/logout`: Sitzung serverseitig widerrufen.

Es gibt keine dokumentierten Standardzugangsdaten. Das erste Systemkonto wird
explizit über `npm run setup:admin` eingerichtet; keine automatische Kontoanlage
beim Lesen oder Starten der App.

Sitzungs- und Browserbindung werden über Cookies verwaltet. Nicht-Browser-Clients
müssen sämtliche erhaltenen Cookies übernehmen, nicht nur den ersten Cookie.
Fachendpunkte verlangen Anmeldung und zusätzliche rollenabhängige Freigaben.
Kundengebundene Lesekonten sehen nur ihren zugeordneten Bereich.

Der Browser zeigt eine Abmeldung erst nach Bestätigung oder HTTP 401 als beendet.
Bei einem Server-/Netzfehler bleibt der Zustand ehrlich erkennbar und die Aktion
kann über „Abmelden“ erneut ausgelöst werden.

## Kunden

| Methode | Adresse | Zweck |
| --- | --- | --- |
| GET | `/api/customers` | Zugängliche Kunden |
| GET | `/api/customers/:id` | Kundendetails |
| POST | `/api/customers` | Kunde anlegen |
| PUT | `/api/customers/:id` | Kunde bearbeiten |
| DELETE | `/api/customers/:id` | Kunde ohne Abhängigkeiten löschen |
| DELETE | `/api/customers/:id?force=true` | Kunde samt verknüpfter Daten löschen |

Schreibaktionen verlangen die bestehende Kundenverwaltungsberechtigung.
Der Request muss ein JSON-Objekt sein; `name` muss bei Anlage und im resultierenden
Änderungsstand ein nicht leerer String sein. PUT darf weiterhin einzelne Felder ändern.
Die Kundenart wird aus `taxId` abgeleitet.

Kundennummern vergibt ausschließlich der Server: `KD-0001`, nach `KD-9999`
entsprechend `KD-10000`. Clientseitige Nummern werden bei POST/PUT ignoriert.
Betriebszuordnung und Identität können über Kunden-POST/PUT nicht umgeschrieben werden.

Zählererhöhung und Anlage erfolgen atomar. Die Datenbank verhindert doppelte Nummern
je Betrieb. Löschen reduziert den persistenten Zähler nicht. Lücken sind zulässig.
Die Garantie für nicht wiederverwendete Nummern gilt ab der neuen Zählerführung;
früher gelöschte Nummern ohne Verlauf können nicht rückwirkend rekonstruiert werden.

Bei vorhandenen Abhängigkeiten liefert normales DELETE
`409 CUSTOMER_DELETE_BLOCKED` mit `error.details.linkedData`.
Die ausdrücklich bestätigte vollständige Löschung umfasst die zugeordneten Standorte,
Gebäude, Räume, Anlagen, Verteiler, Stromkreise, Schutzgeräte, Prüfungen,
Protokolle, Mängel und Dokumentmetadaten. Sie läuft in einer gemeinsamen Transaktion.
Scheitert ein Teil, werden die vorherigen Datenbankänderungen zurückgerollt.
Physische PDF-Dateien werden dabei nicht zusätzlich gelöscht.

## Standorte / Liegenschaften

`/api/locations`: GET und POST; `/api/locations/:id`: GET, PUT und DELETE.

`name` und `customerId` müssen nicht leere Strings sein; dies gilt auch für den
zusammengeführten Änderungsstand. Kunden-IDs werden gegen bestehende SQL-/Legacy-IDs
aufgelöst. Ein unbekannter Kunde führt zu HTTP 400 statt zu einem Standort ohne Zuordnung.
Schreibberechtigung und kundengebundene Lesegrenzen bleiben erhalten.

## Firmeneinstellungen und Frontend-Transport

`GET /api/company-settings` und `PUT /api/company-settings` verlangen die vorhandene
Verwaltungsberechtigung. Das Formular hält ungespeicherte Eingaben sitzungslokal,
über Tabwechsel und Speicherfehler hinweg. Erst eine bestätigte Serverantwort
aktualisiert den gespeicherten Stand. Ein Seitenreload verwirft weiterhin ungespeicherte
Entwürfe; es gibt keine neue dauerhafte Browserablage.

JSON-Datenzugriffe in `app.data.js` nutzen den zentralen `requestJson`-Client:

- Standard-Zeitlimit 12 Sekunden, einschließlich vollständiger Antwortverarbeitung.
- Abbruch über AbortController; externe Abbruchsignale werden berücksichtigt.
- Ungültige JSON-Antworten erzeugen `INVALID_RESPONSE`; HTTP 204 wird ausdrücklich unterstützt.
- Serverstatus, Fehlercode und sichere Details bleiben für Aufrufer verfügbar.
- Ladeanzeige und Timer werden auch bei Fehlern freigegeben.
- Keine automatische Wiederholung von Schreibanfragen.

Ein Timeout oder Verbindungsabbruch beweist nicht, dass der Server nichts gespeichert hat.
Vor erneuter Anlage den Serverstand prüfen. Eine dauerhafte Idempotenzlösung
gegen doppelte Anlagen nach verlorener Antwort ist noch offen.

## Weitere bestehende API-Bereiche

Weiterhin registriert sind Gebäude, Räume, Anlagen, Verteiler, Stromkreise,
Prüfungen, Messprotokolle, Mängel, Dokumente, Benutzer, Prüfer, Messgeräte,
PDF-Export, QR, Baustromvorlagen und Systemfunktionen.
Die genauen Methoden und Berechtigungen stehen in `src/routes/`.
Diese Bereiche wurden nicht pauschal auf einen neuen Vertrag umgestellt.

`/api/measurements` und der bestehende Alias `/api/protocols` bleiben erhalten.
Protokollabschluss, bestätigtes Wiederöffnen und Versionskonflikte sind im
App-Repository in `docs/PROTOCOL_LOCK_2026-09-05.md` beschrieben. Dieser interne
Bericht wird nicht in die öffentliche Dokumentationsablage synchronisiert.
PDF-Vorschau: `GET /api/export/measurements/:id/pdf?preview=1`.
Eine PDF-Ausgabe ist keine automatische fachliche, rechtliche oder normative Freigabe.

`/api/licenses` existiert bereits. Der künftige Vertrag mit der externen
Lizenzplattform ist noch nicht finalisiert; interne Entscheidung im App-Repository:
`docs/LICENSING.md`.
Es werden hier keine erfundenen Limits, Preise oder Lizenzrechte festgelegt.

Alte `/api/preview/*`-Routen sind weiterhin vorhanden und separat stillzulegen;
sie gehören nicht zum neuen App-Vertrag. Auch die öffentliche Route
`/api/public/system` ist keine pauschale Freigabe aller ihrer Unterfunktionen.

## Prüfung und Installation

Die öffentliche [Deployment-Anleitung](DEPLOYMENT.md) beschreibt die kontrollierte
Umstellung. Der interne Bericht `docs/API_STABILIZATION_2026-09-06.md` im
App-Repository enthält die ausführlichen Testergebnisse und Grenzen.
Maschinenlesbare OpenAPI-Dokumentation, umfassende API-Schemata, Pagination,
vollständiges Berechtigungsaudit und Schutz vor verlorenen Schreibantworten
bleiben nachfolgende Arbeitspakete.
