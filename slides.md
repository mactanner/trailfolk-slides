---
theme: default
title: Der DOM ist keine API
info: |
  ## Der DOM ist keine API: WebMCP für KI-Agenten
  DevCon Luzern, Oktober 2026
class: text-center
drawings:
  persist: false
transition: fade
duration: 40min
fonts:
  sans: Inter
  mono: JetBrains Mono
---

# Der DOM ist keine API

## WebMCP für KI-Agenten

<div class="mt-12 text-xl opacity-75">
  DevCon Luzern · Oktober 2026
</div>

<!--
Willkommen. Heute geht es nicht um "noch ein MCP", sondern um die Frage,
wie Agents sinnvoll mit laufenden Web-Apps zusammenarbeiten können - ohne den
DOM als inoffiziellen API-Vertrag behandeln zu müssen.

Timing: 0:00-0:30
-->

---
layout: center
class: text-left
transition: slide-up
---

<div class="text-5xl leading-relaxed mt-18">
Wie kann ein Agent mit einer komplexen Web-App arbeiten,
<span class="text-primary font-bold">ohne ihre menschliche Oberfläche
erraten zu müssen?</span>
</div>

<div class="mt-12 text-xl opacity-70">
Beispiel heute: eine Schweizer Wander-App
</div>

<!--
Das Zielbild kurz setzen: Die UI bleibt für Menschen zentral. WebMCP soll
Agents nicht von der Seite wegführen, sondern sie in denselben Kontext holen.

Timing: 0:30-1:30
-->

---
layout: center
class: text-left
transition: fade
---

<div class="text-sm tracking-widest uppercase opacity-55">Eine konkrete Absicht</div>

<div class="rounded-xl border border-primary/30 bg-primary/10 p-8 mt-6 text-3xl leading-relaxed">
  "Finde mir eine mittelschwere Wanderung in der Zentralschweiz,
  zwischen 8 und 14 Kilometern, maximal vier Stunden und mit mindestens
  500 Höhenmetern."
</div>

<div v-click class="mt-10 text-xl opacity-75">
Für einen Menschen: wenige gezielte Interaktionen.<br>
Für einen Agenten: Was genau muss er über die Seite wissen?
</div>

<!--
Hier Trailfolk kurz mit allen Resultaten und den sichtbaren Filtern zeigen.
Noch keine Live-Demo. Das Publikum soll die Aufgabe verstehen, bevor die
Technik kommt.

Timing: 1:30-3:00
-->

---
layout: two-cols
layoutClass: gap-12
transition: slide-left
---

# Agents lesen Oberflächen

<div class="mt-8 text-left text-xl leading-loose">

<div v-click>1. Screenshots lesen</div>
<div v-click>2. Verschachtelte DOM-Bäume und Accessibility Tree auswerten</div>
<div v-click>3. IDs, Labels und Controls erraten</div>
<div v-click>4. Klicken, tippen, warten</div>
<div v-click>5. Den resultierenden Zustand erneut auslesen</div>

</div>

::right::

<div class="rounded-xl border border-main/20 p-6 mt-8 text-left">

<div class="font-mono text-sm opacity-55 mb-5">Beispielhafte Schrittfolge</div>

1. Finde das passende DOM-Element
2. Öffne das Select
3. Wähle "Zentralschweiz"
4. Finde "Schwierigkeit"
5. Setze "Mittel"
6. Interpretiere Sliders
7. Lies die Resultatliste

</div>

<div class="mt-6 h-26 rounded-xl border-2 border-dashed border-primary/35 bg-primary/5 flex items-center justify-center text-center text-sm opacity-75">
  Bildplatzhalter: Screenshot eines Agents mit DOM- oder Accessibility-Tree
</div>

<!--
Wichtig: Nicht "Agents scrapen nur". Moderne Browser-Agents haben mehrere
Signale. Die Herausforderung ist trotzdem, dass sie Bedeutung aus
verschachtelten DOM-Bäumen, IDs und einer für Menschen optimierten Oberfläche
rekonstruieren.

Timing: 3:00-5:00
-->

---
layout: two-cols
layoutClass: gap-10
transition: fade
---

# Das funktioniert.

<div class="mt-10 text-left text-xl">

- Funktioniert ohne site-spezifische Integration
- Erschliesst auch ältere Websites
- Nutzt vorhandene Semantik und Accessibility

</div>

::right::

# Bis es bricht.

<div class="mt-10 text-left text-xl">

- Labels oder Layout ändern sich
- Dynamische Inhalte laden nach
- Gleichartige Controls sind mehrdeutig
- Sichtbarer und fachlicher Zustand können auseinanderlaufen

</div>

<div class="absolute bottom-10 left-0 right-0 text-center opacity-65">
Gutes semantisches HTML und Accessibility bleiben unverzichtbar.
</div>

<!--
Die Balance bewusst halten. WebMCP ist kein Argument gegen Accessibility.
Eine zugängliche Seite hilft Menschen und UI-automatisierenden Agents.

Timing: 5:00-7:00
-->

---
layout: center
class: text-left
transition: slide-up
---

<div class="text-sm tracking-widest uppercase opacity-55">Die Reibung</div>

<div class="text-5xl leading-relaxed mt-6">
UI-Automation zwingt einen Agenten,
<span class="text-primary font-bold">die Absicht hinter einer menschlichen
Oberfläche zu rekonstruieren.</span>
</div>

<div v-click class="text-2xl leading-relaxed mt-10 opacity-80">
Was wäre, wenn die Anwendung ihre ausgewählten Fähigkeiten selbst beschreiben
könnte?
</div>

<!--
Das ist der Übergang. Nicht mit einer Definition anfangen, sondern mit der
klaren Problemformulierung.

Timing: 7:00-8:00
-->

---
layout: center
class: text-left
transition: slide-left
---

<div class="text-sm tracking-widest uppercase opacity-55">Was ist WebMCP?</div>

# Web Model<br>Context Protocol

<div class="mt-8 text-2xl leading-relaxed">
  Eine vorgeschlagene <span class="text-primary font-bold">Web-Plattform-API</span>,
  mit der eine laufende Website über <code>document.modelContext</code> ihre
  Daten und Fähigkeiten als strukturierte Tools für Browser-Agents verfügbar
  macht.
</div>

<div class="grid grid-cols-2 gap-6 mt-12 text-left">
  <div v-click class="rounded-xl border border-main/20 p-5">
    <div class="font-bold text-primary">Woher kommt es?</div>
    <div class="mt-3 opacity-80">Offene Arbeit der W3C Web Machine Learning Community Group; Chrome erprobt die API experimentell.</div>
  </div>
  <div v-click class="rounded-xl border border-main/20 p-5">
    <div class="font-bold text-primary">Die Grundidee</div>
    <div class="mt-3 opacity-80">Statt Screen-Scraping und geratenen DOM-Details beschreibt die Seite selbst Daten und erlaubte Funktionen.</div>
  </div>
</div>

<!--
WebMCP steht für Web Model Context Protocol. Es ist ein offener Vorschlag aus der W3C Web Machine Learning Community Group, nicht der bestehende MCP-Standard und auch noch kein W3C Recommendation Standard. Die API hängt an document.modelContext.

Die Denkweise ist MCP-verwandt: Eine Anwendung beschreibt ihre Fähigkeiten als Tools. Der entscheidende Unterschied ist der Ausführungsort - die laufende Seite im Browser.

Timing: 8:00-10:00
-->

---
layout: default
class: tools-api-slide
transition: slide-up
---

<div class="text-sm tracking-widest uppercase opacity-55">Zwei APIs</div>

# Tools aus JavaScript<br>oder HTML

<div class="grid grid-cols-2 gap-8 mt-8 text-left">
  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-6">
    <div class="text-primary font-bold text-xl">Imperativ</div>
    <code class="block mt-5 text-sm">document.modelContext<br>.registerTool(...)</code>
    <div class="mt-6 text-lg">Für eigene Client-Logik, Navigation, Zustand und komplexe Abläufe.</div>
  </div>
  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-6">
    <div class="text-primary font-bold text-xl">Deklarativ</div>
    <code class="block mt-5 text-sm">&lt;form toolname="..."<br>tooldescription="..."&gt;</code>
    <div class="mt-6 text-lg">Für bestehende Formulare: Der Browser leitet Tool und Schema aus HTML ab.</div>
  </div>
</div>

<div v-click class="mt-8 text-xl opacity-75">
Beide Varianten halten die Interaktion sichtbar in der Website.
</div>

<!--
WebMCP hat zwei Zugänge. Die imperative API definiert Tools mit JavaScript - etwa für komplexe, zustandsbehaftete Anwendungen wie Trailfolk. Die deklarative API annotiert vorhandene HTML-Formulare über toolname und tooldescription; der Browser erzeugt daraus ein strukturiertes Tool.

Timing: 10:00-12:00
-->

---
layout: default
transition: fade
---

<div class="text-sm tracking-widest uppercase opacity-55">Abgrenzung</div>

# MCP und WebMCP<br>arbeiten zusammen.

<div class="mt-8 text-left text-lg">

| | MCP / OpenAPI im Backend | WebMCP im Browser |
|---|---|---|
| Tool lebt bei | Service oder API | Laufender Web-App |
| Gut für | System- und Server-Workflows | UI-, Session- und Kontext-Workflows |
| Benutzeroberfläche | Kann umgangen werden | Bleibt sichtbar und synchron |
| Beispiel | Flug suchen, Zahlung auslösen | Form ausfüllen, Filter setzen, Design bearbeiten |

</div>

<div class="mt-6 rounded-xl border border-primary/30 bg-primary/10 p-5 text-xl text-left">
WebMCP ersetzt keine Backend-Integration. Es ergänzt sie dort, wo der
Browser-Kontext Teil der Aufgabe ist.
</div>

<!--
MCP und WebMCP sind keine konkurrierenden Optionen. Wenn ein Dienst eine serverseitige Operation für einen Agenten bereitstellt, ist MCP oder OpenAPI passend. WebMCP setzt dort an, wo die bereits geöffnete Webseite, ihr Zustand, die UI und die Kontrolle des Nutzers wichtig sind.

Timing: 12:00-14:00
-->

---
layout: default
transition: slide-left
---

<div class="text-sm tracking-widest uppercase opacity-55">Gemeinsamer Kontext</div>

<div class="mt-3 text-5xl font-bold tracking-tight leading-tight">
  Eine Seite. <span class="text-primary">Ein Zustand.</span>
</div>

```mermaid {scale: 0.62}
sequenceDiagram
    participant U as Nutzer
    participant A as Browser-Agent
    participant P as Web-App
    participant S as Backend

    U->>A: Wunsch
    A->>P: Tool aufrufen
    P->>S: Bestehende API
    S-->>P: Daten
    P-->>A: Tool-Ergebnis
    P-->>U: UI aktualisiert
```

<div class="mt-8 text-lg opacity-70">
Mensch, Agent und Seite arbeiten mit demselben sichtbaren Zustand.
</div>

<!--
Das ist der wichtigste Unterschied zu einem reinen Backend-Connector.
Die Seite kann ihren Login, ihren aktuellen Kontext und ihre UI weiter selbst
besitzen. Backend-MCP und OpenAPI bleiben für reine Server-Workflows sinnvoll.

Timing: 14:00-16:00
-->

---
layout: center
class: text-left
transition: fade
---

<div class="text-sm tracking-widest uppercase opacity-55">Wann ist WebMCP sinnvoll?</div>

# Wenn der Browser-<br>Kontext zählt.

<div class="grid grid-cols-2 gap-5 mt-8 text-left">
  <div v-click class="rounded-xl border border-main/20 p-5">
    <div class="font-bold text-primary">Support</div>
    <div class="mt-2">Komplexe Formulare korrekt finden und vorbefüllen.</div>
  </div>
  <div v-click class="rounded-xl border border-main/20 p-5">
    <div class="font-bold text-primary">Buchungen</div>
    <div class="mt-2">Mehrere Reisende, Termine und sichtbare Bestätigungsschritte.</div>
  </div>
  <div v-click class="rounded-xl border border-main/20 p-5">
    <div class="font-bold text-primary">Interaktive Anwendungen</div>
    <div class="mt-2">Filtern, planen, gestalten oder konfigurieren mit geteiltem Zustand.</div>
  </div>
  <div v-click class="rounded-xl border border-main/20 p-5">
    <div class="font-bold text-primary">Entwickler-Tools</div>
    <div class="mt-2">Diagnosen oder klar begrenzte Aktionen hinter verschachtelten Menüs.</div>
  </div>
</div>

<div class="mt-8 text-xl opacity-75">
Trailfolk ist ein kleines Beispiel für den dritten Fall.
</div>

<!--
Diese vier Cases stammen aus der Chrome-Dokumentation: Support-Formulare, komplexe Reisebuchungen, agentische Interaktionen in nutzerorientierten Oberflächen und Diagnosen in Entwickler-Einstellungen.

Das hilft, Trailfolk richtig einzuordnen: nicht der Hauptgrund für WebMCP, sondern ein anschauliches Beispiel für gemeinsame Interaktion in einer zustandsbehafteten UI.

Timing: 16:00-18:00
-->

---
layout: center
class: text-left
transition: slide-up
---

<div class="text-sm tracking-widest uppercase opacity-55">Live-Demo</div>

<div class="text-5xl mt-4">Trailfolk</div>

<div class="grid grid-cols-2 gap-8 mt-12">
  <div v-click class="rounded-xl border border-main/20 p-7">
    <div class="text-primary font-bold">Entdecken</div>
    <div class="mt-3 text-xl">Filter sichtbar setzen</div>
    <code class="block mt-6 opacity-75">filter_hikes</code>
    <code class="block mt-2 opacity-75">reset_hike_filters</code>
  </div>
  <div v-click class="rounded-xl border border-main/20 p-7">
    <div class="text-primary font-bold">Inspiration</div>
    <div class="mt-3 text-xl">Empfehlungen begründen</div>
    <code class="block mt-6 opacity-75">recommend_hikes</code>
    <code class="block mt-2 opacity-75">show_recommendation_summary</code>
  </div>
</div>

<div class="mt-10 text-xl opacity-75">
Die verfügbaren Tools folgen dem sichtbaren Kontext der Anwendung.
</div>

<div class="mt-8 h-24 rounded-xl border-2 border-dashed border-primary/35 bg-primary/5 flex items-center justify-center text-center text-sm opacity-75">
  Bildplatzhalter: Trailfolk-Startansicht mit den Tabs "Entdecken" und "Inspiration"
</div>

<!--
Zur Live-Demo wechseln. Der Demo-Teil ist bewusst ein erster Draft:
Welche Prompts letztlich gezeigt werden, kann später angepasst werden.
Der Tab-Wechsel ist aber ein starkes Signal: Die Tool-Oberfläche kann zum
aktuellen Kontext passen.

Timing: 16:00-17:00
-->

---
layout: two-cols
layoutClass: gap-12
transition: fade
---

# Sag, was du willst.

<div class="mt-8 text-left">

## Nutzerwunsch

> Filtere auf mittelschwere Wanderungen in der Zentralschweiz, zwischen
> 8 und 14 Kilometern, mit mindestens 500 Höhenmetern und höchstens vier
> Stunden Gehzeit.

</div>

::right::

<div class="mt-8 text-left">

## Sichtbar machen

1. Tool-Aufruf mit strukturierten Werten
2. Filter-Chips ändern sich
3. Resultatzahl aktualisiert sich
4. Passende Wanderkarten bleiben sichtbar

<div class="mt-10 p-4 rounded bg-primary/10">
Die UI ist nicht nur ein Transportmittel. Sie ist die überprüfbare
Arbeitsfläche für den Nutzer.
</div>

<div class="mt-6 h-24 rounded-xl border-2 border-dashed border-primary/35 bg-primary/5 flex items-center justify-center text-center text-sm opacity-75">
  Bildplatzhalter: Trailfolk nach dem Tool-Aufruf mit sichtbaren Filter-Chips und Resultaten
</div>

</div>

<!--
Live-Demo: Start auf "Entdecken". Das konkrete Prompt kann noch geändert
werden. Wichtig ist der Vorher-/Nachher-Effekt in der UI.

Die aktuelle Trailfolk-API unterstützt minElevation, nicht maxElevation.

Timing: 17:00-22:00
-->

---
layout: two-cols
layoutClass: gap-12
transition: slide-left
---

# Von Treffern<br>zu Empfehlungen.

<div class="mt-8 text-left">

## Nutzerwunsch

> Empfiehl mir zwei mittelschwere Wanderungen in der Zentralschweiz,
> maximal vier Stunden, mit einem krönenden Dessert danach.

</div>

::right::

<div class="mt-8 text-left">

## Ablauf

1. Zum Tab **Inspiration** wechseln
2. `recommend_hikes` liefert bis zu drei Treffer
3. Der Agent ergänzt Gründe
4. `show_recommendation_summary` schreibt sie an die Karten

<div class="mt-10 p-4 rounded bg-primary/10">
Der Agent gibt nicht nur Text zurück. Er versetzt die Anwendung in einen
verständlichen, sichtbaren Zustand.
</div>

<div class="mt-6 h-24 rounded-xl border-2 border-dashed border-primary/35 bg-primary/5 flex items-center justify-center text-center text-sm opacity-75">
  Bildplatzhalter: Trailfolk-Empfehlungskarten mit AI-Begründungen
</div>

</div>

<!--
Live-Demo: Erst den Tab "Inspiration" öffnen, da die Tools kontextabhängig
registriert werden. Diesen zweiten Teil nur zeigen, wenn der erste stabil
gelaufen ist und genug Zeit bleibt.

Timing: 22:00-27:00
-->

---
layout: center
class: text-left
transition: slide-up
---

# Tools sind APIs.

<div class="grid grid-cols-2 gap-8 mt-10">
  <div v-click>
    <div class="text-primary font-bold text-xl mb-4">Ein gutes Tool</div>
    <ul class="text-lg leading-relaxed">
      <li>hat eine fachliche, begrenzte Aufgabe</li>
      <li>fordert nur notwendige Parameter an</li>
      <li>validiert Eingaben klar</li>
      <li>liefert fachlichen Zustand zurück</li>
      <li>hat erkennbare Nebenwirkungen</li>
    </ul>
  </div>
  <div v-click>
    <div class="text-primary font-bold text-xl mb-4">Trailfolk als Beispiel</div>
    <ul class="text-lg leading-relaxed">
      <li>Distanz, Dauer und Anzahl sind begrenzt</li>
      <li>Schwierigkeit und Region sind kontrollierte Werte</li>
      <li>Empfehlungen sind auf drei begrenzt</li>
      <li>Begründungen referenzieren bekannte Wanderungen</li>
    </ul>
  </div>
</div>

<div class="mt-12 text-2xl">
Würden wir dieselbe Schnittstelle auch einem externen Entwickler guten
Gewissens geben?
</div>

<!--
Jetzt den Engineering-Mehrwert herausarbeiten. Das Tool-Schema ist nicht nur
LLM-Konfiguration, sondern ein API-Vertrag mit Produkt- und Security-Folgen.

Timing: 27:00-30:00
-->

---
layout: two-cols
layoutClass: gap-12
transition: fade
---

# Kein Freipass<br>für Agents.

<div class="mt-8 text-left text-xl">

- Kein Ersatz für ein zugängliches, gut bedienbares UI
- Kein Ersatz für Backend-MCP oder OpenAPI
- Kein Grund, unausgereifte Agenten unbeaufsichtigt handeln zu lassen
- Kein Versprechen für breite Browser-Verfügbarkeit

</div>

::right::

# Vertrauen<br>braucht Grenzen.

<div class="mt-8 text-left text-xl">

- Welche Aktionen brauchen Bestätigung?
- Wie klein kann ein Tool-Zugriff sein?
- Was ist untrusted Content?
- Welche Daten darf ein Tool verarbeiten?
- Wie funktioniert ein guter Fallback?

</div>

<!--
Ein bewusst nüchterner Moment. Für ein Filter-Tool sind die Risiken gering,
für Kauf, Buchung, Löschen oder Kontoänderungen wesentlich höher.

Timing: 30:00-33:00
-->

---
layout: center
class: text-left
transition: slide-left
---

# Verantwortung<br>ist ein Feature.

<div class="grid grid-cols-3 gap-5 mt-12 text-center">
  <div v-click class="rounded-xl border border-main/20 p-6">
    <div class="font-bold text-primary">Read</div>
    <div class="mt-3">Suchen, filtern, erklären</div>
  </div>
  <div v-click class="rounded-xl border border-main/20 p-6">
    <div class="font-bold text-primary">Write</div>
    <div class="mt-3">Speichern, ändern, teilen</div>
  </div>
  <div v-click class="rounded-xl border border-main/20 p-6">
    <div class="font-bold text-primary">Consequential</div>
    <div class="mt-3">Kaufen, buchen, löschen</div>
  </div>
</div>

<div class="mt-12 text-2xl leading-relaxed">
Je folgenreicher ein Tool, desto klarer müssen Berechtigung, Bestätigung,
Rückmeldung und Abbruch sein.
</div>

<!--
WebMCP kennt Tool-Annotationen und das Thema consequential actions ist im
Entwurf sichtbar. Aber die Anwendung und der Browser-Agent bleiben für die
konkreten Schutzmechanismen verantwortlich.

Timing: 33:00-35:00
-->

---
layout: two-cols
layoutClass: gap-12
transition: slide-up
---

# Experiment<br>mit Rückenwind.

<div class="mt-8 text-left">

## Spezifikation

**Draft Community Group Report**

W3C Web Machine Learning Community Group

<div class="mt-8 opacity-75">
Kein W3C Recommendation Standard.<br>
Kein formaler Recommendation Track.
</div>

</div>

::right::

<div class="mt-8 text-left">

## Implementierungen

- Chrome 149: Origin Trial
- Edge 150: Origin Trial
- Brave Leo: experimentell dokumentiert
- ChatGPT Desktop: dokumentiert

<div class="mt-8 opacity-75">
Für Experimente: ja.<br>
Für breite Produktionsannahmen: noch vorsichtig.
</div>

</div>

<!--
Diese Folie unmittelbar vor der Konferenz aktualisieren. Die Angaben sind ein
Snapshot vom 10. September 2026 und verändern sich bei experimentellen
Browser-APIs schnell.

Timing: 35:00-37:00
-->

---
layout: center
class: text-left
transition: fade
---

<div class="text-sm tracking-widest uppercase opacity-55">Ausblick</div>

<div class="text-3xl leading-relaxed mt-6">
Vielleicht ist das nicht die wichtigste Frage.
</div>

<div v-click class="text-4xl leading-relaxed mt-12 text-primary font-bold">
Welche Fähigkeiten eurer Web-App sind wertvoll, klar abgegrenzt und
zustandsbehaftet genug, dass ihr sie einem Agenten kontrolliert anbieten
möchtet?
</div>

<!--
Nicht auf die Prognose einlassen. Der Wert für das Publikum ist die
Design-Frage, die sie schon heute auf ihre Anwendungen übertragen können.

Timing: 37:00-38:30
-->

---
layout: center
class: text-left
transition: slide-left
---

# Was bleibt?

<div class="mt-12 text-2xl leading-loose">

<div v-click><span class="text-primary font-bold">1.</span> WebMCP macht ausgewählte
Web-Fähigkeiten explizit, statt sie aus der UI erraten zu lassen.</div>

<div v-click><span class="text-primary font-bold">2.</span> Es ergänzt Backend-MCP,
APIs, Accessibility und menschliche Kontrolle - es ersetzt sie nicht.</div>

<div v-click><span class="text-primary font-bold">3.</span> Der Erfolg hängt an
gutem Tool-Design, klaren Grenzen und verantwortungsvoller UX.</div>

</div>

<!--
Timing: 38:30-39:30
-->

---
layout: center
class: text-center
transition: fade
---

# Nicht nur Buttons zeigen.

<div class="text-4xl text-primary font-bold mt-10">
Bewusst Fähigkeiten anbieten.
</div>

<div class="mt-16 text-sm opacity-60">
Quellen: webmachinelearning.github.io/webmcp · github.com/webmachinelearning/webmcp
</div>

<!--
Danke. Bei Fragen auf die Demo, Tool-Design oder den experimentellen
Spezifikationsstand eingehen.

Timing: 39:30-40:00
-->
