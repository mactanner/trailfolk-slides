# Der DOM ist keine API

Slidev-Deck fuer die DevCon Luzern 2026:

> **WebMCP fuer KI-Agenten** - wie Web-Apps ihre Daten und klar abgegrenzten
> Faehigkeiten als strukturierte Tools fuer Browser-Agents anbieten koennen.

Die Praesentation verwendet Trailfolk, eine Schweizer Wander-App, als
anschauliches Beispiel. Sie behandelt die Grenzen von UI-Automation, WebMCP als
Web-Plattform-API, die imperative JavaScript- sowie deklarative HTML-API und
verantwortungsvolles Tool-Design.

## Voraussetzungen

- Node.js
- npm

## Lokal starten

```bash
npm install
npm run dev
```

Slidev oeffnet die Praesentation standardmaessig im Browser. Die Slides liegen in
[`slides.md`](./slides.md).

## Befehle

| Befehl | Zweck |
| --- | --- |
| `npm run dev` | Lokalen Slidev-Entwicklungsserver starten |
| `npm run build` | Statische Produktionsversion nach `dist/` bauen |
| `npm run export` | Praesentation exportieren |

## Projektstruktur

| Pfad | Inhalt |
| --- | --- |
| [`slides.md`](./slides.md) | Slides, Frontmatter und Speaker Notes |
| [`styles/index.css`](./styles/index.css) | Dunkles WebMCP-Theme und globale Typografie |
| [`components/global-top.vue`](./components/global-top.vue) | Fortschrittsanzeige am oberen Rand |
| [`global-top.vue`](./global-top.vue) | Von Slidev erwarteter Einstiegspunkt fuer die globale Komponente |
| [`analysis/abstract.md`](./analysis/abstract.md) | Eingereichtes Session-Abstract |

## Hinweise

- Die Fortschrittsanzeige erscheint im Praesentations- und Fullscreen-Modus,
  wird beim Print-/PDF-Export aber ausgeblendet.
- Einige Folien enthalten Bildplatzhalter fuer die Trailfolk-Live-Demo.
- WebMCP ist zum Zeitpunkt der Praesentation ein experimenteller W3C Community
  Group Draft. Aussagen zur Browser-Unterstuetzung sollten vor dem Vortrag
  aktualisiert werden.
