# Fachliche und technische Spezifikation (Entwurf)

## Bildschirm
Hochformat: kompakter Kopf (aktiver Spieler, Runde, Wurf x/3), großer farbiger Würfelbereich, deutlich sichtbare mögliche Wertungen, dauerhaft eingeblendeter klassischer Kniffel-Block mit Kategorien und Spieler-Spalten. Kleine Kameravorschau und Kalibrierung als zuschaltbares Overlay. Bei Platzmangel scrollbar, ohne den Zettel durch einen separaten Screen zu ersetzen. Tablet quer: Zettel links, Würfel/Vorschläge rechts.

## Regeln (klassisches Kniffel, konfigurierbare Varianten später)
Pro Spieler 13 Wertungsfelder, maximal 3 Würfe pro Zug, nach jedem Wurf darf gewertet werden. Oberteil Einser–Sechser = Anzahl passender Augen mal Augenwert; Bonus +35 bei Oberteil >=63. Unterteil: Dreierpasch und Viererpasch = Summe aller fünf Augen bei mindestens 3 bzw. 4 gleichen; Full House = 25 (3+2 gleicher Augen); kleine Straße = 30 (4 aufeinanderfolgende Augen), große Straße = 40 (5 aufeinanderfolgende), Kniffel = 50 (5 gleiche), Chance = Summe aller Augen. Jede Kategorie genau einmal; nicht erfüllte Bedingung kann mit 0 gestrichen werden. Sonderregeln für zusätzliche Kniffel (Joker/Kniffelbonus) als separat getestete, explizit dokumentierte Regellogik nach Prüfung der gewählten Regelvariante, nicht unbemerkt vereinfachen.

Hinweis: Wertungsvorschläge zeigen **alle aktuell eintragbaren freien Kategorien** einschließlich 0-Punkte-Einträgen. „Passend“/„hohe Punkte“/„strategisch empfohlen“ sind unterschiedliche Kennzeichnungen, kein falsches Versprechen einer optimalen Strategie.

## Kamerapipeline
CameraX ImageAnalysis mit drosselbarer Frame-Rate; Kalibrierung einer Tischfläche per Koordinaten/optional Homografie; ROI für Wurfzone/Haltezone mit sichtbaren Grenzen. MVP: kontrastreiche Würfeloberflächen erkennen, Augenblob-Zählung nach Perspektivkorrektur und Plausibilitätsprüfung, unabhängige Konfidenz für Wert/Position. Optional später trainiertes Modell, wenn klassische OpenCV-Methoden nicht reichen.

Zustände: READY -> MOTION -> SETTLING -> STABLE -> VERIFIED; HELD als Eigenschaft einzelner verfolgter Würfel. Positionszuordnung zwischen Frames per Tracking; bei Verdeckung oder Identitätswechsel konservativ auf manuelle Prüfung wechseln. Erst ein bewusster Wurf der nicht gehaltenen Würfel mit Bewegungs- und Stillstandsschwellen kann den Wurfzähler erhöhen. Reines Verschieben in die Haltezone zählt nicht. Unvollständige/zweifelhafte Beobachtung -> Bestätigung statt automatische Buchung. Kameraausfall -> manuelle Eingabe.

## Datenmodell
Game(id, createdAt, rulesVersion, status); Player(id, name, order); Turn(gameId, playerId, index, rollCount, dice[5], held[5], recognitionConfidence); ScoreCell(playerId, category, value?, filledAt); UndoEvent. Autosave nach jedem bestätigten Schritt. Keine automatische Wertung ohne Spielerbestätigung.

## Qualitätskriterien
- Unit-Tests der 13 Wertungsfelder, Bonusgrenze und Spielerwechsel, Undo.
- Keine Doppelzählung ruhender/verschobener Würfel.
- Zone kalibrierbar, Zonenwechsel visuell markiert.
- Funktioniert ohne Netz und ohne Kamera-Berechtigung im manuellen Modus.
- Bosch-Projektdateien und Repository-Root nicht verändern.

## Modulare Mehrspiele-Architektur (beschlossen)
Die Hardware-/Kameraebene wird strikt von den Spielregeln getrennt. Kniffel ist das erste aktiv implementierte Spiel; weitere Regelpakete (z. B. Yatzy und Mäxchen) sind Erweiterungsoptionen, keine Voraussetzung für das erste APK.

- `camera-core`: CameraX, Tischkalibrierung auch bei schräger Kameraposition, Wurf-/Halte-Zonen, Würfelflächen-/Augenerkennung, Tracking, Bewegung/Stillstand und Konfidenzen.
- `dice-domain`: neutrales Modell von Würfeln, Würfen, Haltestatus und korrigierbaren Erkennungsergebnissen; keine Kniffel-spezifische Logik.
- `game-api`: definierte Schnittstelle für Spiele (Metadaten, Spieleranzahl, Wertungsoptionen, Zugablauf, erlaubte Würfelanzahl, Zustandsserialisierung, Regelvalidierung, UI-Beschreibungen).
- `games/kniffel`: klassische Regeln, Punktetabelle, Bonus und Sonderregeln, Tests.
- `app-ui`: klassischer Kniffel-Zettel als erste spielspezifische UI, große farbige Würfel und Wertungsvorschläge; später andere Spieloberflächen über Schnittstellen.
- `storage`: lokale Spielstände, Statistiken und Korrektur-/Undo-Verlauf, versionierte Spielregeldaten.

Optionale spätere Module: Strategiehilfe (mit nachvollziehbarer Begründung, kein garantierter Optimaltipp), Sprachbefehle mit Bestätigung vor Wertung, Plausibilitäts-/Schiedsrichterhinweise, Statistiken, lokaler Zweitbildschirm und weitere Würfelspiele. Alle zusätzlichen Funktionen sollen abschaltbar und für ein erstes spielbares Kniffel-MVP nicht blockierend sein.
