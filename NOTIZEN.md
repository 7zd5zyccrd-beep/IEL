# Notizen zur Weiterarbeit

Stand: v0.18 · 05.10.2026. Was sich geändert hat, steht in der Änderungsliste oben in `index.html`.

## Noch auf dem iPhone zu prüfen
- Bildschirm bleibt an, solange der Zettel offen ist (Wake Lock; als Home-Bildschirm-App erst ab iOS 18.4 zu erwarten).
- Zoom-Sperre (Zwei-Finger und Doppeltipp).
- Diktieren über die Tastatur: schreibt iOS Zahlen als Ziffern oder Wörter, kommen „und“/Kommas wie erwartet?
- Teilen-Menü beim „Zettel teilen“.
- Dunkelmodus auf dem Gerät.
- Falls „+ Laden“ oder der gelernte Weg nicht speichern: Firebase-Regeln für `haushalte/<uid>/einstellungen/laeden`, `…/standardname` und `…/wege` prüfen.

## Offene Ideen (noch nicht umgesetzt)
- Vorlagen („Grillabend“, „Frühstück“) mit einem Tipp auf den Zettel.
- Knopf „Alle fälligen notieren“.
- Neues vom anderen Haushaltsmitglied markieren.
- Preise und ungefähre Summe.
- „War aus“: Artikel bleibt ohne Kauf auf dem Zettel, mit Vermerk.
- Datensicherung als Datei (Export/Import).
- Verworfen nach Abwägung: Wischen zum Abhaken, Long Press zum Abhaken.
  Falls versehentliches Abhaken doch vorkommt: nur das Kästchen links hakt ab.

## Daten in Firebase (unter `haushalte/<uid>/`)
- `artikel/<id>`: Änderungen am Grundstock und eigene Artikel (`n, g, e, m, kaeufe, zuletzt, letzte, aus …`).
- `zettel/<id>`: `menge, einheit, ab, abT, notiz, t`.
- `einstellungen/gruppen`: Gruppenfolge des ersten Ladens; `standardname`: dessen Name.
- `einstellungen/laeden/<id>`: weitere Läden `{n, gruppen}`.
- `einstellungen/wege/<laden|standard>`: letzte 12 Einkäufe als Gruppenfolge (Abhak-Reihenfolge).
- Welcher Laden aktiv ist, merkt sich jedes Gerät (`localStorage: einkauf.laden`).
