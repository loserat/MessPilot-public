# Security Policy

## Sicherheitspraktiken

MessPilot ist eine Anwendung zur Dokumentation von Elektro-Inspektionen und handhabt teilweise sensible Daten. Sicherheit ist uns wichtig.

### Reporting einer Sicherheitslücke

**Bitte melden Sie Sicherheitsprobleme NICHT als öffentliches Issue.**

Stattdessen nutzen Sie bitte den vertraulichen GitHub-Meldeweg, sobald er im Public-Repository aktiviert ist:

- Public Repo: https://github.com/loserat/MessPilot-public
- Bereich: `Security` > `Report a vulnerability`

Falls dieser Meldeweg noch nicht verfügbar ist, öffnen Sie bitte **kein öffentliches Detail-Issue**. Legen Sie stattdessen ein kurzes Issue ohne technische Details an und bitten Sie um einen vertraulichen Kontaktweg.

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

## Support & Versionierung

### Version Support Matrix

| Version | Status | Released | Support bis | Notes |
|---------|--------|----------|-------------|-------|
| 0.2.x   | 🟢 Aktiv | 2026-06-28 | 2026-12-31 | Aktuell empfohlen |
| 0.1.x   | 🟡 Legacy | 2026-06-01 | 2026-09-30 | Security Patches nur |
| 0.0.x   | 🔴 End-of-Life | - | 2026-03-31 | Nicht mehr unterstützt |

### Patch-Strategie

- **Bug-Fixes & Security Patches**: Werden als `0.2.1`, `0.2.2`, etc. released (Bugfix-Nummern)
- **Minor Features**: Werden als `0.3.0`, `0.4.0`, etc. released (Minor-Versionen)
- **Breaking Changes**: Werden als `1.0.0`, `2.0.0`, etc. released (Major-Versionen)
- **Release-Cadence**: Monatlich (1. Freitag des Monats) oder ad-hoc bei kritischen Patches

### Sicherheits-Updates

- **Kritisch** (CVSS 9.0+): Innerhalb von 24-48 Stunden gepatched
- **Hoch** (CVSS 7.0-8.9): Innerhalb von 1 Woche gepatched
- **Mittel** (CVSS 4.0-6.9): Mit nächstem Release gepatched
- **Niedrig** (CVSS < 4.0): Mit zukünftigen Releases adressiert

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

- **Security**: Vertrauliche Meldung über `Security` > `Report a vulnerability` im Public Repo, sobald aktiviert
- **Issues/Bugs**: https://github.com/loserat/MessPilot-public/issues
- **Diskussionen**: https://github.com/loserat/MessPilot-public/discussions

---

**Letzte Aktualisierung**: 28. Juni 2026
