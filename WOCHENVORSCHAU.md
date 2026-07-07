> [!WARNING]
> Dieses Dokument gerendert lesen, nicht als Rohtext. In VSCode: Strg+Shift+V (Windows) oder Cmd+Shift+V (Mac).
> Diese Vorschau liegt auch als Webseite unter **https://sleek-vision-8ezb.here.now/wochenvorschau.html** — dort mit denselben Links zum Durchklicken.

# WOCHENVORSCHAU — Mittwoch bis Freitag
## Vue.js Deep Dive · Woche 1 · 08.–10.07.2026

| | |
|---|---|
| Lesezeit | 20–25 Minuten, heute (Dienstag) nach dem Generator |
| Zweck | Ihr wisst, was diese Woche passiert und WARUM in dieser Reihenfolge — und ihr habt fertige Beispiele gesehen, bevor ihr selbst baut |
| Kein Vorlernen | Nichts hier ist Stoff zum Pauken. Anschauen, Neugier mitnehmen, fertig |

---

## Das neue Modul, in einem Absatz

Ab Mittwoch lernt ihr **Vue.js** — das Framework, mit dem [GitLab](https://docs.gitlab.com/ee/development/fe_guide/vue.html) sein Produkt-Frontend baut und [n8n aus Berlin](https://github.com/n8n-io/n8n) seinen Workflow-Editor. Aber der Monat heißt nur an der Oberfläche "Vue lernen". Was wirklich passiert: ihr lernt das **Denkmodell**, auf dem jedes moderne Frontend-Framework steht — Zustand ist die einzige Quelle der Wahrheit, das Sichtbare ist nur seine Projektion. Am Wochenende habt ihr sechs Interface-Stationen von Hand gebaut und jeden Zustand einzeln mit Klassen erzwungen. Diese Woche seht ihr, was diese Arbeit übernimmt — und ihr werdet es nicht einfach benutzen: **ihr baut es am Mittwoch zuerst selbst.**

Euer Klient vom Wochenende — ATEM, NORD oder TON — bleibt euer Klient. Der ganze Monat baut SEIN Web-Produkt, das Klienten-Portal. Der Generator von heute liefert die Hintergründe dafür. Und am Freitag um 13:00 steht die erste Version dieses Portals unter einer echten URL im Netz. Drei Tage, drei Schichten, eine Lieferung.

Die Reihenfolge der drei Tage ist kein Zufall, sondern das Bauprinzip des Monats — ihr kennt es aus dem Juni als Gall's Law: erst das einfache System, das funktioniert. Mittwoch der Motor. Donnerstag das Chassis. Freitag die Bauteile — und die Auslieferung.

---

## Die Landkarte — wo Vue steht

Vier Namen tauchen in jeder Frontend-Diskussion nebeneinander auf, und in Bewerbungsgesprächen wird erwartet, dass ihr sie sortieren könnt. Hier die Sortierung — vor dem ersten Unterrichtstag, damit die Einordnung sitzt:

| Werkzeug | Was es ist | Wer dahintersteht | Typischer Einsatz | Für euch heißt das |
|---|---|---|---|---|
| **React** | Bibliothek für UI-Komponenten, Markup als JSX im JavaScript | Meta | Konzern-Frontends, große Teams; das größte Ökosystem | Der größte Markt — und die längste Schlange am Junior-Einstieg |
| **Next.js** | Fullstack-Framework **auf** React: Server-Rendering, Routing, API-Schicht | Vercel | React-Projekte, die mehr als eine Seite sind; im Markt fast immer im Doppelpack mit React | Kein Konkurrent zu Vue, sondern Reacts Überbau — lernt man nach React, nicht statt |
| **Vue** ← unser Monat | Framework mit eigenem Denkmodell: HTML-Templates + Reaktivität, offizieller Router und offizielles State-Management | Unabhängiges Team um Evan You, über Sponsoren finanziert | Produkt-Frontends von GitLab bis n8n; in Deutschland stark bei Agenturen und Mittelstand | Stabile Nummer zwei — mit deutlich dünnerer Junior-Konkurrenz |
| **Astro** | Framework für Inhalts-Seiten: liefert standardmäßig kein clientseitiges JavaScript aus, Interaktivität kommt als „Inseln" dazu | Unabhängig (Astro-Team) | Blogs, Dokumentationen, Marketing-Seiten; kann Vue- und React-Komponenten einbetten | Das Spezialwerkzeug für Content — kein App-Framework, aber gut zu kennen |

**Warum Nummer zwei ein guter Platz ist:** React lädt auf npm rund zehnmal öfter als Vue (Momentaufnahme Anfang Juli 2026: ~604 Millionen gegen ~56 Millionen Downloads in 30 Tagen) — der größte Markt, aber am Junior-Einstieg auch der gesättigtste. Vue hält seit Jahren Platz zwei, mit einem eigenen, stabilen Stellenmarkt in Deutschland (StepStone 541 und Indeed 500 offene Treffer, Anfang Juli, schwankt täglich) und dem am besten dokumentierten Einstieg der Branche. Und das Entscheidende für diesen Monat: wer Vues Reaktivität einmal von Hand gebaut hat, liest danach auch React-Code ohne Schrecken — das Denkmodell transferiert, die Vokabeln unterscheiden sich. Nummer zwei heißt hier: echter Markt, weniger Gedränge, bester Lernpfad.

---

## MITTWOCH 08.07 — Der Motor

**Was passiert:** Wir starten nicht mit einer Vue-Tour. Wir starten mit einem Problem — eurem eigenen vom Wochenende: acht Button-Zustände, vierzig Zeilen Klassen-Schalterei, und vier Code-Stellen, die an denselben Zustand denken müssen. Dann bauen wir die Lösung **von Hand**: das Herzstück eines Frontend-Frameworks, in einer einzigen HTML-Datei, mit einer Handvoll JavaScript-Werkzeugen, die ihr alle längst besitzt — welche genau, bleibt bis Mittwoch früh offen. Erst wenn euer eigener Motor läuft, importieren wir den echten. Und dann vergleichen wir: euer Code und der Vue-Quellcode — fast dieselben Zeilen.

**Warum so herum:** Wer ein Framework zuerst benutzt, lernt Rezepte und rät bei jedem Fehler. Wer den Motor einmal selbst zusammengeschraubt hat, DEBUGGT gezielt — er weiß, was unter der Haube kaputt sein kann, weil er die Haube schon offen hatte. Zwei Stunden Aufwand am Mittwoch, die euch den ganzen Monat tragen.

**Danach könnt ihr:** erklären, wie Reaktivität funktioniert (Lesen wird verfolgt, Schreiben feuert), warum Vue-Code überall `.value` schreibt, und was eine Tabellenkalkulation mit einem Frontend-Framework zu tun hat.

**Vorher anschauen (freiwillig, zusammen ~10 Min):**
- **https://vuejs.org/examples/** — fertige Mini-Apps im Browser: Zähler, Markdown-Editor, Todo-Liste, sortierbares Grid. Klickt zwei, drei davon an und lest den Code NICHT — schaut nur, wie wenig davon nach DOM-Handwerk aussieht. Genau diesen Abstand erklärt der Mittwoch.
- **https://play.vuejs.org/** — der offizielle Spielplatz (kennt ihr aus der Rampe). Merken, nicht vertiefen.

---

## DONNERSTAG 09.07 — Das Chassis

**Was passiert:** Der Motor bekommt ein Zuhause. Ihr scaffoldet das **echte Projekt** eures Klienten — das Portal, das bis zum 31.07 wächst — mit dem Werkzeug, das ihr seit fünf Wochen jeden Tag startet, ohne es zu kennen: Vite. Ihr lernt die Datei-Form, in der die ganze Vue-Welt arbeitet (eine Datei = ein Bauteil, drei Blöcke: Logik, Markup, Stil), das Vokabular, mit dem Templates wirklich geschrieben werden — Listen, Bedingungen, Bindungen — und den Unterschied zwischen einem Wert, der sich ERGIBT, und einer Reaktion, die PASSIERT. Dazu die Werkzeug-Geschichte des Jahres 2026, die euer `bun run dev` diesen Sommer schneller gemacht hat, als es je war. Mehr wird nicht verraten.

**Warum so herum:** Erst wenn ihr Mittwoch gesehen habt, WAS das Framework tut, lohnt sich das Werkzeug drumherum. Andersherum wäre es Kochen nach Bild.

**Danach könnt ihr:** ein Vue-Projekt von null aufsetzen, eine Komponenten-Datei lesen wie einen Bauplan, Listen und Zustände im Template ausdrücken — und euer Portal läuft als echtes Projekt mit einem Wert, der einen Browser-Neustart überlebt.

**Vorher anschauen (freiwillig, ~10 Min):**
- **https://madewithvuejs.com/** — eine Galerie echter Produkte, die mit Vue gebaut sind. Scrollt fünf Minuten und sammelt ein Gefühl dafür, wie verschieden die Ergebnisse aussehen — vom Dashboard bis zur Marketing-Seite.
- **https://vuejsexamples.com/** — dasselbe eine Nummer kleiner: hunderte Komponenten und Mini-Projekte aus der Community. Nicht nachbauen — nur sehen, dass "Komponente" von Knopf bis Kalender alles sein kann.
- **https://devtools.vuejs.org/** — die Röntgenbrille, die ihr Donnerstag zum ersten Mal aufsetzt: ein Werkzeug, das euch den Zustand eurer App live zeigt. Nur die Startseite anschauen, damit ihr sie wiedererkennt.

---

## FREITAG 10.07 — Bauteile + Lieferung

**Was passiert:** Liefertag. Vormittags der letzte Baustein der Woche: eure App zerfällt in **Bauteile mit Verträgen** — was ein Bauteil braucht, was es meldet, und warum diese Strenge euch in Woche 3 den Verstand rettet. Danach wird es realistisch: hartes Zeitfenster, echtes Deployment (dieselben Handgriffe wie im Juni: Vercel und GitHub Pages), und um **13:00 die Premiere** — jeder präsentiert sein Portal v1 von der Live-URL, nicht von localhost. Dazu messen wir zum ersten Mal die Zahl, die uns vier Freitage lang begleitet: den Lighthouse-Performance-Score. Das Portal wird jede Woche größer — und bleibt schnell. Das ist die Disziplin des Monats.

**Warum so herum:** Eine Version eins, die am Freitag echt im Netz steht, schlägt zehn perfekte Pläne. Ihr kennt den Satz-Rhythmus aus dem Juni: gebaut, deployed, gezeigt.

**Danach könnt ihr:** Bauteile mit sauberen Schnittstellen herausschneiden, ein Vite-Projekt bauen und deployen, einen Lighthouse-Report lesen — und ihr habt die erste Kundenlieferung des Monats hinter euch.

**Vorher anschauen (freiwillig, ~10 Min):**
- **https://vite.dev/guide/static-deploy** — die offizielle Deploy-Anleitung. Nur überfliegen: ihr erkennt Freitag jeden Schritt wieder.
- **https://vercel.com/docs/frameworks/vite** — dasselbe aus der Vercel-Perspektive. Euer Juni-Account passt.
- **https://web.dev/learn/performance** — was "Performance" messbar heißt. Die ersten zwei Abschnitte reichen.

---

## Die Beispiel-Galerie (fertige Sachen zum Anschauen, ohne Bau-Auftrag)

| Was | Link | Warum anschauen |
|---|---|---|
| Offizielle Mini-Apps | https://vuejs.org/examples/ | Zähler bis Markdown-Editor — die Woche in Fertigform |
| Produkt-Galerie | https://madewithvuejs.com/ | Echte Produkte, gebaut mit dem, was ihr diese Woche lernt |
| Community-Beispiele | https://vuejsexamples.com/ | Hunderte kleine Bauteile — Ideenspeicher für euer Portal |
| GitLab × Vue | https://docs.gitlab.com/ee/development/fe_guide/vue.html | Wie ein Konzern Vue schreibt: GitLabs eigener Vue-Leitfaden für das Produkt-Frontend |
| n8n (Berlin) | https://github.com/n8n-io/n8n | Echte deutsche Produktions-Codebase; der Editor ist Vue. Unsere Lese-Codebase des Monats |
| Der echte Motor | https://github.com/vuejs/core/tree/main/packages/reactivity | Der Reaktivitäts-Quellcode, gegen den ihr euren Mittwoch-Motor vergleicht. Auch hier gilt: erst ab Mittwoch Nachmittag öffnen, sonst nehmt ihr euch die Pointe |
| Unser Generator-Beispiel | https://sleek-vision-8ezb.here.now/beispiel.html | Die fertige Produktion des heutigen Auftrags — Code lesen erlaubt |

## Die Lern-Regale (wenn ihr tiefer wollt — alles freiwillig)

| Was | Link | Einordnung |
|---|---|---|
| Offizielles Tutorial | https://vuejs.org/tutorial/ | 15 interaktive Schritte im Browser. Der Mittwoch+Donnerstag als Selbstlern-Spur |
| Reactivity in Depth | https://vuejs.org/guide/extras/reactivity-in-depth.html | Die offizielle Von-Hand-Erklärung. Fairer Hinweis: wer sie VOR Mittwoch liest, nimmt sich selbst die Pointe des Vormittags — ab Mittwoch Nachmittag ist sie euer Nachschlagewerk |
| Vue School: Fundamentals | https://vueschool.io/courses/vue-js-fundamentals-with-the-composition-api | Kostenloser Einsteigerkurs im modernen Stil |
| Vue Mastery: Vue 3 Reactivity | https://www.vuemastery.com/courses/vue-3-reactivity | Video-Kurs zum Maschinenraum — dieselbe Empfehlung wie links: erst nach Mittwoch |
| Style Guide | https://vuejs.org/style-guide/rules-essential.html | Die Essenz-Regeln. Zwei davon fallen diese Woche im Unterricht |

## Sehenswert (54 Minuten, für einen Abend)

**Bret Victor — „Inventing on Principle" (CUSEC 2012): https://vimeo.com/906418692**
Der einflussreichste Vortrag über die Frage, wie sich Bauen anfühlen sollte: unmittelbar, mit direkter Verbindung zwischen Hand und Ergebnis. Kein Vue-Video — etwas Besseres. Wer ihn diese Woche schaut, wird an zwei Stellen des Unterrichts leise grinsen.

---

## Bring-mit-Checkliste für Mittwoch 09:00

- [ ] Generator-Datei mit drei Fundstück-Kommentaren (die Premiere eröffnet den Tag)
- [ ] Werk B vom Wochenende griffbereit (das Mittwoch-Warmup schaut hinein — es kommt Mittwoch früh)
- [ ] `portal-probe` von der Rampe startet mit `bun run dev` (nur der Beweis, nicht mehr)
- [ ] Zoom, VSCode, ein Browser mit DevTools — wie immer

Kein Vorlernen. Die Woche holt euch da ab, wo der Generator euch heute Abend absetzt.

---

*Wochenvorschau | Di 07.07.2026 | Vue.js Deep Dive W1 | Morphos GmbH*
