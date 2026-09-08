# Installation und Betrieb

Stand: 2026-09-08 · MessPilot 0.7.9 Beta. Diese Anleitung ist mit den Dateien im
App-Repository abgeglichen. Die beschriebenen Installations-/Restoreabläufe wurden
in diesem Dokumentationsschritt nicht ausgeführt. Keine Produktionsfreigabe.

## Voraussetzungen und Konfiguration

Benötigt werden das vollständige App-Repository, Docker mit Compose oder Node.js
ab Version 20 sowie PostgreSQL mit passendem Schema. Das öffentliche
`MessPilot-public`-Repository enthält synchronisierte Dokumentation; es ist kein
vollständiger App-Checkout zum Bauen.

Compose definiert `messpilot` und `postgres` (PostgreSQL 16). Intern verwendet die
App Port 3100; `MESSPILOT_PORT` steuert die Host-Freigabe. Die Konfiguration aus
`.env.example` vor dem ersten Start mit eigenen Werten einrichten. Eine vorhandene
`.env` nicht überschreiben und keine Geheimnisse ins Repository übernehmen.

| Variable | Verwendung |
| --- | --- |
| `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB` | Einrichtung des Compose-Datenbankcontainers; eigene Zugangsdaten verwenden |
| `DATABASE_URL` | Verbindung der App zur vorgesehenen Datenbank; Compose bildet bei fehlender URL einen Standard aus den PostgreSQL-Werten |
| `PORT` / `MESSPILOT_PORT` | Node-Listener / von Compose veröffentlichter Host-Port |
| `SESSION_COOKIE_NAME`, `COOKIE_SECURE` | Sessioncookie; Secure-Konfiguration passend zum HTTPS-Betrieb prüfen |
| `MESSPILOT_PDF_STORAGE_PATH` | Lokales PDF-Verzeichnis, standardmäßig `storage/pdfs` |
| `MESSPILOT_LICENSE_ENCRYPTION_KEY` | Geheimnis der vorhandenen Lizenzimplementierung; stabil und getrennt vom Code verwahren |
| `GM_CORE_LICENSE_BASE_URL` | Noch vorhandene Altanbindung; kein Vertrag des zukünftigen Website-Lizenzservers |

Die Lizenzplattform wird extern neu geplant und ist noch nicht umgestellt.
`MESSPILOT_LICENSE_ALLOW_UNSIGNED_DEV` ist keine Betriebsfreigabe.
`MESSPILOT_STORAGE_MODE` und `MESSPILOT_SQL_BOOTSTRAP_JSON` schalten den aktuellen
Code nicht auf JSON um: Der Speicherpfad ist fest PostgreSQL.

`npm start` lädt `.env` nicht automatisch. Bei Node-Betrieb müssen benötigte Werte
vor dem Start in der Prozessumgebung stehen. Prisma-CLI und Compose haben eigene
Konfigurationsmechanismen; deren funktionierende Verbindung beweist nicht die App-Konfiguration.

## Leere Neuinstallation mit Compose

Nur in einem neuen, eindeutig getrennten Installationsverzeichnis mit leerer
Zieldatenbank verwenden. Projekt-/Container-/Volume-Namen vorab abgleichen;
die Compose-Datei enthält feste Containernamen und darf nicht versehentlich eine
bestehende Installation übernehmen.

Nach Einrichtung der Konfiguration:

```bash
docker compose up -d postgres
```

Mit `docker compose ps` prüfen, dass PostgreSQL als `healthy` gemeldet wird.
Erst danach das App-Image bauen und das leere Schema einrichten:

```bash
docker compose build messpilot
docker compose run --rm --no-deps messpilot npm run db:migrate:deploy
```

Die Migration legt bei leerer Datenbank die Baseline und anschließend die
Kundennummernerweiterung an. Der App-Start selbst führt keine Migration aus.

Für das erste Systemkonto `MESSPILOT_SETUP_ADMIN_EMAIL`, `MESSPILOT_SETUP_ADMIN_NAME`
und `MESSPILOT_SETUP_ADMIN_PASSWORD` vorübergehend sicher in der Host-Prozessumgebung
bereitstellen. Das Passwort selbst wählen, mindestens 12 Zeichen; keine Werte in
Befehlshistorie oder Dokumentation eintragen. Die folgende Weitergabe enthält nur Variablennamen:

```bash
docker compose run --rm --no-deps \
  -e MESSPILOT_SETUP_ADMIN_EMAIL \
  -e MESSPILOT_SETUP_ADMIN_NAME \
  -e MESSPILOT_SETUP_ADMIN_PASSWORD \
  messpilot npm run setup:admin
unset MESSPILOT_SETUP_ADMIN_EMAIL MESSPILOT_SETUP_ADMIN_NAME MESSPILOT_SETUP_ADMIN_PASSWORD
docker compose up -d --no-deps messpilot
```

`setup:admin` funktioniert ausschließlich bei leerer Benutzertabelle und ist kein
Passwort-Reset. Es gibt keine automatisch angelegten Standardkonten. Bestehende
Konten behalten ihre Zugangsdaten. Demo-Seeds sind keine Installation.

## Bestehende Installation aktualisieren

Der Stand vom 06.09. benötigt eine Schemaänderung. **Nicht einfach neu bauen und
starten.** Die dokumentierte Übernahme der Bestandsinstallation ist noch offen und
bedarf einer ausdrücklichen Freigabe. Folgender Ablauf ist vorbereitet:

1. Zielinstallation, laufenden Build, Datenbank, Schema, Dateivolumes und frühere
   Nummernvergabe lesen und abgleichen. Wartungsfenster und Rückkehrweg festlegen.
2. Schreibzugriffe anhalten; Datenbank und Dateispeicher zusammengehörig sichern.
   Restore auf einer separaten Kopie nachweisen. Alte Writer während der Umstellung
   und danach nicht parallel zum neuen Nummernzähler weiterlaufen lassen.
3. Mit dem neuen Checkout/Build und ausdrücklich gesetzter, geprüfter `DATABASE_URL`
   `npm run db:preflight -- --baseline` ausführen. Es prüft ohne Datenänderung das
   Ausgangsschema, Dubletten und Nummernbereich. Bei Abweichungen stoppen.
4. Nur bei passendem Ausgangsschema und fehlender Migrationshistorie mit
   `npx prisma migrate resolve --applied 0_baseline` die vorhandene Baseline markieren.
   Dies ist ein Schreibschritt. Für eine bereits korrekt migrierte Installation
   stattdessen deren Migrationsstatus prüfen; nicht erneut eine Baseline erzwingen.
5. `npm run db:migrate:deploy` aus dem neuen Stand ausführen. Danach
   `npm run db:preflight` und `npx prisma migrate status` prüfen.
6. Ausschließlich den zum Schema passenden App-Build starten. Anmeldung, SQL-Zugriff,
   vorhandene Kunden/Protokolle und Dateizugriff prüfen. Schreibbetrieb erst nach
   Abnahme freigeben und Build-/Schema-/Prüfstand dokumentieren.

Prisma ist im Checkout auf 5.22.0 festgelegt. Die vollständige interne Begründung
und isolierte Testbelege stehen in `docs/API_STABILIZATION_2026-09-06.md` im App-Repository.
Kein `db:push`, `migrate reset`, Demo-Seed oder automatisches Umnummerieren auf Bestandsdaten.
Ein fehlgeschlagener Migrationslauf verlangt Prüfung; weder Spalten löschen noch
blind den alten Writer starten. Restore muss Datenbank, Dateien, Nummernverlauf und
passenden Build gemeinsam berücksichtigen.

## Persistenz und Wiederherstellung

| Bestandteil | Konfigurierter Speicher |
| --- | --- |
| Konten, Sessions und fachliche Datensätze | PostgreSQL-Volume `postgres_data` unter `/var/lib/postgresql/data` |
| Gespeicherte PDF-Dateien und weitere Laufzeitdateien | Bind-Mount `./storage:/app/storage` |
| Konfiguration und erforderliche Geheimnisse | Geschützte, separate Ablage außerhalb des Repositorys |
| Passender Programmstand | Nachvollziehbarer Commit-/Image-Stand plus Migrationshistorie |

Ein Archiv von `storage/` allein sichert keine SQL-Daten. Ein SQL-Dump allein
sichert keine physischen PDFs. Ein ungeprüft kopiertes laufendes Datenbankvolume
ist kein nachgewiesen wiederherstellbares Backup.

Der noch zu belegende Restoretest muss auf einer separaten Installation mindestens
Schema/Migrationshistorie, Benutzeranmeldung, vorhandene Datensätze und Zuordnungen,
Kundennummernzähler sowie vorhandene PDF-Dateien prüfen. Sicherungszeitpunkt,
Werkzeugversion, Prüfergebnis und Wiederherstellungsdauer festhalten. Aufbewahrung,
Automatisierung und zulässiger Datenverlust sind für die konkrete Installation noch festzulegen.

## Lesende Kontrolle nach einem freigegebenen Start

```bash
docker compose ps
docker compose logs --tail=80 messpilot
docker compose exec -T messpilot wget -qO- http://127.0.0.1:3100/api/health
```

Logs vor Weitergabe auf sensible Inhalte prüfen. Ein erfolgreicher HTTP-Healthcheck
belegt nicht alle Fachabläufe oder ein aktuelles Schema. Zusätzlich die SQL-Anzeige
und den angemeldeten App-Ablauf prüfen. `npm run smoke:sql` schreibt Testdaten und
gehört ausschließlich in eine isolierte Testdatenbank.

Die App ist lokal unter `http://localhost:3100` erreichbar, sofern die Host-Freigabe
unverändert ist. Bei VPS/Coolify PostgreSQL intern erreichbar halten und den
Reverse Proxy mit HTTPS, Cookie-Konfiguration und Zugriffsschutz separat abnehmen.
Ein Dockerfile-Deployment benötigt eine eigens bereitgestellte PostgreSQL-Ressource
und persistente Dateispeicherung; das Image allein stellt beides nicht bereit.

## Verbliebene Altlasten und Grenzen

`docker-compose.local-sql.yml` ist ein altes Override: Es veröffentlicht PostgreSQL
auf Host-Port 5432 ohne explizite Loopback-Bindung und enthält wirkungslose alte
JSON-Bootstrap-Variablen. Es ist keine empfohlene Standardanleitung und wurde hier
nicht verändert. Eine lokale Testdatenbank ausdrücklich isolieren und ihre Erreichbarkeit prüfen.

Offen bleiben vollständige Browser-/SQL-/Fachabnahme, Backup/Restore des Bestands,
Lizenzdurchsetzung, API-/Rollen-/Sicherheitsprüfung und finale PDF-Abnahme.
Weitere Informationen: [Systemübersicht](SYSTEM_OVERVIEW.md), [API](API.md).
