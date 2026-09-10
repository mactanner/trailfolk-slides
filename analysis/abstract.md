# Der DOM ist keine API: WebMCP für KI-Agenten

KI-Agenten im Browser sind nützlich, aber unter der Haube ist es oft ein unsauberer Hack. LLMs müssen sich durch verschachtelte DOM-Bäume wühlen, IDs erraten oder stumpfes Screen-Scraping betreiben, um eine Aktion auf einer Webseite auszuführen.

Das neue Web Model Context Protocol (WebMCP) soll das beenden. Es ist ein W3C-Draft, der dem Browser eine native API (document.modelContext) gibt.
Damit können Webseiten der KI direkt sagen: „Hier sind meine strukturierten Daten und das hier sind die Funktionen, die du ausführen darfst.“

In dieser Session schauen wir uns das hier an:

- Das Problem: Warum das aktuelle LLM-Setup im Browser suboptimal ist.
- Die Lösung: Was WebMCP eigentlich macht (und wie es sich vom serverseitigen MCP unterscheidet).
- Der Code: Wie die imperative (JS) und deklarative (HTML) API in der Praxis aussehen.