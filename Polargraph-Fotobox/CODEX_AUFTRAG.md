# Codex — Phase 0: Architektur und Simulator

Repository: `chmess/BOSCH-GLM-rangefinder`, Arbeitsverzeichnis **ausschließlich `Polargraph-Fotobox/`**. Bestehende Bosch- und Kniffel-Dateien unverändert lassen.

## Aufgabe
- Erstelle ein Pi-3-taugliches, offlinefähiges, modular getestetes Grundprojekt (Python für Host/Simulator ist zunächst sinnvoll) ohne voreilige Festlegung auf die Controller-Firmware.
- Definiere Schnittstellen zwischen Bild-/Pfadplanung, Kinematik/Kalibrierung, Stift-/Papiergeräten, Kamera, USB-Serial und Simulator.
- Implementiere einen **virtuellen Polargraphen**: konfigurierbare Motorpositionen, Arbeitsraum, effiziente Seillängenberechnung und reversible XY-Transformation, Stiftversätze, Sicherheitsbereich; visualisiere erzeugte Zeichenpfade und Seillängen.
- Zeichne ein Testbild per einfachen Konturen/Schraffuren (SVG-Vorschau und simulierte Bewegungen), inklusive automatisierter Tests der Geometrie und Profilpersistenz. Noch keine ungetestete reale Motor-/Schredder-Steuerung.
- Halte den Kern unabhängig vom Host, sodass eine Android-Integration später möglich ist. Dokumentiere USB-OTG als Option, nicht als bereits getestet.
- Dokumentiere Installation/Start ohne Spezialhardware sowie offene Hardware-/Firmwarefragen. Benenne ehrlich, was simuliert oder nicht geprüft ist.

## Weitere Leitlinien
- Drei Stifte initial, vier optional; ein Servo mit Nockenscheibe und Zwischenstellungen.
- Kalibrier-/Zeichenprofile für Flipchart; spätere Hauswand erfordert Reprofilierung.
- Zwei-Tasten-Fotobox, lokale Verarbeitung versus bewusste Online-KI-Verarbeitung.
- Keine hochgeladenen Besucherfotos, API-Schlüssel, persönlichen Daten oder sensiblen Messdaten ins öffentliche Repository.
- Sicherheitsrelevante echte Bewegung erst nach separat geprüften Endlagen und Not-Aus.
