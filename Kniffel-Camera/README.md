# Kniffel-Camera

Android-App für klassisches Kniffel mit echten Würfeln und kameragestützter Erkennung.

## Ziel
Der klassische Kniffel-Spielzettel bleibt dauerhaft sichtbar. Darüber oder daneben zeigt die App groß und farbig die fünf erkannten Würfel, gehaltene Würfel und mögliche Wertungen. Die Handykamera überwacht eine Wurf- und eine Haltezone. Eine Wertung wird erst durch Antippen eines freien Feldes übernommen.

## Anforderungen
- Klassische Kniffel-Wertung mit Einsern bis Sechsern, oberer Summe, Bonus ab 63 Punkten, Dreierpasch, Viererpasch, Full House, kleiner/großer Straße, Kniffel und Chance; Gesamtwertung.
- Mehrere Spieler, individuelle Spalten wie beim Papier-Kniffelblock, automatischer Spielerwechsel nach bestätigter Wertung.
- Je Zug maximal drei Würfe, nach jedem Wurf frei wählbare gehaltene Würfel.
- Große, farbige Anzeige erkannter Augenzahlen und gehaltener Würfel; mögliche Punkteeinträge für noch freie Kategorien anzeigen. Keine automatische Eintragung ohne Bestätigung.
- Live-Kamera mit konfigurierbarer Wurf- und Haltezone; Erkennen von fünf Würfeln, Augenzahlen und stabilem Stillstand.
- Verschieben in die Haltezone erkennen. Wurfzählung nur nach plausibler Bewegung/erneutem Stillstand, nicht bei bloßem Antippen.
- Unsichere Erkennung klar markieren; immer manuelle Korrektur der Würfel und Wurfzählung zulassen.
- Offline-fähig, Speicherung laufender Partien, Rückgängig-Funktion.
- Layout: Hochformat primär, klassischer Zettel permanent sichtbar; Querformat/Tablet später adaptiv.

## Technik (Vorschlag)
- Native Android-App in Kotlin, Jetpack Compose für UI, CameraX für Kamerazugriff.
- OpenCV als erster Ansatz für Würfel- und Augenerkennung bei kontrastreichen Standardwürfeln; später optional ein On-Device-ML-Modell.
- Zustandsmaschine für Spielzug und Wurferkennung, strikt getrennt von Kameraanalyse und Punktelogik.
- Persistenz lokal (z.B. Room/DataStore). Keine Cloud oder Arduino-Hardware erforderlich.

## Implementierungsreihenfolge
1. Spielregeln als reine Logik mit Unit-Tests (einschließlich Nullen/Streichungen, Bonus und Mehrspielerbetrieb).
2. Interaktiver klassischer Kniffel-Zettel und große Würfel-/Vorschlagsanzeige; zunächst manuelle Eingabe.
3. CameraX-Vorschau, konfigurierbare Zonen und stabilisierte Erkennung der fünf Augenzahlen.
4. Haltezone, Wurfzustände, automatische Zählung und Fehlerkorrekturen.
5. Robustheitstests mit verschiedenen Lichtverhältnissen, Hintergründen und Würfeltypen.

## Entscheidungen / Risiken
- Standardwürfel mit gut erkennbaren Augen sowie eine überwiegend senkrechte Kameraposition zunächst voraussetzen.
- Ein Verschieben kann optisch einem Wurf ähneln; automatische Wurfzählung braucht Verifikation und manuelle Korrektur.
- Die Farben sollen Kategorien und Erkennungszustände verständlich unterscheiden, nicht blind die höchste Punktzahl als strategisch beste Wahl ausgeben.
- Ein Projekt-Unterordner in diesem Repository ist vorläufig: `Kniffel-Camera/`. Das gesamte Repository ist derzeit öffentlich. Keine Zugangsdaten oder privaten Daten einchecken.

## Erste Aufgabe für Codex
Erstelle eine lauffähige Android-Studio-Grundstruktur für `Kniffel-Camera` mit sauber getrennten Modulen für Kniffel-Regeln, Spielzustand und Compose-Oberfläche. Implementiere zuerst den Papierblock mit mehreren Spielerspalten, manuell antippbare Würfel und vollständig getestete Wertungsregeln. Noch keine vorgetäuschte Kameraerkennung.

## Schräg aufgestellte Kamera (festgelegtes Entwicklungsziel)
- Kamera seitlich auf Tischständer, beispielsweise ca. 45–60° über der Tischfläche; nicht zwingend senkrecht.
- Vier-Punkt-Kalibrierung der Tischfläche für perspektivisch korrekte Wurf-/Haltezonen.
- Würfel als dreidimensionale Objekte betrachten: nur Augen der **Oberseite** zählen, nicht die sichtbaren Seitenflächen.
- Bei überlappenden, verdeckten oder schräg liegenden Würfeln Konfidenz senken und manuelle Bestätigung verlangen.
- Kamerawinkel und Beleuchtung auf verschiedenen Android-Geräten testen, keine feste Winkelgarantie behaupten.
