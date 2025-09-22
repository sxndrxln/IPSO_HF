
# Zusammenfassung IT Service Level Management (SLA/OLA/UC)

## 1. SLA/OLA/UC

Die Unterscheidung zwischen Service Level Agreement (SLA), Operational Level Agreement (OLA) und Underpinning Contract (UC) ist grundlegend für das **SOUSIS-Modell**.

### SLA (Service Level Agreement)
Ein SLA regelt alle Serviceverpflichtungen gegenüber den **Kunden**. Es ist eine Vereinbarung zwischen Kunde und Provider über die Serviceerbringung.

*   **Zweck:** Standardisierung und Messung der Qualität von IT-Services und Nachweis der zugesicherten Leistung.
*   **Prozess:** Der SLA-Prozess ist verantwortlich für den Entwurf, die Abstimmung, die Überwachung, das Reporting und die Reviews der IT-Services.

### OLA (Operational Level Agreement)
Ein OLA ist eine nach innen gerichtete Vereinbarung zwischen internen Fachbereichen oder Organisationseinheiten der IT-Organisation.

*   **Zweck:** Regelt die Erstellung und Erbringung eines **Teilservices** zur Erfüllung eines SLA.
*   **Rechtliches:** Interne Vereinbarungen in Form eines OLA enthalten **keinen juristischen Anteil**.
*   **Bedeutung:** Die extern vereinbarte Leistung (z.B. Verfügbarkeit) kann niemals höher sein als die intern erzeugte Leistung, weshalb OLAs das SLA massgeblich beeinflussen.

### UC (Underpinning Contract)
Ein UC ist eine extern gerichtete Vereinbarung mit **dritten Parteien** (externen Dienstleistern/Lieferanten).

*   **Zweck:** Definiert die Lieferung von Services als Teilerbringung eines SLA gegenüber dem Kunden.
*   **Rechtliches:** UCs sind Vertragswerke, die einen **rechtswirksamen Anteil** besitzen.
*   **Sicht des Lieferanten:** Aus Sicht des Contractors (Lieferanten) ist der Underpinning Contract selbst ein SLA.

**Wichtig:** OLA und UC müssen mit den Anforderungen des SLA abgestimmt sein.

## 2. Vorteil und Risiken eines SLA

### Vorteile und Zweck
SLAs sind unabdingbare Werkzeuge, um die **IT stärker auf die Geschäftsanforderungen auszurichten**.

*   Sie erhöhen die **Kundenorientierung**.
*   Sie dienen zur Standardisierung, Messung der Qualität und Nachweis der zugesicherten Leistung.
*   Sie dienen zur Schliessung von Lücken in den Informatikleistungen.
*   Sie stellen sicher, dass einheitliche Geschäftsprozesse für alle Servicenehmer gelten, was die Individualität reduziert und die **Kosten tief hält**.

### Risiken
Während Services die Risiken für das Geschäft des Kunden reduzieren, **erhöhen sie gleichzeitig die Risiken für den Service Provider**.

*   Der Service Provider muss sicherstellen, dass seine Kosten gedeckt werden, und gleichzeitig die Preisgestaltung beachten.
*   Das Risikomanagement muss angewandt werden, um Risiken für die **Lifecycle-Phasen** (einschliesslich der Service Pipeline und des Servicekatalogs) zu erkennen und zu reduzieren.
*   Bei Ausfall oder Teilausfall eines Services (Verletzung des SLA) muss eine **Auswirkungsanalyse (Impact Analyse)** durchgeführt werden, um festzustellen, welche Geschäftsprozesse betroffen sind und wie stark.

## 3. Was fehlt in einem vorgegebenen SLA

Ein SLA, das sich nur auf Service-Level-Kennzahlen beschränkt, ist typischerweise unvollständig und benötigt ergänzende Parameter.

### Service übergreifende Aspekte (Teil des SLA)
Diese Aspekte regeln die Rahmenbedingungen, die für alle Services gelten und müssen im SLA aufgeführt werden:

*   **Servicezeiten**.
*   **Wartungsfenster**.
*   **Service Desk-Betrieb**.
*   Übergreifende Kennzahlen.
*   Organisation und Eskalationen.
*   Geltungsbereich.
*   Reporting (Berichtswesen).
*   **Bonus/Malus** Regelungen.

### Juristische Aspekte (Teil des IT-Rahmenvertrags)
Diese Rahmenbedingungen regeln die Geschäftsbeziehung und sind oft im übergeordneten IT-Rahmenvertrag festgelegt:

*   Vertragsgegenstand und Vertragspartner.
*   **Haftung** und Gewährleistung.
*   Umgang mit Bonus/Malus.
*   Beginn, Dauer, Kündigung und Übergangsregelungen.
*   Datenschutz, geistiges Eigentum und Umgang mit Lizenzen.
*   **Mitwirkungspflichten** des Servicenehmers.

## 4. Elemente einer Servicebeschreibung

Die Servicebeschreibung ist im **Servicekatalog** dokumentiert und enthält typischerweise folgende Attribute (im Kontext des SOUSIS-Modells):

*   **Nummer**.
*   **Bezeichnung**.
*   **Servicekategorie** (Gruppierung in logische Einheiten).
*   **Kurzbeschreibung (Text)** (Definition des IT-Service).
*   **Enthalten** (Aufzählung der Leistungen).
*   **Nicht enthalten** (Aufzählung von Ausschlüssen).
*   **Service Level** (Kennzahl/en).
*   **Betrieb** (Störungspriorität/Kritikalität).
*   **Preis**.

Zusätzlich kann die **Serviceklasse** (z.B. Gold, Silber, Bronze) und die **Serviceüberwachung** (Monitoring und Reporting) festgelegt werden.

## 5. Vor- und Nachteile von Penaltys in SLA (Bonus/Malus)

Der Bonus/Malus-Mechanismus ist die **Spezifikation von Konsequenzen** bei Abweichungen (positiv oder negativ) von den vereinbarten Service-Level-Soll-Werten.

*   **Malus (Penalty):** Konsequenzen bei der Verletzung eines Service-Levels, z.B. eine **finanzielle Entschädigung**.
*   **Bonus:** Konsequenzen bei der Übererfüllung eines Service-Levels, z.B. eine **Kostensenkung**.

### Vorteile (Funktion)
*   Schafft **Verbindlichkeit** und ist ein zentrales Instrument zur **Kontrolle der Leistungsvereinbarungen**.
*   Dient der Kompensation bzw. der **Übertragung von Risiken** zwischen Provider und Kunde.

### Hinweise zur Umsetzung
Die Regelungen zum Umgang mit Bonus/Malus müssen im **IT-Rahmenvertrag** festgehalten werden.

*(Die bereitgestellten Quellen führen keine expliziten Nachteile des Bonus/Malus-Systems auf, definieren es jedoch als Konsequenzregelung bei Abweichungen).*

## 6. Verfügbarkeitsberechnung

Die Verfügbarkeit ist eine der wichtigsten Servicekennzahlen und wird mittels des **Service-Level-Kalkulators** (Teil des SOUSIS-Modells) berechnet.

### Grundformel der Verfügbarkeit (in Prozent)
Die Berechnung berücksichtigt die Gesamtzeit (Monat), geplante Unterbrechungen (Wartungsfenster) und ungeplante Nichtverfügbarkeit (Ausfall):

$$ \text{Verfügbarkeit} = \frac{(\text{T}_{\text{Monat}} - \text{T}_{\text{Wartungsfenster}}) - \text{T}_{\text{Nichtverfügbar}}}{(\text{T}_{\text{Monat}} - \text{T}_{\text{Wartungsfenster}})} \times 100 $$

**Beispiel für einen 24/7 Betrieb**:
*   Monatliche Gesamtzeit ($\text{T}_{\text{Monat}}$) = 720 Stunden
*   Geplante Unterbrechung ($\text{T}_{\text{Wartungsfenster}}$) = 6 Stunden
*   Ausfallzeit ($\text{T}_{\text{Nichtverfügbar}}$) = 2 Stunden
*   *Berechnung:* $(720 \text{ Std} - 6 \text{ Std}) - 2 \text{ Std} / (720 \text{ Std} - 6 \text{ Std}) \times 100 = 99.71\%$.

### End-to-End Verfügbarkeit (Kundensicht)
Für den Kunden ist die End-to-End-Leistung des Services relevant, welche die Verfügbarkeit aller Teilkomponenten berücksichtigt.

#### Ohne Redundanz (Kausalkette)
Wenn Komponenten kausal voneinander abhängen, wird die Gesamtverfügbarkeit durch **Multiplikation der Einzelverfügbarkeitsprozentsätze** berechnet.

*   *Beispiel:* System 1 (0.98) * System 2 (0.94) * Netzwerk 1 (0.99) * Netzwerk 2 (0.99) * System 3 (0.98) = **0.88**.

#### Mit Redundanz
Bei redundanten Systemen ändert sich die Berechnung.

*   *Beispiel (Redundanz System 1):* $1 - (1 - 0.98) \times (1 - 0.98) = 0.9996$.
*   *Gesamtverfügbarkeit mit Redundanz System 1 und 2:* $0.9996 \times 0.9964 \times 0.99 \times 0.99 \times 0.98 = 0.9567$.

### Weitere Kenngrössen der Verfügbarkeit
*   **MTTF** (Mean Time to Failure): Mittlere erwartete Zeit bis zum nächsten Ausfall.
*   **MTBF** (Mean Time between Failure): Mittlere Betriebszeit bis zum nächsten Ausfall.
*   **MTTR** (Mean Time to Recover): Mittlere Zeit der Servicewiederherstellung.