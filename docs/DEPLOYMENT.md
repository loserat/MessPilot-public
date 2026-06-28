# Deployment

Diese Anleitung beschreibt den aktuellen Weg, MessPilot auf einem VPS oder Server online zu betreiben.

## Kurzantwort

Ja, MessPilot kann aktuell online auf einem Server laufen.

Der empfohlene Stand fuer jetzt:

- Docker Compose
- Port intern: `3100`
- persistenter Ordner: `./storage`
- Reverse Proxy davor, z. B. Nginx, Caddy, Traefik oder Coolify

## Voraussetzungen auf dem Server

- Linux-VPS oder vergleichbarer Server
- Docker
- Docker Compose Plugin
- Git
- Domain oder Subdomain, falls oeffentlich erreichbar

## Repository holen

```bash
git clone https://github.com/loserat/messpilot.git
cd messpilot
```

Optional `.env` anlegen:

```bash
cp .env.example .env
```

Standard:

```text
MESSPILOT_PORT=3100
```

## Start mit Docker

```bash
docker compose up -d --build
```

Status pruefen:

```bash
docker compose ps
docker compose logs --tail=80 messpilot
```

Healthcheck:

```bash
docker compose exec -T messpilot wget -qO- http://127.0.0.1:3100/api/health
```

## Zugriff

Ohne Reverse Proxy:

```text
http://SERVER-IP:3100
```

Mit Reverse Proxy:

```text
https://messpilot.example.tld
```

## Reverse Proxy Beispiel Nginx

Beispiel fuer eine Subdomain:

```nginx
server {
    listen 80;
    server_name messpilot.example.tld;

    location / {
        proxy_pass http://127.0.0.1:3100;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

TLS sollte danach ueber Certbot, Caddy, Traefik oder die Serverplattform eingerichtet werden.

## Coolify

Aktueller Stand ist Coolify-kompatibel:

- Build per `Dockerfile`
- Start per `docker-compose.yml`
- Port `3100`
- Volume fuer Persistenz: `./storage:/app/storage`
- Healthcheck: `/api/health`

Empfohlene Coolify-Einstellungen:

- Repository: `https://github.com/loserat/messpilot`
- Build Pack: Docker Compose oder Dockerfile
- Interner Port: `3100`
- Healthcheck Path: `/api/health`
- Persistenter Speicher: `/app/storage`
- Optionales Environment:

```text
PORT=3100
NODE_ENV=production
MESSPILOT_PORT=3100
```

Wichtig: In Coolify muss ein persistentes Volume fuer `/app/storage` gesetzt werden, damit angelegte Daten Container-Neustarts und neue Deployments ueberleben.

## Persistenz

MessPilot nutzt aktuell eine JSON-Datei:

```text
storage/demoStore.json
```

Diese Datei ist lokale Laufzeitpersistenz und wird nicht versioniert.

Sichern:

```bash
tar -czf messpilot-storage-backup.tar.gz storage
```

Wiederherstellen:

```bash
tar -xzf messpilot-storage-backup.tar.gz
docker compose restart messpilot
```

## Update auf dem Server

```bash
git pull
docker compose up -d --build
docker compose exec -T messpilot wget -qO- http://127.0.0.1:3100/api/health
```

## Synchronisierung zur öffentlichen Repository

MessPilot betreibt eine **private Development-Repo** und eine separate **öffentliche Community-Repo** für Issues und Releases.

### Automatische Synchronisierung

GitHub Actions synchronisiert automatisch diese Dateien:
- `CHANGELOG.md` — Release-Notizen
- `ROADMAP.md` — Öffentliche Feature-Roadmap
- `SECURITY.md` — Sicherheitsrichtlinien
- `THIRD_PARTY_NOTICES.md` — Lizenzhinweise zu Abhängigkeiten
- `docs/API.md` — API-Dokumentation
- `docs/DEPLOYMENT.md` — Diese Datei
- `docs/SYSTEM_OVERVIEW.md` — System- und Ablaufübersicht
- `LICENSE` — Lizenztext

**Trigger**:
- Bei jedem Push zu `main` (wenn obige Dateien ändern)
- Täglich Montags um 09:00 UTC (Schedule)
- Manuell via `workflow_dispatch`

### Setup der Synchronisierung

1. **Personal Access Token (PAT) erstellen**:
   - GitHub → Settings → Developer settings → Personal access tokens (Tokens classic)
   - Scope: `repo` (vollständiger Zugriff auf Repos)
   - Token kopieren

2. **Secret in privater Repo hinzufügen**:
   - Private Repo → Settings → Secrets and variables → Actions
   - New repository secret: `SYNC_REPO_TOKEN` = [dein PAT]

3. **Workflow testen**:
   ```bash
   # Manueller Trigger (GitHub Web UI)
   # Actions → "Sync to Public Repository" → "Run workflow" → Wähle "main" → "Run workflow"
   
   # Oder über CLI:
   gh workflow run sync-to-public.yml --ref main
   ```

4. **Logs prüfen**:
   - GitHub → Actions → "Sync to Public Repository"
   - Letzter Run sollte mit ✓ markiert sein

### Was wird NICHT synchronisiert

Diese sensiblen Inhalte bleiben privat:
- `src/` — Anwendungsquellcode
- `public/` — Frontend-Code
- `server.js` — Server-Konfiguration
- `.env*` — Umgebungsvariablen
- `docker-compose.yml`, `Dockerfile` — Deployment-Details
- `docs/daily/` — Interne Progress-Logs
- `docs/TECHNICAL.md`, `docs/BACKEND.md` — Interne Doku
- `storage/` — Datenspeicher und Demo-Daten

### Konfiguration anpassen

Die Sync-Konfiguration befindet sich in `.github/SYNC_CONFIG.json`:

```json
{
  "files": {
    "include": [ /* Dateien zum Sync'en */ ],
    "exclude": [ /* Dateien, die NICHT sync'd werden */ ]
  },
  "sync": {
    "targetRepo": "loserat/MessPilot-public",
    "trigger": {
      "onPush": true,
      "onSchedule": "0 9 * * 1",
      "onManualDispatch": true
    }
  }
}
```

---

## Aktuelle Grenzen fuer Online-Betrieb

MessPilot kann online laufen, ist aber noch keine produktiv abgesicherte Mehrbenutzer-Anwendung.

Noch offen:

- Authentifizierung und Rollen sind vorhanden, aber noch nicht produktiv gehaertet
- keine Mandantenfaehigkeit
- keine produktive Datenbank
- keine Backups innerhalb der App
- PDF-Vorschau ist vorhanden, aber noch keine finale Freigabe-/Serienexport-Funktion
- keine E-Mail-Funktion
- keine normativ freigegebenen Berechnungen

## Empfehlung fuer oeffentlichen Betrieb

Fuer Tests:

- Server per HTTPS absichern
- Zugriff falls moeglich zunaechst per VPN, Basic Auth oder IP-Whitelist begrenzen
- Startkonto `admin / admin` sofort aendern
- bei reinem HTTPS-Betrieb `COOKIE_SECURE=true` setzen
- `storage/` regelmaessig sichern

Fuer spaetere Produktivnutzung:

- gehaertete Authentifizierung mit Passwortregeln, CSRF-Schutz, Audit-Log und optional MFA
- PostgreSQL oder SQLite mit Repository-Schicht
- Migrationskonzept
- Backupkonzept
- feineres Rollen-/Rechtekonzept
- serverseitige Validierung der Fachlogik
