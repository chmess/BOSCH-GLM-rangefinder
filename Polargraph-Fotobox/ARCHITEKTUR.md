# Architektur — Host-unabhängiger Polargraph

## Schichten
1. **Gemeinsamer Kern (hostneutral)**: Motorabstände, Arbeitsraum, Polargraph-Kinematik (XY zu effektiven Seillängen), Spulenmodell, Stiftversätze, Pfad- und Schraffurplanung, Farbseparation, Kalibrierparameter, Vorschau und Profile.
2. **Motion-Controller**: Arduino Mega 2560 + RAMPS 1.4, geeignete noch auszuwählende Firmware. Empfängt geordnete Bewegungsbefehle mit Quittierung, verfolgt Zustände und steuert Step/Dir mit verlässlichem Timing. Standard-GRBL allein nicht ungeprüft als fertige Polargraph-Firmware voraussetzen.
3. **Host Raspberry Pi 3**: lokale Weboberfläche, Python/OpenCV, Kamera, Lern-/Optimierungsmodule, USB-Serial und optionale Cloudfilter.
4. **Host Android**: alternative Steuerzentrale (z. B. Redmi Note 9 Pro). USB-OTG zum Mega; nativer Android-USB-Host und Serial-Treiber für verlässliche Kommunikation; optional Web-UI/Capacitor. Browser-WebSerial/WebUSB nur nach Gerätetest, nicht als garantierte Schnittstelle.
5. **Simulation**: identisches abstraktes Motion-Interface als Simulator ohne echte Hardware.

## Kameraverwendung und Lernen
- Lernmodus: Kamera auf Papier, 4-Punkt-Perspektivkalibrierung, Punktraster, ortsabhängige Abweichungen messen, Korrekturparameter speichern. Strukturelle Geometrie und gemessene Restfehler getrennt halten.
- Optimierungsmodus: Kamera erkennt gezeichneten Fortschritt, kann zusätzliche Linien/Schraffuren vorschlagen. Bereits aufgetragenes Material ist nicht entfernbar.
- Autonommodus: ohne Kamera, aus vorhandenen Profilen. Mechanische Fehler/unterbrochene Striche können dann nicht visuell entdeckt werden.
- Fotoboxmodus: Kamera auf Menschen, Aufnahme nur nach Tastendruck. Für Rückblick auf Papier ist mechanisches Drehen oder zweite Kamera nötig.

## Zwei-Tasten-Logik und Datenschutz
- **Taste A: Lokal**: angekündigte Fotoaufnahme, lokale Verarbeitung und lokale Zeichnung ohne Cloud.
- **Taste B: Online-KI**: nur bei Onlineverbindung und konfiguriertem Anbieter; externe Fotoübermittlung erst nach gesonderter informierter Einwilligung. Kein versteckter Upload, klare Löschung und Abbruchmöglichkeit. Knopfdruck allein ersetzt nicht alle Datenschutzanforderungen.
- Kein automatisches Aufnehmen zufälliger Passanten, keine Identitätsbestimmung. Für Minderjährige und öffentliche Nutzung gesonderte Schutzmaßnahmen prüfen.
- Lokale Filter: Konturen, Schraffur, Kontrast, Farbquantisierung, witzige Accessoires. Online optional Comic-/Cartoon-Stilisierung über austauschbaren Anbieter, keine Annahme eines dauerhaft kostenlosen Dienstes.

## Stift und Papier
- Werkzeugprofile für 3/optional 4 Stifte: Servo-Winkel für Aktivierung und nahe Leerlaufposition; X/Y-Offset; optionale Muster zur optischen Kalibrierung.
- Beim Wechsel von weit entfernten Stiften darf der Bewegungsplaner erst nach sicherem Pen-Up fahren. Zwischenliegende Stifte können beim Drehen kurz berührt werden; Farbwechsel nur bei stillstehenden Motoren, Mechanik gegen unbeabsichtigte Striche validieren.
- Papiertransporteinheit: optionaler fertiger Aktenvernichter als Förderer und Vernichter, nach Zeichenende und Präsentationszeit. Wegsensor und Papierstauerkennung erforderlich. Netzspannung und Schutzschalter des Geräts nicht unsachgemäß verändern; nur sicher gestaltete Schaltlösung.
- Not-Aus und Grenzen unabhängig von Host-Software, Schutz vor Neustart nach Verbindungsabbruch, Unterspannung und unbeaufsichtigtem Betrieb.

## Auslegung
- Erst Flipchart, später Wandprofile. Motorabstand/-höhe, Seiltyp, Spulenradius, Wickellagen, Kopfmasse, Stifte und Arbeitsbereich konfigurierbar.
- Bei Fassaden: neue Mechanik- und Sicherheitsprüfung (Wind, Absturz, Befestigungen, Publikum).
- Speichern: versionierte Werkzeug-, Kamera-, Mechanik- und Zeichenstilprofile, ohne persönliche Aufnahmen im Git-Repository.
