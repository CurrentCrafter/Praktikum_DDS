# Exposé v0.1 — DDS für eine modulare Roboter-Assembly-Zelle

**Stand:** 13.11.2026
**Status:** Entwurf, Grundlage für Kickoff und Scope-Freeze
**Gewählte Variante:** B (Assembly-Zelle), Variante A (Krankenhaus) nur als kurzer Kontrast
**Vortrag:** Montag, 11.01.2027 · **Abgabe:** Freitag, 08.01.2027, 10:00 via Ilias
**Team:** 4 Personen · 80 Minuten (4 × 12 min Vortrag + 4 × 8 min Diskussion)

> Dieses Exposé ist die Arbeitsgrundlage. Es enthält bewusst offene Punkte (Abschnitt 12), die bis zum Scope-Freeze am 27.11.2026 entschieden werden müssen.

---

## 1. Ausgangslage und Problem

Eine modulare Roboter-Assembly-Zelle besteht aus Komponenten unterschiedlicher Hersteller: Robotersteuerung, Vision-System, Motion-/PLC-Controller, Safety-Steuerung, Edge-Gateway und MES-Anbindung. Diese Komponenten müssen zyklisch Zustände, Trajektorien, Bildergebnisse, Alarme und Telemetrie austauschen.

Dabei treten vier Probleme gleichzeitig auf:

1. **Heterogenität** — unterschiedliche Betriebssysteme, Rechenleistung und Programmiersprachen.
2. **Echtzeit** — Regel- und Sicherheitsdaten haben Fristen im Millisekundenbereich.
3. **Kopplung** — klassische Client/Server- oder Broker-Architekturen erzeugen einen zentralen Ausfallpunkt und einen zusätzlichen Hop.
4. **Wandlungsfähigkeit** — Zellen werden umgebaut, Komponenten ersetzt, Werkstücke gewechselt.

DDS (Data Distribution Service, OMG) adressiert diese Probleme mit einem **datenzentrischen** Modell: Teilnehmer publizieren und abonnieren typisierte Topics in einem Global Data Space, ohne sich gegenseitig zu kennen. **QoS** legt fest, welche Eigenschaften der Datenstrom haben muss. **RTPS** definiert das Wire-Protokoll, **DDS Security** ergänzt Authentifizierung, Zugriffskontrolle und Verschlüsselung.

**Die Leitfrage des Seminars lautet:** Welche Architektur- und QoS-Entscheidungen machen DDS in einer automatisierten Assembly-Zelle tragfähig — und wo endet die Tragfähigkeit?

---

## 2. Drei Thesen

Die Thesen sind bewusst als **prüfbare Behauptungen** formuliert, nicht als Zusammenfassung der Spezifikation.

### H1 — DDS ist eine datenzentrische Architektur, keine schnelle Message Queue

DDS entkoppelt Teilnehmer in **Raum** (keine Adresskenntnis), **Zeit** (Durability, History) und **Datenfluss** (Topic statt Aufruf). Der Nutzen entsteht nicht durch „schneller als MQTT", sondern durch das Datenmodell: Topics, Keys und Instanzen beschreiben Zustände, nicht Nachrichten.

*Prüfzugang:* Architekturvergleich DDS vs. Broker-Modell; Mapping der Zellen-Komponenten auf Topics; Gegenprobe, wo DDS unnötig komplex ist.

### H2 — QoS ist die eigentliche Architektur; Default-QoS ist ein Entwurfsfehler

Die fachlichen Anforderungen der Zelle (Fristen, Verlusttoleranz, Aktualität, Sicherheitsrelevanz) werden **nicht** im Code, sondern in QoS-Profilen entschieden. Ein `JointState` mit Reliable/KeepAll ist genauso falsch wie ein `SafetyStatus` mit BestEffort.

*Prüfzugang:* QoS-Tabelle pro Topic; RxO-Matching; Demo mit zwei Profilen; Begründung jeder QoS-Achse.

### H3 — DDS passt für viele-zu-viele-Echtzeitdatenströme, nicht für jeden Fall

DDS ist stark bei zyklischen, multicastfähigen Datenströmen mit vielen Teilnehmern. Bei Request/Response, transaktionalen Zugriffen oder tiefen Cloud-Integrationen ist es oft die falsche Wahl. Security und TSN müssen **end-to-end** gedacht werden, nicht als DDS-Feature.

*Prüfzugang:* Abgrenzung zu OPC UA Pub/Sub, MQTT und SOME/IP; Benennung der Grenzen; Diskussion der Nicht-Anwendungsfälle.

---

## 3. Beispielsystem

**Zelle:** modulare Assembly-Zelle mit Roboter, Vision, Motion/PLC, Safety, Edge und MES.

**Teilnehmer und Rollen:**

| Teilnehmer | Rolle | Publiziert | Abonniert |
|---|---|---|---|
| Robotersteuerung (RC) | Bahnplanung, Zellsteuerung | `Trajectory`, `Alarm` | `JointState`, `VisionResult` |
| Vision-System | Lage-/Qualitätsprüfung | `VisionResult` | — |
| Motion/PLC | Achsregelung, Zyklus | `JointState`, `SafetyStatus`, `Telemetry` | `Trajectory` |
| Safety-Steuerung | sicherheitsgerichteter Status | `SafetyStatus` | — |
| Edge-Gateway | Filter, Puffer, Analytik | `Telemetry` | `JointState`, `SafetyStatus`, `Alarm`, `Telemetry` |
| MES/Cloud | Aufträge, Auswertung | — | `Telemetry` (über Edge) |

**Domains und Partitionen:**

- `cell.assembly` — harter Regel- und Sicherheitskontext der Zelle
- `line.assembly` — Koordination mehrerer Zellen
- `edge.telemetry` — Monitoring, Analytik, MES

Partitionen trennen Stationen (Roboter, Vision, Transport) innerhalb einer Domain, ohne zusätzliche Netze.

**Topics und QoS-Klassen:**

| Topic | Key | QoS-Klasse | Kernbegründung |
|---|---|---|---|
| `JointState` | `axis_id` | BestEffort, KeepLast(1), Deadline 1–5 ms | Zyklisch, altes Sample ist wertlos |
| `Trajectory` | `robot_id` | Reliable, KeepLast(1), Deadline 10 ms | Muss vollständig ankommen |
| `VisionResult` | `part_id` | Reliable, KeepLast(1), Deadline 50–100 ms | Ergebnis muss zum Werkstück passen |
| `SafetyStatus` | `cell_id` | Reliable, TransientLocal, Deadline 10 ms, Liveliness | Darf nicht verloren gehen |
| `Alarm` | `alarm_id` | Reliable, TransientLocal, Deadline 50 ms | Späte Teilnehmer sehen den letzten Alarm |
| `Telemetry` | `device_id` | BestEffort, KeepLast(1) | Monitoring verträgt Verluste |

> Die Werte sind **Zielwerte für die Diskussion**, keine Messwerte. Ob sie in der Zelle realistisch sind, wird im Vortrag ausdrücklich als Annahme gekennzeichnet.

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
| Offenheit/Zukunftsfähigkeit | OMG-Standard, Interoperabilität, ROS 2, AUTOSAR AP | Vendor-Interoperabilität in der Praxis prüfen |

---

## 5. Abgrenzung

DDS ist nicht die einzige Antwort auf verteilte Automation. Der Vortrag vergleicht vier Ansätze entlang der Achsen Modell, Transport, Echtzeit und Ökosystem:

| Ansatz | Modell | Stärke | Schwäche im Zellenkontext |
|---|---|---|---|
| DDS | datenzentrisch, Pub/Sub, QoS | viele-zu-viele, Echtzeit, QoS-Vertrag | Komplexität, Konfiguration, Security-Setup |
| OPC UA Pub/Sub | informationsmodellzentriert | Semantik, Companion Specs, Industrieakzeptanz | Echtzeit/QoS weniger fein, Modell-Overhead |
| MQTT | Broker-basiert, Topics | einfach, Cloud-nah, breite Toolbasis | zentraler Broker, QoS nur grob, Latenz |
| SOME/IP | serviceorientiert, Automotive | harte Echtzeit im Fahrzeug, AUTOSAR-Nähe | Automations-/IT-Integration, Ökosystem |

**Variante A (Krankenhaus)** dient nur als kurzer Kontrast in der Einleitung oder Diskussion: gleiche DDS-Mechanismen, andere Anforderungen (Datenschutz, Verfügbarkeit, Regulatorik). Sie ist **kein** zweiter Fall im Hauptteil.

---

## 6. Aufbau der schriftlichen Unterlagen

Zielumfang: 15–20 Seiten plus Anhang; ohne weitere Zusatzliteratur verständlich; PDF mit hellem Hintergrund.

| Abschnitt | Inhalt | Seiten |
|---|---|---|
| 1 | Einleitung: Zelle als verteiltes Echtzeitsystem, Leitfrage | 1–2 |
| 2 | DDS-Grundlagen: DCPS, Global Data Space, Discovery, RTPS | 3 |
| 3 | Architektur der Zelle: Domains, Partitionen, Topics, Komponenten | 3 |
| 4 | QoS und Echtzeit: Achsen, RxO, Deadline, Latenzbudget, TSN | 3 |
| 5 | Security: Bedrohungsmodell, DDS Security, Zero-Trust, Grenzen | 2–3 |
| 6 | Deployment: Embedded, Edge, MES, Ressourcen, Redundanz | 2 |
| 7 | Qualitätsmerkmale und Bewertung | 2 |
| 8 | Abgrenzung: OPC UA Pub/Sub, MQTT, SOME/IP | 2 |
| 9 | Fazit, eigene Hypothesen, Ausblick | 1–2 |
| Anhang | Glossar, IDL, QoS-XML, Quellenverzeichnis | 3–5 |

Jede Kernaussage bekommt eine Quelle oder eine sichtbare Kennzeichnung als eigene Hypothese.

---

## 7. Vortrag und Diskussion

Der 80-Minuten-Block ist in vier Teile à 12 Minuten plus vier Diskussionen à 8 Minuten gegliedert (Empfehlung: Diskussion direkt im Anschluss an den jeweiligen Teil, weil die Individualnote auch die Antwortqualität bewertet).

| Teil | Person | Inhalt | Zeit |
|---|---|---|---|
| A | Architektur + roter Faden | Problem, Anforderungen, DDS-Kern, Mapping auf die Zelle (inkl. 2 min Eröffnung) | 0–12 + 12–20 |
| B | QoS/Real-Time | QoS-Achsen, Deadline, Latenzbudget, RTPS, TSN | 20–32 + 32–40 |
| C | Security/Deployment | Bedrohungsmodell, DDS Security, Deployment, Qualitätsmerkmale | 40–52 + 52–60 |
| D | Vergleich/Demo/Fazit | Abgrenzung, Demo, Bewertung, Fazit | 60–72 + 72–80 |

Details, Alternativformat und Diskussionsregeln: [`Agenda_80min.md`](Agenda_80min.md).

---

## 8. Demo

- **Technologie:** eProsima Fast DDS (Alternative: Cyclone DDS), da beide Open Source, C++ und RTOS-nah genug für ein Beispiel.
- **Typen (IDL):** `JointState` (`@key axis_id`), `Trajectory`, `VisionResult`, `Alarm`.
- **Aufbau:** ein Publisher (Robotersteuerung/Motion), zwei Subscriber (Visualisierung, Edge).
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
- **Ökosystem-Belege:** ROS 2 (DDS als Middleware), AUTOSAR Adaptive Platform (DDS-Binding) — jeweils gegen die Primärquelle prüfen, nicht gegen Blogposts.
- **Vendor-Dokumentation:** Fast DDS, Cyclone DDS, RTI Connext — nur für Implementierungsdetails, nicht als Architekturbeleg.

Legacy-Material (`legacy_*`) wird **nicht** zitiert.

---

## 10. Risiken und Gegenmaßnahmen

| Risiko | Wirkung | Gegenmaßnahme |
|---|---|---|
| Thema zu breit (DDS + TSN + Security + Vergleich) | vier oberflächliche Teile | feste Seiten- und Minutenbudgets pro Teil; Vergleich auf eine Tabelle begrenzen |
| Keine Messwerte für Echtzeit | Behauptungen statt Belege | Werte als Annahmen kennzeichnen; Demo zeigt Verhalten, nicht Latenzgarantien |
| Legacy-Nähe kippt in Nachbau | Eigenständigkeitsverlust | neues Beispiel, neue Quellen, neue Diagramme; A nur als Kontrast |
| Demo scheitert live | Vortragsabbruch | Video-Backup, Code-Ausschnitte, zweites Gerät |
| Security wird juristisch | Fokusverlust | Security auf Architektur und Bedrohungsmodell begrenzen |
| Terminkollision mit Praktikum | Zeitverlust | Praktikumstage 23.11., 07.12., 21.12. sind für das Seminar gesperrt |

---

## 11. Rollen und Meilensteine

| Rolle | Schwerpunkt | Kernartefakte |
|---|---|---|
| A | Architektur, roter Faden, Integration, Moderation | Abschnitte 2–3, Gesamt-PDF, Abgabe |
| B | QoS, Real-Time, TSN | Abschnitt 4, QoS-Tabelle, Latenzbudget |
| C | Security, Deployment, Qualitätsmerkmale | Abschnitte 5–7, Bedrohungsmodell |
| D | Vergleich, Demo, Fazit | Abschnitte 8–9, Demo, Backup-Video |

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

## 12. Offene Punkte bis zum Scope-Freeze

1. **Fast DDS oder Cyclone DDS** — Entscheidung anhand von Build-Aufwand und Dokumentationsqualität.
2. **TSN-Tiefe** — eigene Folie mit 802.1Qbv/Qav oder nur als Architekturbemerkung?
3. **Safety-Abgrenzung** — wie viel IEC 61508/ISO 13849 ist nötig, ohne das Thema zu sprengen?
4. **Variante A als Kontrast** — eine Folie in der Einleitung oder ein Diskussionsimpuls?
5. **Umfang der Demo** — nur `JointState`/`Alarm` oder zusätzlich `VisionResult`?
6. **Messwerte** — gibt es eine kleine Latenzmessung auf dem Desktop, die als Indiz (nicht als Garantie) taugt?
7. **Quellenversionen** — aktuelle OMG-Versionen und TSN-Normenstände prüfen und im Register festhalten.
