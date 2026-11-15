# Denkzirkus

Offline-Android-App: Logik-Training mit sieben erzeugten Rätselarten für
Kinder und Erwachsene. Reine Web-App in einer Datei, die per
[apk-builder](../apk-builder) zur APK wird. Rätsel, Prüfungen und
Datenmodell stehen in [README.md](README.md), Versionen in
[CHANGELOG.md](CHANGELOG.md). Schwester-App: [merkzirkus](../merkzirkus)
(gleiche Profile, Altersgruppen und Stufenlogik).

## Build & Test

Kein Bundler, kein Build-Step. Testserver `denkzirkus` aus der
Workspace-`.claude/launch.json` (Port 8210), dann
`http://localhost:8210/web/`. `?debug=1` führt den Selbsttest aus (Konsole
und Zeile auf der Startseite, auch per `dzTests()`). Er muss komplett `OK`
zeigen; er rechnet für jede Rätselart alle zehn Stufen mehrfach nach.

Alle Rätsel im Browser durchspielen: die `make…`-Funktionen in der Konsole
so umhüllen, dass jede erzeugte Aufgabe in einer Liste landet, und einen
Roboter die richtige Antwort wählen lassen (Auswahl per `click`; bei "Wer
steht wo?" Tier und Platz antippen, beim Code die Farben, beim Sudoku Feld
und Zeichen).

APK bauen über den Wrapper (ohne native Brücke):

```powershell
cd "D:\claude code projects\denkzirkus"
.\build.ps1 -VersionName "1.1" -VersionCode 2 -Release   # signiert -> dist\denkzirkus-<v>.apk
```

## Konventionen

- Alles in `web/index.html`, kein Framework, kein Netzwerk, keine
  vorgefertigten Rätsel.
- Ein Rätsel besteht aus einem reinen Erzeuger `make…(stufe, rnd)` und einem
  Eintrag in `GAMES` (Texte `k` für Kinder, `e` für Erwachsene, `run`).
- **Kein Rätsel ohne Nachweis:** Jeder Erzeuger braucht im Selbsttest eine
  Prüfung, dass die Aufgabe genau eine Lösung hat bzw. die Antwort zur Regel
  passt, über alle zehn Stufen. Neue Schlussformen in `FORMEN` müssen
  `formValid` bestehen.
- Stufen ändern nur Parameter des Erzeugers (Tabellen wie `PLATZ_N`,
  `CODE_P`, `SD_GIVEN`, `MUSTER_MODES`), nicht den Ablauf.
- Kein Tippen von Wörtern; Antworten über Auswahl, Kacheln oder Paletten.
- Deutsche Grammatik in erzeugten Sätzen über feste Wortformen lösen
  (`TIERE` mit Nominativ und Dativ, Kindernamen ohne Artikel), nicht über
  Regeln.
- Kein `confirm()`/`alert()`: eigene Dialoge über `openModal`.

## Aktueller Stand

v1.0 (code 1, 2026-11-15): sieben Rätselarten, Spielerprofile mit
Altersgruppe, zehn Stufen je Rätsel, Sterne. Selbsttest 21/21 (je Rätselart
120 erzeugte Aufgaben nachgerechnet); alle sieben Rätsel liefen im Browser
mit einem Roboter durch, einschließlich Fehlversuch bei "Wer steht wo?" und
"Code knacken". Signierte APK `dist/denkzirkus-1.0.apk`.

**Am Gerät noch nichts getestet, und kein Mensch hat es gespielt.** Offen:
ob die Stufenkurven für Daniels Kinder und für ihn passen (Einstieg
Erwachsene Stufe 4), ob 6×6-Sudoku und sechs Tiere auf dem Handy gut
bedienbar sind, ob die Farbkreise (Emoji) beim Code gut unterscheidbar sind.

Daniels Vorgabe (2026-11-15): Logik-Trainer für Erwachsene und Kinder,
anpassbar nach Alter und Schwierigkeit.
