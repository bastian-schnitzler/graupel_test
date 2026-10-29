# Vorschau der Website (web/S1)

Statische Vorschau des fertigen Stands von WEB-S1 (REQ-439, DEC-034), Version 0.1.0, gebaut aus b61bef0.
Erzeugt mit `pnpm preview:build` (`apps/web/scripts/build-preview.mjs`); nicht von Hand ändern.

**Öffnen:** `index.html` in diesem Ordner über einen beliebigen statischen Webserver, z. B. im Review-Bereich der
Exequiae-App oder lokal mit `python3 -m http.server -d preview/web` und <http://localhost:8000/>. Alle Pfade sind
relativ, die Vorschau läuft unter jedem Unterpfad.

Die Leiste oben wählt die Domain-Konfiguration; die Seite darunter ist dieselbe Website mit der `config.json` der
Domain (Startort, Sprache, Favoriten, Impressum, Datenschutz). Auf dem Telefon (schmaler als 640 px oder quer
gehalten) fehlt die Leiste: Die Seite füllt den Bildschirm und zeigt graupel.eu; eine andere Domain
wählt dort der Hash (`index.html#ch` usw.). Jede Domain hat einen eigenen Ordner:

- `at/index.html`: graupel.at (Startort Großglockner)
- `ch/index.html`: graupel.ch (Startort Matterhorn)
- `fr/index.html`: graupel.fr (Startort Mont Blanc)
- `it/index.html`: graupel.it (Startort Ortler)
- `eu/index.html`: graupel.eu (Startort Brüssel)

`assets/` enthält das gemeinsame Bundle, die Domain-Ordner laden es mit `../assets/`.

## Einschränkungen

- Nicht per Doppelklick (`file://`): Browser laden dort keine ES-Module und kein `config.json` per `fetch`.
- Ortssuche, Höhe und Wetterdaten kommen live von Open-Meteo, die Kartenkacheln von OpenTopoMap. Ohne Internet oder
  wenn die Umgebung, in der die Vorschau läuft, Anfragen an fremde Hosts sperrt (z. B. eine Content Security Policy
  der einbettenden App), bleiben Meteogramm, Suchvorschläge und Karte leer bzw. zeigen ihren Fehlerzustand.
- Alle Domains teilen sich einen Ursprung: Sprache, Farbmodus und Favoriten im `localStorage` gelten in der Vorschau
  für alle Domains zugleich (im Betrieb hat jede Domain ihren eigenen Speicher).
- Installation als App ist in der Vorschau nicht vorgesehen (das Manifest liegt eine Ebene über den Domain-Ordnern).
