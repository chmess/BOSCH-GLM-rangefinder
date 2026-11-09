# Marlin 2.1.2.9 – Polargraph / RAMPS 1.4 (Phase 0)

**Status:** vorläufige Konfigurationsvorlage, **NICHT kompiliert oder hardwaregetestet**. Keine Motoren ansteuern, bevor Treiber, Strom, Drehrichtung, Mechanik und sichere Startposition geprüft sind.

## Ziel
- Host: Android (Redmi Note 9 Pro als Referenz), USB-OTG -> USB des Arduino Mega 2560.
- Arduino Mega 2560 + RAMPS 1.4, Marlin **Tag 2.1.2.9**.
- Zwei Seilmotoren auf X/Y; ein Servo auf SERVO0 für drei Stifte + Parkposition.
- Polargraph-Kinematik in **Marlin**, Kalibrierung und G-Code-Vorbereitung auf Android.
- Vorläufig **kein** Schredder-Ausgang in Marlin; dessen sichere Ansteuerung ist ein separates System.

## Änderungsplan in Marlin/Configuration.h (aus dem exakt passenden Release-Tag)
Die Zeilen sind **Änderungsvorgaben, keine vollständige eigenständige Configuration.h**.

```cpp
#define MOTHERBOARD BOARD_RAMPS_14_EFB
#define SERIAL_PORT 0
#define BAUDRATE 115200

#define POLARGRAPH
#define POLARGRAPH_MAX_BELT_LEN 1035.0  // NUR Platzhalter; vor Mechaniktest bestimmen
#define DEFAULT_SEGMENTS_PER_SECOND 5  // zunächst konservativ, Performance prüfen

#define NUM_SERVOS 1
#define SERVO_DELAY { 300 }
```

**Unbedingt gegen den Quellstand prüfen:** Exakte Abschnittspositionen, mögliche abweichende Defines und Konflikte mit `PEN_UP_DOWN_MENU`, `Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN`, Servo-, Z- und Temperaturoptionen. Marlin hat eigene bedingte Konfigurationen und Sanity-Checks; Definitionszeilen nicht blind mehrfach hinzufügen.

## Weitere Konfigurationsziele
- `EXTRUDERS 0`, keine Heiz-/Temperaturfunktionen oder Displays für die reale Anwendung; erforderliche `TEMP_SENSOR_*`-Werte auf 0, sofern im Tag/Build zulässig.
- `X_DRIVER_TYPE` und `Y_DRIVER_TYPE` zunächst nur nach Identifikation der tatsächlichen Treiberchips (A4988 / DRV8825) setzen. Keine Ratewerte und keine Microsteps behaupten.
- `DEFAULT_AXIS_STEPS_PER_UNIT`, `DEFAULT_MAX_FEEDRATE`, `DEFAULT_MAX_ACCELERATION`, Achs- und Homing-/Softlimit-Optionen **erst anhand der tatsächlichen Mechanik** festlegen.
- EEPROM nur bei vorhandenem Flash-/RAM-Spielraum; Motorsperre und Notstop im späteren Host-Protokoll prüfen.
- Kein Vertrauen auf Software-Endstops oder Homing ohne überprüfte Referenzierung; nach Reset/Power-up keine blinden XY-Fahrten.
- Servo extern mit geeigneter geregelter 5-V-Versorgung; gemeinsame Masse; RAMPS-SERVO-VCC/Jumper vor Anschluss kontrollieren. Niemals Servo allein aus einer ungesicherten 5-V-Schiene versorgen.
- RAMPS 12-V-Motorversorgung separat; Treibermodule nie bei angelegter Spannung stecken/ziehen.

## Phase 0 – Prüfablauf
1. Quellstand **Marlin 2.1.2.9** holen, Boarddefinition und `POLARGRAPH`-Abschnitt im Tag prüfen.
2. Patch auf die unveränderten `Configuration.h` und `Configuration_adv.h` dieses Tags anwenden; keine anderen Versionen mischen.
3. Mit passender PlatformIO-Umgebung für **ATmega2560** (typischerweise `mega2560`, im Tag prüfen) kompilieren.
4. Flash- und SRAM-Bedarf, Warnungen, Servo-/Timerkonflikte und Sanity-Checks dokumentieren.
5. Erst dann eine vollständige geprüfte Konfigurationsdatei und `.hex` bereitstellen. Bis dahin ist die Vorlage **nicht flashbereit**.
6. Ohne Motoren USB-Serial testen (`M115`, `M114`, `M119`, `M280 P0 S...` nur mit korrekt versorgtem Servo). Danach abgesicherte Einzelmotortests und kalibrierte Bewegung.

## Noch zu ermitteln
- Treibertyp und Anzahl der bestückten Treiber; Stromgrenzen und Microstep-Jumper.
- Motortyp und Nennstrom.
- Ob Zahnriemen, Seilscheibe oder Wickelspule (bei Wickelspule verändert sich die effektive Länge pro Schritt).
- Motorabstand, Montagehöhe, Fläche, Seillänge und Start-/Referenzierverfahren.
- Servo-Mechanik, Zielwinkel und stromfeste Versorgung.

## Dokumentation
- Marlin Polargraph: https://marlinfw.org/docs/settings/polargraph.html
- Marlin RAMPS Board-Auswahl: https://marlinfw.org/docs/settings/machine.html
- Marlin Servos: https://marlinfw.org/docs/settings/servos.html
- Marlin Release: https://github.com/MarlinFirmware/Marlin/tree/2.1.2.9
