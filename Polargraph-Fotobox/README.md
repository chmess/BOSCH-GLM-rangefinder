# Polargraph-Fotobox
Eigenständiges Projekt für einen selbstoptimierenden, modularen Wandplotter mit Fotobox, Foto-zu-Zeichnung und Papierrolle. Projektordner im bestehenden öffentlichen Repository; Bosch- und Kniffel-Dateien unverändert lassen.

## Hardware und Vision
- Zwei Schrittmotoren an oberen Wandpositionen, hängender Zeichenkopf (Polargraph). Vorhanden bzw. in Schublade: Raspberry Pi 3, vermutlich Arduino Mega 2560 und RAMPS 1.4; noch keine Firmware. Erster Test am Flipchart, später größere Wände.
- Mehrere Stifte: zunächst drei, optional vier; federnd gelagert im Halbkreis. Ein Servo mit Nockenhebel/-scheibe wählt einen Stift; Leerlaufwinkel heben alle Stifte an. Pro Stift Winkel und geometrischer Versatz. Mechanische Konstruktion durch Nutzer.
- Vereinfachte gegenständliche Zeichnungen statt Fotorealismus oder Abstraktion: klare Konturen, leichte Schraffur, Detailgrad einstellbar, Vorschau vor dem Zeichnen.
- Kamera zum Einlernen der Geometrie und Prüfen gezeichneter Linien; anschließend offline **auch ohne Kamera** nutzbar mit gespeicherten Kalibrierprofilen und Zeichenstrategien.
- Kamera alternativ auf eine Person richten. Zwei Taster: **Lokalporträt** und **Online-KI-Stil**. Online-KI nur bei Verbindung, eingerichteter Schnittstelle und klarer informierter Zustimmung; lokaler Modus immer verfügbar.
- Papierrolle mit optional fertig gekauftem Aktenvernichter unten: Einzug/Vernichtung nach Präsentationszeit. Andere Module (Aufwickeln/Mitnehmen) später möglich. Sicherheitsschalter erhalten, Einzug gekapselt, Papierweg überwacht.
- **Steuerrechner austauschbar:** Raspberry Pi 3 oder Android-Handy (z. B. Redmi Note 9 Pro) per USB-OTG zum Arduino Mega/RAMPS. Bildverarbeitung und Benutzeroberfläche auf dem Host, harte Bewegungszeitsteuerung auf dem Mikrocontroller.

## Unterlagen
- [ARCHITEKTUR.md](ARCHITEKTUR.md): Modulgrenzen, Datenschutz, Sicherheits- und Funktionslogik
- [ROADMAP.md](ROADMAP.md): Entwicklungsstufen
- [CODEX_AUFTRAG.md](CODEX_AUFTRAG.md): erster konkreter Entwicklungsauftrag

**Status:** Konzept, kein ausführbares Projekt und keine getestete Firmware.

## Plattformentscheidung (09.11.2026)
**Android ist die bevorzugte Steuerzentrale.** Das Redmi Note 9 Pro ist Referenzgerät, andere Android-Handys sollen ebenfalls laufen. Raspberry Pi 3 bleibt als späterer Alternativhost. **Kein Root und kein entsperrter Bootloader notwendig** für reguläre Kamera-/USB-Host-APIs. USB-OTG über USB-C zu Arduino Mega/RAMPS; genaue Treiber-/Adapterkompatibilität wird später praktisch geprüft. Echtzeit-Schrittmotorsteuerung bleibt auf dem Mega; das Telefon plant und übermittelt Befehle. Android-App möglichst schlank; modularer wiederverwendbarer Algorithmuskern. Ladebetrieb bei OTG und Hintergrund-/Thermoverhalten prüfen.
