# Roadmap MessPilot

Die öffentliche Roadmap zeigt geplante Features, Status quo und künftige Richtung von MessPilot.

**Status:** Aktive Entwicklung (Beta Phase 0.6.x)  
**Hinweis:** Diese Roadmap ist unverbindlich. Interne Deadlines und Kundenspezifisches werden nicht öffentlich geteilt.

---

## Kurzfristig (Q3-Q4 2026)

### Kritisch
- [ ] **Produktive Persistierung** — PostgreSQL als fuehrende Datenbank fuer lokale Docker-/Server-Installationen
- [ ] **Docker-Kundenbetrieb** — MessPilot so betreiben, dass ein Kunde die App lokal auf eigenem Docker-Host mit persistentem Volume/SQL starten kann
- [ ] **Auth-Hardening** — CSRF-Schutz, Session-Haertung, Passwortregeln, Audit-Log
- [ ] **Backup-/Restore-Konzept** — Datenbank, PDF-Storage und Konfiguration reproduzierbar sichern und wiederherstellen

### Wichtig
- [ ] **Lizenzvorbereitung** — Lizenzschluessel technisch vorbereiten, aber noch nicht produktiv erzwingen
- [ ] **Feature-Gates vorbereiten** — z. B. freie Nutzung bis 2 Kunden, PDF-Wasserzeichen entfernen, erweiterte Benutzer/Rollen nur mit gueltiger Lizenz
- [ ] **Rollenmodell schaerfen** — Systemadmin, Admin, Pruefer, Sachbearbeitung, Viewer und spaeter ggf. Kunde/Auditor sauber trennen
- [ ] **Updatefaehigkeit** — Versionscheck, Updatehinweise und dokumentierter Docker-Updatebefehl
- [ ] **Frontend Modularisierung** — `app.js` aufteilen in dedizierte Module
- [ ] **Fehlerbehandlung** — Konsistente Client- und Server-Side Validierung
- [ ] **API-Docs** — OpenAPI/Swagger Integration
- [ ] **Benutzer-Doku** — Screenshots, Video-Tutorials, Admin-Leitfaden

---

## Mittelfristig (H1 2027)

### In Prüfung
- [ ] **Lizenzverwaltung** — Offline-faehiger Lizenzschluessel, Aktivierungsstatus, Ablaufdatum, Edition und Featureumfang
- [ ] **Mandanten-/Kundengrenzen** — lokale Einzelinstallation zuerst; spaeter optional echte Multi-Tenant-Instanz
- [ ] **Audit- und Revisionsansicht** — wer hat wann Kunden, Objekte, Messwerte, PDFs und Benutzer geaendert
- [ ] **Migrationen** — wiederholbare SQL-Migrationen mit Updatepfad von jeder freigegebenen Beta-/Release-Version
- [ ] **OAuth2 / SSO** — Google, Nextcloud, etc.
- [ ] **LDAP/AD** — Enterprise-Authentifizierung
- [ ] **Import/Export** — CSV, XLS, JSON für Stammdaten
- [ ] **Mehrsprachigkeit** — DE, EN, ggf. weitere Sprachen
- [ ] **Mobile-Support** — Responsive Design, Touch-Optimierung

---

## Längerfristig (2027+)

### Erweiterte Funktionen
- [ ] **Progressive Web App (PWA)** — Offline-Nutzung, Installierbar
- [ ] **Mobile App** — Native iOS/Android Apps
- [ ] **Barcode/QR-Scanner** — Für Ort- und System-Erfassung
- [ ] **Webhooks** — Externe System-Integration
- [ ] **Email-Notifications** — Status-Updates via Mail

### Advanced Analytics
- [ ] **Inspektions-Dashboard** — Statistiken, Trends, Forecasts
- [ ] **Wartungs-Planung** — Automatische Wartungsintervalle
- [ ] **Compliance-Reports** — SLA-Tracking, Audit-Trails

### Skalierung
- [ ] **Multi-Tenant** — Mehrere Organisationen in einer zentralen Instance, erst nach stabiler Einzelkundeninstallation
- [ ] **Redis-Caching** — Performance bei hohem Traffic
- [ ] **Database Sharding** — Große Datenmengen verteilen

---

## Fernzukunft (Evaluierung)

Folgende Technologien/Konzepte werden künftig evaluiert:

- **Machine Learning** — Wartungsvorhersagen, Anomalie-Erkennung
- **GIS/Mapping** — Geografische Visualisierung, Lageplanung
- **IoT Integration** — Temperatur-, Feuchte-, Bewegungs-Sensoren
- **Blockchain** — Revisionssicherheit, Tamper-Protection

---

## Lizenz- und Editionen-Zielbild

MessPilot soll langfristig sowohl als lokale Docker-Installation beim Kunden als auch auf einem eigenen Server betreibbar sein.

Geplante technische Vorbereitung:

- lokale SQL-Datenbank dort, wo Docker laeuft
- Lizenzstatus in der Adminkonsole sichtbar
- Lizenzschluessel optional offline pruefbar
- Feature-Gates zentral im Backend, nicht nur im Frontend
- PDF-Wasserzeichen ueber Lizenzstatus steuerbar
- Kundenlimit als Beispiel: ohne Lizenz maximal 2 Kunden, mit Lizenz frei oder editionabhaengig
- Updatepfad ueber Versioncheck und dokumentierten Docker-Updatebefehl

Hinweis: Die aktuelle Projektlizenz ist MIT. Ein spaeteres kommerzielles Lizenz-/Editionenmodell muss vor produktiver Verteilung rechtlich und organisatorisch sauber entschieden werden.

---

## Feedback & Voting

**Du hast eine Idee?** Teile sie in der öffentlichen Repo:

**[MessPilot-public Issues](https://github.com/loserat/MessPilot-public/issues)**

Du kannst:
- Bugs melden
- Feature-Anfragen stellen
- In Diskussionen teilnehmen
- Votes auf existierende Issues geben

---

**Letzte Aktualisierung:** 3. Juli 2026  
**Status:** Beta (v0.6.x)  
**Community-Repo:** https://github.com/loserat/MessPilot-public
