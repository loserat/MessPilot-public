# Roadmap MessPilot

Dies ist die öffentliche Roadmap für MessPilot. Sie zeigt geplante Funktionen, Themen in Prüfung und später vorgesehene Erweiterungen.

**Hinweis**: Diese Roadmap ist unverbindlich und unterliegt Änderungen. Interne Deadlines und kundenspezifische Anforderungen werden hier nicht veröffentlicht.

---

## 🚀 Nächste Schritte (Q3 2026)

### Backend & Persistierung
- [ ] Migration zu PostgreSQL / SQLite für produktive Deployments
- [ ] Datenbankschema für alle Entitäten (Kunden, Liegenschaften, Gebäude, Räume, Systeme, Messungen, Defekte)
- [ ] Backup & Recovery Mechanismen
- [ ] API-Dokumentation mit OpenAPI/Swagger

### Frontend Modularisierung
- [ ] Aufteilung von `app.js` in dedizierte Module (Helpers, Renderer, Event-Handler)
- [ ] Bessere Fehlerbehandlung und Validierung
- [ ] Performance-Optimierung (Lazy Loading, Caching)

### Dokumentation
- [ ] Benutzerhandbuch mit Screenshots und Video-Tutorials
- [ ] Administratoren-Leitfaden
- [ ] API-Referenz (OpenAPI/Swagger)

---

## 🔄 In Prüfung

### Authentifizierung & Berechtigungen
- OAuth2 / Single-Sign-On (SSO) Integration
- LDAP/Active-Directory Support
- Audit-Logging für Änderungen

### Datenimport/-export
- CSV-Import für Stammdaten
- XLS-Export für Berichte
- JSON-API für externe Systeme

### Erweiterte Messfunktionen
- Protofile Verwaltung (Mehrere Messprotokolle parallel)
- Historische Daten & Trend-Analyse
- Export zu externen Systemen (ERP, CMS)

---

## 🎯 Geplant (H2 2026 / 2027)

### Mobile Support
- Responsive Design für Tablets
- Progressive Web App (PWA) für Offline-Nutzung
- Barcode/QR-Code Scanner für Orte/Systeme

### Erweiterte Reports
- Inspektions-Dashboard mit Statistiken
- Prognose für Wartungsintervalle
- SLA-Tracking und Compliance-Reports

### Integration & API
- Webhook-Support für externe Systeme
- Kalender-Integration (ICS/CalDAV)
- Email-Notifications

### Performance & Skalierung
- Datenbankindexierung und Query-Optimierung
- Caching-Layer (Redis)
- Multi-Tenant Support

---

## 💡 Überlegungen (zukünftig)

Folgende Themen werden evaluiert:

- Machine Learning für Vorhersage von Wartungsbedarfen
- GIS-Integration für geografische Visualisierung
- IoT-Sensor Integration (Temperatur, Luftfeuchte, etc.)
- Blockchain für Audit-Trail Unverbrüchlichkeit

---

## Feedback & Voting

Sie können auf geplante Features **abstimmen** oder neue Ideen in der **Public-Repo** einreichen:

👉 https://github.com/loserat/MessPilot-public/issues

---

**Letzte Aktualisierung**: 28. Juni 2026
