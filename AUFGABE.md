> [!WARNING]
> Dieses Dokument gerendert lesen, nicht als Rohtext. In VSCode: Strg+Shift+V (Windows) oder Cmd+Shift+V (Mac).
> Alles zu diesem Auftrag liegt auch im Netz: **https://sleek-vision-8ezb.here.now/** (Auftrag, Beispiel, Wochenvorschau) und als Starter-Code unter **https://github.com/OthmanAdi/vuejs-day-0-generator**.

# DER HINTERGRUND-GENERATOR
## Der Auftakt-Auftrag · Selbststudium · Dienstag 07.07.2026 · Vue.js Deep Dive

| | |
|---|---|
| Tag | Dienstag 07.07.2026 — Selbststudiumstag, kein Unterricht. Der Unterricht startet Mittwoch 09:00 |
| Kern-Auftrag | Dieser Generator, ~2,5 bis 3 Stunden, solo, in eurem Tempo |
| Danach | Die Wochenvorschau lesen (auf der Website) + die Vue-Rampe (~1,5 Stunden, eigenes Dokument) |
| Stack | Three.js r184 per CDN-Importmap, `ShaderMaterial` + GLSL — euer Juni-Werkzeug |
| Starter | Fertiges Skelett zum Losbauen: Repo oben klonen ODER `starter.html` von der Website speichern |
| Ziel | Kein Bild bauen. Eine **Maschine** bauen, die Bilder baut |
| Ergebnis | Ein klickbarer Generator + drei gespeicherte Fundstücke — Premiere Mittwoch 09:00 |

---

## Der Auftrag

Euer Klient vom Wochenende — ATEM, NORD oder TON — meldet sich noch einmal, bevor das neue Projekt startet. Die Anfrage ist klein formuliert und groß gedacht:

> „Die Szene ist abgenommen. Was uns jetzt fehlt: Hintergründe. Für die Website, für Social-Formate, für Präsentationen — und zwar nicht EIN Bild, sondern ein Vorrat, der nie ausgeht. Immer unsere Stimmung, nie zweimal dasselbe."

Das ist ein echtes Genre. Studios liefern so etwas als **Generator**: ein Stück Software mit einem Knopf. Jeder Klick ein neues Bild, jedes Bild im Marken-Pol des Klienten, keins wiederholt sich. Schaut euch drei Referenzen aus der Industrie an, bevor ihr baut:

- **shadergradient.co** — bewegte Shader-Verläufe als fertiges Produkt für Framer/Figma. Langsam, weich, palettengetrieben.
- **unicorn.studio** — WebGL-Effekte über Regler statt Code. Merkt euch die Bedienung: Slider bewegen, sofort sehen. Genau dieses Gefühl baut ihr heute selbst.
- **gradient.style** von Adam Argyle — dort entsteht Schönheit fast nur aus Farbwahl. Kein Zufall, sondern die Lektion des Tages.

**Worum es heute NICHT geht:** rotierende Objekte, Sternenfelder, Partikelkugeln. Die schönsten Generatoren dieser Gattung sind flache, langsame Farbfelder — die Kunst liegt in der Palette und in der Bewegung des Musters, nicht in 3D-Geometrie. Ihr habt einen Monat lang Maschinen mit zweihunderttausend Teilen gebaut. Heute ist das Gegenteil dran: ein Vollbild-Rechteck, ein Fragment-Shader, und trotzdem ein Ergebnis, das aussieht wie ein Poster.

---

## SO STARTEST DU (3 Wege, nimm einen)

**Weg A — das Repo (empfohlen):**
```bash
git clone https://github.com/OthmanAdi/vuejs-day-0-generator.git
cd vuejs-day-0-generator
```
Dann `STARTER_generator.html` per Doppelklick im Browser öffnen — du siehst den UV-Verlauf von Etappe 0, sofort, ohne Server. Diese Datei ist dein Arbeitsplatz für heute; dieser Auftrag liegt als `AUFGABE.md` gleich daneben.

**Weg B — nur die Datei:** Auf https://sleek-vision-8ezb.here.now/starter.html gehen → Rechtsklick → „Seite speichern unter" → `generator.html`. Gleicher Inhalt wie im Repo, ohne git.

**Weg C — von null:** Leere Datei, alles selbst tippen. Die Importmap und das Skelett stehen in Etappe 0 unten. Der stolzeste Weg, kostet ~15 Minuten mehr.

Egal welcher Weg: es gibt **keinen Build, keinen Server, kein npm**. Eine HTML-Datei, Doppelklick, läuft. Nur die drei CDN-Zeilen der Importmap brauchen einmal Internet.

---

## Die zwei Bausteine (Lesen, ~20 Minuten)

Der ganze Generator steht auf zwei Techniken. Beide stammen von Iñigo Quilez — dem Mann, dessen Shader-Artikel die halbe Demoszene und so ziemlich jedes Studio dieser Gattung ausgebildet haben. Beide Artikel gehören heute in einen offenen Tab.

### Baustein 1 — Die Cosinus-Palette

Quelle: `https://iquilezles.org/articles/palettes/`

Eine Farbpalette als Formel. Ein Wert `t` läuft von 0 bis 1 (Position im Bild, Noise-Wert, egal was), und vier Parameter formen daraus Farbe:

```
color(t) = a + b · cos( 2π · (c·t + d) )
```

In GLSL, wörtlich aus dem Artikel:

```glsl
// cosine based palette, 4 vec3 params
vec3 palette( in float t, in vec3 a, in vec3 b, in vec3 c, in vec3 d )
{
    return a + b*cos( 6.283185*(c*t+d) );
}
```

`a` hebt die Grundhelligkeit, `b` den Kontrast, `c` die Anzahl der Farbwellen, `d` verschiebt die Phase — und weil alle vier `vec3` sind, macht jeder Kanal (R, G, B) seine eigene Welle. Sieben erprobte Parametersätze aus dem Artikel, zum Starten und Zerlegen:

| # | a | b | c | d |
|---|---|---|---|---|
| 1 | 0.5, 0.5, 0.5 | 0.5, 0.5, 0.5 | 1.0, 1.0, 1.0 | 0.00, 0.33, 0.67 |
| 2 | 0.5, 0.5, 0.5 | 0.5, 0.5, 0.5 | 1.0, 1.0, 1.0 | 0.00, 0.10, 0.20 |
| 3 | 0.5, 0.5, 0.5 | 0.5, 0.5, 0.5 | 1.0, 1.0, 1.0 | 0.30, 0.20, 0.20 |
| 4 | 0.5, 0.5, 0.5 | 0.5, 0.5, 0.5 | 1.0, 1.0, 0.5 | 0.80, 0.90, 0.30 |
| 5 | 0.5, 0.5, 0.5 | 0.5, 0.5, 0.5 | 1.0, 0.7, 0.4 | 0.00, 0.15, 0.20 |
| 6 | 0.5, 0.5, 0.5 | 0.5, 0.5, 0.5 | 2.0, 1.0, 0.0 | 0.50, 0.20, 0.25 |
| 7 | 0.8, 0.5, 0.4 | 0.2, 0.4, 0.2 | 2.0, 1.0, 1.0 | 0.00, 0.25, 0.25 |

Der Generator-Gedanke steckt schon hier: **würfle `d` neu, und du hast eine neue Palette.** Halte `a` und `b` im Pol deines Klienten (warm für ATEM und TON, kühl für NORD), und jede gewürfelte Palette bleibt on-brand. Das ist der ganze Trick hinter „endlos, aber immer unsere Stimmung".

### Baustein 2 — Domain Warping

Quelle: `https://iquilezles.org/articles/warp/`

Die Idee in drei Sätzen. Erstens: statt ein Muster direkt auszuwerten, verzerrst du vorher seinen **Eingaberaum** — aus `f(p)` wird `f(p + h(p))`. Zweitens: wenn Muster und Verzerrung beide fBM sind (die Noise-Oktaven-Summe aus eurer Juni-Woche-3), füttert sich das Rauschen selbst, und aus glattem Nebel werden Marmor, Rauch, Strömung. Die Signatur-Form: `fbm( p + fbm( p + fbm(p) ) )`. Drittens: die Zwischenwerte der Verzerrung sind kein Abfall — wer sie in die Farbe mischt, bekommt die Tiefe, die diese Bilder berühmt gemacht hat.

Das Kernstück aus dem Artikel, mit den freigelegten Zwischenwerten:

```glsl
float pattern( in vec2 p, out vec2 q, out vec2 r )
{
    q.x = fbm( p + vec2(0.0,0.0) );
    q.y = fbm( p + vec2(5.2,1.3) );

    r.x = fbm( p + 4.0*q + vec2(1.7,9.2) );
    r.y = fbm( p + 4.0*q + vec2(8.3,2.8) );

    return fbm( p + 4.0*r );
}
```

Und falls euch die Zahlen `5.2, 1.3, 1.7, 9.2, 8.3, 2.8` magisch vorkommen — der Autor selbst räumt damit auf:

> „those particular offset values … don't have any special meaning"
> — Iñigo Quilez, *Domain Warping*, iquilezles.org

Sie entkoppeln nur eine `fbm`-Funktion in mehrere. Merkt euch diesen Moment: die beeindruckendsten Bilder dieser Technik hängen an Konstanten, die jemand einfach gewählt hat. Genau deshalb dürft ihr sie ersetzen — euer Generator würfelt sie.

Für die fBM-Auffrischung, falls Woche 3 verblasst ist: `https://iquilezles.org/articles/fbm/` und Kapitel 13 im Book of Shaders (`https://thebookofshaders.com/13/`).

---

## Der Bauplan (5 Etappen)

Ihr kennt das Format vom Wochenende: Etappen mit eigenem Ergebnis, SELBST-CHECK am Ende jeder Etappe. Die Zeiten tragen die übliche Marge — länger brauchen ist normal, nicht Rückstand. Wer mit dem Starter arbeitet: Etappe 0 ist dort schon gebaut, die Kommentare im Starter zeigen, wo jede weitere Etappe andockt.

### Etappe 0 — Das Skelett (~15 Min · im Starter FERTIG)

Eine Datei, `generator.html`. Die Importmap ist auf r184 gepinnt, dieselbe Version wie euer ganzer Juni:

```html
<script type="importmap">
{
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.184.0/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.184.0/examples/jsm/"
  }
}
</script>
```

Drinnen: Szene, `OrthographicCamera(-1, 1, 1, -1, 0, 1)`, ein `PlaneGeometry(2, 2)` mit `ShaderMaterial`, Renderer mit `setAnimationLoop`. Keine OrbitControls — es gibt nichts zu umkreisen. Der Vertex-Shader reicht nur `uv` durch, alles Weitere lebt im Fragment-Shader. Uniforms für den Start: `uTime`, `uResolution`.

**SELBST-CHECK:** Vollbild-Fläche sichtbar, `gl_FragColor = vec4(vUv, 0.0, 1.0);` zeigt den vertrauten UV-Verlauf von Rot nach Grün. Konsole ohne rote Zeile. (Starter-Nutzer: genau dieses Bild seht ihr beim ersten Doppelklick.)

### Etappe 1 — Palette an Bord (~30–40 Min)

Die `palette()`-Funktion aus Baustein 1 in den Fragment-Shader, Parametersatz 1 aus der Tabelle als Start. Erst statisch: `t = vUv.x` — Farbbänder über die Breite. Dann lebendig: `t = vUv.x + sin(vUv.y * 3.0 + uTime * 0.2) * 0.2` — die Bänder atmen.

Jetzt der erste Generator-Moment: die vier Parameter werden Uniforms (`uA`, `uB`, `uC`, `uD`), und ein Button **Zufall** im HTML würfelt `uD` neu (drei Zufallswerte 0..1). Haltet `uA`/`uB` fest im Pol eures Klienten. Jeder Klick: neue Palette, gleiche Marke.

**SELBST-CHECK:** Fünfmal Zufall geklickt — fünf verschieden gefärbte Bilder, keins fällt aus der Stimmung deines Klienten. Falls doch: `uB` kleiner machen (weniger Kontrast-Ausschläge) oder `uA` in Richtung deines Pols schieben.

### Etappe 2 — Noise zurückholen (~30 Min)

Euer Value-Noise + fBM aus der Juni-Woche-3 in den Shader — zwei bis fünf Oktaven, eine `uOktaven`-Uniform. Wer seinen alten Shader nicht mehr hat: das Book-of-Shaders-Kapitel 13 hat die kompakte Referenz-Implementierung, und das Beispiel auf der Website trägt eine in Etappe 2. `t` speist sich jetzt aus `fbm(vUv * uZoom + uTime * uTempo)` statt aus `vUv.x`.

**SELBST-CHECK:** Weicher, unregelmäßiger Farbnebel statt Bänder. Die Oktaven-Uniform verändert sichtbar die Detaildichte.

### Etappe 3 — Die Warp-Schleife (~45 Min)

Baustein 2 einbauen: die `pattern(p, q, r)`-Funktion mit den zwei Warp-Ebenen. Der Rückgabewert steuert `t` für die Palette — und dann der Schritt, der die Tiefe bringt: mischt `length(q)` und `r.y` in die Farbwahl (zum Beispiel als zweiter und dritter Palette-Aufruf, oder als Helligkeits-Modulation). Ein Slider **Warp-Stärke** ersetzt die feste `4.0`.

Dreht die Zeit langsam: `uTime * 0.05`. Die Referenzen aus dem Auftrag bewegen sich alle in diesem Tempo — Langsamkeit ist ein Gestaltungsmittel, kein Mangel.

**SELBST-CHECK:** Bei Warp-Stärke 0 seht ihr euren Etappe-2-Nebel. Beim Hochziehen beginnt das Bild zu fließen wie Rauch oder Marmor. Die Zwischenwerte färben mit — das Bild hat Schichten, nicht nur eine Textur.

### Etappe 4 — Der Generator-Moment (~30 Min)

Jetzt wird aus dem Shader das Produkt:

1. **Der Zufall-Knopf würfelt alles:** Palette-Phase `uD`, Farbfrequenz `uC`, die Warp-Offset-Konstanten (ersetzt die IQ-Zahlen durch gewürfelte Uniforms `uOff1`…`uOff3`) und den Zoom. Ein Klick = ein komplett neues Werk im Marken-Pol.
2. **Drei Slider:** Tempo, Oktaven, Warp-Stärke. Beschriftet, mit sichtbarem Wert.
3. **Fundstück speichern:** ein Knopf, der die aktuellen Parameter als JSON in die Konsole schreibt (und per `navigator.clipboard.writeText` kopiert). Findet drei Bilder, die ihr Mittwoch zeigen wollt, und legt ihre Parameter als Kommentar ans Ende eurer Datei.

**SELBST-CHECK:** Ein fremder Mensch könnte mit eurem Generator in 60 Sekunden ein schönes Bild finden, ohne eine Zeile Code zu sehen. Das ist die Messlatte — Werkzeug, nicht Demo.

### Stretch-Ebenen (frei, nur wenn Zeit und Lust)

- **Stretch A — Druck-Ästhetik:** eine Bayer-4×4-Matrix quantisiert das fertige Bild auf 3–4 Palettenfarben — Riso-Print-Look, körnig und gewollt unperfekt. Stichwort: ordered dithering. Ein Schalter im UI: an/aus.
- **Stretch B — Die lebende Textur:** Gray-Scott-Reaktions-Diffusion in einem Ping-Pong-RenderTarget — Korallen- und Fingerabdruck-Muster, die live wachsen. Das ist eure Juni-Compute-Denkweise in WebGL-Form. Einstieg: `https://karlsims.com/rd.html`. Deutlich mehr Aufwand; nur anfassen, wenn die Etappen 0–4 stehen.

---

## Das Beispiel

Auf der Website liegt `beispiel.html` — eine vollständige Produktion aller fünf Etappen (plus Stretch A als Schalter), Klient-neutral in kühlem Grün gehalten. Lest den Code wie ein Review: die Kommentare tragen die Etappen-Namen. Was ihr übernehmen dürft: die Struktur, die Formeln, die UI-Verdrahtung als Muster. Was euer sein muss: der Marken-Pol, die gewürfelten Bereiche, die Slider-Grenzen, der Charakter des Bildes.

## Der Rest des Tages

Nach dem Generator, mit frischem Kopf: die **Wochenvorschau** auf der Website lesen (was Mittwoch bis Freitag passiert, mit fertigen Beispielen zum Anschauen) und danach die **Vue-Rampe** durcharbeiten (eigenes Dokument, ~1,5 Stunden: eine Geschichte, ein Marktblick, und eine Probe-Installation, damit Mittwoch nichts klemmt).

## Abgabe

Mittwoch, 08.07, 09:00, im Zoom-Raum: jeder zeigt sein bestes Fundstück, 60 Sekunden, und sagt einen Satz dazu, welcher Regler es geformt hat. Die Datei (mit den drei Fundstück-Kommentaren am Ende) kommt in den Zoom-Chat. Kein Deploy heute — das Werkzeug zählt, nicht die URL.

## Reflexion (eine Frage, zwei Sätze)

Welcher einzelne Parameter hat den Charakter deines Bildes am stärksten verändert — und hättest du das vor dem Bauen vorhergesagt?

---

> „those particular offset values … don't have any special meaning"
> — Iñigo Quilez, *Domain Warping*, iquilezles.org

*Auftakt-Auftrag | Dienstag 07.07.2026 | Vue.js Deep Dive | Morphos GmbH*
