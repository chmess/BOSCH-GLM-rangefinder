# Entwicklungsroadmap

1. **Software-Simulator**: Plottergeometrie, erlaubter Zeichenbereich, Seil-zu-Motorschritt-Umrechnung, Stiftversätze, SVG-Vorschau, Testmuster, automatisierte Tests. Kein mechanischer Aufbau erforderlich.
2. **Mega/RAMPS-Anbindung**: tatsächliche Treiber und Firmware klären; serielles Protokoll mit Acknowledgements, Limits, Pause/Stop, sicheren Startbedingungen; zunächst ein Stift.
3. **Offline-Zeichenpipeline**: Bilder -> Konturen, Schraffuren, Farb-/Stiftauswahl, Detailstufe, geschätzte Dauer; unterstützt Raspberry und später Android.
4. **Mehrstift-Kopf**: Servo-/Leerlaufwinkel, Stiftversätze und Kalibrierung, Prüfung sicherer Pen-Up-Fahrten.
5. **Kamera-Kalibrierung**: Papiervermessung, gelerntes Fehlerfeld/Parameter, Persistenz, später Kamera abziehen und offline zeichnen.
6. **Fotobox**: zwei Knöpfe lokal/Online-KI, lokale Bildfilter, Onlineprovider nur opt-in, Datenschutz und Aufnahmelöschung.
7. **Papierrolle und Aktenvernichter**: einziehendes Vorschubmodul mit Weg-/Stausensor, Präsentationszeit und separat überprüfter Sicherheit.
8. **Zweiter Host Android**: Redmi Note 9 Pro über USB-C-OTG -> USB-Kabel -> Mega. Native USB-Serial-Bridge mit Android USB Host API (z. B. usb-serial-for-android), eigenständige App oder Hybridoberfläche; USB-Reconnect, Stromversorgung und Hintergrundbetrieb testen.

Reihenfolge 3/5/8 bei Bedarf ändern; Abhängigkeiten klar dokumentieren. Kein Zwang zu Tests mit echten Würfeln — gehört zu einem anderen Projekt.

## Prioritätsänderung (09.11.2026)
**Android zuerst**, Raspberry Pi 3 als optionaler weiterer Host. Phase 1 Simulator und Phase 2 Hardware-Schnittstelle sollen deshalb bereits auf Android zielen; die frühere Phase 8 wird nach vorn gezogen. Referenz: Redmi Note 9 Pro, jedoch kein herstellerspezifischer Zwang. Kein Root/Bootloader-Unlock erforderlich. Native Android USB-Host/Serial-Anbindung; Arduino übernimmt deterministisches Motion-Timing. Test ohne angeschlossene Hardware über Simulationsmodus. Keine Motorsteuerung allein über WebSerial voraussetzen.

## Firmware-Festlegung (09.11.2026)
**Marlin 2.1.2.9** ist die bevorzugte Ziel-Firmware für Mega 2560 + RAMPS 1.4. Phase 2 beginnt mit Verifikation des richtigen Marlin-Quellstandes und der Polargraph-Konfigurationsoptionen, dann Erstellen einer minimalen reproduzierbaren Firmwarekonfiguration und zunächst einem **Compile-/Speichercheck ohne angeschlossene Motoren**. Anschließend serielles G-Code-Protokoll und virtuelle Simulation testen. Erst nach Sicherheitsprüfung Hardwarebewegung und Servo-Mehrstiftsteuerung freigeben. Falls Build oder benötigte Funktionen auf dem 8-Bit-Mega nicht sinnvoll zusammenpassen, dokumentiert Codex die Gründe und vergleicht Alternativen, statt stillschweigend die Firmware zu wechseln.
