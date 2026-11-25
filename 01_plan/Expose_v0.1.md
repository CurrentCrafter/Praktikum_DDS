# Exposé — DDS-Architektur: Assembly-Zelle und AMR-Flotte

**Stand:** 25.11.2026
**Revision:** v0.2
**Status:** Entwurf; Assembly-Zelle und AMR-Flotte sind Vergleichskandidaten, Auswahl steht aus
**Thematischer Scope:** DDS-Referenzarchitektur, Vergleich der beiden Anwendungskandidaten und kurzer UMAA-Transfer
**Vortrag:** Montag, 11.01.2027 · **Abgabe:** Freitag, 08.01.2027, 10:00 via Ilias
**Team:** 4 Personen · 80 Minuten (48 min Vortrag + ca. 32 min Diskussion; Ablauf offen)

> Das Exposé wird als gemeinsame Arbeitsgrundlage weiterbearbeitet. Laut Orga-Präsentation sollen alle Rollen Assembly-Zelle und AMR-Flotte vergleichen; die Auswahl des Hauptbeispiels wird danach begründet getroffen. UMAA bleibt ein kurzer Transferfall. Hausautomation und Krankenhaus werden nicht als zusätzliche Fallarchitekturen ausgearbeitet.

---

## 1. Ausgangslage und Problem

Als Anwendungskandidaten werden eine modulare Roboter-Assembly-Zelle und eine AMR-Flotte betrachtet. Die Assembly-Zelle umfasst im Arbeitsentwurf Komponenten unterschiedlicher Hersteller: Robotersteuerung, Vision-System, Motion-/PLC-Controller, Safety-Steuerung, Edge-Gateway und MES-Anbindung. Die DDS-relevanten Zellkomponenten tauschen Betriebszustände, Trajektorien, Bildergebnisse, Alarme und Telemetrie aus. Die Safety-Funktion ist separat abgegrenzt; die MES-Anbindung endet in dieser Kandidatenskizze am Edge-Gateway.

Dabei treten vier Probleme gleichzeitig auf:

1. **Heterogenität** — unterschiedliche Betriebssysteme, Rechenleistung und Programmiersprachen.
2. **Zeitverhalten** — ausgewählte Bewegungs- und Zustandsdaten haben enge Aktualitäts- oder Fristanforderungen; funktionale Safety ist separat zu behandeln.
3. **Kopplung** — zentralisierte Client/Server- oder Broker-Entwürfe können einen zusätzlichen Hop und einen zentralen Ausfallpunkt erzeugen; das ist ein Architekturtrade-off, keine Eigenschaft jedes Broker-Systems.
4. **Wandlungsfähigkeit** — Zellen werden umgebaut, Komponenten ersetzt, Werkstücke gewechselt.

DDS (Data Distribution Service, OMG) adressiert diese Probleme mit einem **datenzentrischen** Modell: Teilnehmer publizieren und abonnieren typisierte Topics in einem Global Data Space, ohne sich gegenseitig zu kennen. **QoS** legt fest, welche Eigenschaften der Datenstrom haben muss. **RTPS** definiert das Wire-Protokoll, **DDS Security** ergänzt Authentifizierung, Zugriffskontrolle und Verschlüsselung.

**Die Leitfrage des Seminars lautet:** Welches der Szenarien Assembly-Zelle oder AMR-Flotte eignet sich besser, um DDS-Architektur, Automatisierungsanforderungen und Qualitätsmerkmale nachvollziehbar zu erklären — und wo liegen die Grenzen von DDS?

**Vergleichsraster (noch zu befüllen):**

| Rollenpaket | Prüfkriterien für beide Kandidaten | Assembly-Zelle: Belege/Bewertung | AMR-Flotte: Belege/Bewertung |
|---|---|---|---|
| A — Architektur | Komponenten, Kommunikationsbeziehungen, Systemgrenze, DDS-Mapping | offen | offen |
| B — Automatisierung | Echtzeit, Events, Scheduling/Synchronisation, Embedded-HW, Heterogenität | offen | offen |
| C — Qualitätsmerkmale | Zuverlässigkeit, Leistung, Flexibilität, Robustheit, Verfügbarkeit, Sicherheit, Anpassbarkeit, Testbarkeit | offen | offen |
| D — Zukunft/DDS-spezifisch | Offenheit, Zukunftsfähigkeit, TSN, Embedded/IoT, DDS-Sicherheit, Anwendungsbezug | offen | offen |

Die Rollen tragen Quellen und eigene Hypothesen getrennt ein; daraus wird die Auswahl des vollständig auszuarbeitenden Beispiels begründet.

---

## 2. Drei Thesen

Die Thesen sind bewusst als **prüfbare Behauptungen** formuliert, nicht als Zusammenfassung der Spezifikation.

### H1 — DDS ist eine datenzentrische Architektur, keine schnelle Message Queue

DDS entkoppelt Teilnehmer in **Raum** (keine Adresskenntnis), **Zeit** (Durability, History) und **Datenfluss** (Topic statt Aufruf). Der Nutzen entsteht nicht durch „schneller als MQTT", sondern durch das Datenmodell: Topics, Keys und Instanzen beschreiben Zustände, nicht Nachrichten.

*Prüfzugang:* Kandidatenvergleich; Mapping der Komponenten des ausgewählten Falls auf Topics; Gegenprobe, wo DDS unnötig komplex ist.

### H2 — QoS ist die eigentliche Architektur; Default-QoS ist ein Entwurfsfehler

Die fachlichen Anforderungen des ausgewählten Anwendungsszenarios (Fristen, Verlusttoleranz, Aktualität und History) bestimmen die Auswahl der QoS-Policies und werden nicht durch QoS ersetzt. Jede Wahl braucht eine Anforderungsbegründung. Safety-Daten sind nicht Teil der DDS-QoS-Beispiele.

*Prüfzugang:* QoS-Tabelle pro Topic; RxO-Matching; Demo mit zwei Profilen; Begründung jeder QoS-Achse.

### H3 — DDS passt für viele-zu-viele-Echtzeitdatenströme, nicht für jeden Fall

DDS ist stark bei zyklischen, multicastfähigen Datenströmen mit vielen Teilnehmern. Bei Request/Response, transaktionalen Zugriffen oder tiefen Cloud-Integrationen ist es oft die falsche Wahl. Security und TSN müssen **end-to-end** gedacht werden, nicht als DDS-Feature.

*Prüfzugang:* Abgrenzung zu OPC UA Pub/Sub, MQTT und SOME/IP; Benennung der Grenzen; Diskussion der Nicht-Anwendungsfälle.

---

## 3. Beispielsystem

**Vergleichskandidaten:**

1. **Modulare Assembly-Zelle:** Roboter, Vision, Motion/PLC, Safety, Edge und MES-Anbindung.
2. **AMR-Flotte:** Transportroboter im Lager, Flottenmanager und Ladestationen. Für diesen Kandidaten gilt als Umsetzungsprofil direkte DDS-API ohne ROS 2; die DDS-Implementierung bleibt offen.

   Architekturentwurf: [`../03_architektur/Variante_C_AMR_Flotte_Architektur_v0.1.md`](../03_architektur/Variante_C_AMR_Flotte_Architektur_v0.1.md).

Alle Rollen bewerten beide Kandidaten anhand ihres Arbeitspakets. Die Entscheidung, welcher Kandidat das Hauptbeispiel wird, ist offen und wird im Scope-Freeze begründet. UMAA bleibt ein kurzer Transferfall; es ist weder der Gegenentwurf zu DDS noch eine dritte vollständige Fallarchitektur.

### Assembly-Zelle — Arbeitsentwurf

**Fachliche Komponenten und Datenflüsse:** Die Komponenten sind keine Festlegung auf gleich viele DDS-`DomainParticipant`s; die Prozesszuordnung wird im Deployment begründet.

| Komponente | Rolle | Publiziert | Abonniert |
|---|---|---|---|
| Robotersteuerung (RC) | Bahnplanung, Zellsteuerung | `Trajectory`, `Alarm` | `JointState`, `VisionResult` |
| Vision-System | Lage-/Qualitätsprüfung | `VisionResult` | — |
| Motion/PLC | Achsregelung, Zyklus | `JointState`, `DeviceTelemetry`, ggf. `Alarm` | `Trajectory` |
| Safety-Steuerung | Sicherheitsfunktion über separaten Safety-Pfad | kein DDS-Topic in dieser Architektur | kein DDS-Topic in dieser Architektur |
| Edge-Gateway | Filter, Puffer, Analytik | externe `CellSummary`-Übergabe (Protokoll offen) | `JointState`, `DeviceTelemetry`, `Alarm` |
| MES/Cloud | Aufträge, Auswertung | außerhalb der Zell-DDS-Domain; Anbindung über Edge | außerhalb der Zell-DDS-Domain; Protokoll offen |

**Domains und Partitionen:**

- `cell.assembly` — betrachtete logische Kommunikationsdomäne; keine Safety-Zertifizierungsgrenze
- Weitere Domains/Partitions für Linie oder Edge werden nur bei begründetem Isolationsbedarf festgelegt.

Partitionen trennen Stationen (Roboter, Vision, Transport) innerhalb einer Domain, ohne zusätzliche Netze.

**Topics und QoS-Klassen:**

| Topic | Key | QoS-Klasse | Kernbegründung |
|---|---|---|---|
| `JointState` | `axis_id` | BestEffort, KeepLast(1); Deadline als zu prüfendes Ziel | Zyklische Zustandsdaten; Aktualität kann wichtiger sein als Nachlieferung |
| `Trajectory` | `robot_id` | Reliable, begrenzte History; Deadline als zu prüfendes Ziel | Vollständigkeits- und Gültigkeitsanforderungen fachlich spezifizieren |
| `VisionResult` | `part_id` | Reliable, begrenzte History; Frist pro Prozess festzulegen | Ergebnis muss zum Werkstück/Zyklus passen |
| `Alarm` | `alarm_id` | Reliable; Durability/History anhand des Alarm-Lebenszyklus festlegen | Aufbewahrung und späte Leser fachlich entscheiden |
| `DeviceTelemetry` | `device_id` | BestEffort, KeepLast(1) als Startannahme | Monitoring kann Verluste je nach Nutzung tolerieren |

> Die Policy-Auswahl und etwaige Zahlenwerte sind **Entwurfshypothesen**, keine Messwerte oder Garantien. Zahlenwerte benötigen eine fachliche Frist-/Zyklusanforderung und Validierung. Safety-Traffic ist ausdrücklich ausgeschlossen.

---

## 4. Qualitätsmerkmale und ihre Grenzen

Der Seminar-Brief verlangt eine Bewertung an allgemeinen Qualitätsmerkmalen. Diese Tabelle ist die Struktur dafür — und benennt jeweils die Grenze.

| Qualitätsmerkmal | DDS-Mechanismus | Grenze |
|---|---|---|
| Zuverlässigkeit | Reliability, History, Durability | Reliable garantiert Zustellung, nicht Rechtzeitigkeit |
| Performance | Multicast, Shared Memory, Zero-Copy, TransportPriority | Latenz hängt an OS, Netz und QoS-Konfiguration |
| Flexibilität | Topics, Partitions, dynamische Discovery | Topic-Explosion und unklare Datenhoheit |
| Robustheit | Liveliness, Deadline, Ownership | Kein Schutz gegen fehlerhafte Anwendungslogik |
| Verfügbarkeit | Redundanz, Durability, mehrere Writer | Discovery und Konfiguration werden komplex |
| Systemsicherheit | DDS Security (Auth, Access Control, Crypto, Logging) | Keine Safety-Zertifizierung, PKI-Aufwand |
| Daten- und Systemsicherheit | Domain-/Partition-Isolation, Encryption | Schlüsselverwaltung, Audit, Kompatibilität |
| Anpassbarkeit | QoS-Profile, XML-Konfiguration | Profilvielfalt wird unübersichtlich |
| Testbarkeit | Reproduzierbare QoS, Logging | Verteilte Fehler sind schwer zu reproduzieren |
| Offenheit/Zukunftsfähigkeit | OMG-Standard, Interoperabilität und dokumentierte Profile | Vendor-Interoperabilität in der Praxis prüfen |

---

## 5. Abgrenzung

DDS ist nicht die einzige Antwort auf verteilte Automation. Der Vortrag vergleicht vier Ansätze entlang der Achsen Modell, Transport, Echtzeit und Ökosystem:

| Ansatz | Modell | Stärke | mögliche Grenze im Anwendungskontext |
|---|---|---|---|
| DDS | datenzentrisch, Pub/Sub, QoS | viele-zu-viele, Echtzeit, QoS-Vertrag | Komplexität, Konfiguration, Security-Setup |
| OPC UA Pub/Sub | informationsmodellzentriert | Semantik, Companion Specs, Industrieakzeptanz | Echtzeit/QoS weniger fein, Modell-Overhead |
| MQTT | Broker-basiert, Topics | einfach, Cloud-nah, breite Toolbasis | zentraler Broker, QoS nur grob, Latenz |
| SOME/IP | serviceorientiert, Automotive | serviceorientierter Kommunikationsansatz | Passung zum gewählten Automatisierungsbeispiel ist zu begründen |

**AMR-Kandidat:** Die AMR-Flotte ist die Alternative zur Assembly-Zelle. Discovery und QoS bei wechselnder Teilnehmerzahl sowie Funknetzbedingungen sind mögliche Analyseaspekte, aber für das Beispiel noch anhand belastbarer Quellen zu prüfen.

**UMAA-Transfer:** Eine öffentliche UMAA-Beschreibung benennt OMG DDS als Kernbestandteil der Kommunikation zwischen Autonomie-Komponenten an Bord unbemannter maritimer Fahrzeuge [UMAA]. Das dient als kurzer Transferbeleg für DDS außerhalb der Fertigungsautomation, nicht als Gegenbeispiel und nicht als dritte vollständige Fallarchitektur. Krankenhaus und autonomes Straßenfahren gehören nicht zum Vortragsscope.

---

## 6. Aufbau der schriftlichen Unterlagen

Zielumfang: 15–20 Seiten plus Anhang; ohne weitere Zusatzliteratur verständlich; PDF mit hellem Hintergrund.

| Abschnitt | Inhalt | Seiten |
|---|---|---|
| 1 | Einleitung: DDS-Fragestellung und Vergleich der Anwendungskandidaten | 1–2 |
| 2 | DDS-Grundlagen: DCPS, Global Data Space, Discovery, RTPS | 3 |
| 3 | Architektur: gewählter Kandidat mit Komponenten, DDS-Entities, Topics und Datenflüssen; UMAA-Transfer kurz | 3 |
| 4 | QoS und Echtzeit: Achsen, RxO, Deadline, Latenzbudget, TSN | 3 |
| 5 | Security: Bedrohungsmodell, DDS Security, Zero-Trust, Grenzen | 2–3 |
| 6 | Deployment: Embedded, Edge, MES, Ressourcen, Redundanz | 2 |
| 7 | Qualitätsmerkmale und vergleichende Bewertung der Kandidaten | 2 |
| 8 | Abgrenzung: OPC UA Pub/Sub, MQTT, SOME/IP | 2 |
| 9 | Fazit, eigene Hypothesen, Ausblick | 1–2 |
| Anhang | Glossar, IDL, QoS-XML, Quellenverzeichnis | 3–5 |

Jede Kernaussage bekommt eine Quelle oder eine sichtbare Kennzeichnung als eigene Hypothese.

---

## 7. Vortrag und Diskussion

Die Rollenaufteilung folgt der Orga-Präsentation. Das konkrete Diskussionsformat ist **noch nicht beschlossen**: Das Deck schlägt alle vier Vorträge nacheinander mit gemeinsamer Diskussion im Anschluss vor; die bisherige Agenda enthält als Alternative Diskussionen direkt nach jedem Teil.

| Rolle | Schwerpunkt | Inhalt | Zeit |
|---|---|---|---|
| A | Architektur, roter Faden, Integration/Abgabe | DDS-Referenzarchitektur und struktureller Vergleich der Kandidaten | 12 min; Diskussion gemäß noch festzulegendem Format |
| B | Automatisierung | Zeitverhalten, Eventmanagement, Scheduling/Synchronisation, Embedded-HW und Heterogenität | 12 min; Diskussion gemäß noch festzulegendem Format |
| C | Qualitätsmerkmale | Zuverlässigkeit, Leistung, Flexibilität, Robustheit, Verfügbarkeit, Sicherheit, Anpassbarkeit, Testbarkeit | 12 min; Diskussion gemäß noch festzulegendem Format |
| D | Zukunft und DDS-spezifische Aspekte | Offenheit, TSN, Embedded/IoT, DDS-Datensicherheit, Anwendungsbezug und Ausblick | 12 min; Diskussion gemäß noch festzulegendem Format |

Details, Alternativformat und Diskussionsregeln: [`Agenda_80min.md`](Agenda_80min.md).

---

## 8. Demo

- **Technologie:** direkte DDS-API ohne ROS 2; FOSS ist Anforderung. Fast DDS Community (Apache-2.0) und Eclipse Cyclone DDS (EPL-2.0/EDL-1.0) sind Kandidaten; Auswahl und Zielplattform-Validierung offen.
- **Typen (IDL):** `JointState` (`@key axis_id`), `Trajectory`, `VisionResult`, `Alarm`.
- **Aufbau:** vorläufig ein Publisher (z. B. Robotersteuerung/Motion), zwei Subscriber (Visualisierung, Edge); endgültig an die Fallauswahl anpassen. Demo-Lead und technischer Umfang sind noch festzulegen.
- **QoS-Profile:** `control` (BestEffort, KeepLast(1), Deadline), `alarm` (Reliable, TransientLocal), `telemetry` (BestEffort).
- **Sichtbarer Effekt:** später startender Reader erhält den letzten Alarm; Deadline-Event bei ausbleibenden Daten; BestEffort verliert Samples.
- **Fallback:** aufgezeichnetes Video plus Code-Ausschnitte; die Demo ist nicht kritisch für die Note.
- **Nicht Teil der Demo:** vollständige PKI, TSN-Konfiguration, Echtzeit-Messung.

---

## 9. Quellenbasis

Geplante Quellenarten (konkrete Einträge folgen im Quellenregister):

- **OMG-Spezifikationen:** DDS 1.4, DDSI-RTPS (aktuelle Version prüfen; die Legacy-Version 2.1 von 2010 ist veraltet), DDS Security 1.1, IDL 4.2.
- **Normen:** IEEE 802.1Q (TSN: Qbv, Qav, Qcc), IEC 61131, IEC 61508/ISO 13849 für die Safety-Abgrenzung.
- **Lehrbuch-/Paper-Basis:** POSA 4 (Distributed Computing), Tanenbaum/van Steen, Publikationen zu DDS-QoS und TSN/DDS-Integration.
- **[UMAA] Use-case-Transfer:** AUVSI, **Unmanned Maritime Autonomy Architecture (UMAA)**: <https://www.auvsi.org/advocacy/advocacy-initiatives/unmanned-maritime-autonomy-architecture/>; NAVSEA, **UMAA Compliance Specification, T0300-BE-IDS-010 Rev. 1**: <https://www.auvsi.org/wp-content/uploads/2025/03/T0300-BE-IDS-010-Rev.-1.pdf>. Öffentliche Quellen; Aussageumfang auf das Dokumentierte begrenzen.
- **Vendor-Dokumentation:** Fast DDS, Cyclone DDS, RTI Connext — nur für Implementierungsdetails, nicht als Architekturbeleg.

Legacy-Material (`legacy_*`) wird **nicht** zitiert.

---

## 10. Risiken und Gegenmaßnahmen

| Risiko | Wirkung | Gegenmaßnahme |
|---|---|---|
| Thema zu breit (DDS + TSN + Security + Vergleich) | vier oberflächliche Teile | feste Seiten- und Minutenbudgets pro Teil; Vergleich auf eine Tabelle begrenzen |
| Keine Messwerte für Echtzeit | Behauptungen statt Belege | Werte als Annahmen kennzeichnen; Demo zeigt Verhalten, nicht Latenzgarantien |
| Use-case-Vergleich wird zu breit | Architekturteil verliert roten Faden | Assembly und AMR anhand gemeinsamer Kriterien vergleichen; nur einen Kandidaten vollständig ausarbeiten; UMAA als kurzen Transfer; keine Krankenhaus- oder Straßenfahrzeugarchitektur |
| Demo scheitert live | Vortragsabbruch | Video-Backup, Code-Ausschnitte, zweites Gerät |
| Security wird juristisch | Fokusverlust | Security auf Architektur und Bedrohungsmodell begrenzen |
| Terminkollision mit Praktikum | Zeitverlust | Praktikumstage 23.11., 07.12., 21.12. sind für das Seminar gesperrt |

---

## 11. Rollen und Meilensteine

| Rolle | Schwerpunkt | Kernartefakte |
|---|---|---|
| A | Architektur, roter Faden, Integration/Abgabe | DDS-Architektur, Kandidatenvergleich aus Architektursicht, integrierte Unterlagen |
| B | Automatisierung | Bewertung anhand der in Folie 7 genannten Automatisierungsanforderungen |
| C | Qualitätsmerkmale | Qualitätsbewertung beider Kandidaten einschließlich System-/Datensicherheit |
| D | Zukunft/DDS-spezifische Aspekte | Offenheit/Zukunft, TSN, Embedded/IoT, DDS-Security-Aspekte und Anwendungsbezug |

| Meilenstein | Datum |
|---|---|
| Exposé v1 | 20.11.2026 |
| Scope-Freeze | 27.11.2026 |
| Review #1 | 04.12.2026 |
| Architektur v1 | 11.12.2026 |
| Vollentwurf v1.0 | 18.12.2026 |
| Content-Freeze | 22.12.2026 |
| Abgabe | 08.01.2027, 10:00 |
| Vortrag | 11.01.2027 |

Vollständiger Plan: [`../Timeline.md`](../Timeline.md).

---

## 12. Offene Detailpunkte bis zum Scope-Freeze

1. **Auswahl des Hauptbeispiels** — Assembly-Zelle oder AMR-Flotte; anhand der Rollenbewertungen bis zum Scope-Freeze begründen.
2. **FOSS-DDS-Implementierung** — Fast DDS Community oder Eclipse Cyclone DDS anhand von Build-Aufwand, Dokumentationsqualität, Zielplattform, benötigten QoS-/Security-Funktionen und transitiven Lizenzen vergleichen; Fast DDS Pro nicht voraussetzen.
3. **TSN-Tiefe** — eigene Folie mit 802.1Qbv/Qav oder nur als Architekturbemerkung?
4. **Safety-Abgrenzung** — wie viel IEC 61508/ISO 13849 ist nötig, ohne das Thema zu sprengen?
5. **UMAA-Transfer** — konkrete Fundstellen der öffentlichen Architektur-/Compliance-Unterlagen im Quellenregister erfassen; keine dritte Fallarchitektur ausarbeiten.
6. **Umfang der Demo** — Beispiel und Zuständigkeit festlegen.
7. **Messwerte** — gibt es eine kleine Latenzmessung auf dem Desktop, die als Indiz (nicht als Garantie) taugt?
8. **Quellenversionen** — aktuelle OMG-Versionen und TSN-Normenstände prüfen und im Register festhalten.
