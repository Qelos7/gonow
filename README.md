# GoNow – ÖPNV oder Auto? Der Pendler-Vergleich für Berlin

**Live ausprobieren: [qelos7.github.io/gonow](https://qelos7.github.io/gonow/)** (am besten auf dem Handy)

GoNow vergleicht für eine Strecke in Berlin die **echte, aktuelle BVG-Verbindung** mit **Auto, Fahrrad und Fußweg** – nach Dauer *und* Kosten. Dazu zeigt die App, wann man losgehen muss, wo die Bahn gerade fährt und welche Linien aktuell gestört sind.

| Vergleich | Losgehen | Störungen |
|:---:|:---:|:---:|
| ![Vergleich von ÖPNV, Auto und Fahrrad](screenshots/vergleich.jpg) | ![Karte mit Route und Live-Position der Bahn](screenshots/losgehen.jpg) | ![Live-Störungen der BVG](screenshots/stoerungen.jpg) |

---

## Das Problem

Wer in Berlin pendelt, fragt sich oft: *Lohnt sich heute das Auto, oder bin ich mit der Bahn schneller und günstiger?* Kartendienste zeigen zwar Routen, aber selten einen ehrlichen Vergleich, der Parkplatzsuche, Parkgebühren, den passenden Fahrschein oder ein vorhandenes Deutschlandticket berücksichtigt.

## Was GoNow kann

- **Ortssuche mit Live-Vorschlägen** für Haltestellen und Adressen, bedienbar per Tastatur – oder mit einem Tipp auf „Mein Standort“
- **Echte ÖPNV-Verbindung** von der BVG mit Abfahrt, Ankunft, Umstiegen und Linien; ausgefallene Verbindungen werden automatisch übersprungen
- **Echte Routen für Auto, Fahrrad und Fußweg** über den OpenStreetMap-Routenplaner
- **Kostenvergleich** mit dem richtigen VBB-Fahrschein, Spritkosten und Parkgebühren
- **Deutschlandticket-Schalter** inkl. Hinweis, ab wie vielen Fahrten im Monat es sich lohnt
- **„Wenn du jetzt losgehst“**: Countdown, Linie, Gleis, Verspätung und eine Karte mit der **Live-Position der Bahn** (alle 15 Sekunden aktualisiert)
- **Live-Störungen** bei S-Bahn, U-Bahn und Regionalzügen (Ausfälle, Teilausfälle, Verspätungen) sowie Warnhinweise zur eigenen Verbindung
- **Handy-Ansicht wie eine App** mit Tab-Leiste; lässt sich auf den Home-Bildschirm legen

## So rechnet GoNow

| Was | Regel |
|---|---|
| **Fahrschein** (VBB-Tarif seit 1.1.2026) | Kurzstrecke **2,80 €** (bis 3 Stationen S-/U-Bahn oder 6 Haltestellen Bus/Tram ohne Umsteigen) · Einzelfahrschein AB **4,00 €** (ganz Berlin) · ABC **5,00 €** (sobald die Fahrt Berlin verlässt, z. B. Potsdam oder BER) |
| **Deutschlandticket** | 63 €/Monat → Einzelfahrt kostet 0 € extra; „lohnt sich ab“ = 63 € ÷ Einzelpreis |
| **Auto – Zeit** | Routenplaner-Fahrzeit × 1,35 (Berliner Verkehr) + Parkplatzsuche (10 min innerhalb des S-Bahn-Rings, sonst 4 min) + 2 min Fußweg |
| **Auto – Kosten** | Sprit (7 l/100 km × 1,75 €/l) + Parken 3 €/h, wenn das Ziel innerhalb des S-Bahn-Rings liegt; Parkdauer wählbar |
| **Fahrrad & Fußweg** | Dauer und Strecke direkt vom Routenplaner, kostenlos |

Ob ein Ziel im S-Bahn-Ring liegt, prüft GoNow geometrisch anhand der Ringbahn-Bahnhöfe; ob eine Haltestelle in Berlin liegt (Tarifbereich AB vs. C), am Haltestellennamen und an den Koordinaten.

## Datenquellen

| Daten | Quelle |
|---|---|
| Haltestellen, Verbindungen, Zugpositionen, Störungen | BVG über die offene Schnittstelle [v6.bvg.transport.rest](https://v6.bvg.transport.rest/) |
| Routen für Auto, Fahrrad, Fußweg | [routing.openstreetmap.de](https://routing.openstreetmap.de/) (FOSSGIS e. V.) |
| Karte | © [OpenStreetMap](https://www.openstreetmap.org/copyright)-Mitwirkende |
| Fahrpreise | [VBB-Tarif ab 1. Januar 2026](https://www.vbb.de/news/neue-fahrpreise-im-vbb-ab-1-januar-2026/) |

GoNow speichert keine persönlichen Daten auf einem Server. Nur zwei Einstellungen (Deutschlandticket, Parkdauer) merkt sich der eigene Browser.

## Technik

- **React 18** (Oberfläche), **Tailwind CSS** (Design), **Leaflet** (Karte)
- Bewusst als **eine einzige HTML-Datei** ohne Build-Schritt gebaut: läuft sofort im Browser, braucht keine Installation und lässt sich kostenlos über **GitHub Pages** veröffentlichen
- Live-Daten werden direkt im Browser abgefragt; mehrere Anfragen laufen parallel, veraltete Suchanfragen werden abgebrochen

## Entstehung & meine Rolle

GoNow begann als Prototyp, den ich bei einem **AWS-Workshop mit dem KI-Werkzeug Kiro** gebaut habe. 
Der Hauptgedanke war dabei, ein Produkt, welches wir im Alltag benötigen könnten, von Scratch zu erstellen und ein Prototyp vorzustellen.
Der Prototyp funktionierte nicht zuverlässig aufgrund der kurzfristigen Zeit.
An einem Sonntag habe ich mich hingesetzt und wollte wissen, wie ich ohne Programmierkenntnisse und kaum Prompting-Tricks ein "Endprodukt" veröffentlichen kann. 
Mithilfe von Claude, der das coding übernommen hat, und meinen kreativen Vorstellungen, wollte ich schauen, wie weit ich kommen kann. 

Meine Aufgaben dabei: die Produktidee, das Festlegen der Prioritäten, die Entscheidung über Funktionen und Aussehen, das Testen und die Veröffentlichung. Die Umsetzung im Code entstand im Dialog mit der KI.

Wichtige Schritte vom Prototyp zur heutigen App:

1. **Fehleranalyse:** Die Suche fand keine einzige Haltestelle (falsch ausgelesene Koordinaten), Verbindungsfehler wurden verschluckt, alte Eingaben blieben gespeichert, die Tastatur funktionierte nicht.
2. **Live-Karte** mit Route und Echtzeit-Position der Bahn
3. **Ehrlicher Vergleich:** echte Routen statt Luftlinie, richtige Tarifzonen und aktuelle Preise, Deutschlandticket, Parkkosten
4. **Echte Störungsdaten** der BVG statt erfundener Beispielmeldungen
5. **Handy-Ansicht** mit Tab-Leiste und Veröffentlichung über GitHub Pages
6. **Zuverlässigkeit:** ausgefallene Verbindungen werden übersprungen

## Grenzen

- Auto-Zeiten und -Kosten sind **Schätzungen** (Verkehrsaufschlag, Spritpreis, Parkgebühr sind Annahmen); Versicherung und Wertverlust sind nicht eingerechnet.
- Die genutzten Dienste sind **kostenlose Gemeinschaftsangebote ohne Garantie** und nur für geringe Nutzung gedacht.
- Die Störungsliste fragt **9 große Knotenbahnhöfe** ab, weil die Schnittstelle keine Gesamtliste anbietet; Störungen am Stadtrand und bei Bus/Tram können fehlen.
- Nutzer-Meldungen sind nur in der eigenen Sitzung sichtbar (keine gemeinsame Datenbank).

## Ideen für später

· Abfahrtszeit wählen 
· Start/Ziel tauschen 
· Lieblingsstrecken speichern 
· mehrere Verbindungen zur Auswahl 
· Wetter und CO₂ einbeziehen 
· gemeinsame Datenbank für Meldungen 
· Umbau zu einem Projekt mit mehreren Dateien und automatischen Tests

## Selbst starten

Die Datei `index.html` herunterladen und über einen kleinen lokalen Webserver öffnen, zum Beispiel:

```bash
python3 -m http.server 8000
```

Dann im Browser `http://localhost:8000` aufrufen.
