# WebMCP an der DevCon Luzern

**Format:** 40 Minuten Vortrag  
**Anlass:** DevCon Luzern, Ende Oktober 2026  
**Zielgruppe:** Entwicklerinnen und Entwickler mit Interesse an AI Agents und Web-Plattform  
**Leitfrage:** Wie können AI Agents mit komplexen Web-Apps zuverlässig zusammenarbeiten, ohne die menschliche Oberfläche und ihren Zustand zu umgehen?

## Zielbild

Der Vortrag soll WebMCP weder als Ersatz für MCP noch als garantierte Lösung
für Agenten-Automation darstellen. Die zentrale Aussage ist:

> WebMCP macht ausgewählte Fähigkeiten einer Web-App für Agents explizit,
> strukturiert und im gemeinsamen Browser-Kontext verfügbar.

Die Trailfolk-Demo zeigt dies anhand einer Schweizer Wander-App. Die Seite
bleibt die sichtbare, zustandsführende Oberfläche; ein Agent unterstützt sie
über klar definierte Werkzeuge.

## Ablauf

| Zeit | Abschnitt | Kernbotschaft | Mögliche Folien |
|---:|---|---|---|
| 0–3 min | Hook | Eine natürliche Absicht muss heute in viele UI-Schritte übersetzt werden. | 1–2 |
| 3–9 min | Status quo | Agents sehen Screenshots sowie DOM- und Accessibility-Tree-Snapshots und simulieren menschliche Eingaben. Das ist nützlich, aber bei dynamischen Oberflächen und Layout-Änderungen fragil. | 3–4 |
| 9–14 min | Was WebMCP ist | WebMCP steht für Web Model Context Protocol. Es ist eine vorgeschlagene Browser-API der W3C Web Machine Learning Community Group, die Tools per JavaScript oder annotierten HTML-Formularen verfügbar macht. | 5–7 |
| 14–17 min | Architektur und Abgrenzung | WebMCP läuft im Browser und nutzt bestehenden UI-, Session- und Client-Zustand. Es ergänzt serverseitiges MCP oder OpenAPI; es ersetzt sie nicht. | 8–10 |
| 17–20 min | Einsatzfelder | Support-Formulare, Buchungen, interaktive Anwendungen und Entwickler-Tools: WebMCP ist sinnvoll, wenn der sichtbare Browser-Kontext Teil der Aufgabe ist. | 11 |
| 20–30 min | Trailfolk als Beispiel | Filter setzen, passende Empfehlungen erhalten und die Begründungen in der sichtbaren UI anzeigen. | 12–14 |
| 30–36 min | Grenzen und Verantwortung | Tool-Design, Bestätigungen bei folgenreichen Aktionen, Eingabevalidierung, Datenschutz und Browser-Support sind Produkt- und Security-Fragen. | 15–17 |
| 36–39 min | Standard und Ausblick | WebMCP ist experimentell, aber die Richtung ist relevant: agentenfähige Web-Apps definieren ihre Fähigkeiten bewusst. | 18–19 |
| 39–40 min | Abschluss | Nicht jede Website braucht WebMCP. Komplexe, zustandsbehaftete Web-Apps sollten aber prüfen, welche Fähigkeiten sie kontrolliert anbieten wollen. | 20–21 |

Falls eine Fragerunde Teil der 40 Minuten ist, werden Demo und Ausblick um
insgesamt vier Minuten gekürzt.

## Dramaturgie

### 1. Einstieg: eine konkrete Absicht

Mit einem Satz beginnen, nicht mit einer Definition:

> „Finde mir eine mittelschwere Wanderung in der Zentralschweiz, zwischen
> 8 und 14 Kilometern, maximal vier Stunden und mit mindestens
> 500 Höhenmetern.“

Dann Trailfolk kurz als menschliche Oberfläche zeigen: Filterleiste,
Resultatliste, Wanderkarten. Erst danach die Frage stellen: Was muss ein
Agent tun, wenn die Seite keine explizite Schnittstelle anbietet?

### 2. Status quo differenziert darstellen

Nicht pauschal sagen, Agents würden nur „scrapen“. Präziser ist:

- Agents kombinieren Screenshots, DOM- und Accessibility-Tree-Snapshots.
- Sie müssen Oberflächenstruktur und Bedeutung von Controls erschliessen.
- Sie klicken, tippen und lesen den resultierenden Zustand erneut aus.
- Dies kann gut funktionieren, bleibt aber an Darstellung, Timing und
  Semantik der Oberfläche gekoppelt.

Die belastbarere These lautet:

> UI-Automation zwingt einen Agenten dazu, die Absicht hinter einer
> menschlichen Oberfläche zu rekonstruieren. WebMCP macht ausgewählte
> Fähigkeiten explizit.

Accessibility bleibt dabei wichtig: Sie hilft Menschen und auch
UI-automatisierenden Agents. WebMCP ist kein Ersatz für gutes semantisches
HTML und eine zugängliche Oberfläche.

### 3. WebMCP erklären

WebMCP steht für **Web Model Context Protocol**. Es ist ein offener,
experimenteller Vorschlag aus der W3C Web Machine Learning Community Group.
Chrome stellt dafür eine experimentelle Implementierung bereit. Die Idee ist
mit MCP verwandt, aber WebMCP ist weder eine Umbenennung noch ein Ersatz des
serverseitigen Model Context Protocols: Es bringt das Tool-Muster in die
laufende Web-Seite im Browser.

Ein WebMCP-Tool besteht im Kern aus:

- einem stabilen, fachlichen Namen,
- einer natürlichsprachlichen Beschreibung,
- einem strukturierten Input-Schema,
- einer `execute`-Funktion, die im Kontext der Seite läuft,
- optionalen Annotationen für die Einordnung einer Aktion.

Es gibt zwei API-Varianten:

- Die **imperative API** registriert Tools mit JavaScript und eignet sich für
  eigene Client-Logik, komplexen Zustand und Navigation.
- Die **deklarative API** annotiert vorhandene HTML-Formulare. Der Browser
  erzeugt daraus Toolname, Beschreibung und strukturiertes Schema.

Die entscheidende Gegenüberstellung:

| UI-Automation | WebMCP |
|---|---|
| „Öffne das Filterpanel und setze diese sechs Controls.“ | „Rufe `filter_hikes` mit diesen fachlichen Kriterien auf.“ |
| Der Agent leitet Bedeutung aus der Darstellung ab. | Die Anwendung beschreibt die angebotene Fähigkeit. |
| Der UI-Zustand wird indirekt verändert und erneut gelesen. | Das Tool nutzt dieselbe Client-Logik und aktualisiert die sichtbare UI. |
| Layout-, Label- oder Timing-Änderungen können Abläufe beeinträchtigen. | Der Tool-Vertrag kann stabil bleiben, während sich die Darstellung ändert. |

Nicht behaupten:

- WebMCP mache Agents fehlerfrei.
- Jedes Tool sei automatisch sicher.
- WebMCP ersetze Backend-MCP oder APIs.
- Jede Website müsse Tools anbieten.

### 4. Architekturfolie

Eine einfache Sequenz genügt:

```text
Nutzerwunsch
      |
      v
Browser-Agent -> WebMCP-Tool der laufenden Seite
                         |
                         v
              Bestehende Client-Logik / API-Aufruf
                         |
                         v
              Sichtbare UI und Tool-Ergebnis aktualisiert
```

Sprecherpunkt: Ein serverseitiges MCP-Tool kann eine Buchung, Suche oder
Transaktion direkt im Backend ausführen. WebMCP eignet sich besonders, wenn
die laufende Webseite, ihr Login, ihr UI-Zustand und die Kontrolle des
Nutzers Teil des Workflows sind.

### 5. Einsatzfelder vor der Demo

Trailfolk sollte nur eines von mehreren Beispielen sein. Die
Chrome-Dokumentation nennt unter anderem:

- **Support:** Ein Agent findet das richtige Formular und befüllt dessen
  strukturierte Felder korrekt.
- **Buchungen:** Mehrere Reisende, Termine und Bestätigungsschritte werden
  innerhalb der sichtbaren Oberfläche koordiniert.
- **Interaktive Anwendungen:** Filtern, planen, konfigurieren oder gestalten
  geschieht im gemeinsamen UI-Zustand.
- **Entwickler-Tools:** Klar begrenzte Diagnosen und Aktionen werden aus
  verschachtelten Einstellungen zugänglich.

Die gemeinsame Eigenschaft: Die Aufgabe profitiert von einer bereits
geöffneten Seite, ihrer Oberfläche und ihrem aktuellen Zustand.

## Trailfolk-Demo

### Was die aktuelle App zeigt

Trailfolk registriert Werkzeuge über `document.modelContext`. Die verfügbaren
Tools hängen bewusst vom aktiven Tab ab:

| Tab | Tool | Wirkung |
|---|---|---|
| **Entdecken** | `filter_hikes` | Setzt sichtbare Filter für Länge, Schwierigkeit, Mindestaufstieg, maximale Dauer und Region und liefert die passenden Wanderungen zurück. |
| **Entdecken** | `reset_hike_filters` | Setzt die Filter zurück und zeigt alle Wanderungen. |
| **Inspiration** | `recommend_hikes` | Ermittelt bis zu drei Empfehlungen anhand strukturierter Kriterien und eines optionalen freien Wunsches. |
| **Inspiration** | `show_recommendation_summary` | Zeigt die vom Agenten formulierten Begründungen direkt auf den sichtbaren Empfehlungskarten an. |

Das ist ein besonders guter Demo-Punkt: Die Seite kann Werkzeuge dynamisch
an den sichtbaren Kontext anpassen. Im Tab **Inspiration** sind Empfehlungen
sinnvoll; im Tab **Entdecken** wären sie nicht Teil der aktuellen Aufgabe.

### Empfohlener Demo-Ablauf

1. **Ausgangslage zeigen.** Tab **Entdecken**, alle Wanderungen sichtbar,
   keine gesetzten Filter.
2. **Kontrast kurz visualisieren.** Ohne WebMCP müsste ein Agent die
   passenden UI-Controls finden, Werte eingeben und die Resultate
   interpretieren. Das nur als einzelne Folie oder als kurzes, vorbereitetes
   Video zeigen – nicht als fehleranfällige Live-Automation.
3. **Filter-Tool live aufrufen.** Prompt:

   > „Filtere auf mittelschwere Wanderungen in der Zentralschweiz, zwischen
   > 8 und 14 Kilometern, mit mindestens 500 Höhenmetern und höchstens
   > vier Stunden Gehzeit.“

   Beobachtbar machen: Der Agent bildet die Absicht auf strukturierte Werte
   wie `difficulty`, `region`, `minLength`, `maxLength`, `minElevation` und
   `maxDuration` ab. Filter-Chips, Resultatzahl und Karten ändern sich in
   derselben Oberfläche.
4. **Kontextwechsel zeigen.** Den Tab **Inspiration** öffnen. Damit ändern
   sich die verfügbaren Tools.
5. **Empfehlung anfordern.** Prompt:

   > „Empfiehl mir zwei mittelschwere Wanderungen in der Zentralschweiz,
   > maximal vier Stunden, mit einem krönenden Dessert danach.“

   `recommend_hikes` liefert Resultate und strukturierte Gründe; der Agent
   ruft danach `show_recommendation_summary` auf. Die textlichen
   Begründungen erscheinen direkt an den Empfehlungskarten.
6. **Abschluss der Demo.** Den sichtbaren Effekt benennen: Der Agent hat
   nicht bloss Daten zurückgegeben. Er hat die bestehende Anwendung in einen
   verständlichen Zustand versetzt, den der Nutzer prüfen und weiter
   bearbeiten kann.

### Wichtige technische Präzisierung

Die aktuelle Filter-API hat `minElevation` (Mindestaufstieg), aber keinen
Parameter für einen maximalen Aufstieg. In Prompt und Folien daher
„mindestens 500 Höhenmeter“ verwenden, nicht „unter 900 Höhenmetern“.
Ebenso verwendet die App `maxDuration` in Minuten, nicht eine freie
Zeitangabe.

### Demoreserve

- Browser und unterstützenden Agent vor dem Vortrag vollständig testen.
- Die Tools nur im passenden Tab erwarten; die Registrierung ist
  tababhängig.
- Einen Screenshot oder ein kurzes Bildschirmvideo des vollständigen
  Happy Paths lokal bereithalten.
- Keine Netzwerkabhängigkeit für die fachlichen Resultate einbauen; die App
  arbeitet mit ihrem lokalen Wander-Datensatz.
- Bei einer Live-Demo immer zuerst die menschlich sichtbare UI zeigen, erst
  danach den Tool-Aufruf und zuletzt die aktualisierte UI.

## Tool-Design als Engineering-Thema

Die Folie dazu sollte die Unterschiede klar machen:

| Gut | Schwach |
|---|---|
| `filter_hikes(criteria)` | `click_filter_button()` |
| `recommend_hikes(preference, limit)` | `select_card(index)` |
| Kleine, begrenzte Schemas mit validierten Werten | Ein einziges freies Feld, das beliebige UI-Operationen auslösen kann |
| Ergebnis enthält den fachlichen Zustand und die Treffer | Ergebnis sagt nur „erfolgreich“ |

Trailfolk liefert hier bereits gute Gesprächspunkte:

- Eingaben werden vor Ausführung validiert.
- Kriterien haben Grenzen, etwa bei Distanz, Dauer und Anzahl Empfehlungen.
- Empfehlungen sind auf drei Resultate limitiert.
- Erklärungstexte werden an bekannte Wanderungsnamen gebunden und begrenzt.

Konstruktive Challenge für das Publikum:

> Ein Tool-Schema ist ein API-Design. Würden wir dieselbe API auch einem
> externen Entwickler guten Gewissens geben?

## Grenzen, Security und UX

Diese Fragen bewusst nicht überspringen:

1. **Folgenreiche Aktionen:** Ein Tool zum Filtern ist etwas anderes als ein
   Tool für Kauf, Buchung, Löschen oder Kontoänderung. Welche Aktionen
   benötigen zwingend eine Bestätigung?
2. **Tool-Rechte:** Ein Tool soll nur die minimal nötigen Eingaben und
   Berechtigungen erhalten. Keine übermächtigen „mache alles“-Werkzeuge.
3. **Untrusted Content und Prompt Injection:** Tool-Beschreibungen,
   Parameter und externe Inhalte dürfen nicht blind als vertrauenswürdige
   Handlungsanweisungen behandelt werden.
4. **Datenschutz:** Die API liefert nicht automatisch private Daten aus,
   aber die implementierten Tools können sensible Abläufe kapseln. Die
   Anwendung bleibt für ihr Tool-Verhalten verantwortlich.
5. **Browser-Support:** Nicht auf eine breite, stabile Plattformverfügbarkeit
   bauen. Progressive Enhancement und ein normal bedienbares UI bleiben
   erforderlich.

Passender Satz:

> WebMCP verlagert Verantwortung nicht weg – es macht die Fähigkeiten und
> Grenzen einer Anwendung expliziter.

## Stand und Ausblick

**Stand 10. September 2026:** WebMCP ist ein *Draft Community Group Report*
der W3C Web Machine Learning Community Group. Es ist kein W3C
Recommendation-Standard und befindet sich nicht auf dem formalen
Recommendation Track.

Der dokumentierte Implementierungsstatus nennt einen Origin Trial in Chrome
149 und Edge 150 sowie Unterstützung in Brave Leo und ChatGPT Desktop. Das
ist ein starkes Signal für Experimente, aber noch keine Zusage für
flächendeckende und stabile Browser-Unterstützung.

Diese Angaben in der Woche vor dem Vortrag aktualisieren:

- [WebMCP-Spezifikation](https://webmachinelearning.github.io/webmcp/)
- [WebMCP-Repository](https://github.com/webmachinelearning/webmcp)
- [Browser- und Agent-Implementierungsstatus](https://github.com/webmachinelearning/webmcp/blob/main/implementation-status.md)
- [Security and Privacy Self-Review](https://github.com/webmachinelearning/webmcp/blob/main/security-privacy-questionnaire.md)

Nicht die schwer beantwortbare Prognose „Wird sich WebMCP durchsetzen?“ in
den Mittelpunkt stellen. Die produktivere Abschlussfrage ist:

> Welche Fähigkeiten eurer Web-App sind wertvoll, klar abgegrenzt und
> zustandsbehaftet genug, dass ihr sie einem Agenten kontrolliert anbieten
> möchtet?

## Schlussfolie

**Drei Takeaways**

1. Gute UI-Automation ist möglich, aber sie muss menschliche Oberflächen
   interpretieren; WebMCP macht ausgewählte Fähigkeiten explizit.
2. WebMCP ist eine Ergänzung für browsernahe, gemeinsame Workflows – kein
   Ersatz für Backend-MCP, APIs, Accessibility oder menschliche Kontrolle.
3. Der Erfolg hängt weniger von der Tool-Registrierung als von gutem
   API-Design, klaren Grenzen und verantwortungsvoller UX ab.

**Schlusssatz**

> Die spannende Frage ist nicht, ob Agents Webseiten bedienen werden.
> Die spannende Frage ist, ob wir ihnen weiterhin nur Buttons zeigen – oder
> bewusst Fähigkeiten anbieten.
