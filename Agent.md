# Agent.md — DDS-Seminar (WS 2026/27)

**Stand:** 13.11.2026  
**Übergeordnet:** `../AGENTS.md` (Kurskorpus SEKM) — zuerst lesen.  
**Zweck:** Orientierung für Agenten, die in `Praktikum_DDS/` am DDS-Seminar arbeiten.

> Diese Datei ist die inhaltliche Agenten-Orientierung. `AGENTS.md` im selben Ordner ist nur ein kleiner Pointer, damit OpenCode sie automatisch lädt.

---

## 1. Was dieser Ordner ist

Arbeitsordner für den **DDS-Seminarvortrag** (Data Distribution Service) im Modul QEKS/SEKM:

- **Vortrag:** Montag, **11.01.2027**, Seminar 4
- **Abgabe Unterlagen:** Freitag, **08.01.2027, 10:00** via Ilias
- **Team:** 4 Personen, 80 Minuten (4 × 12 min + 32 min Diskussion)
- **These/Thema:** DDS für **Smart Factory / Motion Control**, mit Architektur **und** Anwendungsbeispiel
- **Zeitplan:** `Timeline.md` (im Projekt-Root) ist die maßgebliche Planungsdatei.

Es gibt hier **noch keinen Code und kein Build-System**. Neue Inhalte werden als Markdown, DOCX, PPTX, PDF, UML-Export oder C++-Demo abgelegt.

---

## 2. Arbeitsregeln

- **`legacy_*` ist read-only.** Alte Dateien nicht bearbeiten, nicht umbenennen, nicht „aufräumen“.
- **Neue Dateien ohne `legacy_`-Präfix.** Arbeitsdateien nach Schema `YYYY-MM-DD_thema.ext`, finale Abgaben nach `DDS_Seminar_<Art>_v<Version>.<ext>`.
- **Deutsch** ist die Liefer- und Vortragssprache; technische Begriffe dürfen englisch bleiben.
- **Quellenpflicht:** Jede Tatsachenbehauptung im Vortrag/Unterlagen braucht eine Quelle oder eine sichtbare Kennzeichnung als eigene Hypothese.
- **Keine Personennamen** aus Altdateien in neue Dokumente übernehmen (die alte PPTX enthält Namen in der Fußzeile).
- **Keine Altdatei als Quelle zitieren.** Die alte PPTX/Readme ist Inspiration, keine wissenschaftliche Quelle.
- **Aktualität prüfen:** Alte Zusammenfassungen basieren teilweise auf DDS 1.4 (2015) und RTPS 2.1 (2010). Vor dem Zitieren die aktuelle OMG-Fassung prüfen.
- **Nichts erfinden:** Keine erfundenen Tests, Benchmarks, Normen oder Zitate. Unsicherheiten explizit als offen markieren.
- **RTOS-/Embedded-Kontext** des Kurses beachten, auch wenn DDS hier als Seminar (nicht Praktikum) behandelt wird.

---

## 3. Ordnerstruktur

| Ordner | Inhalt | Aktuell |
|---|---|---|
| `01_plan/` | Exposé, Entscheidungen, Meeting-Notizen, Legacy-Kontext | `Projektvarianten.md`, `Expose_v0.1.md`, `Agenda_80min.md`, `legacy_Readme_Altteam.txt`, `legacy_Anmerkungen_Kreiser.txt` |
| `02_quellen/` | OMG-Specs, Tutorials, Papers, Quellenregister, Exzerpte | 3 Legacy-PDFs |
| `03_architektur/` | UML-Diagramme (Component/Deployment/Sequence), Architekturentscheidungen, Exporte | `Variante_A_Krankenhaus_Architektur_v0.1.md`, `Variante_B_Assembly_Zelle_Architektur_v0.1.md` |
| `04_demo/` | Fast-DDS-Demo, IDL, QoS-XML, README, Setup, Backup-Video | `legacy_FastDDS_Anleitung.docx` |
| `05_unterlagen/` | Ausarbeitung, Abschnitte, Glossar, finale PDF-Quelle | 4 Legacy-DOCX |
| `06_folien/` | Foliensatz, Master, Sprechskripte, Probeversionen | `legacy_DDS_Praesentation_4Teile.pptx`, `legacy_Drehbuch_Teil4.docx` |
| `07_qa/` | Fragenbank, Probe-Feedback, offene Fragen | `legacy_Fragen_Teil4.docx` |

Leere Ordner sind Absicht: Sie werden im Laufe des Projekts gefüllt.

---

## 4. Legacy-Bestand: Was ist brauchbar?

Alle Dateien stammen aus einem früheren DDS-Seminar (Vortrag 16.01.2026, 4er-Team, automatisiertes Krankenhaus als Beispiel). Sie sind **Referenz, nicht Abgabe**.

| Datei (neu) | Original | Inhalt | Geeignet für | Einschränkung |
|---|---|---|---|---|
| `01_plan/legacy_Readme_Altteam.txt` | `1readme.txt` | Aufbau des Altordners, Quellenaufteilung, Lessons Learned | Planung, Quellenstrategie | informell; beschreibt alten Stand |
| `01_plan/legacy_Anmerkungen_Kreiser.txt` | `Teil 4/AnmerkungenVomKreiser.txt` | Lecturer-Feedback zu RTPS, Unicast/Multicast, Stateful/Stateless | Q&A, Fallstricke, Review | nur Teil 4; subjektiv/knapp |
| `02_quellen/legacy_DDS_Quelle_OMG_DDS-1.4_2015.pdf` | `DDS_Quelle.pdf` | OMG DDS 1.4, 180 S. | Primärquelle für DCPS/QoS | DDS 1.4 von 2015; Aktualität prüfen |
| `02_quellen/legacy_dds-tutorial_quelle_Corsaro_2014.pdf` | `dds-tutorial_quelle.pdf` | Corsaro, „The DDS Tutorial“, 46 S. | Kompakter Einstieg, Beispiele | 2014; didaktisch, nicht normativ |
| `02_quellen/legacy_RTPS_Quelle_OMG_RTPS-2.1_2010.pdf` | `RTPS_Quelle.pdf` | OMG RTPS 2.1, 216 S. | Historischer Einstieg in RTPS | **veraltet**; aktuelle RTPS-Fassung zitieren |
| `04_demo/legacy_FastDDS_Anleitung.docx` | `FastDDS Anleitung.docx` | Fast DDS unter Linux/VS Code, Raspberry Pi | Demo-Setup, Befehlsreferenz | Linux-spezifisch; Befehle ggf. veraltet |
| `05_unterlagen/legacy_DDS_Merkblatt.docx` | `DDS Merkblatt.docx` | 3-seitiges Merkblatt: Entities, QoS, Discovery | Schnellindex, Stichwortliste | **enthält Fehler** (s. u.); nicht ungeprüft übernehmen |
| `05_unterlagen/legacy_DDS_Tutorial_Zusammenfassung.docx` | `DDS Tutorial.docx` | 7-seitige Zusammenfassung des Corsaro-Tutorials | Verständnis, Formulierungen | Zusammenfassung; am Original prüfen |
| `05_unterlagen/legacy_DDS_Teil1_Spezifikation.docx` | `DDS.docx` | 18-seitiger Tiefeneinstieg in DDS/DCPS | Struktur für Architekturteil | keine Primärquelle; Aussagen prüfen |
| `05_unterlagen/legacy_RTPS_Teil2_Spezifikation.docx` | `RTPS.docx` | 11-seitiger RTPS-Teil (Discovery, Endpoints, QoS) | RTPS-Erklärung, Q&A | basiert auf RTPS 2.1; aktualisieren |
| `06_folien/legacy_DDS_Praesentation_4Teile.pptx` | `DDS.pptx` | 59 Folien, 4 Teile, Krankenhausbeispiel | Struktur, Diagrammideen, Erzählbogen | altes Beispiel, alte Namen, nicht abgabefähig |
| `06_folien/legacy_Drehbuch_Teil4.docx` | `Teil 4/Drehbuch.docx` | Sprechskript zu RTPS/Teil 4 | Formulierungshilfe, Übergänge | an alte Folien gebunden |
| `07_qa/legacy_Fragen_Teil4.docx` | `Teil 4/Fragen.docx` | Q&A-Vorbereitung: Echtzeit, UDP, Serialisierung, History | Fragenbank | Antworten fachlich prüfen |

### Bekannte Fehler/Gefahren im Merkblatt

- „Polling … BLOCKIEREND“ ist **falsch**: `read()`/`take()` sind nicht-blockierend; Polling ist aktiv, aber blockiert nicht.
- „Content-Filtering: Der Sender sendet Daten erst gar nicht“ ist eine **implementierungsabhängige Optimierung**, keine allgemeine DDS-Semantik. In der Regel filtert der Reader bzw. die Middleware; RxO/QoS prüfen.
- „Mit dem DataWriter … empfangen“ beim DataReader ist ein **Tippfehler** (gemeint: DataReader).
- Aussagen zu „22 QoS-Policies“ und einzelnen Policy-Details an der aktuellen Spezifikation prüfen.

---

## 5. Was wiederverwenden, was neu bauen?

**Wiederverwendbar (nach Prüfung):**

- Grobgliederung der alten PPTX: Einordnung → Architektur → QoS/Event Handling → RTPS → Bewertung.
- Erklärungen zu DCPS-Entities, Global Data Space, Discovery, RTPS-Grundprinzip.
- Fast-DDS-Installations- und IDL-Workflow (an aktuelle Version anpassen).
- Fragenkatalog und Lecturer-Anmerkungen als Checkliste.
- Quellenliste (DDS 1.4, Corsaro, RTPS) als Startpunkt.

**Neu zu bauen:**

- Smart-Factory-/Motion-Control-Beispiel statt Krankenhaus.
- Alle Folien und die schriftliche Ausarbeitung (die alte PPTX wurde laut Readme als PDF abgegeben und schlecht bewertet).
- Architekturdiagramme für die Roboter-Assembly-Zelle.
- Security- und TSN-Teil (im alten Material nur am Rand).
- Aktuelle Quellen, korrekte Versionsangaben, eigene Bewertung/Hypothesen.

**Nicht übernehmen:**

- Automatisiertes Krankenhaus als Beispiel.
- Namen, Daten, Fußzeilen, Bewertungsaussagen.
- Ungeprüfte Vendor-Aussagen oder alte QoS-Zahlen.
- Die Aussage, eine PPTX-als-PDF sei ausreichende Seminarunterlagen.

---

## 6. Technischer Rahmen (Kurzfassung)

- **DDS ist ein OMG-Standard**, kein Produkt. Die Implementierung (z. B. Fast DDS, Cyclone DDS) setzt die Spezifikation um.
- **DCPS:** DomainParticipant, Publisher, DataWriter, Subscriber, DataReader, Topic; Global Data Space; Domains/Partitions; Keys/Instances.
- **QoS:** u. a. Reliability, Durability, History, Deadline, LatencyBudget, Ownership, Liveliness, Partition, ResourceLimits; RxO-Matching.
- **RTPS/DDSI:** standardisiertes Wire-Protokoll, dezentrale Discovery (SPDP/SEDP), keine zentrale Broker-Instanz.
- **Security:** DDS Security als Erweiterung (Authentication, Access Control, Cryptography, Logging); nicht mit der Basis-DDS-Spezifikation verwechseln.
- **Beispiel:** Roboter-Assembly-Zelle mit 5 Teilnehmern (Robotersteuerung, Vision, Motion/PLC, Edge-Gateway, MES) und 3 QoS-Klassen (Regelung, Telemetrie, Alarme/Ereignisse).
- **Drei Thesen:** H1 datenzentrische Entkopplung, H2 QoS ist die Architektur, H3 DDS passt für viele-zu-viele-Echtzeitdaten, nicht für jeden Request/Response-Fall.

---

## 7. Quellenhierarchie

1. **OMG-Spezifikationen:** DDS 1.4, DDSI-RTPS (aktuelle Fassung), DDS Security, DDS-XTypes, IDL.
2. **Normen/Paper:** IEEE/TSN, OPC UA, peer-reviewte DDS-/Middleware-Papers.
3. **Corsaro-Tutorial (2014):** gut für Konzepte und Didaktik.
4. **Herstellerdokumentation:** Fast DDS, Cyclone DDS, RTI Connext — nur für Implementierungsdetails.
5. **Legacy-Zusammenfassungen:** nur nach Prüfung gegen 1–4.
6. **Nie:** alte PPTX oder Readme als Belegstelle.

---

## 8. Namens- und Ablagekonventionen

- Legacy: `legacy_<Originalname>` — unverändert lassen.
- Arbeitsdateien: `YYYY-MM-DD_<thema>.<ext>` (z. B. `2026-11-20_expose.md`).
- Finale Unterlagen: `DDS_Seminar_Unterlagen_v1.0.pdf`, `DDS_Seminar_Folien_v1.0.pptx`.
- Quellenregister: `02_quellen/Quellenregister.md` mit Citation-Key, Typ, Fundstelle, Relevanz.
- Diagramme: bearbeitbare Quelle **und** Export (PNG/SVG) in `03_architektur/`.
- Demo: Code, `README.md`, IDL, QoS-XML und ggf. Backup-Video in `04_demo/`; keine Build-Artefakte einchecken.
- Q&A: `07_qa/Fragenbank.md`, sortiert nach A/B/C/D-Themen.

---

## 9. Offene Entscheidungen

| Entscheidung | Empfehlung | Status |
|---|---|---|
| A = Architektur-Kern + Beispiel | Ja | offen |
| Demo-Implementierung | Fast DDS (Alternative: Cyclone DDS) | offen |
| Umfang Unterlagen | 15–20 Seiten + Anhang | offen |
| Diskussionsformat | 4 × (12 + 8), Alternative: 48 + 32 | offen |
| UML-Werkzeug | Visual Paradigm, Export PNG/SVG | offen |
| Genaues Zeitfenster 11.01. | beim Lehrstuhl erfragen | offen |

---

## 10. Nächste Schritte

1. `Timeline.md` lesen und bestätigen.
2. **Variante entschieden:** B (Assembly-Zelle) mit A als Kontrast. Details in `01_plan/Projektvarianten.md`.
3. `01_plan/Expose_v0.1.md` prüfen; offene Punkte in Abschnitt 12 bis zum Scope-Freeze klären.
4. `01_plan/Agenda_80min.md` prüfen; Diskussionsformat (4 × 12+8 oder 48+32) festlegen.
5. Team-Kickoff terminieren; Rollen A/B/C/D personell besetzen.
6. `02_quellen/Quellenregister.md` anlegen; Legacy-PDFs durch aktuelle OMG-Versionen ersetzen.
7. Alte PPTX nur als Struktur lesen; mit dem Neuaufbau für die Zelle beginnen.
8. Fast-DDS-Demo aus der Legacy-Anleitung ableiten und gegen die aktuelle Dokumentation prüfen.

---

## 11. Warnhinweise

- Die Altdateien enthalten **personenbezogene Daten** (Namen in PPTX-Fußzeile und DOCX-Metadaten). Nicht weitergeben, nicht in neue Abgaben kopieren.
- Die alte PPTX ist **kein Vorbild für die Abgabe**: Laut Readme wurde sie nur als PDF exportiert und führte zu einer schlechten Bewertung. Die neuen Unterlagen müssen **ohne Zusatzliteratur nachvollziehbar** sein.
- `DDS_Quelle.pdf` und `RTPS_Quelle.pdf` sind groß und normativ; nicht auswendig zitieren, sondern gezielt Kapitel/Seiten referenzieren.
- Es gibt **keine Tests, keine Benchmarks, keine Build-Anleitung** für die neue Demo — entsprechende Aussagen nicht erfinden.
- Bei Widersprüchen zwischen Altmaterial und aktueller Spezifikation gilt die **aktuelle OMG-Spezifikation**.
