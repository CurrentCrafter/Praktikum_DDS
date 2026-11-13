# Variante A — Architektur v0.1: DDS im automatisierten Krankenhaus

**Status:** erster Mermaid-Entwurf, nicht final  
**Grundlage:** `01_plan/Projektvarianten.md`, Variante A  
**Domäne:** automatisiertes Krankenhaus (Vitaldaten, Alarme, Geräteintegration)  
**Ziel:** Architekturstruktur für den Seminarvortrag und die schriftlichen Unterlagen

> **Hinweis:** Die Diagramme sind bewusst als erste Struktur angelegt. QoS-Werte, Sicherheitsdetails und die HL7/FHIR-Abgrenzung sind noch zu validieren.

---

## 1. Annahmen

- DDS ist die Kommunikationsschicht; es gibt **keinen zentralen Broker**.
- Klinische Domains sind logisch getrennt: `clinic.core`, `ward.icu`, `ward.normal`, `building.technical`.
- Patientendaten verlassen die klinische Domain nicht; Gebäudetelemetrie ist getrennt.
- Die Demo zeigt nur einen Ausschnitt (Vitaldaten + Alarm), nicht das gesamte Krankenhaus.

---

## 2. Kontext- und Komponentensicht

```mermaid
flowchart TB
    subgraph BEDSIDE["Bedside / Station"]
        VM["Vitalmonitor<br/>publiziert VitalSigns"]
        IP["Infusionspumpe<br/>DeviceStatus / ControlCommand"]
        BD["Bettdisplay<br/>liest VitalSigns + Alarm"]
    end

    subgraph CORE["Klinische Kern-Domain clinic.core"]
        AS["Alarm-Server<br/>liest VitalSigns<br/>publiziert Alarm"]
        CS["Therapie-Service<br/>DeviceStatus / ControlCommand"]
        GW["Klinik-Gateway<br/>HIS-/Archiv-Anbindung"]
    end

    subgraph MOBILE["Mobiles Endgerät"]
        DA["Arzt-App<br/>liest Alarm + VitalSigns"]
    end

    subgraph DDS["DDS Global Data Space"]
        TV[("VitalSigns<br/>Key: patient_id")]
        TA[("Alarm<br/>Key: alarm_id")]
        TS[("DeviceStatus<br/>Key: device_id")]
        TC[("ControlCommand<br/>Key: device_id")]
    end

    VM -->|publish| TV
    BD -->|subscribe| TV
    AS -->|subscribe| TV
    DA -->|subscribe| TV

    AS -->|publish| TA
    BD -->|subscribe| TA
    DA -->|subscribe| TA

    IP -->|publish| TS
    CS -->|subscribe| TS
    GW -->|subscribe| TS

    CS -->|publish| TC
    IP -->|subscribe| TC
```

**Lesart:** Die Anwendungen kennen nur Topics und QoS, nicht die Netzwerkadressen der anderen Teilnehmer. Domains/Partitions begrenzen die Sichtbarkeit; DDS Discovery verbindet passende Writer und Reader.

---

## 3. DDS-Grundmodell im Beispiel

```mermaid
flowchart LR
    DP["DomainParticipant<br/>clinic.core"] --> PUB["Publisher"]
    DP --> SUB["Subscriber"]
    DP --> TOPIC["Topic VitalSigns"]

    PUB --> DW["DataWriter für VitalSigns"]
    SUB --> DR["DataReader für VitalSigns"]

    DW --> TOPIC
    DR --> TOPIC
```

Das Modell wiederholt sich für `Alarm`, `DeviceStatus` und `ControlCommand`. Jede Entität besitzt eine QoS-Konfiguration; Writer und Reader müssen im RxO-Matching kompatibel sein.

---

## 4. QoS-Zuordnung

| Topic | Key | Ziel-QoS | Begründung |
|---|---|---|---|
| `VitalSigns` | `patient_id` | Reliable, KeepLast(1–5), Deadline 100 ms | Messwerte müssen ankommen; kurze Historie für späte Reader |
| `Alarm` | `alarm_id` | Reliable, TransientLocal, Deadline 50 ms, Liveliness | Alarme dürfen nicht verloren gehen; späte Teilnehmer sehen den letzten Alarm |
| `DeviceStatus` | `device_id` | BestEffort, KeepLast(1) | Status ist schnell ersetzbar |
| `ControlCommand` | `device_id` | Reliable, Lifespan, Ownership | Befehle brauchen Eindeutigkeit und Verfallszeit |

> Die Werte sind **Zielwerte für die Diskussion**, keine gemessenen Garantien.

---

## 5. Deployment-Sicht

```mermaid
flowchart TB
    subgraph WARD["Station / Bett"]
        VM["Vitalmonitor<br/>Embedded Linux"]
        IP["Infusionspumpe<br/>RTOS"]
        BD["Bettdisplay<br/>Linux"]
    end

    subgraph EDGE["Station-Edge"]
        EG["Edge-Gateway<br/>Linux<br/>Filter / Puffer"]
    end

    subgraph DC["Klinik-Rechenzentrum"]
        AS["Alarm-Server"]
        HIS["HIS / Archiv"]
    end

    subgraph NET["Klinik-LAN"]
        LAN["VLAN / QoS<br/>UDP / Multicast"]
    end

    VM --- LAN
    IP --- LAN
    BD --- LAN
    EG --- LAN
    LAN --- AS
    AS --- HIS
    EG -.->|"clinic.core / ward.icu"| AS
```

**Anmerkung:** Das Edge-Gateway bündelt und filtert Daten, ersetzt aber nicht die DDS-Domains. Die Domain-/Partition-Struktur bleibt die primäre Isolationsgrenze.

---

## 6. Sequenz: Vitaldaten und Alarm

```mermaid
sequenceDiagram
    autonumber
    participant VM as Vitalmonitor
    participant DDS as DDS/RTPS
    participant AS as Alarm-Server
    participant BD as Bettdisplay
    participant DA as Arzt-App

    VM->>DDS: SPDP Announce
    AS->>DDS: SPDP Announce
    DDS-->>VM: Match (SEDP)
    DDS-->>AS: Match (SEDP)

    VM->>DDS: write(VitalSigns)
    DDS-->>AS: VitalSigns (Reliable)
    DDS-->>BD: VitalSigns
    DDS-->>DA: VitalSigns

    AS->>AS: Grenzwert prüfen
    AS->>DDS: write(Alarm, TransientLocal)
    DDS-->>BD: Alarm
    DDS-->>DA: Alarm
    Note over DDS: Später startender Reader<br/>erhält den letzten Alarm
```

---

## 7. Security-Skizze

```mermaid
flowchart LR
    subgraph CLINIC["Klinische Domain"]
        P1["Participant<br/>Monitor"]
        P2["Participant<br/>Alarm-Server"]
    end

    subgraph SEC["DDS Security"]
        AUTH["Authentication"]
        ACL["Access Control"]
        CRYPTO["Cryptography"]
        LOG["Logging"]
    end

    P1 --> AUTH
    P2 --> AUTH
    AUTH --> ACL
    ACL --> CRYPTO
    CRYPTO --> LOG
```

**Threat-Szenario:** Ein fremder Participant gibt sich als Monitor aus und publiziert falsche `VitalSigns`. Authentication und Access Control verhindern die Teilnahme; Encryption schützt vertrauliche Daten; Logging macht Zugriffe nachvollziehbar.

**Grenze:** DDS Security ersetzt keine klinische Zertifizierung und keine Datenschutz-Folgenabschätzung.

---

## 8. Offene Punkte für v0.2

- Genaue Domain-/Partition-Aufteilung (Station vs. Klinik vs. Gebäude).
- QoS-Werte mit dem Team validieren; Deadline/Liveliness begründen.
- HL7/FHIR-Abgrenzung: Wo endet DDS, wo beginnt klinische Interoperabilität?
- Security: PKI, Zertifikatsverteilung, Schlüsselmanagement, Audit.
- Deployment: konkrete Geräte, RTOS-Annahmen, Netzsegmente.
- Demo: nur `VitalSigns` + `Alarm` oder zusätzlich `DeviceStatus`?
