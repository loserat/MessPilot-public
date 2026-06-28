# Security Policy

## Sicherheitspraktiken

MessPilot ist eine Anwendung zur Dokumentation von Elektro-Inspektionen und handhabt teilweise sensible Daten. Sicherheit ist uns wichtig.

### Reporting einer Sicherheitslücke

**Bitte melden Sie Sicherheitsprobleme NICHT als öffentliches Issue.**

Statt dessen kontaktieren Sie uns vertraulich:

📧 **Email**: `security@messpilot.local` (wird weitergeleitet)

**Oder via GitHub Private Security Vulnerability Report:**
- Navigieren Sie zur privaten Repo: https://github.com/loserat/messpilot
- Gehen Sie zu „Security" > „Report a vulnerability"
- Folgen Sie der Anleitung

---

## Verantwortungsvolle Offenlegung

Wir verpflichten uns:

1. ✅ **Schnelle Bearbeitung**: Sicherheitsberichte werden innerhalb von **48 Stunden** bestätigt
2. ✅ **Transparente Kommunikation**: Regelmäßige Updates während der Behebung
3. ✅ **Koordinierte Veröffentlichung**: Patches werden vorbereitet, bevor die Lücke publik wird
4. ✅ **Anerkennung**: Sicherheitsforschern wird (auf Wunsch) Anerkennung zuteil

---

## Sicherheitsstandards

### Datenhandhabung

- ✓ Alle sensiblen Daten sind verschlüsselt (in Transit via TLS 1.2+)
- ✓ Passwörter werden mit bcrypt gehashed (min. 10 Runden)
- ✓ Sessions haben Timeout (konfig. über `SESSION_TIMEOUT`)
- ✓ Demo-Modus enthält **keine echten Kundendaten**

### API-Sicherheit

- ✓ CORS konfiguriert für vertrauenswürdige Origins
- ✓ Input-Validierung auf allen Endpoints
- ✓ Rollenbasierte Zugriffskontrolle (RBAC)
- ✓ Rate-Limiting (in Prüfung)

### Abhängigkeiten

- ✓ Regelmäßige `npm audit` Checks
- ✓ Automatische Updates für kritische Patches
- ✓ Verwendung von pinned Versions in `package-lock.json`

### Deployment

- ✓ Docker-Container mit minimalen Permissions
- ✓ Environment-Variablen für Secrets (keine `.env` im Repo)
- ✓ Regelmäßige Backup-Tests

---

## Bekannte Limitationen

Diese Limitationen bestehen und sollten bei der Nutzung beachtet werden:

- **Beta-Status**: MessPilot befindet sich in aktivem Development. Verwenden Sie es nicht in produktiven Umgebungen mit echten Kundendaten, ohne gründliche Tests.
- **Keine Verschlüsselung auf Disk**: Demo-Datenspeicher (JSON) ist unverschlüsselt. Für sensible Daten verwenden Sie PostgreSQL mit Verschlüsselung.
- **Einfaches Auth-System**: Session-basiert, keine 2FA (für 0.2.x). OAuth2 ist geplant.

---

## Compliance & Datenschutz

Abhängig von Ihrem Einsatzland:

- **DSGVO (EU)**: Datenminimierung, Consent-Management, Recht auf Vergessenwerden
- **Lokale Regulierungen**: Zu prüfen basierend auf Deployment-Region

Siehe `docs/DEPLOYMENT.md` für Konfigurationsoptionen.

---

## Versionierung & Patches

| Version | Status | Support bis |
|---------|--------|------------|
| 0.2.x   | 🟢 Aktiv | 2026-12-31 |
| 0.1.x   | 🟡 Legacy | 2026-09-30 |

Patches werden als `0.2.1`, `0.2.2`, etc. released.

---

## Security Checklist für Deployer

Vor der Produktivnutzung:

- [ ] `.env` Datei mit sicheren Secrets erstellt
- [ ] TLS/HTTPS auf dem Loadbalancer konfiguriert
- [ ] Datenbank-Backup-Strategie definiert
- [ ] Regelmäßige Security Updates einplanen (`npm audit`)
- [ ] Firewall-Regeln: Nur notwendige Ports offen (3100 für App, optional 5432 für DB)
- [ ] Logging & Monitoring eingerichtet
- [ ] Incident Response Plan vorhanden

---

## Kontakt

- **Security**: `security@messpilot.local`
- **Issues/Bugs**: https://github.com/loserat/MessPilot-public/issues
- **Diskussionen**: https://github.com/loserat/MessPilot-public/discussions

---

**Letzte Aktualisierung**: 28. Juni 2026
