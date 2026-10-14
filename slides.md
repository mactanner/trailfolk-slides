---
theme: default
css: unocss
title: Der DOM ist keine API
info: |
  ## Der DOM ist keine API: WebMCP für KI-Agenten
  DevCon Lozärn, 23. Oktober 2026
class: text-center
drawings:
  persist: false
transition: fade
duration: 20min
fonts:
  sans: Inter
  mono: JetBrains Mono
---

<div class="h-full flex flex-col items-center justify-center">
  <div class="text-sm tracking-widest uppercase opacity-60">
    WebMCP für KI-Agenten
  </div>

  <h1 class="!mt-6 !text-center !text-6xl font-sans tracking-tight">
    Der DOM ist<br><span class="text-primary">keine API</span>
  </h1>

  <div class="mt-12 text-xl opacity-70">
    DevCon Lozärn · 23. Oktober 2026
  </div>
</div>

<!--
Kurzer Einstieg mit Titel und Thema.

Timing: 0:00-0:20
-->

---
layout: center
class: text-left
transition: slide-up
---

<div class="mt-12 rounded-xl border border-primary/30 bg-primary/5 px-10 py-9 text-3xl leading-relaxed">
  „Ich suche eine anspruchsvolle Wanderung im Berner Oberland - rund 15 km und mindestens 1000 Meter Aufstieg.“
</div>


<!--
Der Hook ist ein konkreter Nutzerwunsch. Für Menschen ist die Absicht klar;
Software muss sie erst in die Bedienung einer Seite übersetzen.

Timing: 0:20-1:00
-->

---
layout: two-cols-header
layoutClass: gap-10
transition: slide-left
---

# Trailfolk

::left::

<div class="mt-6 text-left text-xl leading-relaxed">

Eine kleine Schweizer Wander-App.

- Filter: Region, Schwierigkeit, Distanz, Dauer, Höhenmeter
- Resultatliste mit Wanderkarten

</div>

::right::

<div class="mt-4">
  <a href="http://localhost:5173" target="_blank" rel="noopener noreferrer">
    <img
      src="./images/trailfolk-filters.png"
      alt="Trailfolk-Startansicht mit Filtern und Resultatliste"
      class="w-full h-80 object-contain object-top"
    />
  </a>
</div>

<!--
Trailfolk kurz aus Sicht eines Menschen vorstellen: Filter setzen, Resultate
sehen, eine Wanderung öffnen. Nur so viel zeigen, dass die App verständlich ist.

Der Screenshot öffnet auf Klick die lokale Trailfolk-App.

Timing: 1:00-3:00
-->

---
layout: center
class: text-left
transition: fade
---


<div class="text-5xl leading-relaxed mt-6">
Wie gehen <span class="text-primary font-bold">Web Agents</span> hier vor?
</div>

<div class="mt-6 text-lg opacity-70">
Web Agents lesen und bedienen Websites im Browser - im Auftrag eines Nutzers.
</div>

<div v-click class="mt-30">
  <div class="grid grid-cols-3 gap-5 mt-3">
    <div class="rounded-xl border border-primary/30 bg-white p-5">
      <img src="./images/logo-browser-use.png" alt="Browser Use" class="w-full h-12 object-contain" />
    </div>
    <div class="rounded-xl border border-primary/30 bg-white p-5">
      <img src="./images/logo-skyvern.png" alt="Skyvern" class="w-full h-12 object-contain" />
    </div>
    <div class="rounded-xl border border-primary/30 bg-white p-5">
      <img src="./images/logo-stagehand.png" alt="Stagehand" class="w-full h-12 object-contain" />
    </div>
  </div>
</div>

<!--
Nach der Trailfolk-Einordnung folgt die Leitfrage: Wie setzt ein Web Agent den
Nutzerwunsch heute um? Browser Use, Skyvern und Stagehand zeigen: Dafür gibt es
bereits mehrere Angebote. Die nächste Folie beantwortet das Vorgehen Schritt
für Schritt.

Timing: 3:00-4:30
-->

---
layout: two-cols-header
layoutClass: gap-10
transition: slide-left
---

# Wie ein Agent das heute macht

::left::

<div class="mt-6 text-left text-lg leading-loose">

<div v-click>1. Screenshot und DOM lesen</div>
<div v-click>2. Accessibility-Tree auswerten</div>
<div v-click>3. Passende Controls raten (IDs, Labels)</div>
<div v-click>4. Klicken, tippen, warten</div>
<div v-click>5. Den neuen Zustand erneut auslesen</div>
<div v-click>6. Zurück zu Schritt 1</div>

</div>

::right::

<div class="mt-4">
  <a href="http://127.0.0.1:7788/?__theme=dark" target="_blank" rel="noopener noreferrer">
    <img
      src="./images/browser-use-webui.png"
      alt="Browser Use Web UI"
      class="w-full h-80 object-contain object-top"
    />
  </a>
</div>


<!--
Nicht "Agents scrapen nur". Moderne Agents nutzen mehrere Signale. Der Punkt:
Bedeutung wird aus einer für Menschen gebauten Oberfläche rekonstruiert - Schritt
für Schritt, jedes Mal neu.

Timing: 4:30-5:30
-->

---
layout: two-cols
layoutClass: gap-10
transition: fade
---

<h1>Das funktioniert</h1>

<div class="mt-8 text-left text-xl leading-relaxed">

  <ul class="list-disc pl-6">
    <li>Braucht keine Integration seitens der Seite</li>
    <li>Funktioniert auch bei alten Seiten</li>
    <li>Nutzt vorhandene Semantik und Accessibility</li>
  </ul>

</div>

::right::

<h1 v-click="1">Aber ...</h1>

<div v-click="1" class="mt-8 text-left text-xl leading-relaxed">

  <ul class="list-disc pl-6">
    <li>Viele Schritte für eine einfache Absicht</li>
    <li>Zustand nach jeder Aktion neu lesen</li>
    <li>Mehrdeutige Controls, Fehlklicks</li>
    <li>Bedeutung wird geraten, nicht gegeben</li>
  </ul>

</div>

<div v-click="2" class="absolute inset-0 z-10 flex items-center justify-center bg-slate-900/20 px-12 backdrop-blur-sm">
  <div class="flex flex-col items-center">
    <a
      href="https://makeameme.org/meme/inefficiency-inefficiency"
      target="_blank"
      rel="noopener noreferrer"
    >
      <img
        src="./images/inefficiency.png"
        alt="Inefficiency Meme"
        class="max-h-[58vh] max-w-3xl object-contain"
      />
    </a>
    <a
      href="https://makeameme.org/meme/inefficiency-inefficiency"
      target="_blank"
      rel="noopener noreferrer"
      class="mt-3 text-xs opacity-40 hover:opacity-70"
    >
      makeameme.org/meme/inefficiency-inefficiency
    </a>
  </div>
</div>


<!--
UI-Automation bricht nicht einfach. Sie ist ein Umweg: ineffizient und ungenau.
Wichtig für dieses Publikum: WebMCP ist kein Argument gegen Accessibility.
Zugängliche Seiten helfen weiterhin Menschen und UI-basierten Agents.

Timing: 5:30-6:30
-->

---
layout: center
class: text-left
transition: slide-up
---

<div class="text-5xl leading-relaxed">
Was, wenn die Webseite ihre Fähigkeiten
<span class="text-primary font-bold">selbst beschreibt</span> -
statt sie erraten zu lassen?
</div>

<!--
Der Übergang. Kurz und ohne Definition. Die Frage öffnet WebMCP.

Timing: 6:30-7:00
-->

---
layout: default
class: text-left
transition: slide-left
---

# WebMCP - Web Model Context Protocol

<div class="mt-12 text-3xl leading-relaxed">
Ein Vorschlag für einen Webstandard, mit dem Websites
<span class="text-primary font-bold">Aktionen für KI-Agenten beschreiben</span>.
</div>

<div v-click class="mt-12 text-2xl leading-relaxed">
Jede Aktion ist ein <span class="font-bold text-primary">Tool</span>: Name, Beschreibung, Eingaben.
</div>

<div class="absolute bottom-6 right-8 text-sm opacity-60">
  <a href="https://webmachinelearning.github.io/webmcp/" target="_blank" rel="noopener noreferrer">Vorschlag der W3C Web Machine Learning Community Group (Google und Microsoft).</a>
</div>

<!--
WebMCP steht für Web Model Context Protocol. Der Vorschlag wird von Ingenieuren
von Google und Microsoft in der W3C Web Machine Learning Community Group
entwickelt; er ist noch kein verabschiedeter Standard. Kern: Die Website
benennt die erlaubten Aktionen und ihre Eingaben. Dadurch muss der Agent
nicht aus der Oberfläche rekonstruieren, welche Klicks nötig wären.
Die technische Umsetzung mit Formularen und JavaScript kommt später.

Timing: 7:00-8:00
-->

---
layout: default
transition: fade
---

# WebMCP in Trailfolk

<div class="mt-16 rounded-xl border border-primary/30 bg-primary/5 px-10 py-9 text-3xl leading-relaxed">
  „Ich suche eine anspruchsvolle Wanderung im Berner Oberland - rund 15 km und mindestens 1000 Meter Aufstieg.“
</div>

<div class="mt-12 text-center">
  <a href="http://localhost:5173" target="_blank" rel="noopener noreferrer"
    class="inline-flex items-center gap-3 rounded-xl bg-primary px-8 py-3 text-xl font-bold text-[#061126] shadow-lg shadow-primary/20 transition hover:bg-[#8dd9f3] focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-primary">
    Demo <span aria-hidden="true">↗</span>
  </a>
</div>

<!--
Jetzt direkt auf der Website zeigen, wie Trailfolk dem Agenten die passende
Aktion anbietet und wie sich das Ergebnis in der Seite zeigt. Keine weiteren
Schritte vorwegnehmen - die Demo spricht für sich.

Timing: 8:00-10:30
-->

---
layout: default
transition: slide-up
---

# Zwei Wege für den Agenten

<div class="grid grid-cols-2 gap-12 mt-8 text-left text-lg leading-relaxed">
<div>
<h2>Co-Browsing</h2>
<p class="mt-4">Mensch und Assistent arbeiten <span class="font-bold text-primary">auf derselben Seite</span> im Browser. Der Mensch kann die Schritte verfolgen und eingreifen.</p>
<div class="mt-6 rounded-xl border border-main/20 p-4">Beispiel: ChatGPT Desktop nutzt WebMCP-Tools im integrierten Browser.</div>
</div>
<div>
<h2>Remote Browsing</h2>
<p class="mt-4">Eine KI-Anwendung öffnet <span class="font-bold text-primary">ihren eigenen Browser</span> und erledigt die Aufgabe, mit oder ohne Live-Ansicht für den Menschen.</p>
<div class="mt-6 rounded-xl border border-main/20 p-4">Die Website kann auch dort Tools bereitstellen - statt nur eine Oberfläche zum Klicken.</div>
</div>
</div>

<div class="absolute bottom-6 right-8 text-sm opacity-60">
  Aktueller Stand: <a href="https://webmcp.com/ecosystem-tracker" target="_blank" rel="noopener noreferrer">webmcp.com/ecosystem-tracker</a>
</div>

<!--
Zwei Einsatzweisen unterscheiden: Co-Browsing teilt den sichtbaren Seitenzustand,
Remote Browsing nutzt einen separaten Browser der KI-Anwendung. ChatGPT Desktop
unterstützt laut webmcp.com WebMCP-Site-Tools seit August 2026; Gemini in Chrome
ist ebenfalls ein Browser-Assistent, nutzt WebMCP-Tools aber noch nicht.
Die 2.982 verifizierten Seiten sind ein Verzeichnis-Snapshot und
keine Aussage über Browser-Abdeckung oder erfolgreiche Agenten-Aufgaben.
Unterstützung und Zahl vor dem Vortrag erneut prüfen.

Timing: 10:30-11:30
-->

---
layout: default
transition: slide-left
---

<div class="text-sm tracking-widest uppercase opacity-55">Under the hood</div>

# Wie funktioniert WebMCP?

<div class="flex items-start justify-center gap-2 mt-6 text-center text-sm">
  <div class="flex-1 h-20 flex flex-col justify-center rounded-xl border border-main/25 p-3">
    <div class="font-bold">🧑 Nutzer</div>
    <div class="opacity-70 mt-1">Wunsch in natürlicher Sprache</div>
  </div>
  <div class="h-20 flex items-center text-primary text-2xl">→</div>
  <div class="flex-1 flex flex-col items-center gap-1">
    <div class="w-full h-20 flex flex-col justify-center rounded-xl border border-main/25 p-3">
      <div class="font-bold">🤖 Browser-Agent</div>
      <div class="opacity-70 mt-1">wählt passendes Tool</div>
    </div>
    <div class="text-amber-400 text-lg leading-none">↕</div>
    <div class="w-full rounded-xl border-2 border-amber-400 bg-amber-400/10 p-2 text-xs">
      <div class="font-bold text-amber-400">KI-Plattform · LLM</div>
      <div class="opacity-80">meist remote · ggf. Token-Kosten</div>
    </div>
  </div>
  <div class="h-20 flex items-center text-primary text-2xl">→</div>
  <div class="flex-[1.3] h-20 flex flex-col justify-center rounded-xl border-2 border-primary bg-primary/10 p-3">
    <div class="font-bold text-primary">Web-App · eigene Tools</div>
    <div class="opacity-80 mt-1">Seiten-Code, kein zusätzliches Modell</div>
  </div>
  <div class="h-20 flex items-center text-primary text-2xl">→</div>
  <div class="flex-1 h-20 flex flex-col justify-center rounded-xl border border-main/25 p-3">
    <div class="font-bold">Backend</div>
    <div class="opacity-70 mt-1">bestehende API (optional)</div>
  </div>
</div>

<div class="text-center mt-4 text-sm leading-relaxed">
  Das <span class="text-amber-400 font-bold">Modell interpretiert den Wunsch</span> - die
  <span class="text-primary font-bold">Tools führen den Code aus</span>.
</div>

<div class="grid grid-cols-2 gap-6 mt-8 text-left text-lg leading-snug">
  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-5">
    <div class="font-bold text-primary text-xl">Kein zusätzlicher Tool-Server</div>
    <div class="mt-2">Tools laufen in der Web-App und können bestehende Backend-APIs nutzen.</div>
  </div>
  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-5">
    <div class="font-bold text-primary text-xl">Session &amp; Kontext nutzen</div>
    <div class="mt-2">Login-, UI- und Anwendungszustand der laufenden Seite stehen zur Verfügung.</div>
  </div>
</div>

<!--
Wichtig: als typische Architektur präsentieren, nicht als zwingenden Ablauf jeder
WebMCP-Implementierung. WebMCP ist derzeit noch ein vorgeschlagener Webstandard.
Das Modell interpretiert den Wunsch (meist remote, ggf. Kosten); die Tools führen
Seiten-Code im Kontext der Webseite aus.

Timing: 11:30-12:30
-->

---
layout: default
class: tools-api-slide
transition: slide-up
---

<div class="text-sm tracking-widest uppercase opacity-55">Der Code</div>

# Imperativ oder deklarativ

<div class="grid grid-cols-2 gap-8 mt-8 text-left">
  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-6">
    <div class="text-primary font-bold text-xl">Imperativ (JS)</div>
    <code class="block mt-4 text-sm">document.modelContext<br>.registerTool({ … })</code>
    <div class="mt-5 text-lg">Für eigene Logik, Navigation, Zustand, komplexe Abläufe.</div>
  </div>
  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-6">
    <div class="text-primary font-bold text-xl">Deklarativ (HTML)</div>
    <code class="block mt-4 text-sm">&lt;form toolname="…"<br>tooldescription="…"&gt;</code>
    <div class="mt-5 text-lg">Für bestehende Formulare - der Browser leitet Tool und Schema ab.</div>
  </div>
</div>

<!--
Überblick vor dem konkreten Code. Imperativ für zustandsbehaftete Apps wie
Trailfolk, deklarativ für vorhandene HTML-Formulare.

Timing: 12:30-13:30
-->

---
layout: default
transition: fade
---

<div class="text-sm tracking-widest uppercase opacity-55">Imperativ · JavaScript</div>

# <i>filter_hikes</i>&nbsp;&nbsp;&nbsp;als Tool

```js {all|1|2|3|4-14|15-18}
await document.modelContext.registerTool({
  name: 'filter_hikes',
  description: 'Filtert Wanderungen nach Region, Schwierigkeit, Distanz, Dauer und Höhenmetern.',
  inputSchema: {
    type: 'object',
    properties: {
      region: { type: 'string', enum: ['zentralschweiz', 'tessin', 'berner-oberland'] },
      difficulty: { type: 'string', enum: ['leicht', 'mittel', 'schwer'] },
      maxDistanceKm: { type: 'number', description: 'Maximale Distanz in km' },
      maxDurationH: { type: 'number', description: 'Maximale Gehzeit in Stunden' },
      minElevation: { type: 'number', description: 'Minimale Höhenmeter' },
    },
    required: ['region'],
  },
  execute: async (args) => {
    const hikes = applyFilters(args)
    return `${hikes.length} Wanderungen gefunden.`
  },
})
```

<!--
Der Kern für Entwickler: Name, Description, inputSchema (Vertrag), execute.
execute ruft dieselbe Logik wie die UI auf. Das Tool ändert den UI-Zustand und
ist deshalb nicht read-only; Annotations kommen auf der Folie «Schema,
Annotations & Ownership».

Timing: 13:30-15:00
-->

---
layout: default
transition: slide-left
---

<div class="text-sm tracking-widest uppercase opacity-55">Deklarativ · HTML</div>

# Ein Formular wird zum Tool

```html {all|1|2-3|5-9|10-12|13}
<form toolautosubmit
  toolname="subscribe_trail_updates"
  tooldescription="Meldet den Nutzer für Wander-Updates einer Region an."
>
  <select name="region" toolparamdescription="Wanderregion">
    <option value="zentralschweiz">Zentralschweiz</option>
    <option value="tessin">Tessin</option>
    ...
  </select>
  <input name="email" 
         type="email"
         toolparamdescription="E-Mail-Adresse für Updates" />
  <button type="submit">Abonnieren</button>
</form>
```

<div class="mt-6 text-lg opacity-75">
Kein JavaScript nötig: Der Browser baut das JSON-Schema aus den Feldern.<br/>
<code>toolautosubmit</code> steuert, ob der Agent selbst absendet.
</div>

<!--
Deklarativ: toolname/tooldescription am Formular, toolparamdescription pro Feld.
Der Browser synthetisiert das Schema. Gut für bestehende Formulare als
Progressive Enhancement.

Timing: 15:00-16:00
-->

---
layout: default
transition: fade
---

<div class="text-sm tracking-widest uppercase opacity-55">Vertrag · Verhalten · Verantwortung</div>

# Schema, Annotations &amp; Ownership

<div class="text-base opacity-70 -mt-1 mb-4">Drei Themen, die jedes WebMCP-Tool adressieren sollte</div>

<div class="grid grid-cols-3 gap-5 text-left text-base leading-snug">

  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-5 flex flex-col">
    <div class="text-xs uppercase tracking-wider text-primary/70">1 · Vertrag</div>
    <div class="font-bold text-primary text-2xl mt-1">Schema</div>
    <div class="mt-2 opacity-80">Was darf das Tool?</div>
    <div class="mt-auto pt-6 text-sm opacity-70"><code>region</code> nur aus Liste<br><code>maxDistanceKm</code> als Zahl</div>
  </div>

  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-5 flex flex-col">
    <div class="text-xs uppercase tracking-wider text-primary/70">2 · Verhalten</div>
    <div class="font-bold text-primary text-2xl mt-1">Annotations</div>
    <div class="mt-2 opacity-80">Wie ist das Tool einzuordnen?</div>
    <div class="mt-auto pt-6 text-sm opacity-70">
      <code>readOnlyHint</code> · ändert nichts<br>
      <code>consequentialHint</code> · folgenreich<br>
      <code>untrustedContentHint</code> · Ergebnis unsicher
    </div>
  </div>

  <div v-click class="rounded-xl border border-primary/30 bg-primary/5 p-5 flex flex-col">
    <div class="text-xs uppercase tracking-wider text-primary/70">3 · Verantwortung</div>
    <div class="font-bold text-primary text-2xl mt-1">Ownership</div>
    <div class="mt-2 opacity-80">Wer kontrolliert die Ausführung?</div>
    <div class="mt-auto pt-6 text-sm opacity-70">Die Web-App: Login, Berechtigungen, Fachregeln</div>
  </div>

</div>



<!--
Mentales Modell in drei Schritten: Erst Vertrag (Schema - was akzeptiert das Tool),
dann Verhalten (Annotations - wie ist es einzuordnen), dann Verantwortung (Ownership -
wer prüft Berechtigungen und autorisiert Aktionen).

Fachliche Präzisierung: consequentialHint ist ein Hinweis auf potenziell folgenreiche
Aktionen - keine Garantie, dass der Browser eine Bestätigung erzwingt. Ebenso ersetzt
untrustedContentHint keine tatsächliche Sanitization; solche Schutzmaßnahmen müssen
explizit implementiert werden. Ownership heißt nicht nur: wem gehört der Code, sondern
auch: wer prüft Login, Berechtigungen und fachliche Regeln.

Timing: 16:00-17:30
-->

---
layout: default
transition: slide-up
---

<div class="text-sm tracking-widest uppercase opacity-55">Aber es gibt doch MCP?</div>

# MCP und WebMCP

<div class="mt-6 text-left text-lg">

| | MCP / OpenAPI im Backend | WebMCP im Browser |
|---|---|---|
| Tool läuft bei | Service oder API | laufender Web-App |
| Gut für | Server- und System-Workflows | UI-, Session- und Kontext-Workflows |
| Beispiel | Zahlung auslösen, Daten abfragen | Filter setzen, Formular ausfüllen |

</div>

<div v-click class="mt-6 rounded-xl border border-primary/30 bg-primary/10 p-4 text-xl text-left">
WebMCP ersetzt kein Backend-MCP.<br/>Es ergänzt es dort, wo der Browser-Kontext Teil der Aufgabe ist.
</div>

<!--
Häufige Frage: Unterschied zu MCP? Kein Entweder-oder. Serverseitige Operationen
→ MCP/OpenAPI. Wenn die geöffnete Seite, ihr Zustand und die Nutzerkontrolle
zählen → WebMCP.

Timing: 17:30-18:30
-->

---
layout: center
class: text-left
transition: slide-left
---

# WebMCP: 3 Dinge zum Mitnehmen

<div class="mt-10 space-y-6 text-2xl leading-relaxed">
  <div v-click class="grid grid-cols-[2rem_1fr] gap-x-3 items-start">
    <span class="text-primary font-bold">1.</span>
    <span>WebMCP macht <span class="text-primary font-bold">Web-Fähigkeiten explizit</span>, statt sie zu erraten.</span>
  </div>

  <div v-click class="grid grid-cols-[2rem_1fr] gap-x-3 items-start">
    <span class="text-primary font-bold">2.</span>
    <span>Es <span class="text-primary font-bold">ergänzt</span> Backend-MCP, APIs und Accessibility - es ersetzt sie nicht.</span>
  </div>

  <div v-click class="grid grid-cols-[2rem_1fr] gap-x-3 items-start">
    <span class="text-primary font-bold">3.</span>
    <span>Der Nutzen hängt am <span class="text-primary font-bold">Tool-Design</span>.</span>
  </div>
</div>

<!--
Drei Kernaussagen zum Mitnehmen.

Timing: 18:30-19:00
-->

---
layout: center
class: text-left
transition: fade
---

<div class="text-sm tracking-widest uppercase opacity-55">Wie geht es weiter?</div>

<div class="text-4xl leading-relaxed mt-6">
Experimentell heute - aber die
<span class="text-primary font-bold">Design-Frage</span> ist schon jetzt nützlich:
</div>

<div v-click class="text-3xl leading-relaxed mt-10 text-primary font-bold">
Welche Funktion eurer Web-App würdet ihr einem Agenten als Tool anbieten?
</div>

<div v-click class="text-xl mt-6 opacity-70">
Klar abgegrenzt, mit Nutzen für den Anwender - und unter eurer Kontrolle.
</div>

<!--
Nicht auf eine Prognose einlassen. Der Mehrwert für das Publikum ist die
Design-Frage, die sie heute auf ihre eigenen Apps anwenden können.

Timing: 19:00-19:30
-->

---
layout: center
class: text-left
transition: slide-up
---

<div class="rounded-xl border border-primary/30 bg-primary/5 px-10 py-9 text-3xl leading-relaxed">
  „Ich suche eine anspruchsvolle Wanderung im Berner Oberland - rund 15 km und mindestens 1000 Meter Aufstieg.“
</div>

<div v-click class="mt-10 text-xl leading-loose">
  <div><span class="opacity-60">Vorher:</span> Screenshot, DOM, Controls raten, klicken, neu lesen …</div>
  <div><span class="text-primary font-bold">Jetzt:</span> <code class="text-lg">filter_hikes({ region: 'berner-oberland', maxDistanceKm: 15, minElevation: 1000 })</code></div>
</div>

<div v-click class="mt-10 text-4xl font-bold text-primary">
  Der DOM ist keine API - die Web-App kann eine anbieten.
</div>

<!--
Bogen zurück zum Hook: derselbe Nutzerwunsch wie am Anfang. Vorher musste der
Agent die Oberfläche in vielen Schritten erraten, jetzt genügt ein Tool-Aufruf
mit klaren Eingaben. Schlusssatz greift den Titel auf.

Timing: 19:30-19:50
-->

---
layout: center
class: text-center
transition: fade
---

<div class="text-6xl font-bold text-center">
  Danke - Fragen?
</div>

<div class="mt-14 text-center text-lg leading-relaxed">
  <div class="font-bold text-primary">Markus Tanner</div>
  <div>Software Engineer</div>
  <a href="mailto:markus.tanner@css.ch">markus.tanner@css.ch</a>
</div>

<!--
Danke und Übergang zu den 5 Minuten Fragen. Bei Bedarf auf Demo, Tool-Design,
Security oder Spezifikationsstand eingehen.

Timing: 19:50-20:00 (+ 5 min Q&A)
-->

---
layout: default
transition: fade
---

# Quellen

<ul class="mt-8 text-xl leading-loose list-disc pl-6">
  <li><a href="https://webmachinelearning.github.io/webmcp/" target="_blank" rel="noopener noreferrer">webmachinelearning.github.io/webmcp</a></li>
  <li><a href="https://developer.chrome.com/docs/ai/webmcp" target="_blank" rel="noopener noreferrer">developer.chrome.com/docs/ai/webmcp</a></li>
  <li><a href="https://webmcp.com" target="_blank" rel="noopener noreferrer">webmcp.com</a></li>
  <li><a href="https://github.com/browser-use/web-ui" target="_blank" rel="noopener noreferrer">github.com/browser-use/web-ui</a></li>
</ul>

<!--
Backup-Folie für die Fragerunde, nicht Teil der 20 Minuten.
-->
