# Arbeitspaket A — Architektur, roter Faden, Integration und Abgabe

**Stand:** 25.11.2026  
**Owner:** Rolle A  
**Grundlage:** Orga-Präsentation vom 15.11.2026, bestätigte Rollenaufteilung und `Timeline.md`  
**Geltungsbereich:** DDS-Seminar; Assembly-Zelle und AMR-Flotte vergleichen, UMAA als kurzer Transfer. Die Wahl des vollständig auszuarbeitenden Hauptbeispiels bleibt bis zum Scope-Freeze offen.

> **Arbeitsregel:** Ein Paket gilt erst als erledigt, wenn die unten genannten Kriterien erfüllt und die Nachweise eingetragen sind. Ein Dokumententwurf allein belegt keine Teamentscheidung oder durchgeführte Abstimmung. Abhängigkeiten zu B/C/D werden sichtbar markiert; die genaue fachliche Abgrenzung wird in den nächsten Besprechungen abgestimmt.

**Prüfspur:** Abgeschlossene Arbeitspunkte bleiben in dieser Datei stehen. Beim Abschluss den Punkt mit `[x]`, Abschlussdatum und konkretem Nachweis/Link versehen, zum Beispiel: `- [x] (2026-12-04; Nachweis: Reviewprotokoll/Abschnitt) ...`. Nicht erledigte oder nur teilweise erledigte Punkte nicht löschen; Status und offene Restarbeit kenntlich machen. Ein separates Änderungsprotokoll ist nicht vorgesehen.

## Statusübersicht

| ID | Arbeitspaket | Solltermin | Status |
|---|---|---:|---|
| A0 | M1 nachführen: Exposé und tatsächlichen Kickoff-Stand klären | 20.11.2026 (überfällig/Status prüfen) | `[~]` laut Timeline |
| A1 | Architekturvergleich und Scope-Freeze vorbereiten | 27.11.2026 | `[ ]` |
| A2 | DDS-Architekturabschnitt und Beispiel-Mapping entwerfen | 04.12.2026 | `[ ]` |
| A3 | Architektur v1: Diagramme, DDS-Zuordnung und IDL-Typen | 11.12.2026 | `[ ]` |
| A4 | Beiträge integrieren und Vollentwurf v1.0 herstellen | 18.12.2026 | `[ ]` |
| A5 | Review einarbeiten und Content-Freeze v1.1 vorbereiten | 22.12.2026 | `[ ]` |
| A6 | Folienintegration, Endkorrektur, finales PDF und Upload | 04.–08.01.2027 | `[ ]` |

**Statuslegende:** `[ ]` offen · `[~]` in Arbeit · `[x]` erledigt · `[!]` blockiert. Status, Abschlussdatum und Nachweis bitte nach tatsächlicher Arbeit aktualisieren.

---

## A0 — M1: Exposé und tatsächlichen Kickoff-Stand nachführen

**Solltermin:** 20.11.2026 · **Status:** `[~]` laut `Timeline.md`, Termin verstrichen; bis zur Bestätigung des tatsächlichen Kickoffs und des gemeinsamen Exposé-Stands nicht als erledigt markieren.  
**Ziel:** Einen belastbaren gemeinsamen Planungsstand für M2 herstellen.

### Anforderungen / Checkliste

- [ ] Prüfen und eintragen, ob/wann ein Team-Kickoff stattgefunden hat; nicht aus dem Exposé ableiten.
- [ ] Exposé als gemeinsamen Entwurf mit den aktuell gültigen Entscheidungen führen: Assembly-Zelle und AMR-Flotte vergleichen, UMAA als kurzer Transfer.
- [ ] Drei Thesen H1–H3 auf Verständlichkeit und Belegbarkeit prüfen; Annahmen als solche kennzeichnen.
- [ ] Rollen A–D entsprechend der bestätigten Aufteilung abbilden.
- [ ] Exposé-Verweise, Scope-Aussagen und Status zwischen README, Timeline und Architekturdateien konsistent halten.

**Erledigt, wenn:** Der tatsächliche Kickoff ist belegt und das gemeinsame Exposé gibt Kandidatenvergleich, Transferfall, Rollen sowie offene Entscheidungen konsistent wieder. Falls der Kickoff nicht stattgefunden hat, Status und weiteres Vorgehen ausdrücklich dokumentieren; der Meilenstein bleibt bis zur gemeinsamen Bestätigung offen/in Arbeit.

**Abschlussdatum / Nachweis / Ablage:** `[Erst bei Abschluss eintragen: Datum, Datei, Protokoll oder Link]`  
**Offene Punkte:** `[Eintragen]`

---

## A1 — M2: Architekturvergleich und Scope-Freeze vorbereiten

**Solltermin:** 27.11.2026 · **Abhängigkeiten:** Beiträge aus B, C und D  
**Ziel:** Die Auswahl zwischen Assembly-Zelle und AMR-Flotte aus Architektursicht belegen. A erstellt die Architektur-Bewertung und Empfehlung; die endgültige Auswahl wird nach Vorliegen der Bewertungen aller Rollen als Teamentscheidung festgehalten.

### Anforderungen / Checkliste

- [ ] Für beide Kandidaten Systemgrenze und wichtigste fachliche Komponenten benennen.
- [ ] Für beide Kandidaten den Architekturfluss skizzieren: Datenproduzenten, Datenkonsumenten, Koordinatoren und externe Schnittstellen.
- [ ] DDS-Eignung und zentrale Architekturannahmen beider Kandidaten vergleichen; eigene Annahmen von belegten Tatsachen trennen.
- [ ] Abhängigkeiten zu B/C/D markieren und deren Beiträge in das gemeinsame Vergleichsraster integrieren; genaue fachliche Zuständigkeitsgrenzen in den nächsten Besprechungen abstimmen.
- [ ] Einen Kandidaten aus Architektursicht empfehlen; die endgültige Auswahl anhand des vollständigen Rollenvergleichs gemeinsam beschließen und dokumentieren.
- [ ] UMAA knapp als Transferfall einordnen; keine dritte vollständige Fallarchitektur eröffnen.
- [ ] FOSS-Anforderung für die AMR-DDS-Implementierung festhalten; konkrete Implementierung bleibt gesondert zu entscheiden.
- [ ] M2-Ergebnisse in Exposé und `DDS_offene_Fragen.md` dokumentieren.

**Erledigt, wenn:** Die Teamentscheidung für einen Hauptfall mit Kriterien und Belegen dokumentiert ist, Abhängigkeiten und noch abzustimmende Abgrenzungen sichtbar sind und die M2-Ausgaben (Beispielspezifikation, QoS-Arbeitstand, Quellenregister-Arbeitstand, Implementierungsentscheidung bzw. verbleibende offene Wahl) auffindbar sind.

**Abschlussdatum / Nachweis / Ablage:** `[Erst bei Abschluss eintragen: Datum, Entscheidungsnotiz, Vergleichsraster, Quellenregister]`  
**Beschlossener Hauptfall:** `[Eintragen, sobald das Team entschieden hat]`  
**Offene Punkte:** `[Eintragen]`

---

## A2 — Architekturabschnitt und Beispiel-Mapping entwerfen

**Solltermin:** 04.12.2026 (Review #1) · **Abhängigkeiten:** Beiträge/Abstimmung mit B, C und D; genaue A/D-Themenabgrenzung wird gemeinsam festgelegt.  
**Ziel:** DDS-Referenzarchitektur verständlich erklären und auf den ausgewählten Kandidaten abbilden.

### Anforderungen / Checkliste

- [ ] DCPS-Grundmodell mit `DomainParticipant`, Publisher/Subscriber, DataWriter/DataReader, Topic und typisierten Daten erläutern.
- [ ] Datenzentrierte Kommunikation und Discovery im Architekturfluss erklären; DDS nicht als zentralen Broker oder gemeinsamen Speicher darstellen.
- [ ] RTPS als DDSI-Wire-Protokoll erklären; den Namen „Real-Time“ nicht als Echtzeitgarantie ausgeben.
- [ ] DDS-Entities und fachliche Komponenten auseinanderhalten; keine unbelegte 1:1-Zuordnung behaupten.
- [ ] Verantwortlichkeiten und Hauptdatenflüsse des ausgewählten Beispiels nachvollziehbar auf Topics und DDS-Teilnehmerrollen abbilden.
- [ ] Systemgrenze zu WMS/MES bzw. Leitsteuerung und die externe Schnittstelle ausdrücklich markieren.
- [ ] Lokale Navigation/Bewegungsregelung und Safety von nicht-sicherheitsgerichteter DDS-Flottenkommunikation abgrenzen.
- [ ] Mit D die Aufteilung zwischen DDS-Grundarchitektur und vertieften DDS-spezifischen Aspekten abstimmen; bis dahin offene Grenze als Abhängigkeit kennzeichnen.
- [ ] Kernaussagen durch OMG-Spezifikationen oder andere belastbare Quellen stützen; Entwurfshypothesen sichtbar kennzeichnen.

**Erledigt, wenn:** Ein zusammenhängender Abschnittsentwurf mit Architekturabbildung, Systemgrenze, Topic-/Teilnehmer-Mapping und Quellenangaben vorliegt und im Review verständlich erklärt werden kann.

**Abschlussdatum / Nachweis / Ablage:** `[Erst bei Abschluss eintragen: Datum, Abschnitt, Diagramm, Quellenfundstellen]`  
**Feedback aus Review #1:** `[Eintragen]`

---

## A3 — M4: Architektur v1 und Diagramm-/Typenpaket

**Solltermin:** 11.12.2026 · **Abhängigkeiten:** ausgewählter Hauptfall; Abstimmung mit C/D, insbesondere zu IDL-Typen, Qualitäts-/QoS-Bewertung und offenen DDS-spezifischen Grenzen.  
**Ziel:** Eine konsistente Architekturansicht erstellen, die in Unterlagen und Vortrag gleich verwendet werden kann.

### Anforderungen / Checkliste

- [ ] Component-/Kontextdiagramm erstellen: Rollen, Systemgrenze, externe Systeme und Kommunikationsverantwortung.
- [ ] Deploymentdiagramm für den ausgewählten Fall erstellen: Rechner/Nodes, Netzgrenzen und externe Adapter passend zum Fall; nicht belegte Hardware als Annahme markieren.
- [ ] Sequenzdiagramm für einen relevanten Kernablauf erstellen (Auftrag → Zuweisung → Status/Rückmeldung).
- [ ] Topic-Matrix mit Name, Datentyp, Key, Writer, Reader und Zweck vervollständigen.
- [ ] IDL-Typen mit den zuständigen Rollen abstimmen; mindestens Identitäten, Zustandsdaten und Auftrags-/Statusdaten nachvollziehbar definieren.
- [ ] Domain-/Partition- und `DomainParticipant`-Zuordnung begründen; offene Punkte im Diagramm oder Begleittext kenntlich machen.
- [ ] Alle Diagramme mit Legende, Versionsstand und passenden Quellen-/Annahmenhinweisen versehen.
- [ ] Gegen QoS- und Qualitätsbewertung von B/C sowie DDS-spezifische Randbedingungen von D auf Widersprüche prüfen.

**Erledigt, wenn:** Component-, Deployment- und Sequenzsicht sowie Topic-/IDL-Arbeitstand konsistent sind und im Architektur-v1-Review vorgelegt werden können.

**Abschlussdatum / Nachweis / Ablage:** `[Erst bei Abschluss eintragen: Datum, Diagrammquellen, Exporte, IDL-Dateien]`  
**Reviewpunkte / Änderungen:** `[Eintragen]`

---

## A4 — Integration und Vollentwurf v1.0

**Solltermin:** 18.12.2026 · **Abhängigkeiten:** Abschnittsentwürfe B/C/D, Architektur v1 und teamweit zu klärender Demo-Beitrag. A integriert die Beiträge; die fachlichen Inhalte verantwortet jeweils die liefernde Rolle.  
**Ziel:** Aus Einzelbeiträgen ein verständliches, konsistentes Gesamtwerk machen.

### Anforderungen / Checkliste

- [ ] Beiträge aller Rollen in eine gemeinsame Gliederung und ein gemeinsames Begriffssystem integrieren; fachliche Aussagen nicht ohne Abstimmung stellvertretend ändern.
- [ ] Roten Faden vom Problem über Architektur und Automatisierungsanforderungen bis Qualitätsbewertung und DDS-spezifischem Ausblick herstellen.
- [ ] Übergänge, Einleitung, Zusammenfassung und Schluss mit den Rollen abstimmen.
- [ ] Widersprüche bei Beispielwahl, Topics, QoS, Security, TSN, Deployment und VDA-5050-/WMS-Grenze auflösen oder ausdrücklich als offen markieren.
- [ ] Quellen, Abbildungen, Versionsangaben und eigene Hypothesen konsistent kennzeichnen.
- [ ] Prüfen, dass der Text ohne zusätzliche Literatur verständlich ist und zum vereinbarten Seiten-/Zeitbudget passt.
- [ ] Architekturfragen und Antwortlinien in der gemeinsamen Q&A-Bank berücksichtigen; keine Professorfragen in `DDS_offene_Fragen.md` ablegen.
- [ ] Demo-Zuständigkeit und Umfang als teamweite Abhängigkeit klären; sie sind A nicht automatisch zugewiesen.

**Erledigt, wenn:** Ein vollständiger, gemeinsam reviewbarer Unterlagenentwurf v1.0 mit einheitlicher Architektur und Quellenapparat vorliegt.

**Abschlussdatum / Nachweis / Ablage:** `[Erst bei Abschluss eintragen: Datum, Masterdatei, Reviewprotokoll, offene Punkte]`  
**Feedback aus Review #2:** `[Eintragen]`

---

## A5 — Content-Freeze v1.1

**Solltermin:** 22.12.2026  
**Ziel:** Inhaltliche Konsistenz und Abgabereife vor der Weihnachtspause herstellen.

### Anforderungen / Checkliste

- [ ] Review-Feedback aus M5 nachverfolgen und dokumentieren.
- [ ] Architekturdiagramme und Textpassagen auf denselben Revisionsstand bringen.
- [ ] Prüfen, dass getroffene Entscheidungen nicht mehr als offen und offene Entscheidungen nicht als beschlossen dargestellt werden.
- [ ] Quellen- und Zitatprüfung für A-Anteile durchführen; offene Fundstellen markieren.
- [ ] Offene, nicht kritische Inhalte in den Parkplatz verschieben; keine neuen Inhalte nach dem Freeze einplanen.

**Erledigt, wenn:** Unterlagen v1.1 eingefroren und verbleibende Punkte dokumentiert sind.

**Abschlussdatum / Nachweis / Ablage:** `[Erst bei Abschluss eintragen: Datum, Freeze-Version, Prüfnotiz]`

---

## A6 — Folienintegration, finales PDF und Upload

**Solltermine:** gemäß `Timeline.md`: Foliensatz v1 am 04.01.2027 · finales PDF intern am 07.01.2027, 18:00 · Upload am 08.01.2027, 10:00.  
**Ziel:** A integriert die schriftlichen Unterlagen, erstellt das finale PDF und dokumentiert den Upload. Jede Rolle bleibt für ihre Fachinhalte verantwortlich. Proben- und Diskussionsformat sind Abhängigkeiten und werden nach Teamklärung in der Planung aktualisiert.

### Anforderungen / Checkliste

- [ ] Die Folienbeiträge in den gemeinsamen Master integrieren/abgleichen; jede Rolle verantwortet ihren Fachinhalt. Architekturdiagramme und Begriffe über alle Teile konsistent halten.
- [ ] Prüfen, dass A-Architekturteil und Auswahlbegründung mit dem finalen Hauptbeispiel übereinstimmen.
- [ ] Quellen und Bildrechte auf Folien und Unterlagen prüfen.
- [ ] Schriftliche Unterlagen als gut lesbares PDF mit hellem Hintergrund exportieren und technisch kontrollieren.
- [ ] Upload- und Dateiversion prüfen; Abgabe fristgerecht über Ilias dokumentieren.
- [ ] Generalproben, Präsentationsreihenfolge und Diskussionsablauf als Teamabhängigkeit klären; widersprüchliche Planangaben nicht als feste A-Frist behandeln, bis das Team sie bestätigt hat.
- [ ] Finalen Abgabestand und Backup-Dateien ablegen.

**Erledigt, wenn:** Finales PDF und Foliensatz versionsgeprüft abgegeben sind, Upload nachgewiesen ist und der Vortrag mit dem Teamstand übereinstimmt.

**Abschlussdatum / Nachweis / Ablage:** `[Erst bei Abschluss eintragen: Datum, finale Dateien, Uploadbestätigung, ggf. Probe-Notiz]`

---

## Laufende Architektur-Qualitätskontrolle

Bei jedem Paket prüfen:

- [ ] DDS wird nicht mit ROS 2, Open-RMF, VDA 5050 oder einer DDS-Implementierung gleichgesetzt.
- [ ] `RELIABLE`, QoS, DDSI-RTPS und „Real-Time“ werden nicht als Garantie für Ende-zu-Ende-Frist, korrekte Ausführung oder funktionale Safety dargestellt.
- [ ] Keine Topic-/Participant-/Domain-Zuordnung wird als Teamentscheidung ausgegeben, solange sie nicht beschlossen ist.
- [ ] Direkte DDS-API ohne ROS 2 und die FOSS-Anforderung für den AMR-Kandidaten bleiben berücksichtigt.
- [ ] Aussagen über konkrete AMR-Produkte oder reale Installationen werden nur mit Quelle gemacht; ansonsten als eigenes Referenzszenario gekennzeichnet.

## Nächster konkreter Schritt

Bis zum Scope-Freeze am **27.11.2026**: A0-Status von Exposé/Kickoff nachführen und gemeinsam mit B/C/D den Architekturvergleich befüllen, damit die Auswahl des Hauptbeispiels begründet getroffen werden kann.
