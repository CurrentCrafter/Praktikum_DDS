# Zwei Projektvarianten für das DDS-Seminar

**Stand:** 13.11.2026  
**Grundlage:** `sekm-seminar-2026.pdf`, `sekm-praktikum2026.pdf`, `DDS_alt/`, `01_plan/Timeline.md`

> **Entscheidung vom 13.11.2026:** Umgesetzt wird **Variante B mit Variante A als kurzem Kontrast**. Dieses Dokument bleibt als Begründung und Vergleichsgrundlage erhalten; die Umsetzung steht in [`Expose_v0.1.md`](Expose_v0.1.md) und [`Agenda_80min.md`](Agenda_80min.md).

> **Begriffsklärung:** „Projekt“ meint hier das **Seminarprojekt DDS** (Vortrag + Unterlagen + Demo). Das **Praktikum MPK** ist eine separate Abgabe; die DDS-Varianten liefern dafür höchstens Architekturvokabular und Demo-Erfahrung, keine gemeinsame Abgabe.

---

## 0. Bewertungsmaßstab

### 0.1 Anforderungen des Profs an das Seminar

- Team aus **2–4 Personen**; DDS ist mit **4 Personen** besetzt.
- Jede Person: **12 min** Vortrag (10–14 min) + ca. **8 min** Diskussion; harte Obergrenze **80 min**.
- Unterlagen: **PDF, heller Hintergrund**, ohne weitere Zusatzliteratur nachvollziehbar, **mind. ein Arbeitstag vorher** via Ilias.
- Inhalt: wissenschaftlich, eigenständig, eigene Hypothesen, Beispiele, klare Struktur.
- DDS-Thema: Architektur (Komponentenmodell, Common Services, Message-Passing, Multi-Plattform, Security), Automatisierungsbezug, Qualitätsmerkmale, Offenheit/Zukunftsfähigkeit.
- Vom Prof. vorgeschlagene Diskussionspunkte: **Echtzeit, TSN, Embedded/IoT, Datensicherheit**.
- Vom Prof. vorgeschlagene Beispielbereiche: **Software-Defined Vehicle, autonome mobile Roboter, Motion Control, Smart Factory, Hausautomation**.
- Benotung: Teamnote für Unterlagen + Individualnote für Vortrag/Diskussion (je 50 %); Modulnote 50 % Seminar + 50 % mündliche Prüfung.

### 0.2 Anforderungen des Praktikums (separat, nur als Brücke)

- C++-MPK (Message Passing Komponente) mit DIRs S1–S7b, I1–I3, C1–C3, R1–R6, M1–M2c.
- Embedded/RTOS-Kontext, nur übliche C/C++-Laufzeit und RTOS-Funktionen.
- UML in Visual Paradigm, SCRUM, Peer-Reviews, Pattern-Nachweis, KI-Nutzung dokumentieren.
- Abschlussvortrag 20–30 min.

### 0.3 Zentrale Bewertungsfragen für die Varianten

1. Erfüllt die Variante den **Automatisierungsbezug** des Seminars?
2. Trägt sie **alle vier Personen** über 80 Minuten?
3. Erlaubt sie **echte eigene Hypothesen** statt Referat?
4. Ist sie **wissenschaftlich belegbar** (OMG, Papers, Normen)?
5. Bleibt sie im Zeitbudget **realistisch**?
6. Ist sie **eigenständig** gegenüber dem Legacy-Material?

---

## 1. Übersicht

| | **Variante A — Legacy-nah** | **Variante B — Losgelöst** |
|---|---|---|
| **Titel** | DDS im automatisierten Krankenhaus | DDS für eine modulare Roboter-Assembly-Zelle |
| **Beispiel** | Patientendaten, Alarme, Geräteintegration | Motion, Vision, Edge, MES |
| **Nähe zu `DDS_alt`** | sehr hoch (gleiches Krankenhausbeispiel) | niedrig (neues Beispiel) |
| **Automatisierungsbezug** | mittel (Gebäude-/Medizingeräteautomation) | hoch (Smart Factory/Motion Control) |
| **Legacy-Reuse** | Struktur, Folienlogik, Demo-Idee, Q&A | nur Grundlagen und Methodik |
| **Rechercheaufwand** | niedrig bis mittel | mittel bis hoch |
| **Differenzierungsrisiko** | „wir haben die alte Präsentation nachgebaut“ | „zu breit“ |
| **Empfehlung** | schnelle, sichere Variante | **stärkere Variante für die Bewertung** |

---

# Variante A — DDS im automatisierten Krankenhaus

## A.1 Pitch

Ein Krankenhaus betreibt viele medizinische Geräte, Monitore, Alarmsysteme und mobile Endgeräte, die miteinander Daten austauschen müssen. DDS wird als **datenzentrische Kommunikationsschicht** eingesetzt: Vitaldaten, Alarme, Gerätestatus und Steuerbefehle werden über einen Global Data Space verteilt, ohne zentralen Broker. Die Architektur zeigt, wie **Echtzeit, Ausfallsicherheit, Datenschutz und Heterogenität** in einem klinischen System zusammenspielen.

**Warum legacy-nah:** Das alte DDS-Seminar nutzte genau dieses Krankenhausbeispiel (Vitaldaten, Alarm-Level, Geräte). Struktur und Beispiele lassen sich schnell reaktivieren — aber Inhalt, Quellen, Folien und Bewertung müssen neu erstellt werden.

## A.2 Szenario und Architektur

**Teilnehmer:**

- Patientendisplay / Bettmonitor
- Vitaldatenmonitor (Herzfrequenz, Blutdruck, Temperatur)
- Infusionspumpe
- Alarm-Server / Leitstelle
- Mobiles Arzt-Endgerät
- Zentrales Klinik-Gateway

**Domains und Partitionen:**

- `clinic.core` — übergreifende Dienste (Alarme, Gerätestatus)
- `ward.icu` — Intensivstation
- `ward.normal` — Normalstation
- `building.technical` — technische Gebäudeautomation (optional)

Partitionen trennen Stationen logisch, ohne physische Netze zu duplizieren.

**Topics und QoS-Klassen:**

| Topic | Key | QoS-Ziel | Begründung |
|---|---|---|---|
| `VitalSigns` | `patient_id` | Reliable, KeepLast(1–5), Deadline 100 ms | Messwerte müssen ankommen, kurze Historie für späte Reader |
| `Alarm` | `alarm_id` | Reliable, TransientLocal, Deadline 50 ms, Liveliness | Alarme dürfen nicht verloren gehen; späte Teilnehmer sehen den letzten Alarm |
| `DeviceStatus` | `device_id` | BestEffort, KeepLast(1) | Status ist schnell ersetzbar; kein teurer Retransmit |
| `ControlCommand` | `device_id` | Reliable, Lifespan, Ownership | Befehle brauchen Eindeutigkeit und Verfallszeit |

**Security:**

- DDS Security: Authentication, Access Control, Encryption, Logging.
- Domains/Partitions als erste Isolationsschicht, DDS Security als zweite.
- Threat-Szenario: fremder Participant gibt sich als Monitor aus; repliziert `VitalSigns`; Access Control und Zertifikate verhindern das.
- Datenschutz: Patientendaten nur in der klinischen Domain; keine Telemetrie in die Gebäudedomain.

**Deployment:**

- Betten/Stationen: embedded Linux oder RTOS-nahe Geräte.
- Edge-Gateway pro Station: bündelt Daten, filtert, puffert.
- Zentrale: Alarm-Server, Archiv, evtl. MES-/HIS-Anbindung.
- Heterogene OS und Netzwerke; DDS/RTPS über UDP, bei Bedarf Shared Memory.

## A.3 80-Minuten-Struktur

| Zeit | Teil | Inhalt |
|---|---|---|
| 0–12 | A | Problem im Krankenhaus, Anforderungen, DDS-Referenzarchitektur, Mapping auf die Klinik |
| 12–20 | A | Diskussion: Architektur, Domains, Modellgrenzen |
| 20–32 | B | QoS für Vitaldaten und Alarme, Deadline/Liveliness, Echtzeitpfad |
| 32–40 | B | Diskussion: QoS-Wahl, Echtzeitgrenzen |
| 40–52 | C | DDS Security, Datenschutz, Deployment, Qualitätsmerkmale |
| 52–60 | C | Diskussion: Security, Datenschutz, Geräte |
| 60–72 | D | Abgrenzung zu HL7/FHIR, MQTT, OPC UA; Demo; Bewertung; Fazit |
| 72–80 | D | Diskussion: Vergleich, Demo-Grenzen, Ausblick |

## A.4 Unterlagenstruktur

1. Einleitung: Klinik als verteiltes Echtzeitsystem
2. DDS-Grundlagen: DCPS, Global Data Space, Discovery, RTPS
3. Architektur: Domains, Partitionen, Topics, QoS-Tabelle
4. Echtzeit und Zuverlässigkeit: Vitaldaten vs. Alarme
5. Security und Datenschutz: DDS Security, Threat-Szenario
6. Deployment und Qualitätsmerkmale
7. Abgrenzung: HL7/FHIR (Interoperabilität), MQTT (Broker), OPC UA (Industrie)
8. Bewertung: Stärken, Grenzen, eigene Hypothesen
9. Fazit und Ausblick
10. Literatur und Glossar

## A.5 Demo

- IDL: `VitalSigns` mit `@key patient_id`, `heart_rate`, `blood_pressure`, `alarm_level`.
- Ein Publisher simuliert den Monitor, ein Subscriber den Alarm-Server.
- Zwei Reader mit unterschiedlicher QoS: Reliable/TransientLocal vs. BestEffort.
- Sichtbarer Effekt: später startender Reader bekommt den letzten Alarm; BestEffort verliert Samples.
- Security nur als Architektur/Konfigurationskonzept, nicht als vollständige PKI-Demo.

## A.6 Anforderungsabgleich

| Anforderung | Erfüllung | Risiko |
|---|---|---|
| Automatisierungsbezug | mittel: Medizingeräte-/Gebäudeautomation | Krankenhaus ist nicht in der Prof.-Liste, nur „o. ä.“ |
| 4 Personen / 80 min | gut: vier klar getrennte Teile | Übergänge können additiv wirken |
| Eigene Hypothesen | gut: Alarme vs. Vitaldaten, Security vs. Latenz | muss über Legacy hinausgehen |
| Wissenschaftlichkeit | gut: OMG, HL7/FHIR, Papers | HL7/FHIR nicht mit DDS verwechseln |
| Eigenständigkeit | schwach bis mittel | gleiches Beispiel wie Altteam |
| Zeitbudget | gut | Legacy-Reuse verkürzt Recherche |

## A.7 Stärken / Schwächen

**Stärken:**

- Schnellster Einstieg; Legacy-Struktur und Beispiele vorhanden.
- Klare, anschauliche QoS-Unterschiede (Vitaldaten vs. Alarme).
- Guter Security-/Datenschutz-Diskurs.
- Demo mit wenigen Topics schnell lauffähig.

**Schwächen:**

- „Wir haben die alte Präsentation neu gebaut“ ist ein reales Bewertungsrisiko.
- Krankenhaus ist nur indirekt Automatisierungstechnik.
- HL7/FHIR-Abgrenzung kann den DDS-Fokus verwässern.
- Security/Datenschutz verleitet zu juristischen Exkursen.

## A.8 Brücke zum Praktikum MPK

- DDS-Topics entsprechen konzeptionell den MPK-Kanälen; QoS-Klassen entsprechen Kanal-Konfigurationen.
- Alarm-/Vitaldaten-Priorisierung erinnert an MPK-DIRs zu Pufferung, Logging und Ausnahmen.
- **Keine Vermischung:** Im Seminar wird DDS beschrieben, nicht die MPK implementiert.

---

# Variante B — DDS für eine modulare Roboter-Assembly-Zelle

## B.1 Pitch

Eine modulare Roboter-Assembly-Zelle besteht aus Robotersteuerung, Vision, Motion/PLC, Edge-Gateway und MES. Die Komponenten müssen Zustände, Trajektorien, Bildergebnisse, Alarme und Telemetrie in Echtzeit austauschen — heterogen, viele-zu-viele, ohne zentralen Broker. DDS liefert den Global Data Space; QoS und TSN entscheiden, ob daraus eine belastbare Architektur wird.

**Warum losgelöst:** Neues Beispiel, direkter Automatisierungsbezug, alle vom Prof. vorgeschlagenen Aspekte (Real-Time, TSN, Embedded, Security, Smart Factory/Motion Control) lassen sich daran zeigen. Legacy-Material liefert nur Grundlagen und Methodik.

## B.2 Szenario und Architektur

**Teilnehmer:**

- Robotersteuerung (RC)
- Vision-System
- Motion-/PLC-Controller
- Edge-Gateway / Zellenrechner
- MES/Cloud-Anbindung
- Sicherheitssteuerung (Safety)

**Domains und Partitionen:**

- `cell.assembly` — harte Echtzeit der Zelle
- `line.assembly` — Koordination mehrerer Zellen
- `edge.telemetry` — Monitoring, Analytik, MES
- Partitionen pro Station (Roboter, Vision, Transport)

**Topics und QoS-Klassen:**

| Topic | Key | QoS-Ziel | Begründung |
|---|---|---|---|
| `JointState` | `axis_id` | BestEffort, KeepLast(1), Deadline 1–5 ms, TransportPriority | Zyklische Regelungsdaten; altes Sample ist wertlos |
| `Trajectory` | `robot_id` | Reliable, KeepLast(1), Deadline 10 ms | Trajektorie muss vollständig ankommen |
| `VisionResult` | `part_id` | Reliable, KeepLast(1), Deadline 50–100 ms | Ergebnis muss zum Werkstück passen |
| `SafetyStatus` | `cell_id` | Reliable, TransientLocal, Deadline 10 ms, Liveliness | Sicherheitsstatus darf nicht verloren gehen |
| `Alarm` | `alarm_id` | Reliable, TransientLocal, Deadline 50 ms | Späte Teilnehmer müssen den letzten Alarm sehen |
| `Telemetry` | `device_id` | BestEffort, KeepLast(1), hoher Durchsatz | Monitoring verträgt Verluste |

**Security:**

- DDS Security für Zellen- und Line-Domain; Access Control für Engineering-Zugriff.
- Threat-Szenario: manipulierter Participant sendet falsche `Trajectory` oder `SafetyStatus`.
- Zero-Trust am Edge: starke Authentifizierung, minimale Rechte, verschlüsselte Domains.
- Safety getrennt denken: DDS Security ersetzt keine Safety-Zertifizierung.

**Deployment:**

- Roboter-/Motion-Controller: RTOS oder embedded Linux, begrenzte Ressourcen.
- Edge-Gateway: bündelt Telemetrie, führt Filter/Analytik aus.
- MES/Cloud: keine harten Echtzeitanforderungen, aber hoher Durchsatz.
- TSN für deterministische Netzsegmente; DDS über UDP/Multicast, Shared Memory auf gleichem Host.

## B.3 80-Minuten-Struktur

| Zeit | Teil | Inhalt |
|---|---|---|
| 0–12 | A | Problem der Zelle, Anforderungen, DDS-Referenzarchitektur, Mapping auf die Zelle |
| 12–20 | A | Diskussion: Architektur, Domains, Modellgrenzen |
| 20–32 | B | QoS, Deadline/LatencyBudget, RTPS-Transport, TSN-Zusammenspiel |
| 32–40 | B | Diskussion: QoS-Achsen, RxO, Echtzeitgrenzen |
| 40–52 | C | DDS Security, Deployment, Zuverlässigkeit/Verfügbarkeit/Testbarkeit |
| 52–60 | C | Diskussion: Bedrohungsmodell, PKI, Embedded-Ressourcen |
| 60–72 | D | Abgrenzung zu OPC UA/MQTT/SOME-IP, Demo, Bewertung, Fazit |
| 72–80 | D | Diskussion: Vergleich, Demo-Grenzen, Ausblick |

## B.4 Unterlagenstruktur

1. Einleitung: modulare Zelle als verteiltes Echtzeitsystem
2. DDS-Grundlagen: DCPS, Global Data Space, Discovery, RTPS
3. Architektur: Domains, Partitionen, Topics, QoS-Tabelle
4. Echtzeit: Deadline, LatencyBudget, Liveliness, TSN
5. Security: DDS Security, Threat-Szenario, Zero-Trust
6. Deployment: Embedded/Edge/MES, Ressourcen, Redundanz
7. Qualitätsmerkmale: Reliability, Performance, Flexibility, Robustness, Availability, Security, Testability
8. Abgrenzung: OPC UA (Pub/Sub), MQTT, SOME/IP
9. Bewertung und eigene Hypothesen
10. Fazit und Ausblick (ROS 2, AUTOSAR Adaptive, DDS+TSN)

## B.5 Demo

- IDL: `JointState` (`@key axis_id`, `position`, `velocity`), `Trajectory`, `VisionResult`, `Alarm`.
- Publisher simuliert Robotersteuerung; Subscriber simuliert Motion/Visualisierung.
- QoS-XML mit drei Profilen: `control`, `telemetry`, `alarm`.
- Sichtbarer Effekt: `control` mit KeepLast(1) vs. `alarm` mit TransientLocal; Deadline-Event bei ausbleibenden Daten.
- Optional: zweiter Reader zeigt Multicast/Discovery; TSN nur als Architektur, nicht als Laboraufbau.

## B.6 Anforderungsabgleich

| Anforderung | Erfüllung | Risiko |
|---|---|---|
| Automatisierungsbezug | hoch: Smart Factory/Motion Control | Thema ist breit |
| 4 Personen / 80 min | gut, aber Disziplin nötig | zu viele Themen (TSN, Security, Vergleich) |
| Eigene Hypothesen | sehr gut: QoS/TSN/Security-Trade-offs | muss messbar/argumentativ belegt werden |
| Wissenschaftlichkeit | gut: OMG, TSN-Normen, Papers | TSN und DDS nicht vermischen |
| Eigenständigkeit | hoch | kein Legacy-Reuse für Inhalte |
| Zeitbudget | mittel | mehr Recherche und Demo-Aufwand |

## B.7 Stärken / Schwächen

**Stärken:**

- Beste Erfüllung der Prof.-Vorschläge (Smart Factory, Motion Control, TSN, Embedded, Security).
- Klare eigene Hypothesen und Trade-offs.
- Gute Abgrenzung zu OPC UA/MQTT/SOME-IP möglich.
- Demo zeigt QoS-Wirkung anschaulich.

**Schwächen:**

- Größerer Recherche- und Abstimmungsaufwand.
- Gefahr, TSN, Security und Vergleich je nur oberflächlich zu behandeln.
- Demo braucht mehr Setup als Variante A.
- Ohne messbare Latenzwerte bleibt die Echtzeit-Diskussion konzeptionell.

## B.8 Brücke zum Praktikum MPK

- Direkte Analogien: Topics ↔ MPK-Kanäle; QoS ↔ Kanal-/Puffer-Konfiguration; Discovery ↔ ConnectUnit; Deadlines ↔ Ausnahmen/Timeouts.
- Die Zellen-Architektur liefert gute Beispiele für N:1 vs. Multicast, Priorisierung und Pufferung.
- **Keine Vermischung:** Die MPK-DIRs werden nicht im DDS-Seminar abgearbeitet.

---

## 2. Vergleich und Empfehlung

| Kriterium | Variante A | Variante B |
|---|---|---|
| Erfüllt Seminar-Brief | 3/5 | **5/5** |
| Automatisierungsbezug | 3/5 | **5/5** |
| Legacy-Reuse | **5/5** | 2/5 |
| Eigenständigkeit | 2/5 | **5/5** |
| Wissenschaftliche Tiefe | 3/5 | **4/5** |
| Demo-Aufwand | **niedrig** | mittel |
| Risiko „zu breit“ | niedrig | **mittel** |
| Risiko „Nachbau“ | **hoch** | niedrig |
| Zeit bis Exposé | **schnell** | mittel |

**Empfehlung:**

- **Variante B** ist die bessere Wahl für die Bewertung: Sie erfüllt die Prof.-Vorgaben (Smart Factory/Motion Control, Echtzeit, TSN, Embedded, Security) und erlaubt echte eigene Hypothesen. Sie ist auch die konsequente Fortsetzung der bisherigen Planung (`Timeline.md`).
- **Variante A** ist die schnellere und sicherere Variante, wenn das Team wenig Zeit hat oder bewusst an das Legacy-Material anknüpfen will. Dann muss die Eigenständigkeit aktiv abgesichert werden: neues Beispiel, neue Quellen, neue Diagramme, klare Abgrenzung.
- **Hybrid möglich:** Variante B als Hauptgeschichte, Variante A nur als kurzer Kontrast „DDS im Krankenhaus“ in der Einleitung oder Diskussion. Das kostet wenig und zeigt Transfer.

---

## 3. Architekturdateien

Die ersten Mermaid-Strukturen liegen getrennt pro Variante:

| Variante | Datei | Inhalt |
|---|---|---|
| A — Krankenhaus | [`../03_architektur/Variante_A_Krankenhaus_Architektur_v0.1.md`](../03_architektur/Variante_A_Krankenhaus_Architektur_v0.1.md) | Kontext, DDS-Modell, QoS, Deployment, Sequenz, Security |
| B — Assembly-Zelle | [`../03_architektur/Variante_B_Assembly_Zelle_Architektur_v0.1.md`](../03_architektur/Variante_B_Assembly_Zelle_Architektur_v0.1.md) | Kontext, DDS-Modell, QoS, Deployment, Sequenz, Security |

Beide Dateien sind Entwürfe (v0.1) und noch nicht render-geprüft. Die QoS-Werte sind Diskussionsgrundlage, keine Messwerte.

---

## 4. Nächste Entscheidung

**Entschieden am 13.11.2026:** Variante **B mit A als kurzem Kontrast**.

Erledigt:

1. Variante gewählt: **B mit A als Kontrast**.
2. Beispielzelle und QoS-Tabelle aus B.2 in das Exposé übernommen.
3. Architektur v0.1 für beide Varianten angelegt (Vergleichsgrundlage bleibt erhalten).

Offen:

4. Rollen A–D personell besetzen; 80-min-Agenda bestätigen (Format: Diskussion nach jedem Teil oder ein 32-min-Block).
5. Quellenregister anlegen und Legacy-PDFs durch aktuelle OMG-Versionen ersetzen.
6. Demo-Technologie entscheiden: Fast DDS oder Cyclone DDS.

**Begründung der Entscheidung:** maximale Passung zu den Prof.-Vorgaben (Smart Factory, Motion Control, Echtzeit, TSN, Embedded, Security), hohe Eigenständigkeit gegenüber dem Legacy-Material, und Variante A bleibt als bekannter Anker für das Publikum verfügbar.
