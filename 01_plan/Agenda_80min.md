# 80-Minuten-Agenda — DDS für eine modulare Roboter-Assembly-Zelle

**Stand:** 13.11.2026
**Vortrag:** Montag, 11.01.2027
**Team:** 4 Personen
**Grundlage:** `sekm-seminar-2026.pdf` (12 min pro Person, 10–14 min erlaubt, ca. 8 min Diskussion, harte Obergrenze n × 20 min)

> **Harte Regel:** Der Block dauert **80 Minuten**. Es gibt keinen Puffer im Block; Puffer entsteht nur durch Unterschreiten der 12 Minuten.

---

## 1. Randbedingungen

| Vorgabe | Wert | Konsequenz für die Planung |
|---|---|---|
| Redezeit pro Person | 12 min (min. 10, max. 14) | Ziel 11:30, damit Übergaben nicht in die Redezeit laufen |
| Diskussion pro Person | ca. 8 min | 4 × 8 = 32 min |
| Gesamtblock | 80 min | 4 × (12 + 8) oder 48 + 32 |
| Abgabe Unterlagen | 08.01.2027, 10:00 | Foliensatz v1 am 04.01., PDF am 07.01. |
| Bewertung | Teamnote Unterlagen + Individualnote Vortrag/Diskussion | jede Person braucht eigenen Diskussionsanteil |

---

## 2. Empfohlenes Format: 4 Blöcke à 20 Minuten

**Empfehlung:** Diskussion direkt nach jedem Teil, nicht als ein 32-Minuten-Block am Ende.

Begründung:

- Die Individualnote bewertet ausdrücklich die **Antwortqualität in der Diskussion**. Wer direkt nach dem eigenen Teil antwortet, ist im Thema.
- Das Publikum hat die Fragen noch frisch; die Zettel-Methode funktioniert pro Teil besser als nach 48 Minuten.
- Der Block bleibt auch bei Verzug einer Person berechenbar.

**Ablauf:**

| Zeit | Dauer | Teil | Person | Inhalt |
|---|---|---|---|---|
| 0:00–0:02 | 2 | Eröffnung | A | Begrüßung, Ablauf, Ziel des Blocks, Hinweis auf Fragenzettel |
| 0:02–0:12 | 10 | A — Vortrag | A | Problem, Anforderungen, DDS-Kern, Mapping auf die Zelle |
| 0:12–0:20 | 8 | A — Diskussion | A | Architektur, Domains/Partitions, Modellgrenzen |
| 0:20–0:32 | 12 | B — Vortrag | B | QoS-Achsen, Deadline/Latenzbudget, RTPS, TSN |
| 0:32–0:40 | 8 | B — Diskussion | B | QoS-Wahl, RxO, Echtzeitgrenzen |
| 0:40–0:52 | 12 | C — Vortrag | C | Bedrohungsmodell, DDS Security, Deployment, Qualitätsmerkmale |
| 0:52–1:00 | 8 | C — Diskussion | C | Security, PKI, Embedded-Ressourcen |
| 1:00–1:12 | 12 | D — Vortrag | D | Abgrenzung, Demo, Bewertung, Fazit |
| 1:12–1:20 | 8 | D — Diskussion | D | Vergleich, Demo-Grenzen, Ausblick |

> A eröffnet mit 2 Minuten und hat dadurch 10 statt 12 Minuten Redezeit. Das ist zulässig (min. 10), muss aber bewusst so geplant werden. Alternative: Eröffnung in 1 Minute und A mit 11 Minuten.

---

## 3. Alternative: 48 Minuten Vortrag + 32 Minuten Gesamtdiskussion

Falls das Team eine gemeinsame Diskussion bevorzugt:

| Zeit | Dauer | Inhalt |
|---|---|---|
| 0:00–0:48 | 48 | vier Vorträge à 12 min, ohne Zwischendiskussion |
| 0:48–1:20 | 32 | Gesamtdiskussion, moderiert von A, ca. 8 min pro Themenschwerpunkt |

**Nachteil:** Die Fragen der ersten Teile liegen 40+ Minuten zurück; die Zuordnung „wer antwortet" wird unschärfer. **Vorteil:** Der rote Faden bleibt ununterbrochen.

**Entscheidung:** bis zum Scope-Freeze (27.11.2026) festlegen. Die Unterlagen und Folien funktionieren in beiden Formaten, die Proben nicht.

---

## 4. Feingliederung der Vorträge

### Teil A (10–12 min) — Problem, Anforderungen, DDS-Kern, Mapping

| Min | Inhalt | Kernbotschaft |
|---|---|---|
| 0–2 | Zelle als verteiltes System: sechs Teilnehmer, vier Probleme | „Die Zelle ist längst verteilt — nur nicht sauber." |
| 2–4 | Anforderungen: Echtzeit, Heterogenität, Entkopplung, Wandlungsfähigkeit | Anforderungen sind der Maßstab, nicht das Werkzeug |
| 4–8 | DDS-Kern: Global Data Space, DomainParticipant, Publisher/Writer, Subscriber/Reader, Topic, Discovery, RTPS | DDS ist ein Datenraum, kein Nachrichtenkanal |
| 8–11 | Mapping auf die Zelle: Domains, Topics, Rollen | dieselbe Mechanik, konkrete Verantwortlichkeiten |
| 11–12 | Übergabe an B | „Ob das trägt, entscheidet QoS." |

**Folien:** 8–10. **Muss-Folie:** Topic-/Teilnehmer-Matrix. **Verzichtsliste:** keine RTPS-Paketdetails (gehört zu B).

### Teil B (12 min) — QoS, Echtzeit, RTPS und TSN

| Min | Inhalt | Kernbotschaft |
|---|---|---|
| 0–2 | QoS als Vertrag zwischen Writer und Reader, RxO-Matching | QoS ist Architektur, nicht Tuning |
| 2–7 | Vier Achsen: Reliability/History, Deadline/LatencyBudget, Durability, Liveliness/Ownership | jede Achse beantwortet eine fachliche Frage |
| 7–10 | Drei Profile der Zelle: `control`, `alarm`, `telemetry` | gleiche Mechanik, drei Verträge |
| 10–11 | RTPS-Transport: UDP, Multicast, Shared Memory; TSN als Netzschicht | DDS garantiert nicht die Latenz — das Netz entscheidet mit |
| 11–12 | Übergabe an C | „Wer das kontrolliert, muss es auch schützen." |

**Folien:** 9–11. **Muss-Folie:** QoS-Tabelle. **Verzichtsliste:** kein TSN-802.1Qbv-Tutorial, nur die Rolle im Zusammenspiel.

### Teil C (12 min) — Security, Deployment, Qualitätsmerkmale

| Min | Inhalt | Kernbotschaft |
|---|---|---|
| 0–2 | Bedrohungsmodell: fremder Participant, falsche `Trajectory`, Mitlesen | Security beginnt mit dem Angreifer, nicht mit dem Plugin |
| 2–6 | DDS Security: Authentication, Access Control, Cryptography, Logging; Plugins und Zertifikate | vier Bausteine, ein Vertrauensmodell |
| 6–9 | Deployment: RTOS-Controller, Edge-Gateway, MES; Ressourcen und Redundanz | DDS läuft auch auf kleinen Knoten — mit Konfigurationsdisziplin |
| 9–11 | Qualitätsmerkmale: was DDS liefert, was nicht | Reliability ≠ Rechtzeitigkeit; Security ≠ Safety |
| 11–12 | Übergabe an D | „Bleibt die Frage: warum nicht OPC UA oder MQTT?" |

**Folien:** 9–11. **Muss-Folie:** Bedrohungsbild plus Security-Bausteine. **Verzichtsliste:** keine PKI-Tiefe, keine Juristerei.

### Teil D (12 min) — Abgrenzung, Demo, Bewertung, Fazit

| Min | Inhalt | Kernbotschaft |
|---|---|---|
| 0–4 | Vergleich DDS / OPC UA Pub/Sub / MQTT / SOME-IP | vier verschiedene Antworten auf vier verschiedene Fragen |
| 4–9 | Demo: `JointState` + `Alarm`, zwei QoS-Profile, Deadline-Event | der Unterschied ist sichtbar, nicht behauptet |
| 9–11 | Bewertung: Stärken, Grenzen, Nicht-Anwendungsfälle | DDS ist keine Universallösung |
| 11–12 | Fazit H1–H3, Ausblick (ROS 2, AUTOSAR AP, DDS+TSN) | drei Thesen, drei Antworten |

**Folien:** 9–11 inkl. Backup-Folien. **Muss-Folie:** Vergleichstabelle. **Verzichtsliste:** keine Live-Installation, kein Terminal-Blindflug.

---

## 5. Diskussionsführung

### 5.1 Ablauf pro Diskussion (8 min)

| Min | Schritt |
|---|---|
| 0–1 | Moderator sammelt die Fragenzettel des Teils, clustert sie sichtbar |
| 1–6 | 3–4 Fragen beantworten, davon mindestens eine kontroverse |
| 6–8 | eine vorbereitete Anschlussfrage stellen (Transfer) |

### 5.2 Regeln

- **Fragen sammeln:** Zettel oder geteiltes Dokument; das Publikum schreibt während des Vortrags mit. Unbeantwortete Fragen kommen auf den **Parkplatz** und werden am Ende des Blocks oder in der Pause adressiert.
- **Moderation:** A moderiert; bei Selbstmoderation der Person D übernimmt A die Zeit und die Reihenfolge.
- **Zeitwächter:** rotierend, immer eine Person, die nicht spricht. Signal bei 10:00, 11:30 und 12:00.
- **Keine Fremdantworten:** Wer eine Frage eines anderen Teils beantworten will, wird kurz eingebunden („C ergänzt"), aber die Hauptantwort bleibt beim Zuständigen.

### 5.3 Vorbereitete Fragen pro Person (Mindestumfang)

| Person | Kernthemen der eigenen Diskussion | Anzahl vorbereitet |
|---|---|---|
| A | Datenmodell, Domains/Partitions, Discovery, Grenzen des Modells | 6 + 2 Ausweich |
| B | QoS-Achsen, RxO, Deadline vs. Latenz, TSN-Zusammenspiel | 6 + 2 Ausweich |
| C | Bedrohungsmodell, PKI, Embedded-Ressourcen, Safety-Abgrenzung | 6 + 2 Ausweich |
| D | Vergleich, Demo-Grenzen, Ausblick, Nicht-Anwendungsfälle | 6 + 2 Ausweich |

Die Fragenbank liegt in [`../07_qa/`](../07_qa/); Ziel sind 24–32 Fragen inkl. Antwortstichpunkten und Quellenverweis.

---

## 6. Übergaben und roter Faden

Die Übergabesätze sind Teil des Drehbuchs, nicht Improvisation:

| Übergabe | Satz |
|---|---|
| A → B | „Damit ist die Struktur klar. Ob sie trägt, entscheidet QoS — B." |
| B → C | „Wer diese Datenströme kontrolliert, muss sie auch schützen — C." |
| C → D | „Bleibt die Frage, warum nicht OPC UA oder MQTT — D." |
| D → Diskussion | „Damit stehen die drei Thesen. Widerspruch ist erwünscht." |

---

## 7. Technik und Material

- **Folien:** ein gemeinsamer Master, vier Teile, durchgehende Nummerierung, Teil-Trenner mit Zeitangabe.
- **Backup:** PDF auf zwei Geräten plus USB; Demo-Video lokal und in der Cloud.
- **Demo:** falls live, vorher im Vortragsraum testen; sonst Video mit sichtbarem Zeitstempel.
- **Fragenzettel:** vorbereitet, mit Teil A/B/C/D beschriftet.
- **Parkplatz:** leere Folie oder Whiteboard, sichtbar für das Publikum.
- **Zeit:** Stoppuhr plus Handy-Signal; kein Blick auf die Uhr während des Satzes.

---

## 8. Probenplan

| Probe | Termin | Fokus | Abbruchkriterium |
|---|---|---|---|
| Trockenprobe | 05.01.2027 | Ablauf, Übergaben, Folienlücken | ein Teil über 13 min |
| Generalprobe 1 | 05.–06.01.2027 | Timing mit Stoppuhr, Diskussion simuliert | Gesamtblock über 80 min |
| Generalprobe 2 | 08.01.2027 | vollständig inkl. Technik und Q&A | zwei Teile über 13 min oder Diskussion unter 6 min |
| Technikcheck | 09.–10.01.2027 | Beamer, Adapter, Audio, Demo-Gerät | Technik nicht verfügbar |

**Regel:** Wer in Generalprobe 2 über 13 Minuten liegt, kürzt bis zum Vortrag um mindestens eine Folie.

---

## 9. Risiken im Ablauf

| Risiko | Sofortmaßnahme |
|---|---|
| Ein Teil läuft über | Zeitwächter signalisiert, Moderator greift ein, Rest wird in die Diskussion verschoben |
| Demo fällt aus | Video starten, Code-Ausschnitt zeigen, nahtlos zu Bewertung übergehen |
| Diskussion springt zwischen Teilen | Parkplatz nutzen, Frage notieren, beim zuständigen Teil beantworten |
| Publikum fragt nicht | vorbereitete Anschlussfrage stellen; Alternativfrage „Was würden Sie anders bauen?" |
| Frage sprengt den Rahmen | „Das ist eine eigene Diskussion — ich gebe eine kurze Einordnung und nehme es mit." |
| Block startet verspätet | Eröffnung auf 1 Minute kürzen; nicht an den Vorträgen sparen |

---

## 10. Offene Entscheidungen

1. **Format:** 4 × (12 + 8) oder 48 + 32 — bis 27.11.2026 entscheiden.
2. **Eröffnung:** 2 Minuten durch A oder 1 Minute und A mit vollem Redeanteil.
3. **Demo live oder Video** — abhängig von der Probe am 05.01.2027.
4. **Fragenzettel digital oder Papier** — abhängig davon, ob WLAN/Beamer mitspielen.
