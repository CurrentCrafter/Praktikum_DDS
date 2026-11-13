# Timeline — DDS-Seminar (WS 2026/27)

**Stand:** 13.11.2026  
**Vortrag:** Montag, 11.01.2027 (Seminar 4)  
**Abgabe der finalen Unterlagen:** Freitag, 08.01.2027, 10:00 via Ilias  
**Team:** 4 Personen · 80 Minuten (4 × 12 min Vortrag + 32 min Diskussion)  
**Thema:** DDS (Data Distribution Service) für Smart Factory / Motion Control

> **Legende:** A = du (Architektur + roter Faden) · B = QoS/Real-Time/TSN · C = Security/Deployment · D = Vergleich/Demo/Fazit  
> **Status:** `[ ]` offen · `[~]` in Arbeit · `[x]` erledigt

---

## 1. Fixpunkte

| Datum | Was | Verbindlichkeit |
|---|---|---|
| **13.11.2026** | Plan v1.0, Rollen und Scope | heute |
| **23.11.2026** | Praktikum | blockiert für Seminar-Deadlines |
| **27.11.2026** | Scope-Freeze: Beispiel, Thesen, Quellen v1 | hart |
| **04.12.2026** | Internes Review #1 | hart |
| **07.12.2026** | Praktikum | blockiert |
| **18.12.2026** | Internes Review #2, Vollentwurf v1.0 | hart |
| **21.12.2026** | Praktikum | blockiert |
| **22.12.2026** | Content-Freeze v1.1 | hart |
| **23.12.2026–03.01.2027** | Weihnachtspause | keine Team-Deadlines |
| **04.01.2027** | Optionales Seminar / Wiedereinstieg | optional |
| **07.01.2027, 18:00** | Finales PDF intern fertig | hart |
| **08.01.2027, 10:00** | Upload via Ilias | **harte Abgabe** |
| **09.–10.01.2027** | Generalprobe #2, Technikcheck, Puffer | empfohlen |
| **11.01.2027** | **Vortrag** | fix |
| **25.01.2027** | Abschlusspräsentation Praktikum | danach Fokuswechsel |

---

## 2. Meilensteine

| ID | Datum | Meilenstein | Ergebnis | Owner | Status |
|---|---|---|---|---|---|
| M1 | 20.11.2026 | Kickoff + Exposé | 1 Seite: Scope, 3 Thesen, Beispielzelle, Rollen | A | [ ] |
| M2 | 27.11.2026 | Scope-Freeze | Beispielspezifikation, QoS-Tabelle v0.1, Quellenregister v1, Implementierungsentscheidung | A + B + D | [ ] |
| M3 | 04.12.2026 | Review #1 | Abschnittsentwürfe B/C/D, Foliengerüst, Demo-Hello-World | alle | [ ] |
| M4 | 11.12.2026 | Architektur v1 | Component-, Deployment-, Sequence-Diagramm, IDL-Typen | A + C | [ ] |
| M5 | 18.12.2026 | Vollentwurf v1.0 | Unterlagen vollständig, Demo lauffähig, Zitierprüfung | alle | [ ] |
| M6 | 22.12.2026 | Content-Freeze | Unterlagen v1.1, keine neuen Inhalte mehr | alle | [ ] |
| M7 | 04.01.2027 | Foliensatz v1 | 4 Einzeldeckungen auf gemeinsamem Master | jede Person | [ ] |
| M8 | 08.01.2027 | Abgabe + Generalprobe | Finales PDF hochgeladen, Timing geprüft, Q&A-Bank | A + alle | [ ] |
| M9 | 11.01.2027 | Vortrag | 80 Minuten inkl. Diskussion | alle | [ ] |

---

## 3. Wochenplan

### KW 46 — 13.11.–15.11.2026
**Fokus:** Entscheidungen, Plan, Team-Kickoff vorbereiten

- [ ] Plan v1.0 bestätigen
- [ ] Rollen A/B/C/D fixieren
- [ ] Termin für 60-min-Kickoff festlegen
- [ ] Ordnerstruktur anlegen
- [ ] Exposé-Gerüst vorbereiten

**Output:** bestätigter Plan, Kickoff-Termin

---

### KW 47 — 16.11.–20.11.2026
**Fokus:** Kickoff, gemeinsames Verständnis, Exposé

- [ ] Team-Kickoff (60 min): Ziel, Scope, Rollen, Beispielzelle
- [ ] DDS-Grundlagen gemeinsam lesen: DCPS, QoS, Discovery, RTPS
- [ ] Smart-Factory-Zelle skizzieren: 5 Teilnehmer, Topics, Datenströme
- [ ] Drei Thesen H1–H3 formulieren
- [ ] Quellenjagd starten: OMG-Specs, Papers, Vendor-Doku
- [ ] **M1: Exposé v1 (20.11.)**

**Output:** Exposé, erste Quellenliste, gemeinsames Glossar

---

### KW 48 — 23.11.–27.11.2026
**Fokus:** Recherche, Architektur v0.1, Scope-Freeze  
**Achtung:** **23.11. Praktikum** — keine Seminar-Deadlines an diesem Tag

- [ ] Architektur v0.1: Komponenten, Domains/Partitions, Topics
- [ ] Beispielspezifikation v1: Teilnehmer, Topics, QoS-Klassen, Latenzbudget
- [ ] Quellenregister v1: 15–25 Quellen mit Citation-Key, Typ, Relevanz
- [ ] Implementierung entscheiden: Fast DDS vs. Cyclone DDS
- [ ] Demo-Hello-World vorbereiten (IDL + Pub/Sub)
- [ ] **M2: Scope-Freeze (27.11.)**

**Output:** Architektur v0.1, Beispiel v1, Quellen v1, Tool-Entscheidung

---

### KW 49 — 30.11.–04.12.2026
**Fokus:** Erste Abschnittsentwürfe, Review #1

- [ ] B: QoS-/Real-Time-Abschnitt entwerfen
- [ ] C: Security-/Deployment-Abschnitt entwerfen
- [ ] D: Vergleichstabelle OPC UA/MQTT/SOME-IP entwerfen
- [ ] A: DCPS/RTPS-Abschnitt und Beispiel-Mapping entwerfen
- [ ] Foliengerüst pro Person (10–12 Folien)
- [ ] Demo: erster lauffähiger Pub/Sub
- [ ] **M3: Review #1 (04.12.)** — Gap-Check gegen Seminar-Brief

**Output:** vier Abschnittsentwürfe, Foliengerüst, Demo v0.1

---

### KW 50 — 07.12.–11.12.2026
**Fokus:** Integration, Diagramme, Vertiefung  
**Achtung:** **07.12. Praktikum**

- [ ] Architekturdiagramme v1: Component, Deployment, Sequence, IDL/Typen
- [ ] Unterlagen v0.5: Abschnitte zusammenführen
- [ ] Security/TSN-Tiefe kalibrieren (nicht überladen)
- [ ] Demo: QoS-XML, reliable vs. best-effort, Deadline
- [ ] Quellen prüfen: mind. 2 unabhängige Quellen pro Kernaussage
- [ ] **M4: Architektur v1 (11.12.)**

**Output:** Diagramme v1, Unterlagen v0.5, Demo v0.5

---

### KW 51 — 14.12.–18.12.2026
**Fokus:** Vollentwurf, Review #2

- [ ] Unterlagen v1.0 vollständig
- [ ] Alle Diagramme final, einheitliche Notation und Legenden
- [ ] Demo v1 inkl. README und Backup-Video
- [ ] Zitierprüfung: Quellen, Bildrechte, Konsistenz
- [ ] Q&A-Bank v0.1: 20–30 Fragen nach Themen
- [ ] **M5: Review #2 (18.12.)**

**Output:** Vollentwurf v1.0, Demo v1, Q&A v0.1

---

### KW 52 — 21.12.–22.12.2026
**Fokus:** Freeze vor Weihnachten  
**Achtung:** **21.12. Praktikum**

- [ ] Feedback aus Review #2 einarbeiten
- [ ] **M6: Content-Freeze v1.1 (22.12.)**
- [ ] Keine neuen Inhalte, keine neuen Quellen
- [ ] Offene Punkte in „Parkplatz“ verschieben

**Output:** eingefrorene Unterlagen v1.1

---

### 23.12.2026–03.01.2027 — Weihnachtspause
- [ ] Keine Team-Deadlines
- [ ] Optional: leichte Lektüre, Folien laut lesen
- [ ] Erholung wichtiger als neue Inhalte

---

### KW 01 — 04.01.–08.01.2027
**Fokus:** Endkorrektur, Layout, Abgabe, Generalprobe

- [ ] 04.01.: Wiedereinstieg, offene Kommentare abarbeiten (optionales Seminar)
- [ ] 05.01.: **Generalprobe #1** mit Stoppuhr
- [ ] 06.01.: Korrekturen aus Generalprobe
- [ ] 07.01., 18:00: **finales PDF intern fertig**
- [ ] 08.01., 10:00: **Upload via Ilias**
- [ ] 08.01.: **Generalprobe #2**, Technikcheck, Q&A-Bank final
- [ ] **M7/M8: Foliensatz v1 + Abgabe**

**Output:** finales PDF, hochgeladene Unterlagen, geprobter Vortrag

---

### 09.01.–10.01.2027 — Puffer
- [ ] Letzter Timing-Check
- [ ] Backup-PDF und Demo-Video auf zwei Geräten
- [ ] Raum/Technik klären: Beamer, Adapter, Audio
- [ ] Ruhiger Sonntag

---

### 11.01.2027 — Vortrag
- [ ] 60 min vorher da sein
- [ ] Backup-PDF und Video dabei
- [ ] 80-min-Block: 48 min Vortrag + 32 min Diskussion
- [ ] **M9: Vortrag**

---

## 4. Gantt-Übersicht

```mermaid
gantt
    title DDS-Seminar — Timeline bis 11.01.2027
    dateFormat  YYYY-MM-DD
    axisFormat  %d.%m.

    section Vorbereitung
    Kickoff + Exposé            :a1, 2026-11-13, 8d
    Recherche + Quellen         :a2, 2026-11-16, 12d
    Beispiel + Architektur v0.1 :a3, 2026-11-23, 5d
    Scope-Freeze                :milestone, m1, 2026-11-27, 0d

    section Entwurf
    Abschnittsentwürfe          :a4, 2026-11-30, 5d
    Review #1                   :milestone, m2, 2026-12-04, 0d
    Diagramme + Integration     :a5, 2026-12-07, 5d
    Vollentwurf                 :a6, 2026-12-14, 5d
    Review #2                   :milestone, m3, 2026-12-18, 0d

    section Freeze
    Content-Freeze              :milestone, m4, 2026-12-22, 0d
    Weihnachtspause             :a7, 2026-12-23, 12d

    section Endphase
    Korrektur + Layout          :a8, 2027-01-04, 4d
    Generalproben               :a9, 2027-01-05, 6d
    Abgabe                      :milestone, m5, 2027-01-08, 0d
    Vortrag                     :milestone, m6, 2027-01-11, 0d
```

---

## 5. Arbeitspakete pro Person

| Person | Arbeitspaket | Kernartefakte | Fällig |
|---|---|---|---|
| **A** | Architektur, roter Faden, Integration, Upload | DCPS/RTPS-Abschnitt, Beispiel-Mapping, Gesamt-PDF | 18.12. / 07.01. |
| **B** | QoS, Real-Time, TSN | QoS-Tabelle, Latenzbudget, QoS-Abschnitt | 04.12. / 11.12. |
| **C** | Security, Deployment, Qualitätsmerkmale | Threat-Szenario, Deployment-Diagramm, Security-Abschnitt | 04.12. / 11.12. |
| **D** | Vergleich, Demo, Fazit/Ausblick | Vergleichstabelle, Demo-Repo, Backup-Video, Fazit | 04.12. / 18.12. |
| **alle** | Unterlagen, Folien, Q&A, Proben | gemeinsamer Master, Q&A-Bank | 08.01. |

---

## 6. Kritischer Pfad und Puffer

**Kritischer Pfad:**

1. Beispielspezifikation (27.11.)
2. Architekturdiagramme v1 (11.12.)
3. Unterlagen v1.0 (18.12.)
4. Content-Freeze (22.12.)
5. Finales PDF (07.01.)
6. Upload (08.01.)

**Puffer:**

- 09.–10.01.2027 als technischer und inhaltlicher Puffer
- Demo ist **nicht** kritisch: Backup-Video und Code-Ausschnitte reichen als Fallback
- Quellenregister hat keinen Puffer mehr nach dem 27.11. → früh starten


---

## 7. Offene Entscheidungen

| Enscheidung | Empfehlung | Status |
|---|---|---|
| A = Architektur-Kern + Beispiel? | Ja | [ ] |
| DDS-Implementierung | eProsima Fast DDS (Alternative: Cyclone DDS) | [ ] |
| Umfang Unterlagen | 15–20 Seiten + Anhang | [ ] |
| Diskussionsformat | ein 32-min-Block | [ ] |
| UML-Werkzeug | Visual Paradigm, Export PNG/SVG | [ ] |
| Sprache | Deutsch | [ ] |
| Genaues Zeitfenster am 11.01. | beim Lehrstuhl erfragen | [ ] |
| Erreichbarkeit 23.12.–03.01. | im Team klären | [ ] |

---

## 8. Nächste Schritte

- [ ] Plan v1.0 bestätigen
- [ ] Ordnerstruktur anlegen: `01_plan`, `02_quellen`, `03_architektur`, `04_demo`, `05_unterlagen`, `06_folien`, `07_qa`
- [ ] Exposé-Gerüst mit H1–H3 erstellen
- [ ] Quellenregister starten
- [ ] Smart-Factory-Zelle skizzieren
