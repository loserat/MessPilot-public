# Roadmap MessPilot

Die Roadmap beschreibt den aktuellen Entwicklungsfokus von MessPilot. Sie ist unverbindlich und wird nach den Ergebnissen der manuellen Prüfungen aktualisiert.

**Stand:** 22. Juli 2026  
**Version:** 0.7.9  
**Phase:** Beta / Stabilisierung

## Aktueller Fokus

### IBN-Protokolle abschliessen

- Gefuehrten Ablauf fuer SiBe-, BMA- und RWA-Inbetriebnahmen manuell abnehmen
- Status und Fortschritt bei Entwurf, Unterbrechung und Abschluss vereinheitlichen
- Wiederholungspruefungen mit Vorwerten pruefen
- PDF-Vorschau und PDF-Export fachlich und optisch an die bestehenden Protokolle angleichen
- Anlagenbezogene Pflicht- und optionale Messwerte sauber pruefen

### Gesamtanwendung stabilisieren

- Rollen, Rechte und Sichtbarkeit der Aktionen abschliessend pruefen
- Protokoll-, Anlagen-, Benutzer-, Pruefer- und Geraete-CRUD pruefen
- SQL-Persistenz lokal und auf dem Server bestaetigen
- Dialoge, Navigation, Login/Logout und Sessionwechsel manuell pruefen
- Audit-Logs fuer relevante Aenderungen nachvollziehbar kontrollieren

### Betrieb vorbereiten

- PostgreSQL-Backup und Restore dokumentieren
- Docker-/Coolify-Updateablauf dokumentieren
- Dauerhafte Speicherung von PDFs, Logos und Unterschriften absichern
- Website-Admin und Besucherstatistiken nach Redeploy bestaetigen

## Naechster Fachausbau

### Anlagenpruefungen

- SiBe-Jahres- und Wartungspruefung als eigener gefuehrter Ablauf
- BMA-Pruefablauf fachlich erweitern
- RWA-Wartungspruefung mit Funktions- und Messwerten ausbauen
- Maengel, Nachpruefungen und Pruefserien verknuepfen
- Anlagen-Snapshots in Folgepruefungen unveraendert erhalten

### Protokoll- und PDF-Ausbau

- Einheitliche Seitenkoepfe fuer alle Protokollarten
- Fachliche deutsche Bezeichnungen in allen Exporten
- Einheitliche Firmenlogo-, Unterschriften- und Statusdarstellung
- PDF-Seitenumbrueche und Tabellenbreiten weiter manuell abnehmen

## Vorbereitet, aber bewusst lokal / Beta

### Verteiler v2 und BSV

- Node- und Flow-Editor weiter als lokale Beta entwickeln
- BSV-Produktdatenbank mit belastbaren Vorlagen vervollstaendigen
- Baumansicht, Stromkreisstruktur und technische Details verbessern
- Flow-v2-Speichern, Verwerfen, Zuruecksetzen und Reload pruefen
- `layout.rows` und den alten Verteilereditor unveraendert erhalten
- Keine automatische Stromkreisuebernahme ohne belastbares Mapping
- Keine Schutzberechnung oder normative Freigabe aus dem Flow ableiten
- Verteiler v2 und BSV vorerst nicht als produktives Online-Modul freischalten

## Technische Grundlagen

- PostgreSQL bleibt der fuehrende Datenpfad
- Docker und Coolify bleiben die vorgesehenen Betriebswege
- Rollen und Feature-Gates werden serverseitig abgesichert
- SQL-Smoke-Checks bleiben Bestandteil der Deployment-Pruefung
- Refactoring erfolgt nur bei klarer fachlicher Verantwortung oder nachgewiesenem Fehler
- `styles.css` bleibt bis zu einem eigenen visuellen Testblock unangetastet

## Spaeter

- Serverseitige Lizenzpruefung und Premiumfunktionen
- Backup-/Restore-Automatisierung
- API-Dokumentation und stabiler Import/Export
- Mobile und Tablet-Optimierung ueber die bestehende Responsive-Basis hinaus
- PWA- oder Offline-Unterstuetzung
- QR-/Barcode-Erfassung
- Externe Integrationen und Webhooks
- Erweiterte Statistik- und Wartungsplanung

## Nicht Bestandteil der aktuellen Beta-Abnahme

- Automatisches Update oder Deployment aus der App heraus
- Produktive Lizenzserver- oder GM-Core-Anbindung
- Automatische Normkonformitaets- oder Freigabeaussagen
- Vollstaendige BSV-Katalogabdeckung ohne belastbare Quelldaten
- Oeffentliche Online-Freischaltung des Verteiler-v2-Editors

## Naechster Meilenstein

Die naechste Roadmap-Aktualisierung erfolgt nach der manuellen Pruefrunde. Erst danach werden abgeschlossene Punkte aus der Stabilisierung entfernt und neue Fachmodule priorisiert.

**Community-Repo:** https://github.com/loserat/MessPilot-public
