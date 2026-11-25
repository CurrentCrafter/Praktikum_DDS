# 80-Minuten-Agenda — DDS: Assembly-Zelle und AMR-Flotte

**Stand:** 25.11.2026
**Vortrag:** Montag, 11.01.2027
**Team:** 4 Personen
**Grundlage:** `sekm-seminar-2026.pdf` (12 min pro Person, 10–14 min erlaubt, ca. 8 min Diskussion, harte Obergrenze n × 20 min)

> **Harte Regel:** Der Block dauert **80 Minuten**. Es gibt keinen Puffer im Block; Puffer entsteht nur durch Unterschreiten der 12 Minuten.

> **Rollenaufteilung:** A Architektur/roter Faden/Integration, B Automatisierung, C Qualitätsmerkmale, D Zukunft/DDS-spezifische Aspekte. Assembly-Zelle und AMR-Flotte sind Vergleichskandidaten; UMAA ist ein kurzer Transfer. Die endgültige Auswahl des Hauptbeispiels steht noch aus.

---

## 1. Randbedingungen

| Vorgabe | Wert | Konsequenz für die Planung |
|---|---|---|
| Redezeit pro Person | 12 min (min. 10, max. 14) | Ziel 11:30, damit Übergaben nicht in die Redezeit laufen |
| Diskussion pro Person | ca. 8 min | 4 × 8 = 32 min |
| Gesamtblock | 80 min | 48 + 32 (Deck-Vorschlag) oder 4 × (12 + 8) (Alternative) |
| Abgabe Unterlagen | 08.01.2027, 10:00 | Foliensatz v1 am 04.01., PDF am 07.01. |
| Bewertung | Teamnote Unterlagen + Individualnote Vortrag/Diskussion | jede Person braucht eigenen Diskussionsanteil |

---

## 2. Formatvorschlag aus der Orga-Präsentation: Vorträge, dann gemeinsame Diskussion

Folie 8 der Orga-Präsentation schlägt vor, alle vier Vorträge nacheinander zu halten und anschließend gemeinsam zu diskutieren. Dieser Ablauf ist **ein Vorschlag, noch kein dokumentierter Beschluss**.

Möglicher Ablauf:

- 0:00–0:48: vier Vorträge à 12 Minuten
- 0:48–1:20: gemeinsame Diskussion (ca. 32 Minuten)

Die Präsentation nennt eine mögliche Vortragsreihenfolge; ob diese beibehalten wird, ist ebenfalls nicht als beschlossen dokumentiert.

## 3. Alternative: Diskussion direkt nach jedem Teil

Diese Alternative steht im bisherigen Repo-Entwurf. Die Kursvorgabe fordert ca. 8 Minuten Diskussion pro Person, legt im hier verfügbaren Planungsstand aber nicht fest, ob die Diskussionen einzeln oder gemeinsam stattfinden.

| Zeit | Dauer | Teil | Inhalt |
|---|---|---|---|
| 0:00–0:12 | 12 | A — Architektur | DDS-Architektur, Kandidatenvergleich aus Architektursicht, roter Faden |
| 0:12–0:20 | 8 | A — Diskussion | Architektur und Modellgrenzen |
| 0:20–0:32 | 12 | B — Automatisierung | Anforderungen beider Kandidaten |
| 0:32–0:40 | 8 | B — Diskussion | Echtzeit, Events, Scheduling/Synchronisation |
| 0:40–0:52 | 12 | C — Qualitätsmerkmale | Vergleichende Qualitätsbewertung |
| 0:52–1:00 | 8 | C — Diskussion | Qualität und Sicherheitsgrenzen |
| 1:00–1:12 | 12 | D — Zukunft/DDS-spezifisch | DDS-Eigenschaften und Transfer |
| 1:12–1:20 | 8 | D — Diskussion | Zukunft und Anwendungsgrenzen |

Diese Alternative entspricht dem früheren Repo-Entwurf und ist ebenfalls nicht als Teamentscheidung bestätigt.

---

## 4. Feingliederung der Vorträge

### Teil A (12 min) — Architektur und roter Faden

| Min | Inhalt | Kernbotschaft |
|---|---|---|
| 0–2 | Leitfrage und Auswahlkriterien für Assembly-Zelle vs. AMR-Flotte | Beispielwahl muss begründet sein |
| 2–8 | DDS-Architektur: Global Data Space, Entities, Topic, Discovery, RTPS | DDS ist ein Datenmodell, kein Nachrichtenkanal |
| 8–11 | Architektur-Mapping des ausgewählten Falls; UMAA als kurzer Transfer | konkrete Rollen und Datenflüsse |
| 11–12 | Übergabe an B | Anforderungen prägen den Automatisierungseinsatz |

**Folien:** 8–10. **Muss-Folie:** Kandidatenvergleich und Topic-/Teilnehmer-Mapping. **Verzichtsliste:** keine RTPS-Paketdetails (D vertieft DDS-spezifische Aspekte).

### Teil B (12 min) — Automatisierung

| Min | Inhalt | Kernbotschaft |
|---|---|---|
| 0–3 | Zeitverhalten und Echtzeitanforderungen der Kandidaten | Anforderungen hängen vom Prozess/Use-Case ab |
| 3–6 | Eventmanagement und Datenströme | verteilte Ereignisse müssen fachlich zugeordnet werden |
| 6–9 | Scheduling und Synchronisation | DDS ist nicht automatisch ein Scheduler oder Zeitgeber |
| 9–11 | Schwache Embedded-Hardware und heterogene Systeme | Ressourcen/Plattformen beeinflussen die Architektur |
| 11–12 | Übergabe an C | „Anforderungen bewerten wir an Qualitätsmerkmalen.“ |

**Folien:** 8–10. **Muss-Folie:** Automatisierungsanforderungen beider Kandidaten. QoS-/TSN-Details sind DDS-spezifisch und werden mit D abgestimmt.

### Teil C (12 min) — Qualitätsmerkmale

| Min | Inhalt | Kernbotschaft |
|---|---|---|
| 0–2 | Bewertungsmaßstab für die beiden Anwendungskandidaten | Qualität ist Anforderung plus begründeter Nachweis |
| 2–8 | Zuverlässigkeit, Leistung, Flexibilität, Robustheit, Verfügbarkeit | DDS-Mechanismen gegen konkrete Anforderungen halten |
| 8–10 | System-/Datensicherheit | Security ist nicht gleich Safety |
| 10–11 | Anpassbarkeit und Testbarkeit | Verteilte Komplexität sichtbar machen |
| 11–12 | Übergabe an D | „Wie zukunftsfähig und DDS-spezifisch ist die Lösung?“ |

**Folien:** 8–10. **Muss-Folie:** vergleichende Qualitätsbewertung. Security-Mechanismen mit D abstimmen, keine doppelte Vertiefung.

### Teil D (12 min) — Zukunft und DDS-spezifische Aspekte

| Min | Inhalt | Kernbotschaft |
|---|---|---|
| 0–3 | Offenheit und Zukunftsfähigkeit | Standardisierung und Interoperabilität einordnen |
| 3–6 | TSN, Embedded/IoT und DDS Security | Grenzen und Systemzusammenspiel erklären |
| 6–9 | Anwendung/Demo am gewählten Fall | Verhalten illustrieren, keine Echtzeitgarantie behaupten |
| 9–11 | UMAA-Transfer und Grenzen von DDS | DDS-Anwendung außerhalb der Fertigung einordnen |
| 11–12 | Gemeinsames Fazit/Ausblick | Ergebnis des Kandidatenvergleichs zusammenführen |

**Folien:** 8–10 inkl. Backup. **Muss-Folie:** DDS-spezifische Eigenschaften und Transfer. Demo-Zuständigkeit/Umfang noch teamseitig bestätigen; keine Echtzeitgarantie behaupten.

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
| A | DDS-Architektur, Vergleich der Kandidaten, Datenmodell und Discovery | 6 + 2 Ausweich |
| B | Automatisierungsanforderungen: Echtzeit, Events, Scheduling, Synchronisation, Embedded/heterogene Systeme | 6 + 2 Ausweich |
| C | Qualitätsmerkmale, Bewertung, Sicherheit und Grenzen | 6 + 2 Ausweich |
| D | Zukunft/DDS-spezifische Aspekte, TSN, Embedded/IoT, Security, UMAA-Transfer | 6 + 2 Ausweich |

Die Fragenbank liegt in [`../07_qa/`](../07_qa/); Ziel sind 24–32 Fragen inkl. Antwortstichpunkten und Quellenverweis.

---

## 6. Übergaben und roter Faden

Die Übergabesätze sind Teil des Drehbuchs, nicht Improvisation:

| Übergabe | Satz |
|---|---|
| A → B | „Die Architektur steht im Anwendungskontext. Welche Automatisierungsanforderungen entstehen daraus?“ |
| B → C | „Diese Anforderungen bewerten wir jetzt anhand der Qualitätsmerkmale.“ |
| C → D | „Zum Schluss: DDS-spezifische Eigenschaften und Zukunftsfähigkeit.“ |
| D → Diskussion | „Damit liegen Vergleich und Bewertung vor. Widerspruch ist erwünscht.“ |

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

1. **Format:** 48 + 32 (Vorschlag aus Folie 8) oder 4 × (12 + 8) — Entscheidung noch offen.
2. **Eröffnung:** 2 Minuten durch A oder 1 Minute und A mit vollem Redeanteil.
3. **Demo live oder Video** — abhängig von der Probe am 05.01.2027.
4. **Fragenzettel digital oder Papier** — abhängig davon, ob WLAN/Beamer mitspielen.
