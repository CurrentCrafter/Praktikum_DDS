# DDS — Vergleichsauftrag und offene Folgearbeit

## AP1: Beschlossene Vergleichsaufgabe

- **Erklärgegenstand:** DDS-Referenzarchitektur (insbesondere DCPS, DDS-Entities, Topics, QoS, Discovery und RTPS) plus ihre Abbildung auf ein konkretes Anwendungsszenario.
- **Vergleichskandidaten:** modulare Roboter-Assembly-Zelle und AMR-Flotte. Alle Rollen prüfen beide Kandidaten anhand ihres Arbeitspakets; die Auswahl des einen vollständig auszuarbeitenden Hauptbeispiels steht noch aus.
- **Transferfall:** UMAA als modulare Softwarearchitektur für unbemannte maritime Fahrzeuge; DDS dient laut öffentlicher UMAA-Beschreibung als Kernmechanismus für die Kommunikation zwischen Autonomie-Komponenten an Bord. UMAA ist ein kurzer Transfer, kein Gegenbeispiel zu DDS und keine dritte Vollarchitektur.
- **Nicht als Fallarchitektur ausarbeiten:** Krankenhaus und Hausautomation; autonomes Straßenfahren bleibt außerhalb des Umfangs. AMR-Flotte ist der bestätigte Vergleichskandidat und nicht mit autonomem Straßenfahren gleichzusetzen.
- **Umfang:** Nach der begründeten Kandidatenwahl erhält der gewählte Fall die vollständige Komponenten-/Datenfluss- und DDS-Entity-Abbildung.
- **AMR-Umsetzungsprofil:** direkte native DDS-API ohne ROS 2; konkrete DDS-Implementierung (z. B. Fast DDS oder Cyclone DDS) bleibt offen.
- **Lizenzanforderung:** FOSS. Fast DDS Community (Apache-2.0) und Eclipse Cyclone DDS (EPL-2.0/EDL-1.0) sind Kandidaten; konkrete Versionen und transitive Abhängigkeiten vor der Weiterverwendung prüfen.

## Offene Folgearbeit

- Vergleichskriterien und begründete Auswahl Assembly-Zelle vs. AMR-Flotte bis zum Scope-Freeze festhalten.
- Für den gewählten Fall Teilnehmer-/Prozessliste und Systemgrenze festlegen.
- AMR-Kandidatenarchitektur in [`03_architektur/Variante_C_AMR_Flotte_Architektur_v0.1.md`](03_architektur/Variante_C_AMR_Flotte_Architektur_v0.1.md) gegen die vier Arbeitspakete prüfen.
- Topic-Mapping mit Verantwortlichkeit, Typ, Key und Leser/Schreiber belegen.
- UMAA-Quellen für den Vortrag präzise nach Dokument, Version und Fundstelle erfassen.
- QoS-Zielwerte, TSN-Annahmen und Implementierungsdetails gegen Primärquellen bzw. Messungen prüfen.
