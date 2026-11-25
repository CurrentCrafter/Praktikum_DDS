# Fragenbank — Architekturrolle A

**Stand:** 25.11.2026  
**Scope:** Assembly-Zelle vs. AMR-Flotte vergleichen; UMAA als kurzer Transferfall

Die Fragen dienen der Vorbereitung auf die Diskussion nach Rolle A. Die Antwortlinien grenzen belegte Aussagen, eigene Architekturannahmen und offene Punkte voneinander ab.

## Scope und Belege

1. **Belegt die Wikipedia-Liste den DDS-Einsatz in jedem genannten Bereich?**  
   Nein. Sie ist ein Einstieg in mögliche Anwendungsfelder, aber kein Beleg für ein konkretes System. UMAA wird anhand der öffentlichen UMAA-Beschreibung und Compliance-Unterlagen belegt. Assembly-Zelle und AMR-Flotte sind unsere Vergleichskandidaten; welche wir vollständig ausarbeiten, ist noch zu begründen.

2. **Ist UMAA ein konkretes DDS-Beispiel oder nur eine Analogie?**  
   Die öffentliche UMAA-Beschreibung sagt ausdrücklich, dass OMG DDS ein Kernbestandteil der Architektur für die Kommunikation der Autonomiekomponenten an Bord ist. UMAA ist ein kurzer Transfer über den Fertigungskontext hinaus, keine dritte vollständige Fallarchitektur und kein Gegenbeispiel gegen DDS. Daraus folgt keine Gleichheit der Datenmodelle oder QoS-Konfigurationen.

3. **Warum vergleichen wir Assembly-Zelle und AMR-Flotte?**  
   Beide passen zum Automatisierungsbezug des Seminars, setzen aber unterschiedliche Schwerpunkte. Die Rollen bewerten sie anhand Architektur, Automatisierungsanforderungen, Qualitätsmerkmalen und DDS-spezifischen Zukunftsaspekten. Erst diese Belege sollen die Wahl des Hauptbeispiels begründen.

4. **Welche Rolle hat UMAA im Vortrag?**  
   UMAA ist ein kurzer, belegter Transferfall: DDS wird auch in einer modularen maritimen Autonomiearchitektur genutzt. Der Vortrag vergleicht nicht die operative UMAA-Architektur mit Assembly/AMR und leitet daraus keine universelle Eignung ab.

## DDS-Architektur und Grenzen

5. **Ist DDS selbst ein zentraler Datenraum oder Server?**  
   Nein. „Global Data Space“ bezeichnet das logische Datenmodell. Topics sind keine zentralen Speicherobjekte. Discovery, Transport und konkrete Teilnehmerstruktur hängen von DDS-Spezifikation, Implementierung und Konfiguration ab.

6. **Ist ein fachlicher Baustein automatisch ein `DomainParticipant`?**  
   Nein. Fachliche Komponenten, Betriebssystemprozesse und DDS-`DomainParticipant`s sind unterschiedliche Sichten. Die Zuordnung muss für den gewählten Kandidaten im Deployment begründet werden.

7. **Garantiert DDS harte Echtzeit oder eine bestimmte Latenz?**  
   Nein. DDS stellt QoS-Mechanismen bereit, aber Ende-zu-Ende-Fristen hängen auch von Anwendung, Betriebssystem, Middleware-Konfiguration, Ressourcen und Netz ab. Zielwerte werden nicht als Messwerte oder Garantie ausgegeben.

8. **Ist `RELIABLE` gleichbedeutend mit „rechtzeitig angekommen und korrekt verarbeitet“?**  
   Nein. `RELIABLE` betrifft die zuverlässige Übermittlung im Rahmen der DDS-/RTPS-Mechanismen. Rechtzeitigkeit, fachliche Gültigkeit und Verarbeitung sind separate Eigenschaften.

9. **Ist Safety-Kommunikation Teil des dargestellten DDS-Datenflusses?**  
   Nein. Die Safety-Funktion ist separat abgegrenzt. DDS Security ist keine funktionale Safety-Zertifizierung. Falls später ein Diagnose- oder Betriebsstatus über DDS verteilt wird, darf er nicht mit dem sicherheitsgerichteten Pfad verwechselt werden.

10. **Ist MES ein direkter DDS-Teilnehmer?**  
    Nicht in der aktuellen Assembly-Kandidatenskizze. Der MES-Übergang liegt außerhalb der Zell-DDS-Domain und endet am Edge-Gateway. Ob dort ein separates DDS-Netz oder ein anderes Protokoll genutzt wird, ist noch festzulegen; bei Auswahl der AMR-Flotte wird diese Frage durch deren Systemgrenze ersetzt.

11. **Warum ist das Edge-Gateway nicht gleichzeitig Subscriber und Publisher desselben Telemetry-Topics?**  
    Das wäre ohne definierte Transformations- und Topic-Grenze mehrdeutig und könnte Schleifen erzeugen. Die überarbeitete Skizze trennt `DeviceTelemetry` innerhalb der Zelle von einer externen `CellSummary`-Übergabe am Edge.

12. **Macht ein TSN-Switch den DDS-Datenpfad automatisch deterministisch?**  
    Nein. TSN und DDS wirken auf unterschiedlichen Ebenen und müssen gemeinsam, aber getrennt, mit Traffic-Klassen und Zeitbudgets begründet werden. Die Deployment-Skizze kennzeichnet TSN daher als optional und noch zu validieren.

13. **Verhindert DDS Security auch falsche, aber autorisierte Daten?**  
    Nicht automatisch. Authentisierung, Zugriffskontrolle, Kryptografie und Logging adressieren definierte Cybersecurity-Bedrohungen. Ein kompromittierter autorisierter Publisher oder fachlich unplausibles Sample benötigt zusätzliche Maßnahmen auf System- und Anwendungsebene.

## Quellen für die Antwortlinien

- OMG, **Data Distribution Service (DDS), Version 1.4**: <https://www.omg.org/spec/DDS/1.4/PDF>.
- OMG, **DDS Interoperability Wire Protocol (DDSI-RTPS), Version 2.5**: <https://www.omg.org/spec/DDSI-RTPS/2.5/PDF>.
- AUVSI, **Unmanned Maritime Autonomy Architecture (UMAA)**: <https://www.auvsi.org/advocacy/advocacy-initiatives/unmanned-maritime-autonomy-architecture/>.
- NAVSEA, **UMAA Compliance Specification, T0300-BE-IDS-010 Rev. 1**, 30.07.2024: <https://www.auvsi.org/wp-content/uploads/2025/03/T0300-BE-IDS-010-Rev.-1.pdf>.

## Noch zu ergänzen

- Fundstellen/Abschnitte und Seitenzahlen für die OMG- und UMAA-Dokumente im Quellenregister.
- Zusätzliche Fragen nach der Fallauswahl und sobald Teilnehmerliste, Systemgrenze und Topic-Mapping feststehen.
