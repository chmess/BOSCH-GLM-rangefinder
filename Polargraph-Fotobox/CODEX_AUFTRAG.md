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

## Geänderter Implementierungsauftrag (09.11.2026; gilt vorrangig)
**Primäre App-Plattform: Android**, Referenz Redmi Note 9 Pro, kompatibel mit weiteren Android-Geräten. Bitte keinen ausschließlich auf Raspberry Pi ausgerichteten Prototyp als Hauptanwendung bauen. Zuerst Android-App mit Simulator, Zeichenpfadvorschau und modularer Polargraph-Kinematik entwickeln. Native USB-OTG/USB-Serial-Integration zur Mega-2560-/RAMPS-Hardware als getrennte, zunächst simulierte Schnittstelle planen; Firmware vor realen Motorversuchen festlegen. Root oder Bootloader-Entsperrung ist keine Voraussetzung. Pi-3-Host ist optional; Kernlogik nach Möglichkeit plattformneutral halten. Erst ohne Hardware vollständigen Zeichnungsablauf demonstrieren und testen.
