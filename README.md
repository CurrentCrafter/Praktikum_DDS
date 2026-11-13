# DDS-Seminar — WS 2026/27

Seminarprojekt zu **Data Distribution Service (DDS)** im Modul QEKS/SEKM bei Prof. Dr.-Ing. Stefan Kreiser.

**Thema:** DDS für eine modulare Roboter-Assembly-Zelle — Architektur, QoS und Security (Variante B mit A als Kontrast)  
**Team:** 4 Personen · **Vortrag:** 11.01.2027 · **Abgabe:** 08.01.2027, 10:00 via Ilias  
**Umfang:** 80 Minuten (4 × 12 min Vortrag + 4 × 8 min Diskussion)

> Dies ist ein Dokumentations- und Präsentationsprojekt, kein Softwareprojekt. Es gibt (noch) keinen Build, keine Tests und keine CI.


> Empfohlene Benutzeroberfläche: VSCodium mit mermaid plugin (Natürlich unter Linux)
---

## Inhaltsverzeichnis

- [Schnellstart](#schnellstart)
- [Zeitplan](#zeitplan)
- [Projektstruktur](#projektstruktur)
- [Ergebnisse](#ergebnisse)
- [Legacy-Material](#legacy-material)
- [Arbeitsweise](#arbeitsweise)
- [Offene Entscheidungen](#offene-entscheidungen)

---

## Schnellstart

| Ich möchte … | Datei |
|---|---|
| den Zeitplan sehen | [`Timeline.md`](Timeline.md) |
| zwei Projektvarianten vergleichen | [`01_plan/Projektvarianten.md`](01_plan/Projektvarianten.md) |
| das Exposé lesen | [`01_plan/Expose_v0.1.md`](01_plan/Expose_v0.1.md) |
| den 80-Minuten-Ablauf sehen | [`01_plan/Agenda_80min.md`](01_plan/Agenda_80min.md) |
| Architektur Variante A ansehen | [`03_architektur/Variante_A_Krankenhaus_Architektur_v0.1.md`](03_architektur/Variante_A_Krankenhaus_Architektur_v0.1.md) |
| Architektur Variante B ansehen | [`03_architektur/Variante_B_Assembly_Zelle_Architektur_v0.1.md`](03_architektur/Variante_B_Assembly_Zelle_Architektur_v0.1.md) |
| die Agenten-Orientierung lesen | [`Agent.md`](Agent.md) |
| offene inhaltliche Fragen sehen | [`DDS_offene_Fragen.md`](DDS_offene_Fragen.md) |
| Quellen und Altmaterial finden | [`02_quellen/`](02_quellen/) |
| die Ausarbeitung schreiben | [`05_unterlagen/`](05_unterlagen/) |
| Folien bauen | [`06_folien/`](06_folien/) |
| Fragen für die Diskussion sammeln | [`07_qa/`](07_qa/) |

---

## Zeitplan

| Meilenstein | Datum |
|---|---|
| Kickoff + Exposé | 20.11.2026 |
| Scope-Freeze | 27.11.2026 |
| Review #1 | 04.12.2026 |
| Architektur v1 | 11.12.2026 |
| Vollentwurf v1.0 | 18.12.2026 |
| Content-Freeze | 22.12.2026 |
| Foliensatz v1 | 04.01.2027 |
| Finales PDF | 07.01.2027, 18:00 |
| **Abgabe** | **08.01.2027, 10:00** |
| Generalproben | 08.01. + 10.01.2027 |
| **Vortrag** | **11.01.2027** |

Details, Puffer und Risiken: [`Timeline.md`](Timeline.md).

---

## Projektstruktur

```text
Praktikum_DDS/
├── 01_plan/          Projektvarianten, Exposé, Entscheidungen, Legacy-Kontext
├── 02_quellen/       OMG-Specs, Tutorials, Papers, Quellenregister
├── 03_architektur/   UML: Component, Deployment, Sequence, IDL-Typen
├── 04_demo/          Fast-DDS-Demo, IDL, QoS-XML, Setup
├── 05_unterlagen/    Ausarbeitung, Abschnitte, Glossar, finales PDF
├── 06_folien/        Foliensatz, Master, Sprechskripte
├── 07_qa/            Fragenbank, Probe-Feedback
├── Agent.md          Orientierung für Agenten
├── AGENTS.md         Auto-Load-Pointer auf Agent.md
├── Timeline.md       Zeitplan, Meilensteine, Risiken
└── README.md         diese Datei
```

Neue Dateien werden ohne `legacy_`-Präfix angelegt. Arbeitsdateien nach Schema `YYYY-MM-DD_thema.ext`, finale Abgaben nach `DDS_Seminar_<Art>_v<Version>.<ext>`.

---

## Ergebnisse

Die Projektmappe besteht aus:

1. **Schriftliche Seminarunterlagen** — ohne weitere Zusatzliteratur nachvollziehbar, PDF mit hellem Hintergrund.
2. **Foliensatz** — 4 Teile, gemeinsamer Master, 12 Minuten pro Person.
3. **Architektur** — DDS-Referenzarchitektur plus Instanziierung in der gewählten Domäne (A: Krankenhaus, B: Roboter-Assembly-Zelle).
4. **Demo** — minimales Fast-DDS-Beispiel mit IDL, Publisher, Subscriber und QoS-XML; Backup-Video als Fallback.
5. **Q&A-Bank** — 20–30 vorbereitete Fragen inkl. Antworten.

Roter Faden mit drei Thesen:

- **H1:** DDS ist eine datenzentrische Architektur zur Entkopplung in Raum, Zeit und Datenfluss — keine „schnelle Message Queue“.
- **H2:** QoS ist die eigentliche Architektur; Default-QoS ist ein Entwurfsfehler.
- **H3:** DDS passt für viele-zu-viele-Echtzeitdatenströme, nicht für jeden Request/Response-Fall; Security und TSN müssen end-to-end gedacht werden.

---

## Legacy-Material

Die Dateien mit `legacy_`-Präfix stammen aus einem früheren DDS-Seminar (Vortrag 16.01.2026, Krankenhausbeispiel) und sind **read-only Referenz**:

- nutzbar als Struktur-, Formulierungs- und Q&A-Vorlage,
- **keine** zitierfähige Quelle,
- nicht ungeprüft übernehmen (das Merkblatt enthält sachliche Fehler),
- keine Personennamen in neue Dokumente kopieren.

Details und Bewertung jeder Datei: [`Agent.md`](Agent.md).

---

## Arbeitsweise

- **Sprache:** Deutsch; technische Begriffe dürfen englisch bleiben.
- **Quellen:** Jede Kernaussage braucht eine Quelle oder eine sichtbare Kennzeichnung als eigene Hypothese. OMG-Specs und Paper vor Vendor-Doku.
- **Keine Personendaten:** Namen aus Altmaterial nicht in neue Dateien übernehmen.
- **Keine erfundenen Ergebnisse:** Keine Tests, Benchmarks oder Zitate behaupten, die nicht existieren.
- **Kleine Schritte:** Änderungen thematisch committen; `main` bleibt integrierbar.
- **Branch-Namen:** `docs/…`, `arch/…`, `demo/…`, `slides/…`, `qa/…`.
- **Commit-Messages:** `docs: …`, `arch: …`, `demo: …`, `slides: …`, `qa: …`.

---

## Offene Entscheidungen

| Entscheidung | Empfehlung |
|---|---|
| Projektvariante | **entschieden:** B (Assembly-Zelle) mit A (Krankenhaus) als Kontrast |
| Anteil A = Architektur-Kern + Beispiel | Ja |
| Demo-Implementierung | Fast DDS (Alternative: Cyclone DDS) |
| Umfang der Unterlagen | 15–20 Seiten + Anhang |
| Diskussionsformat | 4 × (12 min Vortrag + 8 min Diskussion), Alternative: 48 + 32 |
| UML-Werkzeug | Visual Paradigm, Export PNG/SVG |
| Genaues Zeitfenster am 11.01. | beim Lehrstuhl erfragen |

---

## Status

- [x] Projektstruktur und Legacy-Sichtung
- [x] Zeitplan und Agenten-Orientierung
- [x] Zwei Projektvarianten erarbeitet
- [x] Erste Mermaid-Architektur für A und B (v0.1)
- [x] Exposé v0.1 und 80-Minuten-Agenda
- [ ] Scope-Freeze
- [ ] Architektur v1
- [ ] Demo v1
- [ ] Unterlagen v1.0
- [ ] Foliensatz v1
- [ ] Abgabe und Vortrag
