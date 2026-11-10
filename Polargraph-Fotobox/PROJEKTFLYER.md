# Polargraph-Fotobox – Projektvorstellung für den gemeinsamen Selbstbau

*Stand: November 2026 · Projektkonzept, kein fertiges oder erprobtes Gesamtsystem.*

## 1. Die Idee

Eine Zeichenmaschine für Veranstaltungen und Ausstellungen: Ein Besucher stellt sich vor die Kamera. Ein Android-Handy vereinfacht das Motiv zu Linien und Schraffuren. Ein an zwei Seilen geführter Zeichenkopf bringt diese Linien sichtbar auf Papier – Strich für Strich. Anders als bei einem Drucker gehört die Entstehung der Zeichnung zum Erlebnis.

Zunächst wird auf einem Flipchart gezeichnet; später sind größere Flächen denkbar. Geplant sind Porträts und weitere Motive, mehrere Zeichenstile, drei automatisch wählbare Stifte, eine spätere kameragestützte Genauigkeitsverbesserung und schließlich weitgehend autonomer Betrieb.

## 2. Was wird womit verbunden?

```text
Android-Handy (Kamera, Bedienung, Bildverarbeitung)
       │ USB-OTG
       ▼
Arduino Mega 2560 + RAMPS 1.4
       ├─ X-Treiber ─ linker Schrittmotor
       ├─ Y-Treiber ─ rechter Schrittmotor
       └─ SERVO0 ─ Servo zur Stiftauswahl

Motorversorgung: geeignetes Netzteil für RAMPS
Servo: stabile separate 5-V-Versorgung, gemeinsame Masse
```

Das Handy fotografiert, zeigt die Vorschau, berechnet Zeichenwege und übermittelt Bewegungsaufträge. Das Redmi Note 9 Pro ist das erste vorgesehene Testgerät; weitere Android-Geräte sollen möglich sein.

Arduino Mega und RAMPS übernehmen die zeitgenaue Ansteuerung zweier Schrittmotoren und eines Servos. Von den fünf üblichen Motortreiber-Steckplätzen werden anfangs zwei genutzt.

Je ein Motor befindet sich links und rechts oben. Seile oder Zahnriemen führen den Zeichenkopf. Die Schwerkraft spannt den Kopf; seine Mechanik führt drei Stifte und wählt sie mit einem Servo aus. Die genaue Seilführung und Aufwicklung müssen noch festgelegt werden.

**Vor dem ersten Motorlauf:** Versorgung, Strombegrenzung, Steckerbelegung, gemeinsame Masse, Absicherung und Notabschaltung kontrollieren.

## 3. Was ist bereits entwickelt – und was müssen wir selbst bauen?

| Vorhandene Grundlage | Unsere Entwicklungs- und Bauarbeit |
|---|---|
| Arduino Mega, RAMPS-Steuerplatine, Schrittmotortreiber | Rahmen, Motorhalterungen, Seilführung und Zeichenkopf fertigen |
| Etablierte Drucker-Firmware für Motorbewegungen und Servobefehle | Auf unsere konkrete Mechanik einstellen und praktisch testen |
| Bekannte Polargraph-Geometrie und Open-Source-Ansätze | Geometrie, Grenzen und Korrekturen abstimmen |
| Android-Kamera und Bibliotheken für USB und Bildverarbeitung | Intuitive Bedienung, Zeichenvorschau und Zeichenstile integrieren |
| Erhältliche Papierfördertechnik und Aktenvernichter | Sichere Papierführung, Stauerkennung und Schutzvorrichtungen konstruieren |

**Wichtig:** Die vorhandenen Einzeltechniken garantieren noch nicht, dass ihr Zusammenspiel im geplanten Gerät funktioniert. Insbesondere Stiftwechsel, Bildqualität und automatische Kalibrierung müssen wir erproben.

## 4. Die eigentlichen Herausforderungen

**Präzision:** Dehnung, Spiel, Reibung, ungleichmäßiges Aufwickeln und Schwingungen können Linien verschieben. Die Wickel- und Seilmechanik ist deshalb entscheidend.

**Drei Stifte:** Ein Servo soll die Stifte zuverlässig auswählen und abheben. Versetzte Stiftspitzen erfordern mechanische Genauigkeit und Kalibrierung.

**Erkennbare Porträts:** Fotos enthalten zu viele Details für schnelle Strichzeichnungen. Gesichter sollen wiedererkennbar sein, während die Zeichenzeit vertretbar bleibt.

**Kamerabasierte Korrektur:** Später soll eine Kamera gezeichnete Testlinien mit den Soll-Linien vergleichen. Beleuchtung, Perspektive und Papierlage machen das anspruchsvoll.

**Publikumsbetrieb:** Start, Pause und Stopp müssen zuverlässig sein. Bewegliche Teile und besonders ein späterer Aktenvernichter benötigen geeignete Schutzmaßnahmen und Verriegelungen.

Die erste Version wird ausdrücklich **ohne Aktenvernichter, automatische Papierrolle und selbstlernende Korrektur** gebaut.

## 5. Der Bau in Etappen

1. **Virtueller Test:** Zeichenwege und Motorbewegungen simulieren, zunächst ohne Mechanik.
2. **Erster realer Plotter:** Rahmen, Motoren, Seile, Steuerung und einen Stift montieren; Testmuster zeichnen.
3. **Drei Stifte und Porträts:** Stiftwechsel ergänzen, Handy-Fotobilder vereinfachen, Zeichnungen per USB ausgeben.
4. **Fotobox für Besucher:** Kamera, einfache Auswahl und lokale Zeichenstile; freiwillige Online-KI als separate Option.
5. **Mehr Genauigkeit und Automatik:** Kamerakalibrierung und gespeicherte Korrekturen, später Papierrolle, Präsentationszeit und geschützter Aktenvernichter.

### Was wir vor dem Aufbau gemeinsam festlegen müssen

Motorabstand, Papiergröße, Seil- oder Riemenantrieb, konkrete Schrittmotoren und Treiber, Gewicht und Abmessungen des Zeichenkopfs, Stifttypen und Stromversorgung.

**Ziel von Version 1:** Eine zuverlässig vom Android-Handy gesteuerte Maschine, die auf einem Flipchart gut erkennbare Zeichnungen mit automatischem Stiftwechsel erzeugt. Erweiterungen folgen erst, wenn diese Basis funktioniert.

---

Die gestaltete druckbare A4-Fassung gehört dazu: `Polargraph_Fotobox_Projektflyer.pdf`.
