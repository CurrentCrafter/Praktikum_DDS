# Abgleich: Orga-Präsentation und aktueller Repo-Plan

**Stand:** 25.11.2026  
**Maßgebliche Vergleichsquelle:** `06_folien/2026-11-15_Orga_DDS_kurz.pptx`  
**Verglichene Repo-Dokumente:** `Timeline.md`, `01_plan/Expose_v0.1.md`, `01_plan/Agenda_80min.md`, `01_plan/Projektvarianten.md`, `README.md`, `Agent.md` sowie die Assembly- und AMR-Kandidatenarchitekturen.

## Kurzfazit und nachfolgende Festlegungen

Die Präsentation ist ein **Arbeits-/Orga-Deck mit Entscheidungsfragen**, keine verabschiedete Protokollfassung. Folie 12 („Ergebnisse“) hält nur einzelne Ansätze fest; mehrere Ergebnisfelder sind leer. Daher gilt: Die Präsentation ist hier der Maßstab für den **Abgleich der vorgesehenen Arbeitspakete**, aber ein Fragezeichen im Deck ist kein Beschluss.

Der deutlichste ursprüngliche Konflikt betraf die **Rollen-/Themenaufteilung**: Das Deck sieht Architektur, Automatisierung, Qualitätsmerkmale und Zukunft/DDS-spezifische Punkte vor; zuvor plante das Repo Architektur, QoS/Echtzeit/TSN, Security/Deployment und Vergleich/Demo/Fazit.

**Festlegungen des Auftraggebers am 25.11.2026:** (1) Assembly-Zelle und AMR-Flotte bleiben Vergleichskandidaten; UMAA wird als kurzer Transfer statt Hausautomation genutzt. Die Auswahl eines vollständig auszuarbeitenden Hauptbeispiels bleibt offen. (2) Rollenverteilung aus Folie 9 ist verbindlich. (3) Reihenfolge und Diskussionsformat bleiben Vorschlag. (4) Der Repo-Gantt wird als interner Zeitplan übernommen. Der Repo-Plan wurde daran angepasst; der Abgleich unten hält den vorherigen Stand und die jetzt geltenden Entscheidungen fest.

**Nachfolgende Architekturfestlegung:** Für den AMR-Kandidaten ist direkte Nutzung der DDS-API ohne ROS 2 beschlossen. Die konkrete DDS-Implementierung bleibt offen. Dadurch wird die Wahl des AMR-Kandidaten als Seminar-Hauptbeispiel nicht vorweggenommen.

## Arbeitspaket-Abgleich

| Arbeitspaket laut Präsentation | Fundstelle im Deck | Aktueller Repo-Stand | Abgleich / Klärungsbedarf |
|---|---|---|---|
| **Anwendungsbeispiel auswählen:** Assembly-Zelle gegen AMR-Flotte prüfen; UMAA statt Hausautomation als kurzer Transfer | Folien 4–5 und 12; Festlegung 25.11. | `Expose_v0.1.md` und `DDS_offene_Fragen.md` führen beide Kandidaten; AMR-Entwurf liegt in `03_architektur/Variante_C_AMR_Flotte_Architektur_v0.1.md`; UMAA-Transfer und offene Auswahl sind dokumentiert | **In Arbeit.** Alle Rollen bewerten beide Kandidaten; ein Hauptbeispiel muss bis zum Scope-Freeze begründet gewählt werden. Krankenhaus/Hausautomation sind keine Fallarchitekturen. |
| **Exposé gemeinsam erstellen/überarbeiten** | Folie 6 und Ergebnisse auf Folie 12 | `Expose_v0.1.md` ist ein Entwurf und wurde auf Vergleichsscope/Rollen angepasst | **Arbeitsstand vorhanden; gemeinsame Durchführung bleibt nicht belegt.** Weitere Überarbeitung ist bis zum Scope-Freeze vorgesehen. |
| **Vortragsthemen auswählen** | Folie 7; Festlegung 25.11. | Repo-Aufteilung wurde auf Architektur, Automatisierung, Qualitätsmerkmale, Zukunft/DDS-spezifisch umgestellt | **Festgelegt** nach Orga-Präsentation und Nutzerbestätigung. |
| **Reihenfolge und Diskussionsformat festlegen** | Folie 8 | `Agenda_80min.md` enthält den Ablauf „alle Vorträge, dann Diskussion“ nur als Vorschlag; Einzel-Diskussion bleibt Alternative | **Offen.** Noch keine Auswahl zwischen gemeinsamem Diskussionsblock und Diskussion nach jedem Beitrag dokumentiert. |
| **Rollen zuteilen** | Folie 9; Festlegung 25.11. | `Timeline.md`, `Expose_v0.1.md`, `Agent.md` führen die bestätigten Themenpakete | **Festgelegt:** A=Architektur (inkl. Integration/Abgabe), B=Automatisierung, C=Qualitätsmerkmale, D=Zukunft/DDS-spezifisch. |
| **Zeitplan übernehmen oder ändern** | Folie 10; Festlegung 25.11. | `Timeline.md`-Gantt als interner Basisplan übernommen | **Übernommen.** Vergangene interne Termine sind auf Status zu prüfen; die Präsentation belegt nicht, welche bereits erledigt wurden. Kurs-Abgabe/Vortrag bleiben feste externe Termine. |
| **Werkzeuge und Abstimmung organisieren** | Folien 11–12 | Repo beschreibt Git-Arbeitsweise; Teams-Gruppe/Teamkanäle sind noch nicht als eingerichtet dokumentiert | **Offen / nicht protokolliert.** Die Folie enthält einen Ergebnisansatz zur Teams-Gruppe; Einrichtung und Abstimmungsregeln müssen bestätigt werden. |
| **Kontakt zum Professor / Rückmeldung an Repo-Verantwortliche klären** | Folien 11–12 | `Timeline.md`/`Agent.md` enthalten noch keine dokumentierte Kontaktentscheidung oder Antwort | **Offen / nicht protokolliert.** Zuständigkeit und tatsächliche Anfrage/Antwort sind festzuhalten. |

## Konsequenz für die Repo-Arbeitspakete

1. **Hauptbeispiel auswählen:** Vergleich Assembly vs. AMR anhand der vier Rollenpakete abschließen; UMAA bleibt ein kurzer Transfer.
2. **Diskussionsformat abstimmen:** gemeinsame Diskussion laut Folie 8 ist noch Vorschlag.
3. **Zeitplan-Status nachführen:** übernommene Gantt-Termine beibehalten und bei vergangenen Sollterminen Erledigungs-/Verschiebungsstatus dokumentieren.
4. **Tools und Professor-Kontakt klären:** Einrichtung der Teams-Gruppe sowie Kontaktzuständigkeit/Antwort protokollieren.

## Quellen- und Aussagehinweis

- Deck-Fundstellen sind nach Foliennummer angegeben. Folien 4, 6, 8, 10 und 11 sind überwiegend Fragen/Optionen; Folie 12 ist nur teilweise ausgefüllt.
- Der aktuelle Repo-Arbeitsstand folgt der Orga-Präsentation und der Festlegung vom 25.11.: Assembly vs. AMR vergleichen, UMAA als Transfer; Auswahl des Hauptbeispiels noch offen.
- Personenbezogene Namen aus der Präsentation werden in diesem Abgleich nicht wiederholt.
