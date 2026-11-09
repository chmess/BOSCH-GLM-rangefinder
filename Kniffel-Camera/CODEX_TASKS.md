# Auftrag an Codex

Arbeite **ausschließlich** im Verzeichnis `Kniffel-Camera/` des Repositories `chmess/BOSCH-GLM-rangefinder`. Keine vorhandenen Bosch-Dateien verändern oder löschen.

## Erster konkreter Auftrag
Erstelle ein eigenständig baubares Android-Studio-Projekt in diesem Unterordner auf Basis von Kotlin und Jetpack Compose.

1. Klassische Kniffel-Tabelle mit 13 Wertungsfeldern, Oberteil-/Unterteil-Summen, Bonus und Gesamt, mehreren Spielern. Der Zettel bleibt während des gesamten Spielzuges sichtbar.
2. Große, farbige fünf Würfel (zunächst manuelle Augeneingabe 1–6), separate Markierung `gehalten` und Wurfzähler 1–3.
3. Große Liste aller noch freien Kategorien mit aktuell erzielbaren Punkten, inklusive 0 bei Streichungen; Antippen der Kategorie öffnet eine Bestätigung vor dem Eintrag.
4. Regel-Engine und Tests (1–6, Pasche, Full House, Straßen, Kniffel, Chance, Bonus). Sonderfälle zusätzlicher Kniffel nachvollziehbar spezifizieren und testen.
5. Speichern/Fortsetzen, Spielerwechsel, Undo, manuelle Korrekturen.
6. Dokumentation zum Bau einer APK, mindestens ein Screenshot oder Compose Preview, sinnvolle Gradle-Konfiguration.

## Danach
CameraX-Integration mit Kalibrierung der Wurf- und Haltezone; dann erst die Bilderkennung, Tracking und verlässliche Wurfzählung. Kamerapipeline als austauschbares Modul und immer manueller Fallback.

## Akzeptanz
Projekt lässt sich in Android Studio öffnen und bauen; Unit-Tests sind grün; auf einem Android-Handy spielbar ohne Internet und ohne Kamerazugriff. Bericht über umgesetzte und offene Punkte mit Commit-Hash und Build-/Teststatus. Keine vorgetäuschten Testergebnisse.
