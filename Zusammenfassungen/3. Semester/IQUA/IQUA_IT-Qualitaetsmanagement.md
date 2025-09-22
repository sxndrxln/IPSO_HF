# Zusammenfassung für die Prüfung: IT Qualitätsmanagement und DevOps

### **I. DevOps: Grundlagen und Motivation**

DevOps ist ein **neuer Ansatz** zur schnellen und effizienten Bereitstellung von IT-Lösungen. Die Motivation dafür liegt in der **volatilen Geschäftswelt**, die schnelle Ideen erfordert, und dem **signifikanten Kostendruck in der IT**. Die Anwendung von DevOps kann zu einer **Kostenreduktion von 10-20%** und einer **massiven Verkürzung der Zeit bis zum Einsatz des Systems** führen.

**Unterschied zum klassischen Ansatz:**
*   **Klassische Wasserfallmodelle** (wie z.B. das HERMES-Modell) umfassen Phasen wie Voranalyse, Konzept und Realisation. Dabei vergeht eine **relativ lange Zeit, in welcher der Kunde sein Produkt nicht sieht**. Korrekturen von Abweichungen in späten Phasen sind sehr teuer.
*   **Iterative Modelle (Agil)** stellen den **Einbezug des Kunden in kurzen Zeitintervallen** sicher. Dies führt zu kleineren Rückantwortzeiten und damit geringeren Fehlerkosten.

**Die DevOps-Pipeline im Überblick:**
Die DevOps-Pipeline besteht aus einer Reihe von Schritten, die einen **kontinuierlichen Kreislauf** bilden:
*   **Plan:** Strategische und operative Planung (Business, Realisation).
*   **Code:** Realisation.
*   **Build:** "Release" abbilden.
*   **Test:** Unit-, Integration- und Abnahmetests.
*   **Release:** Iterationskontrolle.
*   **Deploy:** Ausliefern.
*   **Operate:** Verwendung.
*   **Monitor:** Überwachung und Analyse.

**Vorteile von DevOps:**
*   Regelkreise.
*   Informationsbedarf.
*   **Erkennen kritischer Elemente:** Durch Ableitung messbarer Kundenanforderungen aus Use Cases, Erstellung von Zustandsdiagrammen des Systems und Korrelation von Anforderung mit Systemzustand zur Definition von **KPIs (Key Performance Indicators)**.
*   **Beispiele:**
    *   **Netflix** verbesserte die Streaming-Qualität durch ein umfangreiches Monitoring-System (Prometheus, Grafana), um Pufferungszeiten, Ladezeiten und Videoqualität zu überwachen, was zu einer **deutlichen Reduzierung der Pufferungszeiten und verbesserter Benutzererfahrung** führte.
    *   **Airbnb** implementierte ein umfassendes Monitoring-System (Datadog, New Relic) und integrierte es in die CI/CD-Pipeline, um hohe Verfügbarkeit und Leistung auch in Spitzenzeiten zu gewährleisten und Probleme frühzeitig zu erkennen und zu beheben.

---

### **II. IT Qualitätsmanagement (QM)**

**Was ist Qualität?**
Qualität ist die **Gesamtheit aller Merkmale und Merkmalswerte eines Softwareprodukts, die sich auf die Eignung beziehen, festgelegte oder vorausgesetzte Erfordernisse zu erfüllen** (nach ISO 25010:2011).
*   **Ergebnis = Qualität:** Erfüllung der (An)-Forderung.
*   **Ergebnis = Über-Qualität:** Übertreffen der Anforderungen.
*   **Ergebnis = Unter-Qualität:** Nichterfüllung der Anforderungen.

**Was ist Qualitätsmanagement (QM)?**
QM ist ein **systematischer Ansatz zur Sicherstellung und Verbesserung der Qualität** von Produkten, Dienstleistungen und Prozessen. Es umfasst alle organisatorischen Maßnahmen, die darauf abzielen, die Anforderungen und Erwartungen der Kunden zu erfüllen oder zu übertreffen.

**Qualitätsmanagementsystem (QMS) nach ISO 9001:**
Ein QMS (z.B. nach ISO 9001) bietet Unternehmen eine **strukturierte Methode zur Qualitätssicherung**. Die **ISO 9001** ist ein internationaler Standard, der Unternehmen hilft, ihre Prozesse zu optimieren und die Kundenzufriedenheit zu steigern.
**Hauptprinzipien der ISO 9001:**
1.  **Kundenorientierung:** Die Bedürfnisse und Erwartungen der Kunden stehen im Mittelpunkt.
2.  **Führungsverantwortung:** Führungskräfte spielen eine entscheidende Rolle.
3.  **Einbeziehung der Mitarbeiter:** Alle Beteiligten tragen zur Qualitätssicherung bei.
4.  **Prozessorientierter Ansatz:** Die Organisation wird als eine Reihe von miteinander verbundenen Prozessen betrachtet.
5.  **Kontinuierliche Verbesserung:** Ständige Optimierung der Prozesse und Systeme.
6.  **Sachbezogene Entscheidungsfindung:** Entscheidungen basieren auf Daten und Fakten.
7.  **Lieferantenbeziehungen zum gegenseitigen Nutzen:** Zusammenarbeit mit Partnern zur gemeinsamen Qualitätssteigerung.
Die ISO 9001 ist für Unternehmen jeder Größe und Branche geeignet und kann zertifiziert werden. Die Kapitel der ISO 9001:2015 folgen dem **PDCA-Zyklus (Plan-Do-Check-Act)**.

**Prozesse als Grundlage des QM:**
Ein Prozess ist eine **geregelte Abfolge von Aktivitäten, welche einerseits Ressourcen konsumiert und andererseits eine Leistung erbringt**. Typisch für einen Prozess sind: geregelter Ablauf, Rückkopplung (Feedback), Ressourcen (Mensch, Kapital), Informationsaustausch und Kommunikation. Prozesse sind komplex und ein **Mehrwert** muss gegenüber dem Kunden und der Firma erzeugt werden (meist monetär).

**Teilbereiche des Qualitätsmanagements:**
*   **Strategisches QM:** Sicherstellung eines effektiven Systems der kontinuierlichen Verbesserung und Aufbau eines umfassenden Customer-Feedback-Systems (z.B. Bewertungen, Umfragen).
*   **Operatives QM:** Sicherstellen der systematischen Erfassung von Fehlern (z.B. beim Versand) und Aufbau von Messmöglichkeiten für eingekaufte Produkte.

**Qualitätssicherung:**
Qualitätssicherung ist ein Sammelbegriff für Maßnahmen zur Sicherstellung festgelegter Qualitätsanforderungen. Beispiele sind Wareneingangskontrolle, Lieferantenauswahl und -bewertung sowie Reklamationsmanagement.

---

### **III. Anforderungsmanagement**

**Arten von Anforderungen:**
*   **Funktionale Anforderungen:** Definieren, welche Dienste, Funktionen und Interaktionen das System abbilden muss (z.B. "Adresse muss überprüft werden").
*   **Nicht-funktionale Anforderungen:** Legen Qualitätsmerkmale wie Performance, Zuverlässigkeit, Usability und Sicherheit fest.
*   **Randbedingungen (Constraints):** Beschränkungen durch Technik, Gesetze, Budgets oder bestehende Systeme.
*   **Anforderungen aus Lebenszyklus:** Z.B. Migration von Daten.

**Der Kano-Prinzip:**
Das Kano-Prinzip bewertet die Kundenzufriedenheit anhand von fünf Kategorien von Kundenanforderungen:
1.  **Basisanforderungen (Must-Haves):** Selbstverständlich, Fehlen führt zu großer Unzufriedenheit, Erfüllung wird kaum bemerkt (z.B. Sicherheit bei einem Auto, funktionierende Tastatur eines Laptops).
2.  **Leistungsanforderungen (One-Dimensional Requirements):** Je mehr erfüllt, desto zufriedener der Kunde; liefern direkten Mehrwert (z.B. Benzinverbrauch eines Autos, Prozessorgeschwindigkeit eines Laptops).
3.  **Begeisterungsanforderungen (Excitement Requirements):** Werden nicht erwartet, sorgen für besondere Zufriedenheit; Überraschungen (z.B. Massagesystem im Autositz, leichtes Design eines Laptops).
4.  **Unerhebliche Anforderungen (Indifferent Requirements):** Haben kaum Einfluss auf Zufriedenheit oder Unzufriedenheit (z.B. Farbe des Autoschlüssels, Farbe des Laptops).
5.  **Rückweisungsanforderungen (Reverse Requirements):** Können Zufriedenheit verringern, wenn vorhanden (z.B. übermäßig kompliziertes Unterhaltungssystem im Auto, lauter Lüfter eines Laptops).

**Dokumentation von Anforderungen:**
*   **Lastenheft:** Beschreibt das **WAS** aus Sicht des Auftraggebers (Anforderungen und Ziele).
*   **Pflichtenheft:** Übersetzt das **WAS** ins **WIE** (technische Umsetzungsvorgaben durch den Auftragnehmer).
*   **Use-Case-Modelle:** Verdeutlichen Akteure, Ereignisflüsse und Systemreaktionen in konkreten Anwendungsszenarien.

**Relevante Standards für Anforderungsmanagement (Requirements Engineering, RE):**
*   **ISO/IEC/IEEE 29148:2018:** Weltweiter Referenz-Leitfaden für das Erheben, Analysieren, Dokumentieren, Prüfen und Verwalten von Anforderungen.
*   **ISO/IEC/IEEE 12207:2017:** Definiert Software Life-Cycle Processes, in dem RE als integrierter Prozessschritt verankert ist.
*   **ISO/IEC 15288:2015:** Systemisches Gegenstück für Hardware-Software-Kopplung.
*   **ISO/IEC 25010 / 25023 (SQuaRE-Familie):** Liefert Qualitätsmodell (Funktionalität, Zuverlässigkeit, Usability) und Metriken, um Anforderungen messbar auszuschreiben.
*   **IREB CPRE Syllabi / V-Modell-XT:** De-facto-Standard in D-A-CH für Rollen, Artefakte und Techniken des RE.

**Datenschutz (nach Schweizer DSG):**
Wesentliche Pflichten für Organisationen sind **Privacy by Design** und **Privacy by Default**. Ein Verzeichnis der Verarbeitungstätigkeiten ist zu führen (mit Ausnahmen für kleine KMU bei geringem Risiko). Verletzungen der Datensicherheit müssen unverzüglich dem Eidgenössischen Datenschutz- und Öffentlichkeitsbeauftragten (EDÖB) gemeldet werden. Personen haben **neue Betroffenenrechte** wie Information, Auskunft, Berichtigung, Löschung und Datenübertragbarkeit.

---

### **IV. DevOps Pipeline-Phasen im Detail und Qualitätsaspekte**

#### **A. Plan Phase**
*   **Analyse der Anforderungen** über Stakeholder und Use Cases, Abgleich mit Standards.
*   Erstellung eines **Testkonzepts**.

#### **B. Code Phase**
*   **Modellgetriebene Entwicklung (MDD):** Entwurf wird in formale Modelle überführt, aus denen Code automatisiert generiert werden kann.
*   **Architekturgetriebene Umsetzung:** Basierend auf Softwarearchitekturen (Schichten, Microservices, MVC) werden Komponenten systematisch entwickelt.
*   **Testgetriebene Entwicklung (TDD):** **Erst der Test, dann der Code.** Man schreibt zuerst einen fehlschlagenden Test (Red), implementiert minimalen Code zum Bestehen (Green), und optimiert dann den Code (Refactor).
*   **Pair Programming / Mob Programming:** Zwei oder mehr Entwickler setzen gemeinsam Teile des Entwurfs um, reduziert Fehler und fördert Wissenstransfer.
*   **Komponentengesteuerte Umsetzung:** Entwurf stark durch vorhandene Module (Libraries, Frameworks) geprägt.

#### **C. Build Phase**
*   Code Kompilierung, Konfigurations- und Abhängigkeitsmanagement, Erstellung von Artefakten.
*   **Statische Codeanalyse (Linting):** Überprüfung des Quellcodes ohne Ausführung auf Syntax, Formatierung, logische Fehler, Sicherheitslücken und Einhaltung von Coding-Standards. Erkennt potenzielle Schwachstellen frühzeitig im Entwicklungsprozess.
*   **Build-Automatisierung:** Einsatz von Tools und Skripten für repetitive Aufgaben (Kompilieren, Unit-Tests, Code-Analyse), reduziert manuellen Aufwand und Fehleranfälligkeit (z.B. Jenkins, GitLab CI/CD).
*   **Build-Orchestrierung:** Verbindet und steuert automatisierte Schritte zu einem durchgängigen Workflow (z.B. Build -> Test -> Deployment).
*   **Softwarekonfigurationsmanagement (SKM):** Systematische Erfassung, Versionierung und Kontrolle aller Projektelemente (Quellcode, Konfigurationen, Bibliotheken, Dokumentation). Wichtig für Nachvollziehbarkeit, Konsistenz und Integrität.

#### **D. Test Phase**
*   **Allgemeiner Testprozess:**
    1.  **Analyse und Planung:** Anforderungsanalyse, Testplanerstellung (Umfang, Strategie, Ressourcen, Risiken).
    2.  **Testdesign:** Testfall-Erstellung und Festlegung von Testdaten.
    3.  **Aufbau der Testumgebung:** Einrichtung von Hardware, Software, Netzwerken und Tools.
    4.  **Testausführung:** Manuell oder automatisiert (z.B. Selenium, JUnit).
    5.  **Fehleranalyse und Reporting:** Defekterfassung, Reporting an Entwickler.
    6.  **Regressionstests und Abschluss:** Überprüfung nach Fehlerbehebung, Abschlussbericht.
*   **Typen von Tests:**
    *   **Unit-Tests:** Prüfen einzelne Code-Einheiten.
    *   **Integrationstests:** Prüfen das Zusammenspiel mehrerer Einheiten.
    *   **Abnahmetests (User Acceptance Testing, UAT):** Prüfen das System aus Benutzersicht.
    *   **Smoke Test:** Erste grobe Prüfung eines neuen Software-Builds, um gravierende Fehler schnell zu identifizieren.
    *   **Black-Box-Test:** Tests basierend auf Spezifikation/Anforderung ohne Kenntnisse der internen Funktionsweise.
    *   **White-Box-Test:** Tests mit Kenntnis der internen Funktionsweise und des Quellcodes.
    *   **Usability-Test:** Überprüfung der Gebrauchstauglichkeit mit potenziellen Benutzern.
*   **Reifegradmodelle - TMMi (Test Maturity Model Integration):** Bewertet und verbessert den Reifegrad von Software-Testprozessen in 5 Stufen:
    1.  **Initial:** Unstrukturiert, ad-hoc.
    2.  **Managed:** Grundlegender Testprozess etabliert, systematische Planung.
    3.  **Defined:** Gut dokumentierte, standardisierte Prozesse.
    4.  **Measured:** Prozesse durch Kennzahlen und quantitative Analysen überwacht.
    5.  **Optimization:** Ständige Verbesserung und Fehlerprävention.
*   **Fehleranalyse mit Ishikawa-Diagramm (Fischgräten-Diagramm):** Stellt ein Problem (Fischkopf) dar und zerlegt dessen Ursachen in Hauptkategorien (z.B. die 6 M's: Mensch, Maschine, Material, Methode, Messung, Milieu) und Unterkategorien.

#### **E. Release Phase**
*   **Release Readiness Review (RRR):** Systematische Prüfung aller technischen, organisatorischen und operativen Voraussetzungen für den Produktiv-Rollout, endet mit einer Go-/No-Go-Entscheidung. Beinhaltet Prüfung von Scope & Objectives, Teststatus, Qualität & Stabilität, Deployment- & Rollback-Plan, Operations & Monitoring, Dokumentation & Training sowie Risikoanalyse und Go/No-Go-Kriterien.
*   **Tests in der Release-Phase:** Automatisierte Regressionstests, Smoke-Tests, Performance- und Lasttests, Sicherheitstests (Security Assessments), Abnahme- und Freigabetests (UAT).
*   **Sicherheitsanalysen:**
    *   **SAST (Static Application Security Testing):** "White-Box"-Verfahren, untersucht Quellcode auf Schwachstellen ohne Ausführung. Frühzeitiges Auffinden, detailliertes Feedback, vollständige Code-Abdeckung, aber hohe False-Positive-Rate.
    *   **DAST (Dynamic Application Security Testing):** "Black-Box"-Verfahren, prüft laufende Anwendung unter realen Bedingungen durch simulierte Angriffe. Erkennt echte Angriffsflächen, prüft Infrastruktur-/Konfigurationsfehler, liefert pragmatische Belege, aber keine Vollabdeckung und späte Identifikation.

#### **F. Deploy Phase**
*   **Automatisierte End-to-End-Tests (E2E):** Validieren die Anwendung aus Sicht der Endanwender, decken komplette Workflows ab, inklusive externer Schnittstellen.
*   **Infrastructure as Code (IaC):** Verwaltung und Bereitstellung von Rechenzentrumsressourcen mittels maschinenlesbarer Definitionsdateien. Kernprinzipien: Deklarativ vs. Imperativ, Idempotenz, Versionskontrolle. (z.B. Terraform).
*   **Vorausschauende Aktionen zur Risikominimierung:**
    *   **Canary-Releases:** Neue Version wird zuerst an einen kleinen Teil der Nutzer ausgeliefert; bei Problemen ist ein schneller Rollback möglich.
    *   **Blue-Green-Deployments:** Zwei identische Produktionsumgebungen (blue und green) parallel; Traffic wird bei Freigabe von alt auf neu umgeschaltet, minimiert Ausfallzeiten.
*   Automatisierte Rollbacks und Dokumentation.

#### **G. Operate & Monitor Phase**
*   **Monitoring-Typen:** Infrastructure Monitoring, Application Performance Monitoring (APM), Log-Management, Distributed Tracing.
*   **Security Monitoring & Compliance:** Vulnerability Scanning, SIEM-Systeme (Korrelation von Security-Events zur frühzeitigen Bedrohungserkennung), Audit Trails und Compliance-Reports.
*   **Service Level Management:**
    *   **SLA (Service Level Agreement):** Vertragliche Vereinbarung mit messbaren Leistungs- und Qualitätsaussagen und Konsequenzen bei Nichteinhaltung.
    *   **SLI (Service Level Indicator):** Spezifische, quantifizierbare Messgröße zur Bewertung eines Aspekts der Serviceleistung (z.B. Verfügbarkeit, Latenz, Fehlerquote).
    *   **SLO (Service Level Objective):** Internes Ziel, basierend auf SLIs, das beschreibt, wie gut ein Service in einem bestimmten Zeitraum laufen soll (z.B. 99,9 % Verfügbarkeit).

---

### **V. Kennzahlen (KPIs)**

**Key Performance Indicators (KPIs):**
**Messbare Leistungskennzahlen**, die Auskunft darüber geben, ob definierte Prozess- und Qualitätsziele erreicht werden. KPIs sind eng an übergeordnete Geschäfts- oder Qualitätsziele gekoppelt und helfen, sich auf die relevanten Indikatoren zu fokussieren. Die Ausprägung der KPIs wird basierend auf der Bedeutung des IT-Systems für den Kunden festgelegt.

**Ableitung von KPIs:**
1.  Ausgangspunkt sind die **Kundenanforderungen**.
2.  Erstellung eines **Fehlerbaums**, der die Erfüllung der Anforderung gefährden könnte.
3.  Erkennen **potenziell kritischer Ereignisse** mit hoher Eintrittswahrscheinlichkeit aus dem Fehlerbaum.
4.  Für diese Ereignisse oder deren Ursachen werden ein oder mehrere KPIs festgelegt.
*   **Beispiel (Online-Shop):** Bei einem Online-Shop, der mehrfach nicht erreichbar war, kann ein Fehlerbaum aufzeigen, dass das **Netzwerk der Hauptschwachpunkt** ist. Entsprechende KPIs wären dann **Latenzzeiten, Lost Packages, Durchsatz pro Segment und Fehler/Zeit** im Netzwerk.

**Kritische Erfolgsfaktoren (KEF) und Messgrößen (Beispiel):**
Bei der Erweiterung der Infrastruktur durch personifizierte Bestellmöglichkeiten sind KEFs zu beachten:
1.  **Anzahl der relevanten Vorschläge durch personifiziertes System:** Messgröße ist der Anteil der relevanten Vorschläge, Zielgröße z.B. **≥ 90%**. Begründung: Irrelevante Vorschläge nerven und trüben die User Experience.
2.  **Look and Feel ist wie vom Kunden parametriert und bleibt bestehen:** Messgröße ist die Beurteilung durch Kunden (Canaries) zu 90% positiv, Zielgröße z.B. **≥ 90% Zustimmung**.
3.  **Datensicherheit ist auf allen Ebenen gegeben:** Messgröße ist die Anzahl der Datenlecks pro Periode, Zielgröße **Keine**.

---
```