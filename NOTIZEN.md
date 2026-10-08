# Notizen zur Weiterarbeit

Stand: v0.20 · 07.10.2026. Was sich geändert hat, steht in der Änderungsliste oben in `index.html`.

## Noch auf dem iPhone zu prüfen
- Bildschirm bleibt an, solange der Zettel offen ist (Wake Lock; als Home-Bildschirm-App erst ab iOS 18.4 zu erwarten).
- Zoom-Sperre (Zwei-Finger und Doppeltipp).
- Diktieren über die Tastatur: schreibt iOS Zahlen als Ziffern oder Wörter, kommen „und“/Kommas wie erwartet?
- Teilen-Menü beim „Zettel teilen“.
- Dunkelmodus auf dem Gerät.
- Falls „+ Laden“ oder der gelernte Weg nicht speichern: Firebase-Regeln für `haushalte/<uid>/einstellungen/laeden`, `…/standardname` und `…/wege` prüfen.

## Startablauf und Verbindung (seit v0.19/v0.20)
- Das Schloss ist im HTML ausgeblendet. `start()` zeigt bei gesetztem Merker (`einkauf.angemeldet`) und vorhandener Kopie (`einkauf.spiegel`) sofort die App, sonst das Schloss. Das Schloss kommt erst, wenn `onAuthStateChanged` keinen Nutzer meldet.
- `appZeigen()` tut nichts, wenn die App schon sichtbar ist (sonst springt der Reiter zurück).
- `schreibsperre()` sperrt auch, solange `BASIS` leer ist (SDK geladen, Anmeldung noch nicht bestätigt). Sonst würde an die Wurzel der Datenbank geschrieben.
- `F.set/update/remove` sind über `mitgezaehlt()` gezählt. Der Streifen „Keine Verbindung“ erscheint nur, wenn keine Verbindung besteht und Schreibvorgänge offen sind (`wartehinweisPruefen()`). Beim Start gibt es keinen Hinweis, nur den orangen Punkt.
- Vom Nutzer auf dem iPhone bestätigt.
- Möglicher Feinschliff: In der ersten Sekunde nach dem Start (bis Firebase geladen und angemeldet ist) bekommt eine Aktion „Ohne Verbindung nicht änderbar.“ Man könnte solche Aktionen stattdessen zurückhalten und danach ausführen.

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
