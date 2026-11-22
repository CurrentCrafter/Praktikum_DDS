# DDS — Scope-Entscheidung und Härtungsfragen

## AP1: Beschlossener Scope

- **Erklärgegenstand:** DDS-Referenzarchitektur (insbesondere DCPS, DDS-Entities, Topics, QoS, Discovery und RTPS) plus ihre Abbildung auf ein konkretes Anwendungsszenario.
- **Hauptbeispiel:** modulare Roboter-Assembly-Zelle.
- **Transferfall:** UMAA als modulare Softwarearchitektur für unbemannte maritime Fahrzeuge; DDS dient laut öffentlicher UMAA-Beschreibung als Kernmechanismus für die Kommunikation zwischen Autonomie-Komponenten an Bord.
- **Nicht im Vortrag:** Krankenhaus und autonomes Fahren. Die Krankenhausdatei bleibt nur als ausgeschlossener älterer Entwurf erhalten.
- **Umfang:** Die Assembly-Zelle erhält die vollständige Komponenten-/Datenfluss- und DDS-Entity-Abbildung. UMAA wird nur als knapper Transferbeleg verwendet, nicht als zweite Architektur.

## Architektur- und Professorfragen mit belastbarer Antwortlinie

### Scope und Belege

1. **Belegt die Wikipedia-Liste den DDS-Einsatz in jedem genannten Bereich?**  
   Nein. Sie ist ein Einstieg in mögliche Anwendungsfelder, aber kein Beleg für ein konkretes System. UMAA wird anhand der öffentlichen UMAA-Beschreibung und Compliance-Unterlagen belegt; die Assembly-Zelle ist ausdrücklich ein eigenes Referenzszenario.

2. **Ist UMAA ein konkretes DDS-Beispiel oder nur eine Analogie?**  
   Die öffentliche UMAA-Beschreibung sagt ausdrücklich, dass OMG DDS ein Kernbestandteil der Architektur für die Kommunikation der Autonomiekomponenten an Bord ist. Die Übertragung auf unsere Zelle ist eine Analogie auf Architekturebene; daraus folgt keine Gleichheit der Datenmodelle oder QoS-Konfigurationen.

3. **Warum UMAA nur als Transferfall und nicht als Hauptarchitektur?**  
   Die Assembly-Zelle passt direkter zum Seminarfokus Smart Factory/Motion Control und ermöglicht eine vollständige, nachvollziehbare Zuordnung der DDS-Begriffe. UMAA zeigt knapp, dass das Architekturprinzip auch außerhalb der Fabrikautomation relevant ist. Öffentliche Dokumente belegen nicht alle Implementierungsdetails eines konkreten Fahrzeugs.

4. **Warum Krankenhaus und autonomes Fahren nicht mehr?**  
   Sie gehören nicht zum beschlossenen Scope. Das Krankenhaus wäre zusätzlich stark legacy-nah und würde klinische Interoperabilität, Datenschutz und Medizinprodukt-Safety in den Vordergrund rücken. Autonomes Fahren würde eine weitere vollständige Architektur und die Abgrenzung ROS 2/DDS erfordern. Beide würden den Architekturteil verbreitern, ohne die gewählte Leitfrage besser zu beantworten.

### DDS-Architektur und Grenzen

5. **Ist DDS selbst ein zentraler Datenraum oder Server?**  
   Nein. „Global Data Space“ bezeichnet das logische Datenmodell. Topics sind keine zentralen Speicherobjekte. Discovery, Transport und konkrete Teilnehmerstruktur hängen von DDS-Spezifikation, Implementierung und Konfiguration ab.

6. **Ist ein fachlicher Zellbaustein automatisch ein `DomainParticipant`?**  
   Nein. Fachliche Komponenten, Betriebssystemprozesse und DDS-`DomainParticipant`s sind unterschiedliche Sichten. Die Zuordnung muss im Deployment begründet werden und bleibt für die AP2-Komponenten-/Teilnehmerliste offen.

7. **Garantiert DDS harte Echtzeit oder eine bestimmte Latenz?**  
   Nein. DDS stellt QoS-Mechanismen bereit, aber Ende-zu-Ende-Fristen hängen auch von Anwendung, Betriebssystem, Middleware-Konfiguration, Ressourcen und Netz ab. Zielwerte werden nicht als Messwerte oder Garantie ausgegeben.

8. **Ist `RELIABLE` gleichbedeutend mit „rechtzeitig angekommen und korrekt verarbeitet“?**  
   Nein. `RELIABLE` betrifft die zuverlässige Übermittlung im Rahmen der DDS-/RTPS-Mechanismen. Rechtzeitigkeit, fachliche Gültigkeit und Verarbeitung sind separate Eigenschaften.

9. **Ist Safety-Kommunikation Teil des dargestellten DDS-Datenflusses?**  
   Nein. Die Safety-Funktion ist separat abgegrenzt. DDS Security ist keine funktionale Safety-Zertifizierung. Falls später ein Diagnose- oder Betriebsstatus über DDS verteilt wird, darf er nicht mit dem sicherheitsgerichteten Pfad verwechselt werden.

10. **Ist MES ein direkter DDS-Teilnehmer?**  
    Nicht in der AP1-Skizze. Der MES-Übergang liegt außerhalb der Zell-DDS-Domain und endet am Edge-Gateway. Ob dort ein separates DDS-Netz oder ein anderes Protokoll genutzt wird, ist eine spätere Architekturentscheidung, keine bereits belegte Tatsache.

11. **Warum ist das Edge-Gateway nicht gleichzeitig Subscriber und Publisher desselben Telemetry-Topics?**  
    Das wäre ohne definierte Transformations- und Topic-Grenze mehrdeutig und könnte Schleifen erzeugen. Die überarbeitete Skizze trennt `DeviceTelemetry` innerhalb der Zelle von einer externen `CellSummary`-Übergabe am Edge.

12. **Macht ein TSN-Switch den DDS-Datenpfad automatisch deterministisch?**  
    Nein. TSN und DDS wirken auf unterschiedlichen Ebenen und müssen gemeinsam, aber getrennt, mit Traffic-Klassen und Zeitbudgets begründet werden. Die vorhandene Deployment-Skizze kennzeichnet TSN daher als optional und noch zu validieren.

13. **Verhindert DDS Security auch falsche, aber autorisierte Daten?**  
    Nicht automatisch. Authentisierung, Zugriffskontrolle, Kryptografie und Logging adressieren definierte Cybersecurity-Bedrohungen. Ein kompromittierter autorisierter Publisher oder fachlich unplausibles Sample benötigt zusätzliche Maßnahmen auf System- und Anwendungsebene.

## Noch offene Folgearbeit

- Teilnehmer-/Prozessliste und MES-Grenze in AP2 endgültig abstimmen.
- Topic-Mapping mit Verantwortlichkeit, Typ, Key und Leser/Schreiber belegen.
- UMAA-Quellen für den Vortrag präzise nach Dokument, Version und Fundstelle erfassen.
- QoS-Zielwerte, TSN-Annahmen und Implementierungsdetails gegen Primärquellen bzw. Messungen prüfen.
