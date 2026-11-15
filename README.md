# Denkzirkus

Offline-Android-App: Logik-Training für Kinder und Erwachsene. Sieben Arten
von Rätseln, alle vom Handy erzeugt und vor dem Stellen nachgerechnet, damit
jedes genau eine Lösung hat. Mehrere Spieler, Alter und Schwierigkeit passen
sich an. Schwester-App des [Merkzirkus](../merkzirkus).

APK: [dist/denkzirkus-1.0.apk](dist/denkzirkus-1.0.apk)

## Rätsel

| Rätsel | Aufgabe | Stufe 1 → 10 | Runde geschafft, wenn |
|---|---|---|---|
| Zahlenreihen | nächste Zahl aus vier wählen | feste Schritte, Abziehen, Malnehmen, zwei Schritte im Wechsel, wachsende Abstände, Summen- und Quadratreihen, ×2/−c im Wechsel, zwei verschachtelte Reihen, ×k+c | 4 von 5 |
| Muster-Lücke | fehlendes Bild in einem 3×3-Feld wählen | Form, Farbe und Anzahl folgen je einer Regel (überall gleich, je Zeile, je Spalte, oder in jeder Zeile und Spalte alle drei); ab Stufe 5 sechs Antworten, ab Stufe 6 Lücke an beliebiger Stelle | 3 von 4 |
| Wer steht wo? | Tiere nach Hinweisen in eine Reihe stellen | 3 → 6 Tiere; Hinweise erst Platz und "direkt links von", dann "neben", "irgendwo links von", ab Stufe 5 Verneinungen, ab 7 "zwischen", ab 8 kein fester Platz mehr | gelöst mit höchstens einem Fehlversuch (nach drei wird aufgelöst) |
| Wer ist größer? | aus einer Kette von Vergleichen schließen | 3 → 6 Kinder; Fragen nach dem Größten/Kleinsten, ab Stufe 4 Paarvergleich, ab 7 "Wie viele sind größer als …?" | 3 von 4 |
| Code knacken | geheimen Farbcode erraten | 3 Stellen/3 Farben → 5 Stellen/7 Farben, 7–8 Versuche; ab Stufe 4 Farben doppelt möglich | innerhalb der Versuche geknackt |
| Mini-Sudoku | Feld ausfüllen | 4×4 mit 10 → 6 Vorgaben (Stufe 1–5), 6×6 mit 22 → 14 Vorgaben (Stufe 6–10) | gelöst mit höchstens einem Fehlversuch |
| Stimmt das sicher? | folgt eine Behauptung zwingend aus zwei Sätzen? | 12 Schlussformen mit Quatsch-Wörtern (Blubbs, Zapps …), zuerst mit einer Figur, dann mit ganzen Gruppen | 5 von 6 |

Nach jeder Antwort erscheint die Erklärung (Regel der Reihe, Reihenfolge,
Grund für den Schluss). Kinder von 6–13 bekommen beim 4×4-Sudoku Obst statt
Ziffern.

## Warum die Rätsel stimmen

Jeder Erzeuger ist eine reine Funktion mit eigener Zufallsquelle und wird im
Selbsttest (`?debug=1`) auf allen zehn Stufen je zwölfmal geprüft:

- **Muster:** Von den angebotenen Bildern erfüllt genau eines die Regeln
  (`musterFits`).
- **Wer steht wo?:** Alle Anordnungen werden durchprobiert; genau eine
  erfüllt die Hinweise, und kein Hinweis ist überflüssig.
- **Mini-Sudoku:** Ein Löser zählt die Lösungen; es muss genau eine sein.
- **Stimmt das sicher?:** Jede Schlussform wird in allen Welten mit drei
  Dingen durchgerechnet (`formValid`) und muss zur Einstufung passen.
- **Zahlenreihen, Vergleiche, Code:** Antwort gegen die erzeugende Regel
  geprüft, Antwortmöglichkeiten verschieden.

## Alter und Schwierigkeit

Wie im Merkzirkus: beliebig viele Spieler mit Altersgruppe (Kind 6–9, Kind
10–13, ab 14 und Erwachsene). Die Gruppe bestimmt Einstiegsstufe (1, 2, 4)
und die Fassung der Erklärung. Je Rätsel und Spieler zehn Stufen: geschafft
→ eine höher, nicht geschafft → eine tiefer. Sterne in Höhe der Stufe.

## Einordnung

Rätseln verbessert die Leistung in diesen Rätselarten und übt geduldiges,
schrittweises Schließen. Dass man dadurch allgemein intelligenter wird, ist
nicht belegt; die App sagt das auch.

## Datenmodell (localStorage)

`denkzirkus.data.v1`: `{schema, cur, profiles: [{id, name, age, levels,
stats: {spiel: {n, ok, best}}, stars}]}`. Kein Backup, keine Brücke zu
Android: Der Spielstand liegt nur auf dem Gerät.
