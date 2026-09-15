# lernspiele

Kleine Mathe-Lernspiele für meine Kinder. Link öffnen, spielen, fertig — ohne App-Store, ohne
Anmeldung. Ein Spiel = ein Ordner = eine HTML-Datei, ausgeliefert über GitHub Pages.
Kein Build, kein Server, kein Konto.

Live: https://husameldin-92.github.io/lernspiele/

`index.html` im Wurzelverzeichnis ist die private Übersicht. Verschickt wird immer nur die
Adresse eines einzelnen Spiels, nie die Sammlung.

## Verzeichnisbaum

```
lernspiele/
├── index.html          Private Übersicht aller Spiele — nicht die Adresse für die Klasse
├── elfmeter/
│   └── index.html      Spiel "Elfmeter-Einmaleins", unverändert übernommen
├── radrennen/
│   └── index.html      Spiel "Radrennen gegen Papa", unverändert übernommen
├── .nojekyll           sagt GitHub Pages: Dateien direkt ausliefern, nicht verarbeiten
├── .gitignore          ignoriert .DS_Store
└── README.md           diese Datei
```

## Spiele

| Spiel | Fach | Klasse | Adresse |
| --- | --- | --- | --- |
| Elfmeter-Einmaleins | Mathe | Klasse 2-3 | `./elfmeter/` |
| Radrennen gegen Papa | Mathe | Klasse 2-3 (Mix-Modus bis Klasse 4) | `./radrennen/` |

## Ein neues Spiel dazu

1. **Ordner anlegen.** Name = EIN kurzes Wort, klein geschrieben, ohne Datum, ohne
   Versionsnummer (`elfmeter`, `radrennen`, …).
2. **Fertige HTML-Datei als `index.html` hineinlegen — unverändert.** Am Spiel selbst wird
   nichts angepasst, nichts herausgelöst, nichts "noch schnell" umgebaut. Änderungen am Spiel
   laufen über die Werkstatt, nicht über dieses Repo.
3. **Kachel in der Übersicht `index.html` ergänzen:** Titel, Fach, Klasse, ein Satz zum Spiel,
   Link auf `./<ordner>/`.
4. **Committen und pushen.**

```
git add <ordner> index.html
git commit -m "Spiel <ordner> dazu"
git push
```

GitHub Pages aktualisiert sich **nur durch einen Push**. Lokal geändert heißt nicht online —
erst der Push (plus ein, zwei Minuten Build) macht die neue Adresse erreichbar.

## Adressen

**Der Ordnername *ist* die Adresse.** Daraus folgt alles Weitere:

- Keine Datumsstempel, keine Versionsnummern, keine Umlaute im Ordnernamen.
- **Eine einmal verschickte Adresse wird NIE umbenannt.** Die Links stehen in der
  Eltern-/Klassen-WhatsApp-Gruppe. Ein umbenannter Ordner macht sie sofort tot — 404 für alle,
  auch Monate später. Umbenennen ist hier kein Refactoring, sondern ein kaputter Link.
- Neue Fassung eines Spiels: Datei im bestehenden Ordner ersetzen, Ordnername und Adresse
  bleiben.
- Links im Repo immer **relativ** (`./elfmeter/`), nie absolut. So läuft die Sammlung unter
  GitHub Pages, unter einer eigenen Domain und per `file://` gleich.

## Spielstände

Der Fortschritt — Sterne, Bestzeiten, gewählte Reihen — liegt ausschließlich lokal im Browser
(`localStorage`: `elfmeter-einmaleins-v2`, `radrennen-papa-v1`). Kein Konto, kein Server, keine
Übertragung. Der Stand hängt an Gerät, Browser **und Adresse**: Wer woanders geübt hat — anderes
Handy, anderer Browser, privates Fenster, `file://` statt Pages — fängt hier bei null an.
Browserdaten löschen löscht den Stand; Export oder Backup gibt es nicht.

## Technisch

Einzelne HTML-Dateien (je ca. 26 KB), kein Build, kein Framework, keine Abhängigkeiten außer
Google Fonts per `<link>` (`fonts.googleapis.com` / `fonts.gstatic.com`: Bungee + Nunito bzw.
Titan One + Nunito). Sonst lädt nichts von außen nach — kein `fetch`, kein XHR, keine externen
Skripte oder Bilder; alle Grafik ist Inline-SVG, der Ton kommt aus der Web Audio API. Ohne
Internet läuft alles weiter, nur mit Systemschrift.

Layout auf Handybreite ausgelegt (max. 480 px), Bedienung per Touch oder Tastatur (Ziffern,
Backspace, Enter), festes dunkles Design, `prefers-reduced-motion` wird respektiert.

Lokal testen: Spieldatei direkt im Browser öffnen (`open elfmeter/index.html`) — das Spiel
verhält sich per `file://` genau wie auf Pages. Nur die Kachel-Links in der Übersicht greifen
dort nicht: `./elfmeter/` löst erst ein Webserver auf `index.html` auf, per `file://` kommt
stattdessen die Ordnerliste des Browsers. Wer die Übersicht mitsamt Links testen will, startet
kurz einen Server im Repo-Ordner (`python3 -m http.server`) und geht auf
`http://localhost:8000/`.
