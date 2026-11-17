# Now Playing

Ein ruhiges Lo-Fi-Display für Spotify, gedacht fürs iPad am Schreibtisch.
Großes Cover, langsam treibende Farbflächen in den Farben des Albums, leichtes Filmkorn, Uhrzeit und Datum.

Die Seite zeigt automatisch, was gerade auf deinem Spotify-Account läuft – egal ob am PC, Handy oder iPad.

## Features

- Hintergrundfarben werden live aus dem Album-Cover berechnet
- Sanfte Übergänge beim Songwechsel, Fortschrittsleiste, Pausen- und Leerlauf-Zustand
- Hält den Bildschirm wach (Screen Wake Lock, nach einmaligem Tippen)
- Quer- und Hochformat, randlos als Home-Bildschirm-App
- Unterstützt auch Podcasts
- Kein Server, kein Build-Schritt – eine einzige `index.html`

## Einrichtung

### 1. GitHub Pages aktivieren

Im Repo unter **Settings → Pages** als Quelle den Branch `main` (Ordner `/root`) wählen und speichern.
Nach ca. einer Minute ist die Seite erreichbar unter:

```
https://robynumberone.github.io/nowplaying/
```

### 2. Spotify-App anlegen

1. Auf [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard) einloggen → **Create app**
2. Name und Beschreibung frei wählen
3. **Redirect URI** exakt so eintragen (inkl. Schrägstrich am Ende):
   `https://robynumberone.github.io/nowplaying/`
4. Bei den APIs **Web API** anhaken, speichern
5. Die **Client ID** kopieren

### 3. Am iPad verbinden

1. Die Pages-Adresse in Safari öffnen
2. Client ID einfügen → **Mit Spotify verbinden**
3. Teilen → **Zum Home-Bildschirm** – von dort geöffnet läuft die Seite im Vollbild

Tipp: Unter Einstellungen → Anzeige & Helligkeit die automatische Sperre auf „Nie“ stellen, falls der Wake Lock nicht greift.

## Sicherheit

- Login über das offizielle **Authorization Code Flow mit PKCE** – kein Client Secret im Code
- Nur Leserechte: `user-read-currently-playing`, `user-read-playback-state`
- Tokens liegen ausschließlich im lokalen Speicher des Browsers auf dem Gerät
- Die Seite kommuniziert nur mit `accounts.spotify.com`, `api.spotify.com` und Google Fonts
- Zugriff jederzeit widerrufbar unter spotify.com → Konto → Apps verwalten

## Technik

Reines HTML/CSS/JavaScript ohne Abhängigkeiten. Pollt alle 3 Sekunden `GET /v1/me/player/currently-playing`, interpoliert den Fortschritt lokal und erneuert den Access Token automatisch über den Refresh Token.

Abmelden: kleiner Button „abmelden“ unten rechts.
