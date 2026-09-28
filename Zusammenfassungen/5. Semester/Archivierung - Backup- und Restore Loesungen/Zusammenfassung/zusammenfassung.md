# Zusammenfassung: Archivierung – Backup- und Restore-Lösungen (ABRL)

**Fach:** ABRL.TA1A · IPSO HF, 5. Semester · Dozent: Mevluet Polat · April – Juni 2026

> **Wie diese Zusammenfassung entstanden ist**
> *   **Grundlage:** alle 8 Foliensätze (Block 1–8), alle 31 Fachartikel, sämtliche Gruppenaufgaben inkl. Musterlösungen, die Fallbeispiele (Mobiliar/«Mobirama» und DE&C inkl. Lösungen), die Übungsfragen (Excel), die Infoblätter (RAID/3-2-1-1-0, Liste agentenbasierter Software), die Gruppen-Präsentationen (PPTX) sowie die E-Books von Acronis («Backup für Dummies») und Veeam («Microsoft 365 Backup for Dummies»).
> *   **Aufbau:** Die Inhalte sind **nach Thema** und nicht nach Quelle geordnet, weil Folien, Artikel und Übungen sich stark wiederholen.
> *   **Online-Recherche:** Ergänzungen aus eigener Recherche sind mit **🔎 Ergänzung (Recherche)** markiert. Die Links stehen im Quellenverzeichnis am Schluss.
> *   **Eigene Lösungen:** Für Aufgaben ohne offizielle Musterlösung (Excel-Übungen, einzelne Gruppenaufgaben) sind die Lösungen als **✍️ eigene Lösung** gekennzeichnet.
> *   **Nicht verarbeitet:** Die 31 Podcasts (.m4a) wurden nicht transkribiert. Ihre Titel entsprechen den Artikeln, es handelt sich sehr wahrscheinlich um Audio-Fassungen davon. Die PNG-Dateien in den Übungsordnern sind nur Screenshots der Aufgabenfolien.
> *   **⚠️ Widersprüche** zwischen den Quellen sind jeweils markiert und nicht stillschweigend aufgelöst.

---

## Inhaltsverzeichnis

1.  [Kursüberblick](#i-kursüberblick)
2.  [Risiken der Datensicherung und Archivierung](#ii-risiken-der-datensicherung-und-archivierung)
3.  [Risikomatrix und Risikosteuerung](#iii-risikomatrix-und-risikosteuerung)
4.  [Ursachen und Auswirkungen von Datenverlust](#iv-ursachen-und-auswirkungen-von-datenverlust)
5.  [Ransomware: Angriff, Erkennung, Schutz](#v-ransomware-angriff-erkennung-schutz)
6.  [Incident Response und Wiederherstellung nach Ransomware](#vi-incident-response-und-wiederherstellung-nach-ransomware)
7.  [Datenklassifizierung und Schutzbedarf](#vii-datenklassifizierung-und-schutzbedarf)
8.  [RPO, RTO, SLA und Verfügbarkeit](#viii-rpo-rto-sla-und-verfügbarkeit)
9.  [Das Backup-Konzept](#ix-das-backup-konzept)
10. [Von 3-2-1 zu 3-2-1-1-0, Air-Gap und Immutability](#x-von-3-2-1-zu-3-2-1-1-0-air-gap-und-immutability)
11. [Backup vs. Disaster Recovery](#xi-backup-vs-disaster-recovery)
12. [Das Datenhaltungskonzept](#xii-das-datenhaltungskonzept)
13. [Speichertechnologien](#xiii-speichertechnologien)
14. [Datensicherungstechnologien](#xiv-datensicherungstechnologien)
15. [Kapazitätsplanung](#xv-kapazitätsplanung)
16. [Performance-Planung](#xvi-performance-planung)
17. [Konzeptionelle Bausteine und Lebenszyklus des Konzepts](#xvii-konzeptionelle-bausteine-und-lebenszyklus-des-konzepts)
18. [Beratung, Machbarkeit und Konzeptbeurteilung](#xviii-beratung-machbarkeit-und-konzeptbeurteilung)
19. [Testverfahren und Validierung](#xix-testverfahren-und-validierung)
20. [Kontrollen, Monitoring, Audits](#xx-kontrollen-monitoring-audits)
21. [Rechtliche und regulatorische Rahmenbedingungen (Schweiz)](#xxi-rechtliche-und-regulatorische-rahmenbedingungen-schweiz)
22. [Fallbeispiele](#xxii-fallbeispiele)
23. [Prüfungsschema für Fallbeispiele](#xxiii-prüfungsschema-für-fallbeispiele)
24. [Gruppenaufgaben und Musterlösungen im Überblick](#xxiv-gruppenaufgaben-und-musterlösungen-im-überblick)
25. [Übungsfragen mit Lösungen](#xxv-übungsfragen-mit-lösungen)
26. [Formelsammlung und Merkzahlen](#xxvi-formelsammlung-und-merkzahlen)
27. [Glossar](#xxvii-glossar)
28. [Quellen](#xxviii-quellen)

---

### **I. Kursüberblick**

| Block | Thema | Kerninhalte |
| :--- | :--- | :--- |
| **1** | Risiken, Datenverlust, Ransomware (Teil 1) | Risikoarten, Risikomatrix, Ursachen/Auswirkungen von Datenverlust, Einführung Ransomware |
| **2** | Ransomware (Teil 2), Datenklassifizierung I | Erkennung und Analyse, Incident Response, Grundlagen Klassifizierung, Klassifizierungskriterien |
| **3** | Datenklassifizierung II, Anforderungen, 3-2-1 | Volumen/Periodizität/Zugriffssicherheit, RTO/RPO/SLA, 3-2-1-Regel, Air-Gap, Sicherungsarten |
| **4** | Backup vs. DR, Datenhaltung, Testing | Abgrenzung Backup/DR, vertiefte Klassifizierung, Datenhaltungskonzept, 3-2-1-1-0, Testverfahren |
| **5** | Speichertechnologien | Block/File (SAN/NAS), Tape, Deduplication Appliances, Object Storage |
| **6** | Datensicherungstechnologien | Agent-basiert, Agentless (Hypervisor-API), dateibasiert, Snapshots, Replikation, CDP, Technologieauswahl |
| **7** | Kapazität und Performance | Kapazitätsplanung, Performance-Analyse, RPO/RTO-Einflüsse, konzeptionelle Bausteine |
| **8** | Beraten, Testen, Kontrollieren | Machbarkeit, Lösungsberatung, Testverfahren, Kontrollmechanismen, Compliance |

**Rahmen:** Zu jedem Kapitel gibt es einen Artikel (6–17 Seiten) und einen Podcast (~15 Min.). 80 % Anwesenheit sind Pflicht, die Gruppenaufgaben werden präsentiert. In Block 8 berichteten zwei System Engineers der ETH Zürich (D-USYS und D-EAPS) als Gastreferenten über die Datensicherung an der ETH.

**Leitgedanke des ganzen Kurses:** Datensicherung ist **kein einmaliges IT-Projekt**, sondern ein **kontinuierlicher Managementprozess**. Die Kette lautet:

> **Risiken erkennen → Daten klassifizieren → Anforderungen (RPO/RTO/Retention) ableiten → Technologie wählen → Kapazität und Performance dimensionieren → umsetzen → testen → kontrollieren/auditieren → verbessern.**

*   **Randnotiz «Microsoft Project Silica»:** Am Ende jedes Foliensatzes gezeigt. Daten werden als **Voxel in dünnem Quarzglas** gespeichert, laut Folie bis zu ca. 7 TB auf einem 2 mm dünnen Glasplättchen, haltbar für ~10'000 Jahre. Es ist ein Ausblick auf künftige Langzeitarchive.

---

### **II. Risiken der Datensicherung und Archivierung**

**Grundlagen:**
*   **Backup ≠ Archivierung.** Ein **Backup** dient der **kurzfristigen Wiederherstellung** nach Datenverlust (kurze Retention, z. B. 30 Tage). Die **Archivierung** dient der **langfristigen, revisionssicheren (unveränderbaren) Aufbewahrung**, meist wegen gesetzlicher Pflichten (z. B. 10 Jahre nach OR).
*   Die **zunehmende Vernetzung** (Cloud SaaS/PaaS/IaaS, On-Premises, mobile Geräte, APIs, VPN, Identitätsprovider) erhöht die Anzahl **Single Points of Failure** und damit die Fehlerwahrscheinlichkeit. **Schatten-IT** erzeugt Daten ausserhalb der zentralen Sicherung.
*   **Nur systematische Risikoanalysen** erkennen Gefahren frühzeitig.
*   **Die Geschäftsleitung trägt die übergeordnete Verantwortung** für den Schutz unternehmenskritischer Daten (siehe unten: Art. 716a OR).

**Die vier Risikokategorien (nach Polat):**

| Kategorie | Typische Risiken | Beispiele / Prävention |
| :--- | :--- | :--- |
| **Technisch** | Hardwaredefekte (Festplatten, Medien), Netzwerkstörungen, Stromausfälle, veraltete/minderwertige Speichermedien, Systemausfälle | RAID-Controller-Defekt; Rebuild-Stress bei RAID 5; **Bit-Rot** (stille Datenkorruption); SSD-Verschleiss und Ladungsverlust bei stromloser Lagerung; Consumer-Hardware im 24/7-Betrieb; Abbruch bei Transaktionen; **Dirty Shutdown** (Cache-Verlust); USV nicht gewartet oder Storage an separatem Stromkreis ohne USV |
| **Menschlich («Layer 8»)** | Fehlbedienung (versehentliches Löschen), Unwissenheit, Sabotage, schwache Passwörter, fehlende Schulung | Daten lokal auf Desktop = «backupfreie Zone»; Copy-Paste-Fehler bei Backup-Ausschlüssen; Offboarding im Streit («Logic Bombs»); Social Engineering. **Gegenmittel:** Security Culture, Schulungen, **Least Privilege**, **Vier-Augen-Prinzip**, MFA |
| **Organisatorisch** | Fehlende/veraltete Backup-Strategie, fehlende Dokumentation, unklare Zuständigkeiten, keine Restore-Tests, mangelnde Compliance | Keine **BIA** (Business Impact Analysis) → keine RPO/RTO; **Wissens-Silos**; **Silent Failure** (Software meldet «Job successful», sichert aber nur die Verzeichnisstruktur); fehlende **RACI-Matrix** |
| **Extern** | Cyberangriffe, Naturereignisse, Lieferantenausfall (Cloud-Provider), Diebstahl, längere Stromausfälle | Ransomware sabotiert gezielt die «Rettungsboote» (Backups); Brand/Hochwasser/Erdbeben; **Shared Responsibility Model** (der Kunde bleibt für seine Daten verantwortlich); **Cloud Concentration Risk**; Diebstahl unverschlüsselter Medien |

**Risikoidentifikation und Prävention:**
*   **Strukturierte Risikoanalyse:** Inventarisierung der Assets → Bedrohungsmodellierung → Bewertung (Eintrittswahrscheinlichkeit × Schadensausmass) → Visualisierung in einer **Risk Map**. Die Bewertung erfolgt nach der **CIA-Triade** (Confidentiality, Integrity, Availability).
*   **Defense-in-Depth**, Massnahmen kombinieren:
    *   **Präventiv:** Verschlüsselung, Firewalls, Zugangskontrollen, Schulungen, Passwortrichtlinien.
    *   **Detektiv:** Monitoring der Backup-Jobs **und** der Datenwachstumsraten. Ein plötzlicher Anstieg im Backup kann auf laufende Verschlüsselung hindeuten, SIEM meldet Anomalien.
    *   **Korrektiv:** Notfallplan / **Disaster Recovery Playbook** mit Rollen, Step-by-Step-Anleitungen und Kommunikationsstrategie, dazu **Table-Top-Übungen**.
*   **Regelmässigkeit:** Sicherungen in festen Intervallen, damit stets aktuelle Wiederherstellungspunkte existieren.
*   **Exit-Strategie / Multi-Cloud** und **BYOK** (Bring Your Own Key) reduzieren das Lieferantenrisiko.

**Rolle der Geschäftsleitung (Governance):**
*   **Art. 716a OR:** Der Verwaltungsrat hat die **unübertragbare Oberleitung**. Versäumnisse bei der Datenverfügbarkeit können als **Sorgfaltspflichtverletzung** gelten, mit möglicher **persönlicher Haftung**.
*   Die GL stellt Budget und Personal bereit und definiert den **Risikoappetit**, also RPO/RTO. Das ist **nicht an die IT delegierbar**.
*   **Three Lines of Defense:**
    1.  Operative Einheiten / IT-Betrieb (Umsetzung).
    2.  Risk Management / Compliance (Überwachung).
    3.  Interne/externe Revision (unabhängige Prüfung).
*   **«Tone at the Top»:** Die Führung lebt die Sicherheit vor.
*   **Murphy's Law:** «Alles, was schiefgehen kann, wird schiefgehen.» Oft verketten sich banale Ursachen (fehlendes USV-Kabel, falsche Annahme, fehlendes Update) zur Katastrophe.

---

### **III. Risikomatrix und Risikosteuerung**

**Zwei-Achsen-Modell:** Jedes Risiko wird anhand von **Eintrittswahrscheinlichkeit (EW)** und **Schadensausmass (SA)** bewertet.
> **Risikowert (RW) = EW × SA** (bei einer 5×5-Matrix: 1–25)

**Nutzen der Matrix:**
*   **Objektivität und Vergleichbarkeit** statt Bauchgefühl. Sie reduziert Verzerrungen wie den **Availability Bias** (man fürchtet das, was gerade in den Medien ist) und bildet eine «Single Source of Truth».
*   **Priorisierung:** Ressourcen fliessen gezielt zu den grössten Bedrohungen.
*   **Kommunikationsgrundlage** zwischen IT, Management und Fachbereichen. Beispiel: «Mit 40'000 CHF schieben wir ein rotes Risiko (potenzieller Schaden 1 Mio. CHF) in den gelben Bereich.»
*   **Risk Owner:** Jedes Risiko erhält einen fachlichen Besitzer, es ist nicht «die IT» für alles zuständig.
*   Die Matrix verhindert, dass man Kleinstrisiken («Parkschäden») überbewertet oder seltene Katastrophen («Black Swans») ignoriert.

**Skala Eintrittswahrscheinlichkeit (5 Stufen):**

| Stufe | Bezeichnung | Häufigkeit (Artikel 1.2) | Häufigkeit (Musterlösung 1.2) |
| :---: | :--- | :--- | :--- |
| 1 | Sehr unwahrscheinlich | seltener als alle 10 Jahre | < 1× in 10 Jahren |
| 2 | Unwahrscheinlich | alle 5–10 Jahre | 1× in 5–10 Jahren |
| 3 | Möglich | alle 2–5 Jahre | 1× in 1–5 Jahren |
| 4 | Wahrscheinlich | ca. 1× pro Jahr | 1× pro Jahr |
| 5 | Sehr wahrscheinlich | mehrmals pro Jahr / nahezu sicher | mehrmals pro Jahr |

*   **Datenquellen:** interne Vorfall-Logs, Branchenberichte (NCSC/BACS), Vulnerability Scans.
*   **Dynamik:** Werte sind nicht statisch. KI-Malware oder neue Betrugswellen (z. B. CEO-Fraud) verschieben sie. Jede Einschätzung wird **nachvollziehbar dokumentiert**, auch wegen der Rechenschaftspflicht nach DSG.

**Schadensausmass:**
*   **Kategorien:** finanzielle Verluste, Reputationsschäden, rechtliche Konsequenzen (z. B. DSG-Bussen bis CHF 250'000 gegen Privatpersonen), betriebliche Ausfälle (Business Continuity). Dazu kommen **Kaskadeneffekte**: technischer Fehler → Datenleck → Reputationsschaden → Umsatzrückgang.
*   **Abstufung (Artikel):** geringfügig → moderat → wesentlich → schwerwiegend → **existenzbedrohend**.
*   **Abstufung (Musterlösung):** 1 geringfügig (schnell behebbar), 2 gering (Stunden), 3 moderat (Tage), 4 erheblich (hoher finanzieller Schaden), 5 katastrophal (existenzbedrohend, Totalverlust).
*   **Kontextabhängig:** Ein 4-stündiger Mailausfall ist für eine Schreinerei ärgerlich, für einen Online-Händler eine Katastrophe. Polat empfiehlt, den **realistischen Worst Case** als Basis zu nehmen.

**Farbcodierung und Schwellenwerte:**
*   **Grün:** akzeptabel, Beobachtung/Monitoring genügt.
*   **Gelb:** Aufmerksamkeit, Massnahmen im ordentlichen Budget.
*   **Orange:** Handlungsbedarf innert 3–6 Monaten.
*   **Rot:** inakzeptabel, **sofortige Massnahmen durch die GL**, oft ein «Stop-Go»-Entscheid.
*   Wo die Grenzen liegen, hängt vom **Risk Appetite** ab: Ein Start-up akzeptiert mehr als eine Privatbank.

> ⚠️ **Zwei verschiedene Schwellenwert-Skalen im Kursmaterial:**
>
> | Quelle | Niedrig / Grün | Mittel / Gelb | Hoch / Orange | Kritisch / Rot |
> | :--- | :---: | :---: | :---: | :---: |
> | **Risikomatrix-Tool (Folie Block 1)** | 1–4 | 5–9 | 10–15 | 16–25 |
> | **Musterlösung Gruppenaufgabe 1.2** | 1–5 | 6–12 | 13–19 | 20–25 |
>
> In der Prüfung angeben, welche Skala man verwendet.

**Die vier Strategien der Risikosteuerung:**

| Strategie | Beschreibung | Beispiel |
| :--- | :--- | :--- |
| **Vermeidung** (Avoidance) | Risikobehaftete Aktivität ganz einstellen | Kein BYOD für Kundendaten |
| **Minderung** (Mitigation) | Wahrscheinlichkeit und/oder Schaden senken, die Kernaufgabe der IT-Sicherheit | MFA (senkt EW), Incident-Response-Plan (senkt SA), Verschlüsselung, Redundanz, Offline-Backup |
| **Transfer** | Finanzielle Folgen auf Dritte übertragen | Cyberversicherung, Outsourcing. Stillstand und Reputationsverlust lassen sich nur teilweise transferieren, die rechtliche Mitverantwortung bleibt |
| **Akzeptanz** | Bewusst nichts tun, wenn die Kosten den Nutzen übersteigen (typisch für grüne Risiken) | Muss **formell dokumentiert** werden (**Management Sign-off**) |

*   **Kontinuität:** Die Wirksamkeit der Massnahmen regelmässig prüfen, die Matrix ist ein **«lebendes Dokument»**.
*   **Praxis:** interdisziplinäre **Workshops** (IT + Jurist + Fachbereich), konkrete **Szenarioanalysen** (z. B. «Ex-Mitarbeiter hat noch Cloud-Zugriff und löscht Projektfiles») statt abstrakter Risiken, **GRC-Tools** statt Excel. «Das Tool ist nur so gut wie der Prozess.» Aus der Matrix wird ein **Massnahmenplan** mit Verantwortlichen, Fristen und Zielen abgeleitet.
*   **Kurs-Tool:** Eine 5×5-Risikomatrix-Webanwendung (abrl.mpol.ch/risikomatrix) erfasst Basis- und mitigiertes Risiko, Export als PDF/CSV/JSON/HTML.

**Beispiel aus Musterlösung 1.2 (AlpinTech GmbH):**

| Nr. | Risiko | EW | SA | RW | Farbe | Steuerung |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- |
| R1 | Ransomware-Angriff | 4 | 5 | 20 | Rot | Minderung: Offline-Backup, Endpoint-Protection, Schulung, Notfallplan |
| R4 | Fehlende Restore-Tests | 5 | 4 | 20 | Rot | Minderung: monatliche Restore-Tests, halbjährlicher DR-Test |
| R3 | Menschlicher Bedienfehler | 4 | 3 | 12 | Gelb | Minderung: Vier-Augen-Prinzip, Automatisierung, Versionierung |
| R2 | Hardwareausfall Backup-Server | 3 | 4 | 12 | Gelb | Minderung + Transfer: Redundanz, Wartungsvertrag, Versicherung |
| R5 | Stromausfall ohne USV | 2 | 4 | 8 | Gelb | Akzeptanz + Minderung: USV für die Dauer des Backup-Fensters |

---

### **IV. Ursachen und Auswirkungen von Datenverlust**

**Kategorisierung der Ursachen:** hardware-, software-, personen- und umweltbezogen (inkl. Cyberangriffe). **Wechselwirkungen** verstärken sich: Ein Hardwaredefekt plus ein Konfigurationsfehler im Backup führt zum Totalverlust.

**Hardware:**
*   **HDD:** Leseköpfe schweben Nanometer über der Platte. Erschütterung oder Verschleiss führen zum **Head-Crash**. Die Ausfallwahrscheinlichkeit folgt der **Badewannenkurve** (Frühausfälle durch Herstellungsfehler, Spätausfälle durch Verschleiss). Die **MTBF** täuscht oft über die reale Zuverlässigkeit hinweg.
*   **SSD:** begrenzte Schreibzyklen (P/E-Cycles) trotz **Wear Leveling**. Ausfälle kommen oft «digital» ohne Vorwarnung. Bei stromloser Lagerung droht **Data-Retention-Verlust (Bit-Rot)**.
*   **RAID ist kein Backup:** Es schützt nicht vor logischen Fehlern, Viren, Diebstahl oder Löschung. **Rebuild-Stress:** Platten aus derselben Charge fallen oft fast gleichzeitig aus, und bei RAID 5 bedeutet der Ausfall einer zweiten Platte oder des Controllers den **Totalverlust**. **Silent Data Corruption** kann sogar ins Backup repliziert werden.
*   **Umwelt:** Überhitzung (Haarrisse, Controller), Feuchtigkeit (Korrosion), Staub (Kurzschluss), EMI/Blitzschlag, Wasserrohrbruch, Brand. **Regelmässiger Hardwareersatz** senkt das Risiko.

**Software und Mensch:**
*   Fehlerhafte Updates und Inkompatibilitäten beschädigen Datenbankstrukturen. Der **Write-Hole-Effekt** entsteht, wenn das OS Daten als geschrieben meldet, der Controller sie aber noch nicht gesichert hat.
*   **Konfigurationsfehler:** Backup sichert unvollständig (geänderter Pfad, Zielmedium voll) und bleibt bis zum Ernstfall unentdeckt. Werden offene Dateien gesichert, entsteht ein inkonsistentes Backup (Beispiel Webshop Bern).
*   Versehentliches Löschen/Überschreiben, Schatten-IT (Dropbox & Co.), Phishing/Social Engineering, böswillige Insider.
*   **Gegenmittel:** Security Awareness, Vier-Augen-Prinzip, Versionierung/«Papierkorb» auf Serverebene.

**Auswirkungen:**

| Dimension | Inhalte |
| :--- | :--- |
| **Finanziell** | Direktkosten (Datenrettung im Reinraumlabor Klasse 100, Forensik, Hardware, Beratung), Umsatzausfall, **Opportunity Costs**, Konventionalstrafen bei verletzten SLAs, Regressforderungen, steigende Cyberversicherungsprämien oder Kündigung der Police, ungeplante Investitionen (CAPEX) |
| **Betrieblich** | Betriebsunterbrechung für Stunden bis Tage, Produktivitätsverlust, **Kaskadeneffekt** (ERP weg → Produktion, Logistik und Administration stehen), Auswirkungen auf die ganze Lieferkette |
| **Rechtlich** | Meldepflicht an den **EDÖB** bei hohem Risiko (DSG), Bussen, persönliche Haftung von VR/GL, Verstoss gegen **Aufbewahrungspflichten** (OR 958f: 10 Jahre), **Beweisnot** bei Steuerprüfung (Ermessenseinschätzung), verweigertes Revisionstestat |
| **Reputation** | Vertrauensverlust bei Kunden und Partnern (besonders Finanz- und Gesundheitssektor), Medien/Shitstorm, «digitale Narbe» in Suchmaschinen, sinkender Markenwert, schlechteres **Employer Branding** |

*   **Präventionssäulen:** 3-2-1-Regel, regelmässige Wartung und Hardwareersatz, Patch-Management, Mitarbeiterschulung, **Business Continuity Planning (BCP)**.
*   **Musterlösung 1.3 (HelvetiaMed AG, 14 Tage Datenverlust):**
    *   **Ursachen:** Der 5 Jahre alte Server mit defektem RAID-5-Controller fällt aus. Das Backup-Volume war voll, der Job schlug 14 Tage lang fehl, die Logs las niemand. Es gab kein Monitoring und seit 18 Monaten keinen Restore-Test.
    *   **Geschätzter Schaden:** ~CHF 240'000.
    *   **Massnahmen:** Backup-Alarmierung (sofort, kostenlos), monatliche Restore-Tests, georedundante Kopie, Server mit RAID 6, Dokumentation und Rollen, Schulung, IT-Notfallplan.
    *   **Merksatz:** «Ein Backup ohne Monitoring ist wie ein Alarm ohne Leitstelle.»

---

### **V. Ransomware: Angriff, Erkennung, Schutz**

**Definition:** **Ransomware** (engl. *ransom* = Lösegeld + *software*) ist Schadsoftware, die Daten auf infizierten Systemen **verschlüsselt** (oder das System **sperrt**) und **Lösegeld** fordert, meist in **Kryptowährung** (Bitcoin, zunehmend **Monero**, Verschleierung über Mixer/Tumbler). Die erste Form war der AIDS-Trojaner 1989, heute ist Ransomware eine professionelle Industrie.

**Hybride Verschlüsselung (warum Daten ohne Schlüssel verloren sind):**
1.  Die Dateien werden lokal mit einem schnellen **symmetrischen** Schlüssel verschlüsselt (z. B. **AES**).
2.  Dieser AES-Schlüssel wird mit dem **öffentlichen RSA-Schlüssel** des Angreifers verschlüsselt.
3.  Nur der Angreifer besitzt den **privaten RSA-Schlüssel**, Brute-Force ist praktisch unmöglich. Beispiel **WannaCry 2017**: AES-128, gesichert mit RSA-2048.

**Ransomware-Typen:**

| Typ | Merkmal |
| :--- | :--- |
| **Verschlüsselungs-Ransomware** (Crypto) | Verschlüsselt Dateien vollständig, am weitesten verbreitet |
| **Locker-Ransomware** | Sperrt den kompletten Systemzugang |
| **Doppelerpressung** (Double Extortion) | Verschlüsseln **und** Daten stehlen, Drohung mit Veröffentlichung auf **Leak Sites** (Pionier: «Maze», 2019) |
| **Triple Extortion** | Zusätzlich DDoS-Angriffe oder direkte Kontaktaufnahme mit Kunden/Partnern des Opfers |
| **Ransomware-as-a-Service (RaaS)** | Entwickler vermieten die Plattform an «Affiliates» und erhalten einen Anteil am Lösegeld (z. B. **LockBit**) |
| **Wiper-Malware** | Als Ransomware getarnt, zerstört Daten unwiderruflich (keine Wiederherstellung möglich) |

*   **Big Game Hunting:** Gezielte Angriffe auf Konzerne und kritische Infrastruktur (z. B. Ryuk/Conti gegen Spitäler), weil diese eher Millionen zahlen.
*   **Bekannte Fälle:** WannaCry (2017, NHS), NotPetya (legte ganze Netze inkl. Backup-Speicher lahm), Colonial Pipeline (2021, 75 BTC ≈ 4.4 Mio. USD bezahlt), Kaseya (2021, Supply Chain), Hafnium (Exchange-Zero-Days).
*   **Initial Access Brokers** verkaufen im Darknet Zugänge zu bereits kompromittierten Netzen.

**Verbreitungswege (Angriffsvektoren):**
*   **Phishing-E-Mails:** der **häufigste Weg** (Folie: über 90 % der Infektionen). Anhänge mit Makros führen zu PowerShell, der Payload wird in den RAM nachgeladen. Unterschieden wird Spam-Phishing und **Spear-Phishing**.
*   **Ungepatchte Schwachstellen / Exploit-Kits / Zero-Days.** Das Problem ist oft der **Patch-Gap**: Der Patch existiert, wurde aber nicht eingespielt (z. B. VPN/Firewall mit Buffer Overflow).
*   **Unsicherer Remote-Zugriff (RDP)** ohne MFA: Brute-Force, **Credential Stuffing** (Passwortlisten aus anderen Leaks).
*   **Drive-by-Downloads:** Der blosse Besuch einer kompromittierten Seite genügt.
*   **Wechseldatenträger:** USB-Stick «Gehaltsliste» auf dem Parkplatz, **BadUSB** (gibt sich als Tastatur aus), Doppelendung `.pdf.exe`.
*   **Supply-Chain-Angriffe:** manipulierte, korrekt signierte Updates oder kompromittierte Managed Service Provider.

**Angriffsablauf (Cyber Kill Chain):**
1.  **Erstinfektion** (Initial Access): Anhang, Link, Drive-by.
2.  **Command-and-Control (C2):** «Beaconing», getarnt als HTTPS, lädt Werkzeuge nach.
3.  **Auskundschaften / Netzwerk-Scanning** und **Lateral Movement** mit legitimen Admin-Tools (PowerShell, PsExec, WMI, «Living off the Land», **Human-Operated Ransomware**).
4.  **Rechteausweitung** (Privilege Escalation) bis **Domain-Admin**: Mimikatz, Pass-the-Hash, Kerberoasting.
5.  **Exfiltration** der Daten (für Double Extortion).
6.  **Backup-Sabotage:** `vssadmin delete shadows /all /quiet` löscht die Schattenkopien, Backup-Server (z. B. Veeam) werden gesucht und formatiert, Kataloge manipuliert. Angreifer bleiben oft **Wochen** im Netz, sodass auch die Backups bereits kompromittiert sind (**Re-Infection** beim Restore).
7.  **Verschlüsselung** – bevorzugt **nachts, an Wochenenden oder Feiertagen** (weniger Überwachung).
8.  **Lösegeldforderung** (Ransom Note, z. B. `READ_ME.txt`) mit Frist und Tor-Portal / «Helpdesk» zur Verhandlung.

**Auswirkungen:** Datenverlust (verschlüsselte Daten haben hohe Entropie und sind ohne Schlüssel nicht nutzbar, Decryptoren sind oft fehlerhaft), Betriebsstillstand für Tage bis Wochen (Wiederherstellungskosten oft das **Zehnfache** des Lösegelds), Datendiebstahl, Vertrauensverlust, psychische Belastung des IT-Teams (Burnout, Fluktuation).

**Erkennungsmethoden:**

| Methode | Stärke | Schwäche | Wirksamkeit gegen moderne Ransomware |
| :--- | :--- | :--- | :--- |
| **Signaturerkennung** (klassisches AV) | schnell, ressourcenschonend, zuverlässig bei bekannten Varianten | versagt bei Zero-Day, **polymorpher** Malware, **fileless** Angriffen (PowerShell), Verschleierung | **gering** als alleinige Methode |
| **Verhaltensanalyse** (EDR) | erkennt die **Aktion** (Massenverschlüsselung, Umbenennung), auch unbekannte Varianten | Fehlalarme, Rechenleistung | **hoch** |
| **IoC-Analyse** (Indicators of Compromise: Hashes, IPs, Domains, massenhafte Umbenennungen) | gut für bekannte Kampagnen und Forensik | reaktiv, braucht aktuelle Threat-Intelligence-Feeds, Angreifer wechseln IPs schnell | **mittel** (Ergänzung) |
| **Netzwerkmonitoring** (NDR, SIEM) | erkennt Lateral Movement, C2-Kommunikation, Exfiltration | braucht Baseline, verschlüsselter Traffic erschwert es | **hoch** |

*   **Weitere Mittel:** **Honeypots/Köderdateien** (Alarm bei Zugriff), **SIEM** (Korrelation von Ereignissen aus vielen Quellen), Anomalieerkennung, Alarmmanagement mit Eskalationsstufen, **Threat Intelligence**, Entropie-Überwachung im Backup.
*   **EDR / XDR / MDR:** **EDR** = Endpoint Detection & Response (Verhalten am Endpunkt, isoliert das Gerät automatisch). **XDR** verknüpft zusätzlich Netzwerk- und Cloud-Telemetrie. **MDR** = Managed Detection & Response (externes 24/7-SOC, ideal für KMU).
*   **Mehrstufiges Erkennungskonzept (Musterlösung 2.1, «Defense in Depth»):**
    1.  Perimeter (E-Mail-/Web-Gateway mit Sandboxing).
    2.  EDR am Endpunkt.
    3.  Netzwerkmonitoring + SIEM.
    4.  Threat-Intelligence-Integration.

**Schutzmassnahmen und Anforderungen an die Datensicherung:**
*   **Offline-Backups / Air-Gap:** Ransomware erreicht keine Kopien ohne Netzwerkverbindung (Tape, RDX).
*   **Immutable Storage** (WORM, Object Lock): Löschen oder Ändern ist für eine definierte Frist unmöglich, **selbst mit Admin-Rechten**.
*   **Hohe Backup-Frequenz** (kleines RPO), **regelmässige Restore-Tests**.
*   **Netzwerksegmentierung:** Backup in eigenem VLAN, **nicht Mitglied der produktiven AD-Domäne**, eigene Konten, MFA, «Default Deny», **Zero Trust**.
*   **Awareness-Schulungen** («Human Firewall», simulierte Phishing-Kampagnen mit Just-in-Time-Training, Quishing = QR-Code-Phishing), **Patch-Management** (risikobasiert, z. B. innert 48 h; «virtuelles Patching» mit IPS für nicht patchbare Systeme), **Endpoint-Protection (EDR)**, **Notfallplan**.
*   **Governance-Bausteine (Artikel 2.2):** Risikobewertung, Sicherheitsrichtlinien (Acceptable Use, Password Policy, BYOD/MDM mit Remote Wipe), Threat Intelligence, **Penetration-Testing** (Red Team findet z. B. einen vergessenen Testserver als Einfallstor), **Cyberversicherung** (Risikotransfer plus Incident-Response-Retainer, setzt aber MFA und Offline-Backups voraus).
*   **Musterlösung 1.4 (FinSecure AG), Top-5-Anforderungen an die Datensicherung:**
    1.  Offline-Backup (Air-Gap).
    2.  Immutable Storage.
    3.  3-2-1-Regel.
    4.  Tägliches Monitoring mit Alarmierung.
    5.  Monatliche Restore-Tests.

---

### **VI. Incident Response und Wiederherstellung nach Ransomware**

**Grundlagen:** Ein dokumentierter **Incident-Response-Plan (IRP)** legt Abläufe, Rollen und Eskalationsstufen fest. Das **IR-Team / CSIRT** besteht aus IT-Security, Management, Kommunikation und bei Bedarf externer Forensik. Die **Reaktionszeit** bestimmt massgeblich den Gesamtschaden. **Übungsszenarien** decken Schwachstellen auf. Merksatz: **«Ein Notfallplan muss vor der Krise existieren.»**

**Sofortmassnahmen (erste 60 Minuten, Musterlösung 2.2):**

| Minute | Massnahme | Ziel |
| :--- | :--- | :--- |
| 0–5 | **Netzwerkverbindungen trennen**: Systeme isolieren (Containment), VPN sperren | Ausbreitung stoppen |
| 5–10 | Krisenteam bilden (IT-Leitung, GL, Fachbereich, Kommunikation) | Entscheidungsfähigkeit |
| 10–20 | Schadensinventar: Was ist betroffen? Sind die Backups intakt? | Lagebild |
| 20–30 | Externe IT-Forensik beauftragen | Professionelle Hilfe |
| 30–45 | **Polizei und NCSC/BACS** informieren, Cyberversicherung melden | Pflichten erfüllen, Ermittlungen |
| 45–60 | Entscheid Lösegeld: **nicht zahlen**, sofern Backups vorhanden | Strategische Entscheidung |

*   **Nicht sofort neu aufsetzen:** Zuerst **forensische Beweissicherung** (Bit-für-Bit-Kopien von RAM und Disk des «Patient Zero»), dann **Root Cause Analysis**. Sonst greift der Täter am nächsten Tag durch dieselbe Lücke erneut an.
*   Alle Fehlermeldungen und Beobachtungen sofort **protokollieren**.

**Kommunikation im Krisenfall:**
*   **Mitarbeitende:** sofort informieren, Verhaltensanweisungen geben (keine Systeme nutzen), tägliches Briefing, **Out-of-Band-Kanäle** nutzen (private Handys, Threema), weil E-Mail offline ist.
*   **Kunden:** proaktiv und transparent (Top-Kunden telefonisch, dann alle per E-Mail).
*   **Medien:** vorbereitetes Statement, Informationshoheit behalten.
*   **Behörden/Regulatoren:** Polizei, BACS, **EDÖB** (bei Personendaten mit hohem Risiko), **FINMA** bei Finanzdienstleistern.
*   Ein **Kommunikationsplan** mit Sprachregelungen, Ansprechpersonen und Kanälen liegt im Voraus fest.

**Wiederherstellungsstrategie:**
1.  **Forensik und Schliessen der Lücke.**
2.  **Neuinstallation** der betroffenen Systeme von verifizierten Medien (verschlüsselte Installationen können versteckte Malware enthalten).
3.  **Backup-Verifizierung** auf Vollständigkeit, Konsistenz und **Schadsoftwarefreiheit** (letztes *sauberes* Backup finden, Malware-Scan vor dem Restore).
4.  **Priorisierte, stufenweise Wiederinbetriebnahme** (Application Tiering: **Tier 0** = AD, DNS, Netzwerk vor **Tier 1** = ERP, Buchhaltung vor Tier 2/3). Nach jedem Schritt prüfen, sonst entstehen Fehler durch fehlende Abhängigkeiten. Parallel startende Systeme erzeugen «**Boot Storms**».
5.  **Intensives Monitoring mindestens 30 Tage** nach der Wiederherstellung.

**Umgang mit Lösegeldforderungen – Empfehlung: nicht zahlen:**
*   Es gibt **keine Garantie** für Schlüssel oder Datenfreigabe, Decryptoren sind oft fehlerhaft (Beispiel: 20 % der Datenbanken irreversibel beschädigt).
*   Zahlungen **finanzieren** kriminelle Organisationen und neue Varianten.
*   Wer zahlt, markiert sich als **zahlungswillig** («Double Dipping», Backdoors, erneuter Angriff).
*   **Rechtslage:** Zahlungen an sanktionierte Gruppen können strafbar sein.
*   **Alternative:** in Offline-Backups, Immutable Storage und IR-Pläne investieren, damit man nicht erpressbar ist.

**Nachbereitung / Lessons Learned:** strukturierte Nachbesprechung, Schwachstellen priorisiert schliessen, Prozesse, Notfallpläne und Backup-Strategie verbessern, obligatorische Schulungen, **Abschlussbericht** an die GL.

---

### **VII. Datenklassifizierung und Schutzbedarf**

**Definition:** Datenklassifizierung ist die **systematische Kategorisierung** betrieblicher Daten nach **Schutzbedarf und Geschäftswert**. Sie ist die **Grundlage** für Backup-Strategie, Zugriffskontrollen und Informationssicherheit. **Alle weiteren Bausteine des Backup-Konzepts leiten sich aus der Klassifizierung ab.**

**Ziele und Nutzen:** differenzierter Schutzbedarf, **Priorisierung** geschäftskritischer Daten, **Compliance** (DSG, Aufbewahrungspflichten), **Kostensenkung** (nicht alles braucht Höchstschutz), **Transparenz** (welche Daten wo, wer verantwortlich). Ohne Klassifizierung gilt: Entweder ist alles überteuert geschützt, oder sensible Daten sind unterschützt.

**Klassifizierungsstufen:**

> ⚠️ **Die Quellen verwenden unterschiedliche Stufenmodelle:**
> *   **Folien Block 2/3:** 4 Stufen: Öffentlich – Intern – Vertraulich – **Streng vertraulich**. Block 3 nennt zusätzlich «**Gesetzlich**» (revisionssichere, unveränderbare Speicherung).
> *   **Folien Block 4:** Öffentlich – Intern – Vertraulich – **Streng-Geheim**.
> *   **Artikel 2.3:** 5 Kategorien: Öffentlich – Intern – Vertraulich – **Geheim** – **Personendaten**. Personendaten sind eine **Sonderkategorie**, weil sie die informationelle Selbstbestimmung schützen und nicht nur den Firmenwert.

| Stufe | Beschreibung | Beispiele | Typische Schutzmassnahmen (Musterlösung 2.3) |
| :--- | :--- | :--- | :--- |
| **Öffentlich** | frei zugänglich, Veröffentlichung erwünscht. Nur **Integrität** und Verfügbarkeit zählen | Webseite, Medienmitteilung, Werbeflyer, Kantinenmenü | keine Zugangskontrolle/Verschlüsselung, wöchentliches Backup |
| **Intern** | nur für Mitarbeitende, der Standard (Default) | Telefonbuch, Richtlinien, Organigramm, Protokolle | Firmennetz/SSO, TLS, tägliches Backup, 1 Jahr Retention |
| **Vertraulich** | eingeschränkter Personenkreis, **Need-to-know** | Finanzdaten, HR/Lohndaten, Budgets, M&A, Partnerverträge | RBAC, Verschlüsselung (AES-256), tägliches georedundantes Backup, 10 Jahre, Access-Logging |
| **Streng vertraulich / Geheim** | unbefugter Zugriff **existenzgefährdend** | Quellcode, Rezepturen/Patente, Mandantendossiers (Anwaltsgeheimnis), Prozessstrategien | individuell mit MFA, Verschlüsselung auf Dateiebene, Isolation, Offline-Kopie, lückenloser Audit-Trail, zertifizierte Löschung |
| **Personendaten** (Sonderfall) | Schutz nach **DSG**, «besonders schützenswerte Personendaten» (Gesundheit u. a.) | CRM, AHV-Nr., HR-Dossiers, Patientenakten (EPD) | strikte Zugriffskontrolle, Verschlüsselung, Löschkonzept, Meldepflicht bei Verlust |

**Rollen und Verantwortlichkeiten:**
*   **Dateneigentümer (Data Owner):** fachlich verantwortlich, legt die Klassifizierungsstufe fest und vergibt Zugriffsrechte, z. B. die Leitung Marketing für das CRM.
*   **IT-Abteilung / Data Custodian:** setzt die technischen Schutzmassnahmen um und **haftet für die technische Umsetzung** (Patching, Verschlüsselung).
*   **Management/GL:** genehmigt das Schema, stellt Ressourcen bereit, erlässt verbindliche Weisungen («**Tone from the Top**», Information Security Policy).
*   **Mitarbeitende:** müssen die Vorgaben einhalten.
*   **Revision:** prüft unabhängig und meldet Abweichungen.
*   Die Einstufung erfolgt **nie durch die IT allein**, sondern durch den Data Owner mit Datenschutzbeauftragtem (DPO) und Compliance.

**Schutzbedarfsanalyse:**
*   **Dimensionen:** **Vertraulichkeit, Integrität, Verfügbarkeit** (CIA-Triade / VVI). Dazu kommen **Nachvollziehbarkeit** (Audit Trails) und **Beweiskraft** (unveränderbare WORM-Archive gelten vor Gericht als Beweismittel).
*   **Stufen:** meist **normal – hoch – sehr hoch**.
    *   **Normal:** rechtfertigt nur Grundschutz, sonst übersteigen die Schutzkosten den Wert.
    *   **Hoch / sehr hoch:** rechtfertigt und **erzwingt** kostenintensive Massnahmen.
*   **Schadensszenarien:** finanziell, Reputation, rechtlich, **Personenschäden** (Beispiel: gelöschte Penicillin-Allergie in der Patientenakte = Integritätsverletzung mit Lebensgefahr).
*   **Ergebnis:** Daraus werden technische und organisatorische Massnahmen (**TOM**) abgeleitet und nachvollziehbar dokumentiert. Das ist die Basis des Sicherungskonzepts.

**Klassifizierungskriterien für Applikationen und Datenbestände:**

| Kriterium | Frage | Auswirkung auf das Konzept |
| :--- | :--- | :--- |
| **Volumen** | Wie viele Daten, wie schnelles Wachstum? | Speicherkapazität, **Backup-Dauer/-Fenster**, Bandbreite, Netzwerklast, Kosten, Skalierbarkeit; Gegenmittel Komprimierung/Deduplizierung; Wachstumsprognose über Historisierung; Archivierung entlastet den Primärspeicher |
| **Periodizität** (Änderungshäufigkeit / Change Rate) | Wie oft ändern sich die Daten? | Bestimmt **Sicherungsintervall und RPO**. Hochfrequente Daten (Transaktionen) → kurze Intervalle/CDP/Log-Backups; statische Archivdaten → selten. Nächtliche **Batchläufe** brauchen danach eine Sicherung, Logdateien eine Rotation, Konfigurationsänderungen sofortige Dokumentation, Systemzustand vor Updates sichern |
| **Zugriffssicherheit** | Wie sensibel? Wer darf zugreifen? | Verschlüsselung (Transport + Ruhe), MFA, **Least Privilege**, RBAC, zentrale lückenlose **Auditierung**, Prüfsummen für Integrität, **Vier-Augen-Prinzip** für Löschungen |

*   **Weitere Faktoren auf Applikationsebene:** **Geschäftskritikalität**, **Datenabhängigkeit** (eigene DB → konsistente Sicherung), **Nutzungszeiten** (24/7 vs. Bürozeit), **Integrationstiefe** (vernetzte Systeme zeitsynchron sichern). Daraus ergibt sich die **Recovery-Klasse** (RTO/RPO).
*   **Bewertungsmatrix (Musterlösung 3.1, SwissLogistics AG):** Jedes Kriterium wird mit 1–3 bewertet, die Summe ergibt die Backup-Priorität.
    *   Logistik-DB: Volumen 3, Periodizität 3, Sicherheit 2 = **8/9 → Tier 1 kritisch** (CDP auf Flash).
    *   HR-Akten: 1 + 1 + 3 = **5 → Tier 2** (täglich inkrementell, stark verschlüsselt, RBAC).
    *   Webseite: 2 + 1 + 1 = **4 → Tier 3** (wöchentlich Full + täglich inkrementell auf günstigem NAS/Object Storage).
*   **Zusammenspiel:** Hochsichere, sehr häufige Backups riesiger Datenmengen sind unverhältnismässig teuer, deshalb braucht es **bewusste Kompromisse** zwischen Sicherheit und Budget. Die Klassifizierung wird **regelmässig überprüft** (sie ist dynamisch).

**Vertiefte Klassifizierung (Block 4) – Dimensionen Verfügbarkeit, Sicherheit, Aufbewahrung, Kritikalität, Zugriffshäufigkeit:**

| Verfügbarkeitsklasse (Folien) | Tolerierter Ausfall | Konsequenz |
| :--- | :--- | :--- |
| **Hochverfügbarkeit** | wenige Minuten | teure, nahtlose Redundanz |
| **Standardverfügbarkeit** | einige Stunden | reguläres Backup/Restore |
| **Basisverfügbarkeit** | ~1 Tag | einfache Sicherung |

*   Jede Erhöhung der Verfügbarkeit steigert die Kosten **praktisch exponentiell**. Die Klasse definiert auch die vertraglichen Reaktionszeiten des Supports.
*   **Aufbewahrungsklassen (Retention):**
    *   **Kurzfristig:** temporäre Dateien, einige Wochen.
    *   **Mittelfristig:** Projektunterlagen, 3–5 Jahre.
    *   **Langfristig:** steuerrelevante Daten, **10 Jahre** auf unveränderbaren Medien.
    *   **Dauerhaft:** Gründungsurkunden, historische Verträge.
    *   Zu jeder Klasse gehört ein **Löschkonzept** (zertifizierte Vernichtung).
*   **Vorgehen Datenhaltungskonzept:**
    1.  Inventarisierung aller Applikationen und Datensammlungen.
    2.  Klassierung (Verfügbarkeit, Sicherheit, Aufbewahrung).
    3.  Regelwerk.
    4.  Lebenszyklus festlegen.
    5.  Stakeholder einbinden.
*   **Ableitung verbindlicher Vorgaben:** Streng geheime Hochverfügbarkeitsdaten liegen auf verschlüsseltem Flash, dauerhaft aufzubewahrende Daten auf Tape im Brandschutztresor.
*   **Tool-Unterstützung:** **Scanner** finden Muster (Kreditkarten-, AHV-Nummern), die Klassifizierung wird als **Metadaten-Label** gespeichert, **Office-Plug-ins** erzwingen die Einstufung beim Speichern, **DLP** (Data Loss Prevention) blockiert den Versand, Dashboards zeigen die Verteilung.
*   **Herausforderungen:**
    *   Datenwachstum.
    *   **Subjektivität:** Fachbereiche stufen alles zu hoch ein. Gegenmittel: **Chargeback**, also teuren Tier-1-Speicher intern verrechnen.
    *   Veränderliche Sensibilität.
    *   Ein zu komplexes Schema wird ignoriert.
    *   Die Nachklassifizierung von Altdaten ist aufwendig.
*   **Governance-Durchsetzung:** Richtlinien der GL, RBAC, **Verschlüsselungspflicht auf mobilen Geräten** (Full Disk Encryption: BitLocker/FileVault; ein verlorener Laptop ist dann «nur» ein Hardwareverlust), Cloud-Vorgaben (die Klasse bestimmt, ob Public Cloud oder Schweizer «Sovereign Cloud»), **Sanktionen** (Verwarnung bis Kündigung, Strafanzeige bei Spionage).

---

### **VIII. RPO, RTO, SLA und Verfügbarkeit**

**Die zwei zentralen Kennzahlen:**

| | **RPO – Recovery Point Objective** | **RTO – Recovery Time Objective** |
| :--- | :--- | :--- |
| **Frage** | Wie viel **Datenverlust** (in Zeit) ist tolerierbar? | Wie lange darf das System **ausfallen**, bis es wieder produktiv läuft? |
| **Blickrichtung** | **zurück**: Zeit zwischen letzter Sicherung und Ausfall | **vorwärts**: Zeit vom Ausfall bis zur vollständigen Wiederherstellung |
| **Bestimmt** | **Sicherungsintervall/-frequenz** (Intervall ≤ RPO) | **Wiederherstellungstechnologie** und Restore-Durchsatz |
| **Kurze Werte erfordern** | häufige Inkremente, Log-Backups, Snapshots, **CDP**, **synchrone Replikation** (RPO = 0) | Snapshots, **Instant Recovery**, Hot Standby, Cluster, **aktive Replikation / Failover** |
| **Lange Werte erlauben** | tägliche/wöchentliche Backups, Tape | Restore von Disk, Tape, Cloud-Archiv |
| **Beispiel** | RPO 4 h = max. 4 Stunden Arbeit verloren → mindestens alle 4 h sichern | RTO 4 h = System spätestens 4 h nach Ausfall wieder nutzbar |

*   **Das RTO umfasst die ganze Prozesskette**, nicht nur das Kopieren: Hardware beschaffen (Lieferfristen!), Medien holen (Distanz zum Lager), OS/Applikation konfigurieren, Konsistenz prüfen, DNS umstellen.
*   **RPO und RTO sind unabhängig voneinander:** RPO 4 h und RTO 2 h bedeuten: Das System läuft nach 2 h wieder, es können aber 4 h Daten fehlen (Acronis-E-Book).
*   **Kostenkurve:** Mit sinkendem RPO/RTO steigen die Investitionen **überproportional/exponentiell**. Faustregel (Artikel 4.3): **Eine Halbierung des RTO verdoppelt oft die Infrastrukturkosten.** Extreme RTO-Anforderungen führen zu **Aktiv-Aktiv-Lösungen** statt Backup/Restore.
*   **Festlegung:** Die Werte sind eine **geschäftliche Entscheidung** (BIA), **schriftlich mit der Fachabteilung** zu vereinbaren und von der GL freizugeben. **«So schnell wie möglich» ist kein RTO.** Für **jede** Applikation wird ein konkreter Wert definiert.
*   **Nachweis:** Die tatsächlich erreichbaren Werte werden durch **Restore-Tests gemessen** und dokumentiert. Bei Abweichung (Test 12 h statt 4 h) muss sofort gehandelt werden.
*   **Business Impact Analysis (BIA) / Kritikalitätsanalyse:** Wie wichtig ist ein System für den Geschäftsbetrieb? Sie trennt **Kernsysteme** (ERP, Kassen: Ausfall führt sofort zu Umsatzeinbussen, braucht Geo-Redundanz/HA) von **Supportsystemen** (Intranet: toleriert kurzzeitigen Ausfall).
*   **Technologiekorridor:** Erst die Kombination aus RPO und RTO grenzt die möglichen Technologien ein. «RPO 0 und RTO 5 Min. mit Tape-Budget» geht nicht.

**Verfügbarkeitsklassen im Datenhaltungskonzept (Artikel 4.3):**

| Klasse | Kritikalität | RTO | Technik |
| :---: | :--- | :--- | :--- |
| **1** | sehr hoch, Ausfall nicht tolerierbar | **< 1 Stunde** | Hot Standby, synchrone Replikation, Clustering |
| **2** | wichtig | wenige Stunden | Warm Standby oder sehr schneller Restore |
| **3** | moderat | bis 1 Tag | tägliches Backup |
| **4** | gering | mehrere Tage | wöchentliche Sicherung |

*   **Hochverfügbarkeits-Design (Klasse 1):** **Redundanz N+1** (Server, Switches, zwei Provider, A/B-Stromeinspeisung, USV, Diesel), **synchrone Replikation**, **Clustering** mit Heartbeat und automatischem Failover, permanentes **Monitoring** mit Pikett-Alarmierung, **Wartung ohne Downtime** (Hot Swap, Last verschieben).

**Service Level Agreements (SLA):**
*   Ein SLA ist ein (internes oder externes) **Vertragswerk** zwischen IT und Fachbereich bzw. Dienstleister. Darin stehen **RTO/RPO und Verfügbarkeitsziele** (meist in %).
*   Messung und **Reporting** laufen über Monitoring (nicht «gefühlt»). **Eskalation** und bei Externen **Malus-/Vertragsstrafen**.
*   **Lebenszyklus:** an veränderte Rahmenbedingungen anpassen.
*   **Regel:** Mit einem externen Anbieter keine schlechteren Werte vereinbaren, als das interne Konzept verlangt.

> 🔎 **Ergänzung (Recherche) – «Neunen» der Verfügbarkeit (auf 365 Tage):**
>
> | Verfügbarkeit | max. Ausfall pro Jahr | pro Monat (≈30 T.) |
> | :--- | :--- | :--- |
> | 99 % | ≈ 3.65 Tage (87.6 h) | ≈ 7.2 h |
> | 99.5 % | ≈ 43.8 h | ≈ 3.6 h |
> | 99.9 % | ≈ 8.76 h | ≈ 43 min |
> | 99.95 % | ≈ 4.38 h | ≈ 22 min |
> | 99.99 % | ≈ 52.6 min | ≈ 4.3 min |
> | 99.999 % | ≈ 5.3 min | ≈ 26 s |
>
> Formel: *Ausfallzeit = (1 − Verfügbarkeit) × Betrachtungszeitraum*. Die Werte aus dem Kurs (99.9 % ≈ 8.7 h, 99.99 % ≈ 52 min) stimmen damit überein.

**Beispiel Musterlösung 3.2 (AlpinBank SA, «Zero Downtime für alles»):**
*   **E-Banking:** RPO 0–1 Min. (synchrone Spiegelung), RTO 5–15 Min. (automatisches Failover-Cluster). Sehr teuer, aber gerechtfertigt.
*   **Intranet:** RPO 24 h (nächtliches Backup), RTO 8–12 h (Next Business Day). Das kostet nur einen Bruchteil.
*   **Argument:** «Zero Downtime für alles» würde das IT-Budget voraussichtlich **verdreifachen**. Deshalb eine **«Zwei-Klassen-Gesellschaft»** in der IT-Architektur.

---

### **IX. Das Backup-Konzept**

**Was ist ein Backup-Konzept?** Ein **formelles, verbindliches Regelwerk** für das ganze Unternehmen, quasi ein «Vertrag» zwischen IT (Dienstleister) und Fachabteilungen (Dateneigentümer). Es regelt nicht nur Technik, sondern auch **Verantwortlichkeiten, Prozesse und Kontrollen**. Ohne Konzept gilt ein Backup als «grobe Fahrlässigkeit der Geschäftsführung».

**Pflichtinhalte je Applikation/Datenbestand:** **Periodizität** (Frequenz) · **Sicherungsart** · **Verfügbarkeit** (RTO/RPO, meist als SLA) · **Lagerung** (Medium, Ort, Zugang, Retention, Rotation, Entsorgung).

**Elemente eines Datensicherungskonzepts (Folie Block 3):** Architektur/Topologie, **Rollenverteilung**, **Prozessbeschreibung** (Erstellen und Prüfen der Backups), **Notfallplan** (erprobte Anleitung zur kompletten Wiederherstellung), **Lebenszyklus** (regelmässige Reviews).

**Sicherungsarten im Vergleich:**

| Sicherungsart | Was wird gesichert? | Backup-Dauer / Speicher | Restore | Bemerkung |
| :--- | :--- | :--- | :--- | :--- |
| **Vollsicherung** (Full) | alle Daten | lang / sehr viel Speicher | **am einfachsten und schnellsten** (1 Satz) | höchste Konsistenz, technisch einfach |
| **Inkrementell** | Änderungen seit dem **letzten Backup** (Full oder Inkrement) | **am schnellsten, am kleinsten** | **komplex**: Full + **alle** Inkremente in Reihenfolge | ein defektes Glied macht alle folgenden wertlos. Faustregel Acronis: tägliche Inkremente ≈ 3–5 % eines Fulls |
| **Differenziell** | Änderungen seit dem **letzten Full** | wächst täglich an | **2 Sätze**: letztes Full + letztes Differenzielles | guter Kompromiss |
| **Synthetisch voll** | Software **berechnet** aus altem Full + Inkrementen ein neues Full | spart Übertragung | wie Full | mit Deduplizierung kaum Zusatzspeicher |
| **Incremental Forever** | nur einmal Full, danach nur Inkremente | sehr effizient | über Software/Synthese | **nicht direkt auf Tape** möglich, nur Disk-to-Disk(-to-Tape) |
| **CDP** (Continuous Data Protection) | **jede Schreiboperation** in Echtzeit (Journal) | permanente Last, viel Speicher | **jeder beliebige Zeitpunkt** | RPO ≈ 0, teuer, nur Tier 1 |
| **Snapshot** | Momentaufnahme (Zeiger/Metadaten) auf dem Storage | Sekunden | Sekunden, auf demselben Storage | **ersetzt kein Backup** (gleiche Hardware) |

*   **Kombinationen** sparen Platz und Zeit, z. B. Sonntag Full, Montag–Samstag inkrementell oder differenziell.
*   **Beispiel inkrementell:** Full am Sonntag, Ausfall am Donnerstag → Full + Mo + Di + Mi einspielen. **Beispiel differenziell:** Full am Sonntag + Differenzielles vom Mittwoch.

**Periodizität:**
*   **Tagessicherung:** Basisintervall (nachts ausserhalb der Kernzeit), RPO ≈ 24 h.
*   **Wochensicherung:** meist Vollsicherung am Wochenende (grösseres Backup-Fenster), dient als «Ankerpunkt».
*   **Monatssicherung:** Langzeitaufbewahrung, lange unentdeckte Fehler, **Compliance** (OR).
*   Das **Intervall muss kleiner oder gleich dem RPO sein.** Kurze Intervalle erhöhen Last und Kosten.

**Generationenprinzip Grossvater-Vater-Sohn (GFS / GVS):**

| Generation | Rhythmus | Typische Aufbewahrung |
| :--- | :--- | :--- |
| **Sohn** | täglich (z. B. Mo–Do) | 1–2 Wochen |
| **Vater** | wöchentlich (z. B. Freitag, Full) | ca. 1 Monat (4–5 Wochen) |
| **Grossvater** | monatlich/jährlich | 1 Jahr oder länger, oft als unveränderbares Archiv ausgelagert (z. B. auf Tape im Tresor für 10 Jahre) |

*   **Türme von Hanoi (TVH):** Das Acronis-E-Book empfiehlt dieses effizientere Rotationsschema nach dem Muster des Puzzles (binäres Muster, verteilt Backups gut auf verschiedene Medien). Es ist komplex und sollte deshalb von der Software automatisiert werden.
*   **Einfachste Retention** («immer das älteste löschen, wenn der Speicher voll ist») ist **nicht empfohlen**, weil man bei spät entdeckten Problemen alte Stände braucht.
*   Funktional reichen oft 4–6 Monate, rechtlich (Steuer, OR) kann es länger sein. Nach Projektabschluss genügt oft die finale Dokumentversion.

**Speichermedium und Lagerung:**
*   **Disk** (HDD/SSD, NAS/SAN): schnell, für Söhne und Väter. **Tape** (LTO): günstig, langlebig (bis 30 Jahre), offline, für Grossväter. **Cloud:** skalierbar, automatisch offsite.
*   **Hybride Verfahren:** **D2D2T** (Disk-to-Disk-to-Tape) und **D2D2C** (Disk-to-Disk-to-Cloud). Das primäre Backup geht schnell auf Disk, danach wird asynchron auf Tape oder in die Cloud kopiert.
*   **Grundsatz aus dem Fallbeispiel: «Backup to Disk first».** Das erste Backup wird immer auf Disk geschrieben, Tape nur als zweite Kopie.
*   **Aufbewahrungsort:** mindestens eine Kopie **offsite**. **Zugangsregelungen** zum Tresor bzw. Cloud-Tenant, **Vier-Augen-Prinzip**. Transport durch **Sicherheitskuriere** mit lückenloser **Chain of Custody**.
*   **Retention und Medienrotation:** Die Retention richtet sich nach Gesetz und Compliance. Regelmässige, dokumentierte Rotation verhindert volle Medien und Verschleiss («immer dasselbe Band überschreiben» erhöht das Defektrisiko).
*   **Sichere Entsorgung (End of Life):** **kryptographische Löschung / Mehrfach-Überschreiben** (z. B. DoD 5220.22-M), **Degaussing** (Entmagnetisierung), **physisches Schreddern** nach **DIN 66399**. Es wird immer ein **Vernichtungszertifikat** ausgestellt (Nachweis im Audit).

**Verschlüsselung und Schlüsselmanagement:**
*   **Data in Transit:** z. B. **TLS 1.3**. **Data at Rest:** z. B. **AES-256**.
*   **Schlüsselmanagement ist die kritischste Komponente:** Schlüssel **nie am gleichen Ort wie die Backups**, z. B. in einem **HSM** (Hardware Security Module) mit Rotation und Notfallwiederherstellung. **Ist der Schlüssel weg, ist das Backup weg.** Beispiel Musterlösung/Folie Block 8: Die Patientendatenbank konnte nicht wiederhergestellt werden, weil der Verschlüsselungskey unauffindbar war.
*   Ein verlorenes, aber AES-verschlüsseltes Band ist **kein meldepflichtiger Datenschutzvorfall**.

**Datenkonsistenz:**
*   **Crash-konsistent:** entspricht einem Stromausfall. Dateien sind strukturell intakt, aber RAM-Inhalte und halbe Transaktionen fehlen.
*   **Applikationskonsistent:** Die Applikation wird vor dem Snapshot in einen konsistenten Zustand versetzt (**Quiescing**). Unter Windows geschieht das über **VSS** (Volume Shadow Copy Service) mit **VSS-Writern** für SQL und Exchange. Für Datenbanken ist das **Pflicht** (Beispiel: Geld abgebucht, Lager aber nicht reduziert → inkonsistent).

---

### **X. Von 3-2-1 zu 3-2-1-1-0, Air-Gap und Immutability**

**Die klassische 3-2-1-Regel** (weltweiter «Goldstandard»):

| Ziffer | Bedeutung | Zweck / Umsetzung |
| :---: | :--- | :--- |
| **3** | **drei Kopien** der Daten (Original + 2 Backups) | kein Single Point of Failure. Kopie 1 = Produktion, Kopie 2 = lokales Backup für schnellen Restore, Kopie 3 = weitere Absicherung. Mehrere historisierte Versionen schützen vor schleichender Korruption |
| **2** | auf **zwei verschiedenen Medientypen** | Schutz vor Serienfehlern einer Hardwaregeneration/Charge, Firmwarefehlern, unterschiedlicher Lebensdauer. Z. B. Disk + Tape oder Disk + Cloud (S3). Ein **Protokollwechsel** (SMB → S3/HTTPS) erhöht die Sicherheit zusätzlich |
| **1** | **eine Kopie extern (offsite)** | Schutz vor Brand, Wasser, Erdbeben, Diebstahl. **Geografisch weit genug** entfernt (anderer Brandabschnitt/Erdbebenzone), per verschlüsseltem VPN, Cloud oder Kurier mit Bändern in Bunker/Tresor |

**Schwachstelle der 3-2-1-Regel:** Sind alle Kopien **online/netzwerkgebunden** (SMB/NFS), kann Ransomware alle gleichzeitig verschlüsseln (Beispiel NotPetya). Deshalb die Erweiterung:

**Die erweiterte 3-2-1-1-0-Regel** (heute «Mindeststandard»):
*   **3** Kopien, **2** Medien, **1** offsite, wie oben.
*   **1 Kopie offline (air-gapped) ODER unveränderbar (immutable):** die direkte Antwort auf Ransomware.
*   **0 Fehler:** Alle Backups werden **automatisch verifiziert**, regelmässige **Restore-Tests**. «**Kein Backup gilt ohne erfolgreiche Verifikation als gültiges Backup.**»

**Air-Gap (Luftspalt):**
*   **Physisch:** Das Medium ist nach dem Backup physisch vom Netzwerk und Strom getrennt (**Tape im Tresor**, RDX, externe Disk). Das ist der **sicherste** Schutz: «Ein Virus kann nicht auf Speicher zugreifen, der nicht verbunden ist.» Roboter in Tape Libraries können Medien automatisch stromlos schalten bzw. auswerfen.
*   **Virtuell/logisch:** isoliertes Netzsegment bzw. Immutability, das kommt einem Air-Gap nahe.

**Immutability / WORM / Object Lock:**
*   **WORM** = *Write Once, Read Many*. Einmal geschriebene Daten sind für eine definierte **Retention-Frist** (z. B. 30 Tage) **weder lösch- noch veränderbar**, **auch nicht durch Administratoren** mit Root-Rechten oder den Cloud-Provider.
*   Umsetzung: **S3 Object Lock im Compliance-Modus** (API lehnt Löschbefehle ab), **Linux Hardened Repository**, WORM-Tape, spezielle Hardware.
*   Das schützt auch vor **Innentätern** (gekündigter Admin) und gestohlenen Admin-Passwörtern.

**Automatisierte Verifikation («0»):**
*   Beispiel **Veeam SureBackup / Auto-Verify:** Die Software startet die gesicherte VM nach dem Backup in einer isolierten **Sandbox/«Bubble»**, prüft den Boot (Heartbeat), testet Dienste (z. B. SQL antwortet), scannt auf Malware, erstellt einen Bericht und fährt wieder herunter.
*   Zusätzlich werden **Prüfsummen/Hashes** beim Schreiben erzeugt und beim Lesen verglichen.

**Praxis-Architektur nach 3-2-1-1-0 (Artikel 3.2):**
*   **Kopie 1 – Performance-Tier:** lokales Disk-/Dedup-Backup für schnelle Restores (tiefes RTO).
*   **Kopie 2 – Redundanz-Tier:** anderer Speicher/Medientyp, anderer Brandabschnitt.
*   **Kopie 3 – DR-Tier (offsite):** Schweizer Cloud oder zweiter Standort (Datenschutz).
*   **Kopie 4 – Air-Gap-Tier:** Tape oder Wechselmedium, physisch getrennt.
*   **0 Fehler:** Skripte, Prüfsummen, Restore-Tests, Compliance-Report an CISO/GL.

**RAID ist kein Backup (Infoblatt «RAID-Übersicht»):** RAID schützt vor dem **Ausfall einzelner Festplatten** (Hochverfügbarkeit), **nicht** vor versehentlichem Löschen, Ransomware, Dateikorruption oder Elementarschäden.

| RAID | Prinzip | Vorteile | Nachteile | Min. Disks | Nutzkapazität (n Disks à C) |
| :---: | :--- | :--- | :--- | :---: | :--- |
| **0** | Striping, keine Redundanz | max. Performance, 100 % Kapazität | **keine Ausfallsicherheit**: eine Disk weg = alles weg | 2 | n × C |
| **1** | Mirroring | hohe Ausfallsicherheit, schnelles Lesen, schneller Rebuild | 50 % Kapazitätsverlust, Schreiben wie eine Einzeldisk | 2 | C (bei 2 Disks) |
| **5** | Striping + einfache Parität | gute Balance, 1 Disk darf ausfallen | Paritätsberechnung bremst Schreiben, **sehr langsamer, belastender Rebuild** | 3 | (n − 1) × C |
| **6** | Striping + doppelte Parität | **2 Disks** dürfen gleichzeitig ausfallen | noch langsameres Schreiben, intensiver Rebuild | 4 | (n − 2) × C |
| **10** | Mirroring + Striping (1+0) | sehr schnell, hohe Sicherheit, schneller Rebuild | 50 % Verlust, hohe Kosten | 4 | n/2 × C |

*   **Empfehlung:** **RAID 10** für kritische Datenbanken und Virtualisierung, **RAID 6** für grosse Archiv-«Datengräber». **RAID 5** wird bei sehr grossen Disks zunehmend vermieden (Lesefehler während des Rebuilds).
*   **Fazit Infoblatt:** «Das RAID sorgt dafür, dass die Benutzer beim Ausfall einer Festplatte am Dienstagmorgen weiterarbeiten können. Die 3-2-1-1-0-Strategie stellt sicher, dass das Unternehmen einen Ransomware-Angriff oder einen Rechenzentrumsbrand überlebt.»

**Auslagerung in die Schweizer Cloud (Folie Block 3):** Die Daten verlassen das **Schweizer Territorium** nicht (Rechtsraum), gute Glasfaserinfrastruktur, **FINMA**-Konformität, Geo-Redundanz der Anbieter, politische Stabilität.

---

### **XI. Backup vs. Disaster Recovery**

| Merkmal | **Backup** | **Disaster Recovery (DR)** |
| :--- | :--- | :--- |
| **Fokus** | **Daten und Dateien**, Datenintegrität, historische Kopie, Versionierung | **gesamte IT-Betriebsfähigkeit** (Daten + Systeme + Netzwerk + Applikationen + Prozesse), **Geschäftsfortführung** |
| **Leitfrage** | «Haben wir die Daten noch?» | «Können Mitarbeitende damit arbeiten und Kunden bedient werden?» |
| **Auslöser** | kleinere, lokal begrenzte Verluste, Alltagsaufgabe, Betrieb läuft weiter | **schwerwiegende Katastrophe**, formeller **Management-Entscheid**, Krisenstab |
| **Granularität** | einzelne Datei, Mail, Tabelle | ganze IT-Landschaft (AD, Hunderte VMs, Netze) |
| **Zeitrahmen** | Minuten bis wenige Stunden | Stunden bis Tage (Systeme in fester Reihenfolge) |
| **Kennzahl** | orientiert sich stark am **RPO** | orientiert sich stark am **RTO** |
| **Infrastruktur** | Speichermedium genügt | **Ausweichinfrastruktur** (CPU, RAM, Netz, Standby, oft zweiter Standort) |
| **Kosten** | günstiger (z. B. ~CHF 5'000/Jahr) | deutlich teurer (Hot Site: mehrere 100'000 CHF/Jahr) |

**Gemeinsamkeiten:**
*   Beide brauchen **verifizierte Kopien der Produktionsdaten** (ein mitverschlüsseltes Backup lässt auch das DR scheitern).
*   Beide orientieren sich am **RPO**.
*   Beide müssen **geplant, dokumentiert und getestet** werden.
*   Beide brauchen klare **Verantwortlichkeiten und Eskalationswege**.
*   Sie sind **komplementär**: Ein funktionierendes Backup ist **Voraussetzung** für DR. Zusammengeführt werden sie im **Business-Continuity-Plan (BCP)**.

**Typische Anwendungsfälle:**
*   **Backup:** gelöschte Excel-Datei, logisch korrupte Datenbank(tabelle), gelöschtes Postfach.
*   **DR:** Defekt eines zentralen Hardware-Controllers mit langem Ausfall, **Brand** im RZ, Hochwasser, Erdbeben.
*   **Ransomware:** verlangt **oft beide Strategien** (Folie Block 4). Im Mobirama-Fall gilt sie als DR, weil die ganze Umgebung ausgefallen war.

**Entscheidungskriterien Restore oder DR:**
1.  **Schadensausmass:** Einzelne Daten bei intakter Hardware → Restore. Ganze Systeme weg → DR.
2.  **Ursache:** Benutzerfehler oder Defekt einer Einzelkomponente → Restore. Elementarereignis, Standortausfall (auch logisch, z. B. durchtrennte Glasfaser) → DR.
3.  **RTO-Abgleich:** Schafft der normale Restore das RTO (z. B. 2 h Restore bei 4 h RTO), braucht es kein teures DR.
4.  **Eskalationsmatrix:** z. B. «nach 3 h Diagnose nicht behoben ODER mehr als 3 Hosts ausgefallen → Krisenstab, DR-Stufe 1».

**Typische DR-Szenarien:** Rechenzentrumsausfall (Feuer, Wasser, Strom), Ransomware-Totalschaden inkl. Backups, langer Netzwerkausfall (Core-Switch-Firmware), Hardwaretotalschaden mehrerer Systeme, **Lieferantenausfall** (Cloud-Provider insolvent).

**DR-Strategien:**

| Strategie | Beschreibung | RTO | Kosten | Beispiel |
| :--- | :--- | :--- | :--- | :--- |
| **Cold Standby** | Räume vorhanden, Hardware nicht betriebsbereit, im Ernstfall liefern, aufbauen, installieren, Backups einspielen | Tage bis Wochen (realistisch > 48 h) | am günstigsten | leerer gemieteter Raum, Tape-Restore |
| **Warm Standby** | Systeme vorhanden, laufen teilweise, Daten **asynchron** repliziert (stündlich/täglich), manuelle Umschaltung (DNS, Dienste) | Stunden | mittel | Zweit-RZ in anderem Stadtteil, nächtliche DB-Kopie, ~4 h |
| **Hot Standby** | Spiegelsystem permanent aktiv und **synchron** (Active-Active/Active-Passive-Cluster), automatisches Failover | ≈ 0 (Sekunden/Minuten), RPO ≈ 0 | am teuersten (doppelte Hardware, Lizenzen, Dark Fiber) | Airline-Buchungssystem Zürich ↔ Genf |
| **Cloud-DR / DRaaS** | VMs werden in die Cloud repliziert, sind im Normalfall ausgeschaltet, im Ernstfall per Knopfdruck gestartet | Minuten bis Stunden | **OPEX**, Pay-as-you-go | Azure Site Recovery; Achtung Internetabhängigkeit, Vendor Lock-in, Datenschutz |

*   **Dark Site** (Acronis-E-Book): externer Raum mit minimaler Ausrüstung (v. a. Speicher). Backups werden dorthin übertragen und die Site wird periodisch zum DR-Test in Betrieb genommen. Das ist eine Zwischenlösung.
*   **Geografische Distanz:** Der DR-Standort darf nicht vom selben Ereignis betroffen sein. Zürich → nicht Winterthur (gleicher kantonaler Stromausfall), sondern Bern/Genf oder Cloud.
*   **Umfang eines DR-Plans:** Daten, Systeme/Hardware, **Netzwerke** (Routing, VPN, **DNS-Umstellungen werden oft vergessen**), Applikationen mit Abhängigkeiten, Betriebsprozesse (Entscheidungen, Kommunikation).
*   **DR-Plan / Runbook:** Wiederherstellungsreihenfolge (Tier 1: AD, Netzwerk, ERP-DB → Tier 2: Intranet → Tier 3: Archiv), Entscheidungsmatrix, Krisenstab, Eskalationsstufen, Kommunikation, **gedruckte Notfallpläne** (für den Fall ohne digitalen Zugriff), Protokollant mit Zeitstempeln.
*   **Rückführung (Failback):** Nach der Reparatur des Primär-RZ müssen die im DR-Betrieb entstandenen Daten zurücksynchronisiert werden. Das ist **genauso komplex** wie das Failover und muss getestet werden.
*   **Fallstricke:**
    *   Backup vorhanden heisst nicht, dass der Server schnell wieder läuft.
    *   Die Datenbank nützt nichts ohne den Applikationsserver.
    *   Das Ausweich-RZ muss die **volle Produktionslast** tragen.
    *   DNS wird vergessen.
    *   Zu wenig Tests.
*   **Lessons Learned** nach jedem Ereignis oder jeder Übung fliessen iterativ in den Plan ein.

**DR-Testverfahren (Folie Block 4):**

| Testart | Beschreibung |
| :--- | :--- |
| **Tabletop-Test** | Verantwortliche spielen das Notfallszenario am Tisch gedanklich Schritt für Schritt durch |
| **Simulation** | Ausfallsicherung isoliert in separaten Netzen testen, ohne den Betrieb zu stören |
| **Teilumschaltung** | einzelne Applikationen am Wochenende probeweise ins Notfall-RZ umleiten |
| **Volltest** | Haupt-RZ geplant abschalten, vollständige Übernahme durch die Zweitsysteme verifizieren |
| **Rückführung** | Test endet erst mit dem reibungslosen Zurückschwenken in den Normalbetrieb |

---

### **XII. Das Datenhaltungskonzept**

**Definition:** Ein **strategisches, normatives Leitdokument** (Data Storage Policy / Data Management Framework), verabschiedet vom Top-Management (CIO/VR). Es definiert das **«Was» und «Warum»** der Datenspeicherung, nicht das detaillierte technische «Wie». Aus ihm werden alle Richtlinien, SOPs und Konfigurationen abgeleitet. Ohne Konzept entstehen Datensilos und Sicherheitslücken. «Datenhaltungskonzepte sind **Chefsache** und kein IT-Thema» (Podcast-Titel).

*   **Ziele:** hohe **Verfügbarkeit**, strikte **Vertraulichkeit**, absolute **Integrität** (CIA/VVI) kritischer Geschäftsinformationen.
*   **Geltungsbereich:** verbindlich für **alle internen Systeme, Cloud-Dienste und externen Dienstleister** (Third-Party Risk, **Data Processing Agreement**, Audits beim Dienstleister, Data Residency z. B. in EU/CH wegen CLOUD Act).

**Data Lifecycle Management (DLM / ILM) – fünf Phasen:**

| Phase | Vorgabe | Beispiel |
| :--- | :--- | :--- |
| **1. Erfassung** (Creation/Capture) | bei Entstehung **klassifizieren** (Metadaten), sicher speichern, «Security by Design» | Scan eines Arztgutachtens: Dropdown «Gesundheitsdaten», danach automatisch «streng vertraulich» und verschlüsselt |
| **2. Aktive Nutzung** (Hot Data) | hohe Performance (IOPS), **schnelle tägliche/stündliche Sicherungen**, enges RPO | Kassensystem/ERP auf All-Flash, stündliche Snapshots |
| **3. Inaktive Phase** (Warm/Cold) | selten genutzte Daten auf **günstigere Speicher** verschieben (Tiering), bleiben sichtbar | fertige CAD-Pläne von SSD auf HDD |
| **4. Archivierung** | **unveränderbar und gesetzeskonform** (WORM) langfristig aufbewahren, **Archiv ≠ Backup** | Rechnungen 10 Jahre auf Tape/Cloud-Archiv mit Sperrfrist |
| **5. Löschung** | nach Fristablauf **nachvollziehbar, sicher und endgültig** vernichten (Datenminimierung) | Personalakten nach 10 Jahren: Schreddern, Vernichtungszertifikat an CISO |

**Verantwortlichkeiten:** **RACI-Matrix** (Responsible, Accountable, Consulted, Informed) gegen **Verantwortungsdiffusion**. **Data Owner** (fachlich, definiert Anforderungen) und **Data Custodian** (technische Umsetzung, **haftet dafür**) sind strikt getrennt. Beispiel: Ein fehlender Patch geht auf den CISO bzw. die IT-Infrastrukturleitung, nicht auf den Owner.

**Technische und operative Umsetzungsvorgaben:**
*   **Backup-Strategie:** Frequenz (RPO) und Aufbewahrung pro Klasse. Beispiel: ERP-RPO 15 Min., also viertelstündlich inkrementell; operative Backups 30 Tage, monatliches Full 10 Jahre im Archiv.
*   **Auslagerung:** kritische Sicherungen an einen **zweiten, geografisch getrennten Standort** (3-2-1).
*   **Zugriffskontrolle:** Zero Trust, IAM, **MFA** (Wissen + Besitz, z. B. FIDO2-Key + Biometrie), Conditional Access.
*   **Verschlüsselung:** verbindliche Algorithmen, **TLS 1.3** (Transit) und **AES-256** (at Rest, BitLocker/FileVault).

**Physische Speicherarchitektur / Tiering:**
*   **Primärspeicher:** All-Flash (NVMe/SSD) für Hot Data, niedrige Latenz, teuer.
*   **Sekundärspeicher:** günstigere HDDs für Warm Data und als lokales kurzfristiges Backup-Ziel.
*   **Archivspeicher:** **Objektspeicher oder Magnetband** (WORM, stromlos) für Cold Data und gesetzliche Aufbewahrung.
*   **Cloud-Storage:** skalierbare Ergänzung (Pay-per-Use), z. B. S3 Glacier für Petabyte-Archive.
*   **Automated Storage Tiering / HSM** (Hierarchical Storage Management): Daten wandern je nach Nutzung automatisch zwischen den Klassen. Beispiel Röntgenbild: Tag 1 Flash, nach 30 Tagen HDD, nach 5 Jahren Tape/Cloud. Der Arzt sieht weiterhin nur eine Datei.

**Kontrolle, Auditierung, Qualitätssicherung (PDCA – Check):** interne Audits, **Zugriffsreviews** (Access Recertification gegen «**Privilege Creep**»), tägliche **Backup-Kontrolle** mit schriftlicher Dokumentation, **Restore-Tests**, **automatisierte Sicherheits-Scans** (DLP/Data Discovery sucht z. B. AHV-Nummern auf offenen Laufwerken → Quarantäne).

**Vertiefung (Block 4) – das Konzept anwenden:**
*   **Auf neue Systeme übertragen (Onboarding):** **Gap-Analyse**, standardisierte Checklisten/ITSM-Workflows, **Security by Design**. Das System wird im Inventar klassifiziert und dokumentiert, **bevor** es produktiv geht (Beispiel Cloud-HR-System: SaaS-Vorgaben ergänzen, Datenstandort CH/EU vertraglich sichern).
*   **Auf bestehende Systeme anwenden (Legacy):** **Bestandsanalyse/Inventar** (Schatten-IT aufdecken), Metadaten aktualisieren, **Technologievergleich** (z. B. wöchentliches Tape im selben Brandabschnitt statt stündlicher Offsite-Sicherung), **priorisierter Massnahmenplan** (kritische Systeme und Personendaten zuerst).
*   **3-2-1 verankern:** als **Mindeststandard** mit **dokumentierten Ausnahmen** (z. B. rekonstruierbare Gen-Sequenzier-Rohdaten nur lokal), Datenschutzkonformität der Offsite-Kopie, Technologievorgaben (AES-256, Immutability), **Umsetzungsnachweis** (monatlicher Bericht).
*   **Mit DR verzahnen:** Die RTO/RPO-Werte aus dem Datenhaltungskonzept diktieren die DR-Architektur (async vs. sync). Das Konzept schreibt **DR-Tests** vor (Tabletop bis Failover) und legt eine **Gesamtverantwortung** fest (CISO / IT Service Continuity Manager).

**Verbindliche Vorgaben – Sicherheit, Aufbewahrung, Speicherort (Artikel 4.3):**
*   **Sicherheit:** Verschlüsselungspflicht ab einer bestimmten Klasse, Übertragungssicherheit, Schlüsselverwaltung (HSM), Zugriff nach Need-to-know, **revisionssicheres Logging** jedes Zugriffs.
*   **Aufbewahrung:** Fristen je Kategorie (**OR 958f: 10 Jahre** vs. **DSG: löschen, wenn der Zweck entfällt**), **Archivklasse vs. Backup** (30 Tage vs. 10 Jahre WORM), nachweisbarer **Löschprozess**.
*   **Speicherort:** **Datenlokalisierung** in der Schweiz für sensible Daten (CLOUD Act), physische Sicherheit (Biometrie, Video, Brandschutz, Stickstoff-Löschanlage), externe Lagerung mit zertifiziertem Kurier.
*   **Umsetzung und Kontrolle:**
    *   **Konfigurationsstandards** und Automatisierung (Infrastructure as Code, technisches **Enforcement**).
    *   Tägliche Compliance-Scanner.
    *   **Ausnahmemanagement** (Risk Acceptance, befristet und genehmigt).
    *   **Auditfähigkeit** über unveränderliche Logs.

**Prüfkonzept zur Einhaltung der Vorgaben (Artikel 4.4):**
*   Ein systematischer Plan: **wie, wann, durch wen** geprüft wird.
*   **Prüfarten:** internes Audit, externes Audit (ISO 27001), technische Kontrolle (Monitoring), **Restore-Test als «Königsdisziplin»**.
*   **«Schrödinger-Backup»:** Ob ein Backup funktioniert, weiss man erst, wenn man es wiederherstellt.
*   **Restore-Tests:** fest im Jahresplan terminiert, verschiedene Szenarien (Datei, Datenbank, Full-Site), **isolierte Testumgebung**, Erfolgskriterien (RTO, RPO, Integrität), Testbericht.
*   **Protokollierung:** Start/Ende, Volumen, Status (Success/Warning/Failed), Objekte, **Trendanalyse** (z. B. +30 % statt +5 % Wachstum), **Management-Reporting** mit KPIs und automatischer Eskalation.
*   **Abweichungen:** Root-Cause-Analyse → Sofortmassnahmen → Massnahmenplan (Was? Wer? Bis wann?) → **Wirksamkeitskontrolle** → bei Wiederholung das Konzept anpassen (KVP).

---

### **XIII. Speichertechnologien**

**Grundsatz:** Die Speicherwahl ist das zentrale Element jedes Backup- und Archivkonzepts. **Alle Technologieentscheide basieren auf den Vorgaben des Datenhaltungskonzepts** (RPO/RTO, Klassifizierung) und werden regelmässig überprüft.

**Kategorien:**
*   **Primärspeicher:** hochperformant, produktiver Betrieb (All-Flash für DB/VMs).
*   **Sekundärspeicher:** günstiger, für Backups, Snapshots, warme/kalte Daten (HDD-Arrays).
*   **Archivspeicher:** tiefste Kosten pro GB, langsamer Zugriff, Compliance (Tape Library, 10 Jahre).
*   **Cloud-Storage:** extern, skalierbar, ortsunabhängig. **Hybrid-Storage** kombiniert On-Premises und Cloud (z. B. lokale Primärdaten, Backups in Amazon Glacier).

**Technische Kenngrössen:**
*   **Kapazität:** TB/PB.
*   **Durchsatz/Bandbreite:** MB/s bzw. GB/s, entscheidend für grosse sequentielle Datenströme (z. B. 8K-Videoschnitt).
*   **IOPS:** Input/Output Operations per Second, entscheidend für viele kleine parallele Zugriffe (z. B. Buchungssystem, Datenbank).
*   **Latenz:** Zeit bis zum Beginn der Datenübertragung, in ms bzw. µs (z. B. Hochfrequenzhandel).
*   **Skalierbarkeit:**
    *   **Scale-up:** mehr Disks in ein bestehendes System.
    *   **Scale-out:** zusätzliche Knoten im Cluster, bevorzugt bei starkem Wachstum. Vermeidet eine teure «**Forklift-Migration**».

**Kosten:**
*   **CAPEX** (Anschaffung: Hardware, Lizenzen, Installation) + **OPEX** (Strom, Kühlung, Rackplatz, Wartung, Support) = **TCO** (Total Cost of Ownership) über den ganzen Lebenszyklus.
*   Die Kosteneffizienz wird oft in **CHF pro TB** ausgedrückt.
*   **Die Kosten verhalten sich meist umgekehrt proportional zur Performance.**
*   **Tiered Storage** senkt die TCO: **Tier 0** NVMe-SSD (aktuelle CAD-Pläne) → **Tier 1** SAS-HDD (letzter Monat) → **Tier 2** Tape (abgeschlossene Projekte).

**Block-, File- und Object-Storage:**

| Merkmal | **Block-Storage** | **File-Storage** | **Object-Storage** |
| :--- | :--- | :--- | :--- |
| **Organisation** | gleich grosse Blöcke ohne Dateisystem, Adresse = **LUN**. Der **Server formatiert** selbst (NTFS, ext4, VMFS) | hierarchische Ordner/Verzeichnisse, das **Speichersystem verwaltet** das Dateisystem | **flacher Pool (Bucket)**: Daten + **frei definierbare Metadaten** + eindeutige ID |
| **Zugriff** | Fibre Channel (FC), iSCSI, NVMe-oF | **SMB/CIFS** (Windows), **NFS** (Linux/Unix) | **REST-API über HTTP(S)**, De-facto-Standard **Amazon S3** |
| **Performance** | **höchste**, geringste Latenz | mittel (Netz- und Protokoll-Overhead) | hoher sequentieller Durchsatz, **hohe Latenz** (HTTP), ungeeignet für Transaktionen |
| **Skalierung** | begrenzt, aufwendig | durch Disks erweiterbar, Grenzen bei sehr vielen Dateien | **praktisch grenzenlos** (horizontal, Standard-Hardware) |
| **Kosten** | **am höchsten** | mittel | **sehr günstig** bei grossen Volumen, Pay-as-you-go |
| **Einsatz** | **transaktionale Datenbanken** (nur ein 4-KB-Block wird geändert), **VMs**, E-Mail-DB | File-Sharing, Home-Laufwerke, Office/CAD-Kollaboration, Webinhalte | Backup-Ziel, Archive, Medien/Streaming, Big Data, Webapps, Röntgenbilder |
| **Besonderheit** | Verwaltung aufwendig, Fachwissen nötig | einfach, viele Nutzer gleichzeitig, File-Locking | Objekte werden **nicht geändert, nur überschrieben**, eingebaute Prüfsummen/Selbstheilung, Georedundanz, **Object Lock (WORM)** |

**Bereitstellungsmodelle DAS, SAN, NAS:**

| | **DAS** (Direct Attached Storage) | **SAN** (Storage Area Network) | **NAS** (Network Attached Storage) |
| :--- | :--- | :--- | :--- |
| **Anbindung** | direkt, exklusiv an **einen** Server (kein Netz) | **separates Hochgeschwindigkeitsnetz** (FC/iSCSI) mit HBAs und SAN-Switches | ins bestehende **LAN** (Ethernet) |
| **Zugriffsart** | Block | **Block** | **Datei** (NFS, SMB, teils iSCSI) |
| **Stärken** | tiefste Latenz, einfach, günstig | maximale Performance, **Hochverfügbarkeit** (redundante Komponenten, **Multipathing**, RAID), zentrale Zuteilung als virtuelle Laufwerke, SAN-Snapshots | einfach integrierbar, kostengünstig, AD-Rechte, Snapshots, Backup-Funktionen, ideal für KMU |
| **Schwächen** | keine Skalierung, keine gemeinsame Nutzung, Server weg = Daten weg | **teuer**, komplex | teilt die Bandbreite mit dem übrigen Netzverkehr, Engpässe bei hoher Last |
| **Sicherheitskonzept** | – | **Zoning**: legt fest, welcher Server mit welchem Speicher reden darf | AD-Integration, Verschlüsselung |

*   **Unified Storage:** ein System, das logisch Block (SAN) und File (NAS) trennt. Beispiel Musterlösung 5.1: ERP-DB auf SAN (All-Flash, Multipathing, 99.99 %), CAD-Ablage auf NAS (Tiering SSD→HDD). Gesichert wird das ERP über Storage-Snapshots mit Quiescing, das NAS über **NDMP**.
*   **Backup-Besonderheiten:** Block wird über **Snapshots/Replikation** gesichert. Bei File sichert man inkrementell nur geänderte Dateien, aber **Millionen kleiner Dateien** dauern oft viel länger als Block-Backups.

**Magnetband (Tape) und Archivierung:**
*   **Technik:** Daten werden **sequenziell** auf ein dünnes Kunststoffband geschrieben. Standard ist **LTO** (Linear Tape Open) mit Kompatibilität über Generationen. **LTFS** (Linear Tape File System) erlaubt Zugriff «wie auf einen USB-Stick». **Bariumferrit** ermöglicht höhere Dichte.
*   **Kapazität:** **LTO-9** fasst **18 TB nativ / 45 TB komprimiert** (2.5:1). Jede Generation verdoppelt die Kapazität nahezu.
*   **Lebensdauer:** bis **30 Jahre** bei korrekter Lagerung, **0 Watt** Strom im Regal (nachhaltig/«grün»).
*   **Tape Library:** Roboterarme laden Kassetten automatisch, mehrere Laufwerke sorgen für Redundanz, die Steuerungssoftware katalogisiert, beschriebene Bänder können entnommen und ausgelagert werden.

| Vorteile Tape | Nachteile Tape |
| :--- | :--- |
| **tiefste Kosten pro GB** (Faustregel Acronis: ab ca. 3 Jahren die billigste Backup-Methode) | **langsamer Zugriff** auf einzelne Dateien (Band holen, spulen, sequenziell lesen) |
| **echter physischer Air-Gap**, bester Ransomware-Schutz («Last Line of Defense») | **Logistikaufwand**, manueller Transport (fehleranfällig, Medium kann verloren gehen) |
| **Medienbruch** für die 2 in 3-2-1 | Laufwerksverschleiss (Wartung), Bandverschleiss durch häufiges Spulen |
| Langlebigkeit, Compliance (10 Jahre) kosteneffizient | **Tape-Streaming**: Laufwerke brauchen einen konstanten Datenstrom («Shoe-shining» bei Stopps), **Multiplexing** verschlechtert den Restore |
| hoher sequenzieller Durchsatz beim Schreiben | Restore oft mit **De-Staging** auf Disk, dadurch hohes RTO |

*   **Einsatzgebiete:** Spitalarchive, Forschungsrohdaten, TV-Medienarchive, **Cloud-Provider (kalte Speicherklassen)**, Banken (revisionssichere Transaktionsdaten).
*   **Argumentarium gegen die Abschaffung (Musterlösung 5.2):**
    1.  **Ransomware-Resilienz** durch Air-Gap (Disk/Cloud sind «online»).
    2.  **3-2-1 und Compliance**: Medienbruch, 30 Jahre Lebensdauer vs. 3–7 Jahre bei HDD, keine ständige Migration.
    3.  **TCO/Energie**: günstigste CHF/GB, 0 W.
    *   Empfehlung: hybrid **D2D2T**.

> 🔎 **Ergänzung (Recherche) – LTO-10:** Seit 2025 ist **LTO-10** verfügbar, mit **30 TB nativ (75 TB komprimiert)**. Im November 2025 kündigte das LTO-Konsortium eine **40-TB-LTO-10-Kassette (100 TB komprimiert)** an, die im selben LTO-10-Laufwerk läuft und seit Anfang 2026 ausgeliefert wird. Die Kompressionsrate bleibt bei 2.5:1. Der Folieninhalt (LTO-9 = 18/45 TB) bleibt korrekt, ist aber nicht mehr die neueste Generation.

**Deduplication Storage Appliances:**
*   **Prinzip:** Redundante Datenblöcke werden erkannt (**Hash = digitaler Fingerabdruck**, zentrale **Index-Datenbank**) und nur **einmal** gespeichert. Duplikate werden durch kleine **Zeiger (Pointer)** ersetzt.
*   **Inline vs. Post-Process:**
    *   **Inline:** Deduplizierung während des Schreibens, spart sofort Platz, braucht **viel CPU/RAM**, keine Landing Zone.
    *   **Post-Process:** erst unverändert schreiben, später (nachts) optimieren. Anfänglich schneller, braucht aber **temporären Zusatzspeicher**.
*   **Source vs. Target:**
    *   **Source:** Deduplizierung **auf dem Quellserver** vor der Übertragung, **entlastet das Netzwerk**. Bei Mehrfachsicherungen wird die Appliance nur gefragt: «Kennst du diesen Block schon?» (z. B. DD Boost).
    *   **Target:** Alles geht übers Netz und wird erst auf der Appliance reduziert, **entlastet die Quellserver**.
    *   Die Wahl hängt stark von der verfügbaren **Bandbreite** ab.

| Vorteile | Nachteile |
| :--- | :--- |
| Kapazitätsreduktion oft **> 90 %** (Raten 10:1 bis 50:1 je nach Daten; typisch 2:1 bis 20:1) | **Restore langsamer**: Daten müssen «rehydriert» (zusammengesetzt) werden, das beeinflusst das RTO |
| kürzeres Backup-Fenster | **komprimierte/verschlüsselte Daten** lassen sich kaum deduplizieren |
| schnelle **WAN-Replikation** (Aussenstellen, Cloud-Gateway) | **ein defekter Block** kann unzählige abhängige Dateien zerstören |
| mehr Versionen / längere Retention auf gleichem Platz, synthetische Fulls fast gratis | hohe Anschaffungskosten (starke CPUs), komplexe Integration |

*   **Ideal für:** viele gleichartige **VMs** (identische OS-Dateien), wiederholte **DB-Dumps**, **VDI**, Aussenstellen.
*   **Beispiel Musterlösung 5.3 (MediCare Bern AG):** 300 Windows-VMs, Backup über 18 h. Lösung: Appliance mit **Source-Deduplizierung** und **Inline**-Verfahren (kein Platz für eine Landing Zone). Erwartete Reduktion bei VMs 80–90 % (10:1–20:1), bei DB-Dumps bis 95 % (20:1). Das Backup-Fenster schrumpft auf etwa 2–4 h. **Risiko: Rehydrierung beim Restore** im Notfallplan berücksichtigen.
*   **Tipp aus Artikel 7.4:** Verschlüsselte Datenbanken zerstören die Dedup-Rate (15:1 → 1.2:1). Besser erst deduplizieren und dann auf der Appliance verschlüsseln (**Target-Side Encryption**).

**Object Storage im Backup:**
*   S3 als Backup-Ziel, **Object Lock** gegen Ransomware, **Tiering** in günstigere Cloud-Klassen, Georedundanz (z. B. **Erasure Coding** über Nodes), Kosten nur für belegten Platz.
*   **Nachteile:** HTTP-Latenz, keine Datenbank-Transaktionen, Objekte nur ganz überschreibbar, Bandbreite ins Internet, Migration alter File-Anwendungen aufwendig.
*   **Object Lock im Compliance Mode (Musterlösung 5.4):** Das Objekt wird z. B. 30 Tage auf API-Ebene gesperrt. **Weder ein Hacker mit gestohlenem Kundenpasswort noch ein böswilliger Provider-Admin** kann es löschen. «Digitales Bankschliessfach, dessen Schlüssel ein Notar für 30 Tage wegschliesst.»

**Technologievergleich (Artikel 5.2):**

| Technologie | Performance | Kosten | Typischer Einsatz | Ransomware-Schutz |
| :--- | :--- | :--- | :--- | :--- |
| **Block/SAN** | höchste, tiefste Latenz | höchste | Produktions-DBs, VMs | Snapshots (schnell, extrem kurzes RPO), aber netzwerkgebunden |
| **NAS** | mittel | mittleres Preis-Leistungs-Verhältnis | File-Sharing, Backup-Ziel KMU | Snapshots («Vorherige Versionen»), **nur solange der Admin-Zugang nicht kompromittiert ist** |
| **Object** | hoher sequentieller Durchsatz | sehr günstig bei Volumen | Backup-Ziel, Archive, Cloud | **Object Lock / Immutability** |
| **Tape** | hoher Schreibdurchsatz, hohe Zugriffslatenz | **günstigste pro GB** | Langzeitarchiv, Offsite | **höchster Schutz (Offline/Air-Gap)** |
| **Dedup-Appliance** | optimiert fürs Schreiben, Restore abhängig von Rehydrierung | teuer in der Anschaffung, langfristig wirtschaftlich | primäres Backup-Ziel | netzwerkgebunden, muss segmentiert werden |

> **Wichtig:** **Alle netzwerkgebundenen Speicher** (SAN, NAS, Appliance) sind potenziell durch Ransomware erreichbar. Deshalb **VLAN-Segmentierung, IAM, Zero Trust**.

---

### **XIV. Datensicherungstechnologien**

**Kategorien:**
1.  **Agenten-basiert:** Software auf dem Quellsystem.
2.  **Agentless / Hypervisor-API.**
3.  **Dateibasiert:** SMB/NFS/SFTP.
4.  **Snapshot-basiert.**
5.  **Replikation:** synchron/asynchron.
*   Ergänzend: **CDP** und **Cloud-/SaaS-Backup**.

**Einordnung nach Ebene:**

| Ebene | Beschreibung | Einsatz |
| :--- | :--- | :--- |
| **Block** | physische Datenblöcke, hohe Performance | grosse virtuelle Umgebungen, SAN |
| **Datei** | einzelne Dateien | unstrukturierte Daten, Fileserver |
| **Image** | komplettes Systemabbild inkl. OS, schneller Wiederanlauf | Hardwareausfall, Ransomware, **Bare-Metal-Restore** |
| **Applikation** | konsistent und transaktionssicher im Betrieb | Datenbanken, Mailserver, ERP |
| **Cloud** | API-basiert | SaaS (M365) und IaaS-Workloads |

*   **Auswahlkriterien:** **Systemtyp** (physisch/virtuell/Cloud), **Datenkonsistenz**, **Performance-Impact** auf die Produktion, **Integrationsaufwand**, **Skalierbarkeit**, Wiederherstellungs-Granularität, Betriebskosten/Lizenzen, Sicherheit/Compliance (FINMA, DSG), Wiederanlaufzeit.

**Agenten-basierte Datensicherung:**
*   **Funktionsweise:** Ein Software-Agent (Dienst/Daemon) läuft **im Betriebssystem** des Quellsystems. Er meldet sich beim Backup-Server, empfängt Jobs nach zentralem Zeitplan und überträgt die Daten verschlüsselt (**Source-Side Encryption**). Kernfunktionen: Applikation erkennen und **quiescen** (DB-Agent: Oracle **RMAN**, Exchange über **VSS-Writer**), transaktionssicher extrahieren, komprimieren/verschlüsseln, mit dem Server kommunizieren, lokal und zentral protokollieren.

| Vorteile | Nachteile |
| :--- | :--- |
| **hohe Granularität**: einzelne Dateien, DBs, Postfächer, Mails (**Item-Level-Restore**) | **Verwaltungsaufwand**: auf jedem System installieren, updaten, lizenzieren |
| **Applikationskonsistenz** über native Schnittstellen | **Ressourcenverbrauch** (CPU, RAM, I/O) auf den Produktivsystemen |
| **plattformunabhängig** (Windows, Linux, Unix, macOS), auch **physisch** | **Pro-Host-Lizenzen** werden bei vielen Servern teuer |
| Kompression, Verschlüsselung und **Quell-Deduplizierung** schon auf der Quelle | **Kompatibilität**: OS- oder Applikations-Updates brechen den Agenten |
| schneller selektiver Restore | **zusätzliche Angriffsfläche** (Agent mit hohen Rechten), lokale Manipulation möglich (Mobirama: Ausschlüsse ändern) |

*   **Einsatz:** **physische Server** (Bare Metal, die Standard-Methode), **Datenbanken** (Oracle, SQL, SAP), **Exchange/SharePoint**, **Endgeräte/Laptops** im Aussendienst, Spezialsysteme (Industriesteuerungen, Medizintechnik, CNC mit Hardware-Dongle), hybride Umgebungen.
*   **Fallbeispiel Mobirama:** Das Gerät muss **eingeschaltet** sein. Bare-Metal-Recovery muss explizit unterstützt und getestet werden, denn Treiberänderungen können den Restore scheitern lassen.

**Agentless / Hypervisor-API-basiert:**
*   **Funktionsweise:** Es wird **keine Software in der VM** installiert. Die Backup-Software spricht mit der **Hypervisor-API**:
    *   **VMware VADP** (vStorage APIs for Data Protection).
    *   **Hyper-V RCT** (Resilient Change Tracking).
*   Ablauf: Hypervisor-**Snapshot** → geänderte Blöcke lesen (**CBT – Changed Block Tracking**) → Snapshot löschen/konsolidieren. **Backup-Proxys** verarbeiten die Daten und entlasten die ESXi/Hyper-V-Hosts. Applikationskonsistenz entsteht über die **VMware Tools / Hyper-V Integration Services**, die im Gast einen VSS-Snapshot auslösen.

| Vorteile | Nachteile |
| :--- | :--- |
| **kein Agenten-Management**, weniger Kosten und Angriffsfläche | **Hypervisor-Bindung / Lock-in**, nur unterstützte Plattformen |
| **massive Skalierbarkeit** (Hunderte VMs zentral, neue VMs werden automatisch erkannt) | **nur virtuelle Systeme**, physische brauchen Agenten |
| **Image-basiert**: ganze VM inkl. Konfiguration in einem Vorgang | **Snapshot-Last / «VM Stun»** beim Erstellen/Konsolidieren |
| **CBT**: nur geänderte Blöcke, kleines Backup-Fenster, wenig Bandbreite | Applikationskonsistenz hängt an VMware Tools/Integration Services, sonst nur **crash-konsistent**. DBs brauchen oft trotzdem Agenten |
| Restore von ganzen VMs, Dateien oder Items aus demselben Image, **Instant Recovery**, **SureBackup** | Granularer Datei-Restore braucht Zusatzschritte (Image mounten). API-Änderungen bei neuen Releases |

*   **Einsatz:** VMware-Farmen, Hyper-V-Cluster (z. B. Veeam, Commvault, Rubrik), **Multi-Tenant/MSP** (keine Agenten im Kundensystem), Testumgebungen, Cloud-Integration (Azure/AWS).
*   **Praxis = hybrid:** VMs agentless, physische und kritische DB-Systeme mit Agenten, alles in einer zentralen Konsole (Beispiel Spital: Verwaltungs-VMs über VADP, physischer EPA-DB-Cluster mit DB-Agent).

**Dateibasierte Sicherung:**
*   **Funktionsweise:** Die Software durchläuft das Dateisystem («**Tree-Walking**») und kopiert Dateien über **SMB, NFS, SFTP** oder lokal. **NDMP** (Network Data Management Protocol) sichert grosse NAS-Systeme performant direkt vom Storage aufs Backup-Ziel, ohne das LAN zu belasten.
*   **Selektivität:** Einschluss/Ausschluss über Filter, z. B. `node_modules`, `.tmp`, `.iso` ausschliessen. **Achtung** (Acronis): Zu grosszügige Ausschlüsse sind ein häufiger Fehler, lieber in Speicher investieren.
*   **Versionierung** über die Zeit (z. B. Excel-Version vom Dienstag).

| Vorteile | Nachteile |
| :--- | :--- |
| **einfach** zu konfigurieren | **Performance-Einbruch bei Millionen kleiner Dateien** (Overhead je Datei), Block-Backup ist dort um ein Vielfaches schneller |
| **höchste Granularität** beim Restore (eine Datei in Sekunden) | **keine Systemsicherung** (OS, Registry, Applikationen), kein Bare-Metal-Recovery |
| **plattformunabhängig**, Dateien oft ohne Spezialsoftware lesbar | **offene/gesperrte Dateien** (File Lock) werden übersprungen oder inkonsistent gesichert, DBs brauchen VSS/Agenten |
| **Self-Service** («Vorherige Versionen»/Shadow Copies) | **Metadaten/ACLs** gehen evtl. verloren (Berechtigungsprobleme nach Restore) |
| wirtschaftlich für KMU | **Skalierungsgrenzen**: Tree-Walking über Hunderte Mio. Objekte sprengt das Backup-Fenster |

*   **Einsatz:** Fileserver/Netzlaufwerke, Dokumentenmanagement, Home-Verzeichnisse, **Ergänzung zum VM-Image-Backup** (z. B. zusätzlich alle 15 Min. nur den Upload-Ordner sichern), kleine IT-Umgebungen.

**Snapshots:**
*   **Copy-on-Write (CoW):** Beim ersten Überschreiben wird der **alte Block** zuerst in den Snapshot-Bereich **kopiert**, dann der neue geschrieben. Das kostet zusätzliche I/O (**Read-Modify-Write Penalty**).
*   **Redirect-on-Write (RoW):** Der neue Schreibvorgang geht auf einen **neuen freien Block**, der Snapshot behält den alten. Besser bei schreibintensiven Lasten (VDI-Boot-Storm), aber **Fragmentierung** bei vielen Snapshots.
*   **Stärken:** Sekunden für Erstellung und Rollback (z. B. vor Patches), sehr kurze Backup-Fenster, Basis für konsistente Backups und Self-Service-Restore.
*   **Grenzen:** **«Snapshots sind kein Ersatz für Backups»**, sie liegen auf **demselben Storage**. Lange laufende Snapshots belasten die Performance und verursachen Konsolidierungsprobleme. Empfehlung: Snapshot als **Kurzzeitwerkzeug (max. ~24 h)**, Image-Backup mit Offsite-Replikat als strategisches Mittel.

| Merkmal | Image-Backup | Snapshot |
| :--- | :--- | :--- |
| Speicherort | separates Backup-Ziel | originaler Storage |
| Mechanik | vollständige VM-Kopie inkl. Konfiguration | differenzielle Zeiger auf Blöcke |
| Nutzungsdauer | langfristig (Tage bis Jahre) | kurzfristig (Minuten bis Stunden) |
| Desaster-Schutz | ja (mit Offsite-Kopie) | **nein** |

**Replikation:**
*   **Synchron:** Die Applikation erhält das «Acknowledge» erst, wenn **beide** Standorte geschrieben haben. **RPO = 0**. Latenzbedingt nur über **kurze Distanzen** (meist max. 50–100 km).
*   **Asynchron:** sofortige lokale Bestätigung, zeitversetzte Übertragung (Batch oder kontinuierlich). Beliebige Distanz (z. B. Basel → Singapur), **RPO > 0** (Minuten bis Stunden). Die Replikationsrate muss **grösser als die Change-Rate** sein, sonst entsteht ein Rückstau.
*   **Wichtig:** **Replikation schützt nicht vor logischen Fehlern.** Löschung oder Verschlüsselung werden sofort mitrepliziert («der Datenverlust wird hochverfügbar gemacht»). Deshalb immer mit versionierten Backups oder unveränderlichen Snapshots kombinieren.

> 🔎 **Ergänzung (Recherche) – Lichtgeschwindigkeit in Glasfaser:** ca. **5 µs pro km** (≈ 200'000 km/s). 100 km bedeuten ≈ 0.5 ms pro Richtung bzw. **≈ 1 ms Round-Trip** (ohne Switch-/Storage-Overhead). Synchrone Replikation verlangt typischerweise < 2 ms RTT, daher die Faustgrenze von **~100 km**.

**Cloud-Backup:**
*   **Vorteile:** kein CAPEX für einen Zweitstandort, skalierbar, Pay-as-you-go, Offsite «mit wenigen Klicks», **S3-kompatibel**, **S3 Object Lock** (Immutability).
*   **Nachteile:**
    *   **Bandbreite beim Restore**: 50 TB über 1 Gbit/s dauern mehr als 4 Tage.
    *   **API- und Egress-Gebühren** (Download kostet).
    *   Abhängigkeit vom Provider.
*   **Initial Seeding:** Das erste Voll-Backup wird per Disk zum Provider geschickt, im Notfall auch zurück.
*   **Schweiz:** Datenschutz (DSG, FINMA), **US CLOUD Act** (US-Behörden können unter Umständen auf Daten von US-Firmen im Ausland zugreifen). Deshalb oft **Schweizer Anbieter mit Data Residency CH** und **BYOK**.

**Continuous Data Protection (CDP):**
*   Ein Filtertreiber oder Agent fängt **jeden Schreibvorgang** ab (**Split-Write**) und schreibt ihn mit Zeitstempel in ein **Journal** («Flugdatenschreiber»).
*   **RPO ≈ 0** und **Any-Point-in-Time Recovery** («Rewind» auf 14:32:14, eine Sekunde vor dem Vorfall).
*   **Kosten:** doppelte Schreiblast, schnell wachsendes Journal, braucht schnellen Speicher. Deshalb **nur für Tier-1-Systeme** (ERP, Kernbanken, Shop-DB zum Black Friday).

**Eignung nach Systemtyp (Artikel 6.4):**

| Systemtyp | Geeignetste Methode |
| :--- | :--- |
| **Physische Server** | **Agenten-basiert** (VSS, Bare-Metal-Restore) |
| **Virtuelle Maschinen** | **Hypervisor-API (agentless)**, CBT |
| **Dateiserver** | dateibasiert bzw. **NDMP** bei grossen NAS |
| **Datenbanken** | **Datenbank-Agenten** / applikationsspezifisch, **Log-Backups** z. B. alle 15 Min. (Point-in-Time) |
| **Cloud-Workloads** | **Cloud-native Backup-Dienste** (z. B. AWS Backup) / S3-Ziele, keine Egress-Kosten |

**Eignung nach RPO und RTO:**

| Anforderung | Geeignete Technologie |
| :--- | :--- |
| **RPO < 1 h** (Sekunden/Minuten) | **CDP** oder **synchrone Replikation** |
| **RPO 1–4 h** | häufige **inkrementelle Hypervisor-Backups** (CBT) oder **Storage-Snapshots** |
| **RPO 4–24 h** | **tägliche** agenten- oder dateibasierte Backups (nachts) |
| **RPO > 24 h** | **Tape** oder wöchentliche Cloud-Backups |
| **RTO < 1 h** | **Instant Recovery** aus Snapshots/Backup-Speicher, **aktive Replikation** |
| **RTO 1–4 h** | agentless VM-Backups mit Instant Recovery, performante Dedup-Speicher |
| **RTO 4–24 h** | agenten-/dateibasierte Backups auf schnellem **Disk**-Speicher |
| **RTO > 24 h** | **Tape-Restore**, Cloud-Archiv (z. B. Glacier) |

*   **Kombinieren (Tiering):** z. B. Spital: tagsüber Snapshots alle 15 Min., nachts ein Voll-Backup auf Disk, am Wochenende Tape (Air-Gap).
*   **Instant (VM) Recovery:** Die VM startet **direkt aus dem Backup-Speicher** (in Minuten). Die Daten werden im Hintergrund zurückmigriert (Storage vMotion). **Achtung:** Der Backup-Speicher arbeitet dann temporär als Produktivspeicher, deshalb vorher eine Engpassanalyse.

**Entscheidungsmatrix / Nutzwertanalyse:**
1.  Kriterien (Performance, Kosten, Sicherheit, Compliance, Wiederherstellbarkeit, Integration).
2.  Unternehmensspezifische **Gewichtung** (z. B. Online-Shop: Performance 40 %, Kosten 20 %; Gemeindearchiv: Kosten 40 %, Skalierbarkeit 30 %, Performance 10 %).
3.  **Scoring** je Technologie.
4.  **Shortlist** der besten drei → **Proof of Concept**.
5.  **Entscheid durch die GL**.
*   Die **Begründung, der Eignungsnachweis und die verworfenen Alternativen** (mit Grund) werden im Konzept dokumentiert, dazu Testplan und Review-Zyklus.

**Microsoft 365 / SaaS – Shared Responsibility (Veeam-E-Book, Musterlösung 6.4):**
*   Der Provider garantiert **Infrastruktur und Service-Verfügbarkeit** (Redundanz/Replikation), **nicht** den Schutz vor versehentlichem Löschen, Ransomware, Insidern oder Compliance-Lücken. **Redundanz ≠ Backup:** Gelöschte oder korrupte Daten werden mitrepliziert.
*   **Retention-Lücken:** Exchange «Recoverable Items» (Standard 14 Tage, max. 30), SharePoint/OneDrive-Papierkorb 93 Tage, danach ist die Datei endgültig weg. Teams hat eigene Richtlinien. **Retention-Policy ≠ Backup.**
*   Microsoft ist **Data Processor**, der Kunde **Data Owner**. Deshalb braucht es eine eigene **SaaS-Backup-Lösung** (Drittanbieter).

**Agentenbasierte Backup-Software (Infoblatt, Auswahl):**
*   **Kommerziell:** Acronis Cyber Protect, **Veeam Agent**, Commvault, Arctera (ex Veritas) Backup Exec, MSP360, Druva (SaaS), EaseUS, Zmanda Pro.
*   **Open Source:** **Bacula**, **Bareos** (Fork), **Amanda**, BackupPC, **BorgBackup**, **Restic**, Duplicity, rsnapshot (rsync + Hardlinks).
*   **Plattformspezifisch:** Proxmox Backup Client, **Windows Server Backup (WBAdmin)**, QNAP NetBak, TimeDicer.

---

### **XV. Kapazitätsplanung**

**Warum?**
*   **Unterschätzung:** Speicher läuft voll, Backup bricht ab, das **RPO wird verletzt** (Beispiel E-Commerce im Weihnachtsgeschäft: Transaktionslog wächst, Backup bricht am Sonntag ab, Serverausfall am Montag, ein ganzes Wochenende Bestellungen verloren).
*   **Überschätzung:** unnötiges CAPEX/OPEX, brachliegende Ressourcen.
*   **Planungshorizont:** Lebenszyklus der Hardware, meist **3–5 Jahre** (Abschreibung, End of Support).
*   **Konzeptgrundlage:** Datenklassifizierung + Retentionzeiten + Backup-Strategie.

**Einflussfaktoren:**
*   **Primärdatenvolumen** (Ausgangspunkt, Bestandsaufnahme aller Quellsysteme). **Datenbanken:** Transaktionslogs separat betrachten. **Fileserver:** unstrukturierte Daten wachsen unvorhersehbar, grosszügig planen.
*   **Retentionzeit** und Anzahl **Backup-Generationen** (GFS multipliziert den Bedarf).
*   **Änderungsrate** (Change Rate): Bildarchiv ~0.5 %/Tag, ERP ≥ 10 %/Tag.
*   **Datenwachstum** (typisch 10–30 % p. a., Kursbeispiele bis 40 %), **Applikations-Roadmap** (neue Projekte).
*   **Overhead:** Metadaten-Katalog/Indizes der Backup-Software, Dateisystem-Overhead (nie 100 % nutzbar), Prüfsummen, DB-Logs, **RAID-Overhead**, **Hot Spares**.
*   **Brutto- vs. Netto-Kapazität:** Brutto = physisch installiert (minus RAID-Reserve). Netto = tatsächlich nutzbar nach allen Overheads. **Reserve ca. 20 %** gegen Instabilität bei voller Belegung.

**Effizienzfaktoren:**
*   **Deduplizierung:** typisch **2:1 bis 20:1**.
*   **Komprimierung** (z. B. LZ4, Zstandard): typisch **1.2:1 bis 2:1**. Bereits komprimierte (JPEG, MP4) oder verschlüsselte Daten lassen sich kaum weiter reduzieren.
*   **Reduktionsfaktor = Deduplizierungsrate × Komprimierungsrate** (z. B. 3 × 1.5 = 4.5:1).
*   **Annahmen realistisch und belegbar** wählen (Proof of Concept, Erfahrungswerte).

> **Fehlerabschätzung (Mobirama-Musterlösung):** Realistisch ist oft eine Kompression von ca. **1:2 (50 %)**.
> *   **Zu optimistische Reduktion** (z. B. 1:3) führt dazu, dass **zu wenig Speicher** eingeplant wird und der Speicher ausgehen kann. **Das ist die kritischere Fehleinschätzung.**
> *   Zu pessimistische Reduktion (z. B. 1:1.1) führt zu zu viel Speicher, also brachliegenden Ressourcen.

**Speicherschichten (jede separat berechnen):**
*   **Primär-Backup** (Performance-Tier, schneller Restore).
*   **Sekundär-Backup** (Capacity-Tier, anderes Medium/Standort).
*   **Langzeitarchiv** (Archive-Tier).
*   **Offsite-Kapazität.**

**Berechnungsschema:**
1.  **Vollbackup-Grösse** = Primärvolumen.
2.  **Inkrement-Grösse** = Primärvolumen × tägliche Change-Rate.
3.  **Rohkapazität** = (Anzahl Vollbackups × Vollbackup-Grösse) + (Anzahl Inkremente × Inkrement-Grösse).
4.  **Puffer** +20–30 %.
5.  **Effektiver Bedarf** = Roh × Puffer ÷ Reduktionsfaktor (die Reihenfolge spielt mathematisch keine Rolle).
6.  **Wachstum:** Zielkapazität = Startkapazität × (1 + g)ⁿ.

**Rechenbeispiel (Artikel 7.1, Helvetia Data Solutions AG):**
*   **Annahmen:** 10 TB Primärdaten, 5 % Change-Rate, wöchentliches Full + 6 Inkremente, 4 Wochen Retention.
*   **Fulls:** 4 × 10 TB = **40 TB**.
*   **Inkremente:** 6 × 4 × 0.5 TB = **12 TB**.
*   **Roh:** **52 TB**.
*   **Reduktion:** Dedup 3:1 × Kompression 1.5:1 = 4.5:1 → 52 / 4.5 ≈ **11.6 TB**.
*   **Puffer 25 %:** ≈ **14.4 TB**. Physisch rund **15 TB** beschaffen (plus RAID-Overhead).
*   **Wachstum 20 % über 5 Jahre:** 10 × 1.2⁵ ≈ **24.9 TB**.

**Rechenbeispiel (Artikel 3.2, KMU mit 3-2-1-1-0):**
*   **Annahmen:** 2 TB Daten, 10 % Change-Rate, 30 Tage Retention.
*   **Kopie 1 lokal:** 2 TB Full + 29 × 0.2 TB = **7.8 TB** (NAS realistisch 10–12 TB).
*   **Kopie 2:** nochmals **7.8 TB**.
*   **Kopie 3 Cloud** mit Dedup/Kompression 3:1: 7.8 / 3 = **2.6 TB**.
*   **Kopie 4 Tape:** 4 wöchentliche Fulls × 2 TB = **8 TB** (Rotation von 4 Bändern). Auf Tape keine Inkremente, weil der Restore sonst mehrere Bänder braucht.

**Langzeitarchiv:**
*   Das Volumen **akkumuliert** über 10+ Jahre (OR 958f) und ist oft der grösste Kostentreiber.
*   Geringe Performance-Anforderungen, deshalb **Tape** oder **Cold-Storage-Cloud** (S3 Glacier Deep Archive, Azure Archive). Achtung bei Egress-/Abrufgebühren.
*   Der Fokus liegt auf **TCO**, nicht auf IOPS.

**Revision:** Die Kapazitätsplanung **mindestens jährlich** mit den Ist-Werten vergleichen. Skalierungsstrategie (**Scale-out** für dynamische Umgebungen). Ein **Erweiterungsplan** wird dokumentiert (Beispiel: neue CAD-Software mit schlecht deduplizierbaren 3D-Modellen, 50 % statt 20 % Wachstum → frühzeitig Budget beantragen).

---

### **XVI. Performance-Planung**

**Backup-Fenster:** der Zeitraum, in dem gesichert werden kann, **ohne das Tagesgeschäft zu beeinträchtigen** (klassisch nachts/Wochenende). In 24/7-Betrieben schrumpft es. **Reicht die Performance nicht, ragt das Backup in die Arbeitszeit** (langsame Systeme, verfehltes RPO).

**Restore-Performance ist oft wichtiger als Backup-Performance**, denn sie bestimmt das **RTO**.

**Einflussfaktoren und Flaschenhälse** (die Kette ist nur so stark wie ihr schwächstes Glied):
*   **Netzwerkbandbreite:** 1 GbE ≈ 110–125 MB/s. Grosse Datenmengen brauchen **10 GbE** oder Fibre Channel. Der **Protokoll-Overhead** reduziert die Nutzdatenrate.
*   **Speicher-IOPS** am Ziel (viele kleine Dateien belasten die IOPS, nicht den Durchsatz). HDD vs. SSD, Anzahl Disks, **SSD-Caching** für Spitzen und Metadaten.
*   **CPU/RAM** für Deduplizierung, Kompression und Verschlüsselung (Backup-Server und bei Source-Dedup auch die Quelle). RAM für Metadaten-Kataloge und parallele Jobs.
*   **Quellsystem:** Lesegeschwindigkeit, Systemlast, **Snapshot-Impact**, Change-Rate. **I/O-Limits** pro Quelle schützen die Produktion.
*   **Zielmedien:** Schreib-Performance, Latenz, **Tape-Streaming** (konstanter Datenstrom nötig).
*   **Produktiver Betrieb** (Mobirama-Musterlösung): Arbeiten Anwender oder Maschinen während des Backups, konkurrieren sie um Netz und Disk. Beispiel Fileserver mit SATA-HDDs: hohe Latenzen für die User.

**Formeln:**
*   **Benötigter Backup-Durchsatz = Datenmenge ÷ Backup-Fenster**
    *   Beispiel: 10 TB / 8 h = **1.25 TB/h** → mit **20 % Reserve** auf **1.5 TB/h** dimensionieren.
*   **Benötigter Restore-Durchsatz = wiederherzustellende Datenmenge ÷ RTO**
    *   Beispiel: 5 TB / 4 h = **1.25 TB/h**.
*   **Umrechnung:** 1 TB/h ≈ 278 MB/s. 1 Gbit/s ≈ 125 MB/s ≈ 450 GB/h ≈ 10.8 TB/Tag (theoretisch).
*   **Beispiel Artikel 7.3:** 20 TB in 8 h = 2.5 TB/h ≈ **700 MB/s**, also ist 1 GbE (~110 MB/s) viel zu klein und es braucht 10 GbE oder FC.
*   **Beispiel Musterlösung 7.2 (AlpinMedia GmbH):** 4 TB in 5 h (1 h Puffer) = 4'000'000 MB / 18'000 s = **222 MB/s**, also mehr als 1 GbE.
    *   **Massnahmen:** 10-GbE-Upgrade, **Parallelisierung** (4 Streams à ~60 MB/s), **Storage-Snapshots**.
*   **Beispiel Artikel 2 Block 7:** 2 TB über 1 Gbit/s dauern mindestens ca. 4.5 h.

**RPO- und RTO-Einflüsse:**
*   **RPO:** Das **Intervall muss ≤ RPO** sein. Kurze Intervalle erfordern Inkremente, **Log-Backups**, **CDP** oder **Replikation**. Ein kürzeres Intervall bei gleicher Datenmenge verlangt mehr Durchsatz über den Tag.
*   **RTO:** Hardware-Bereitstellung (Ersatzteile!), **Automatisierung** (Skripte, Workflows), Standort der Medien, **Priorisierung** (Tier 1 bekommt dedizierte Restore-Ressourcen), **Instant Recovery** für RTO < 1 h.
*   **Replikation:** **synchron** (hohe Anforderungen an die Latenz), **asynchron** (RPO > 0). Die Replikationsrate muss grösser als die Change-Rate sein, dazu **Failover** und **Konsistenzprüfung**.
*   **Hardware-Snapshots:** Sekunden, wenig Impact, sehr schneller Restore **auf dem Produktiv-Storage**, belegen aber dessen Platz. **Nie alleiniges Backup.** Applikationskonsistenz sicherstellen, **Snapshot-Kaskaden** über den Tag ermöglichen ein tiefes RPO.
*   **Kosten-Nutzen:** Mit sinkendem RPO/RTO steigen die Kosten. **Service-Level pro Applikationsklasse** statt einem Level für alle.
*   **Musterlösung 7.3 (Chronos Precision AG):** RPO 15 Min., RTO 2 h, ein Ausfall kostet CHF 50'000 pro Stunde.
    *   **RPO:** **SQL-Log-Backups alle 15 Min.** plus **CDP**.
    *   **RTO:** **Instant VM Recovery** (< 15 Min.) plus **Replikation/Failover** an einen zweiten Standort.

**Parallele Datenströme:**
*   **Multi-Streaming** und **Lastverteilung** auf mehrere Media-Server nutzen die Bandbreite besser aus.
*   Die Zahl der **Concurrent Tasks** muss zur Zielhardware passen.
*   **Multiplexing** (mehrere Streams auf ein Band) verschlechtert den Restore.
*   **Startzeiten staffeln:** z. B. HR um 20:00, Finanzen um 22:30, Produktion um 02:00, statt aller 500 Jobs um 20:00 (**I/O-Storm**).
*   **Mehr Parallelität ohne passende Hardware verschlechtert** die Leistung.

**Architektur:**
*   **Dediziertes Backup-Netzwerk/VLAN.** Backup-Verkehr («Elephant Flows») stört sonst den Benutzerverkehr («Mice Flows»).
*   **WAN-Optimierung** (Source-Dedup, Kompression) für Offsite und Cloud.
*   **Flash** für schnelle Restores und Instant Recovery, **HDD** als Rückgrat, **Tiered Storage**.

**Monitoring und Optimierung:**
*   Job-Laufzeiten überwachen (schleichende Verschlechterung erkennen) und eine **Bottleneck-Analyse** machen.
*   **Tuning** (Puffergrössen, Timeouts, Netzwerkparameter) bringt oft ohne Investition mehr Leistung.
*   **Trendanalyse** und **Reporting** an die GL.
*   **Lessons Learned:** Wenn Millionen kleiner Dateien beim Restore zu langsam sind, auf **Image-/Block-Level** umstellen.

---

### **XVII. Konzeptionelle Bausteine und Lebenszyklus des Konzepts**

**Die Bausteine der Umsetzung (Block 7) bauen aufeinander auf:**
1.  **Datenklassifizierung** (Grundstein).
2.  **Backup-Strategie** (Sicherungsart, Periodizität, Retention) und **Technologieauswahl** nach RPO/RTO.
3.  **Speicherkapazität:** dokumentierter **Kapazitätsplan** für alle Schichten und den Planungshorizont, begründete **Effizienzannahmen**, **Erweiterungsplan**, periodische Überprüfung.
4.  **Performance:** **Performance-Plan**, **Durchsatzberechnung** (Backup **und** Restore), **Netzwerkplan**, **Engpassanalyse**, **Testnachweis** (z. B. 5-TB-Test-DB in 1 h 45 Min. wiederhergestellt → RTO < 2 h belegt).
5.  **Umsetzbarkeit:** **Machbarkeitsbeurteilung** (technisch: Strom/Kühlung/Rack; organisatorisch: Personal; finanziell: **Budgetrahmen/TCO**), **Ressourcen**, **Alternativen**, **begründete Empfehlung**.
*   **Beispiel:** Kantonale Verwaltung mit 150'000 CHF Budget, die gewünschte synchrone Replikation kostet 500'000 CHF plus 50'000 CHF/Jahr. Die Alternative ist eine Hybrid-Cloud (lokales Backup + verschlüsselte Schweizer Cloud). Nachteil: höheres RTO bei Standortverlust, das Restrisiko wird von der GL formell akzeptiert.

**Weitere Bausteine (Folien Block 7):**
*   **Speicherarchitekturen:** SAN (Performance), NAS (einfaches, günstiges Ziel), DAS (tiefste Latenz für dedizierte Backup-Server), Objekt-Speicher (Skalierung), Hybrid.
*   **Backup-Server-Dimensionierung:** CPU (Dedup/Verschlüsselung), RAM (Kataloge, parallele Jobs), Netzwerk-/FC-Karten, stabiles Betriebssystem, physisch oder virtuell.
*   **Tape-Libraries:** LTO, Robotik, Medienmanagement/Katalog, externe Lagerung, Lesbarkeit regelmässig prüfen und auf neue Medien migrieren.
*   **Appliances vs. Software-Defined Storage**, zentrale **Management-Konsole**, **Plugins** für DBs, **Lizenzmodelle** (nach Datenmenge statt Agentenzahl).
*   **Cloud-Integration:** Cloud-Gateways, **Latenz** (lokaler Cache nötig), **Verschlüsselung vor der Übertragung**, **Egress-Gebühren**, Unveränderbarkeit.
*   **Redundanz und Sicherheit der Backup-Infrastruktur selbst:** redundante Server und Pfade, **MFA**, **Air-Gap**, **USV**, **Härtung** (unnötige Dienste deaktivieren).
*   **Integration ins Ökosystem:** Schnittstellen zu Hypervisor und Storage, **API/ITSM**, Monitoring-Anbindung, BI-Reporting, **Schulungskonzept**.

**Lebenszyklus der Kapazitäts- und Performance-Planung (Artikel 7.4):**
*   **Dokumentation im Konzept:** eigenständiger Abschnitt, **Nachvollziehbarkeit für Dritte** (Auditor, FINMA), **Versionierung/Historisierung** (warum war ein Server damals «out of scope»?), **formelle Genehmigung** durch GL/Governance (Verantwortung und Budget), **Kommunikation** an alle Teams.
*   **Übertragung auf neue Systeme:**
    *   Backup ist **Pflicht beim Go-Live** («Hard-Gate» im Change Request).
    *   Klassifizierung (z. B. Platin/Gold/Silber/Bronze) → RPO/RTO → Anforderungen.
    *   Konzept anpassen und erneut genehmigen.
    *   **Auswirkungsanalyse** auf bestehende Reserven (z. B. reicht die Firewall-Performance?).
    *   **Eskalationsprozess** bei Ressourcenmangel.
*   **Monitoring und Steuerung:** Kapazität mit Schwellenwerten (Warnung ~80–85 %, kritisch ~90 %), Performance-Monitoring (z. B. Einbruch 500 → 50 MB/s wegen defekter Glasfaser), **Trendanalyse** («in 114 Tagen voll» bei 90 Tagen Beschaffungszeit, also jetzt bestellen), **proaktive Alarmierung** (Pikett, Pager), **Management-Reporting** (Erfolgsquote, freie Kapazität, Fenster-Verstösse).
*   **Kontinuierliche Optimierung** (Continual Service Improvement): Potenziale erkennen (CBT statt Voll-Backups), **Dedup-Rate** optimieren, **Job-Staffelung**, **Technologie-Updates** evaluieren (z. B. Immutability), **Lessons Learned** einarbeiten.

---

### **XVIII. Beratung, Machbarkeit und Konzeptbeurteilung**

**Grundlagen der Konzeptbeurteilung** (strukturiert, anhand definierter Kriterien):
*   **Beurteilungsgrundlage:** Datenklassifizierung, RPO/RTO-Vorgaben, rechtliche Anforderungen (DSG, FINMA).
*   **Vollständigkeit:** Sind alle Datenkategorien und Systeme erfasst (Cloud/SaaS wie M365, Schatten-IT, Laptops der GL, **OT-Netz/Maschinensteuerungen**)?
*   **Konsistenz:** keine inneren Widersprüche. Klassiker **Henne-Ei-Problem**: Das Cloud-Backup-Login braucht das lokale AD, das selbst noch wiederhergestellt werden muss.
*   **Aktualität:** Passt das Konzept zur heutigen Landschaft (Cloud-Migration, Kubernetes)?

**Beurteilungskriterien im Detail:**

| Kriterium | Prüffrage | Typischer Befund |
| :--- | :--- | :--- |
| **RPO-Abdeckung** | Halten die Intervalle das RPO ein? | RPO 15 Min., aber nur nächtliches Backup → Log-Backups/Replikation |
| **RTO-Erfüllung** | Kann die Infrastruktur rechtzeitig wiederherstellen? | 10 TB über 100 Mbit/s dauern mehrere Tage (rechnerisch ≈ 9 Tage) → «nicht realistisch» |
| **3-2-1-Umsetzung** | korrekt und vollständig? | Prod + NAS + NAS im selben Rack = 1 Medientyp, kein Offsite → kritisch |
| **Sicherheitsstandards** | Verschlüsselung, Least Privilege, MFA, Immutable? | Backup-Repository als offener SMB-Share → hochkritisch |
| **Wirtschaftlichkeit** | TCO, Oversizing? | alles auf All-Flash → Tiering |

**Empfehlungen strukturieren** (nach Dringlichkeit, Aufwand, Nutzen):
*   **Sofortmassnahmen (Prio 1):** kritisch, wenig Aufwand (z. B. Passwort «Admin123» ändern + MFA aktivieren).
*   **Mittelfristig (Prio 2):** moderater Aufwand, klarer Nutzen (z. B. manuelle Bandauslagerung durch automatisches Cloud-Connect-Backup ersetzen).
*   **Langfristig (Prio 3):** strategisch, grosses Budget (z. B. drei Backup-Silos durch eine Plattform ersetzen).
*   **Jede Empfehlung wird in der Sprache des Business begründet** (Risiko, Kosten, Compliance), nicht «wir brauchen Immutable Storage».

**Kommunikation:**
*   **Beurteilungsbericht** für zwei Zielgruppen:
    *   **Management Summary** für die GL: Risiken, Kosten, Massnahmen.
    *   **Technischer Anhang** für die Admins: z. B. «10G-NICs nachrüsten».
*   **Visualisierung:** Risikomatrix, **Ampel**, Vergleichstabellen.
*   **Massnahmenplan:** ID, Beschreibung, Priorität, **Verantwortlicher**, **Termin**.
*   **Follow-up (PDCA):** die Wirksamkeit live nachweisen lassen (z. B. Login ohne zweiten Faktor ist unmöglich).

**Machbarkeitsbeurteilung (Feasibility Study) – vier Dimensionen:**
*   **Technisch:** Integration, Kompatibilität (z. B. kein Agent für AS/400).
*   **Organisatorisch:** Personal und Know-how (z. B. Ceph ohne Linux-Wissen).
*   **Finanziell:** CAPEX/OPEX vs. Budget (z. B. Dark-Fiber-Kosten sprengen das Budget).
*   **Zeitlich:** Deadline machbar? (z. B. Migration von 500 TB dauert 8 Monate → physischer Transport, z. B. AWS Snowball).

**Kriterien der Auditierung / Machbarkeit (Folien Block 8):**
*   **Vergleichsanalyse** Umsetzung vs. Anforderungen.
*   **Klassifizierungs-Check.**
*   **RPO-Validierung** unter allen Lastbedingungen.
*   **RTO-Abgleich.**
*   **Ressourcen-Prüfung.**
*   **Abgleich mit Business-Zielen:** Geschäftsrelevanz, **Risikotoleranz** (Restrisiken von der GL akzeptiert), Skalierungspotenzial, Kosten-Nutzen, Prozessintegration.
*   **Risikobewertung des Konzepts:** **Single Point of Failure**, Ransomware-Resilienz, Standortrisiken, **Komplexitätsrisiko** (zu komplizierte Restores führen unter Stress zu Fehlern), **Herstellerabhängigkeit** (offene Standards).
*   **Personelle Ressourcen:** Fachkompetenz, **24/7-Verfügbarkeit**, **Stellvertretung** (kein Wissen nur bei einer Person), Schulung, klare Rollen.
*   **Technische Integration:** native Unterstützung, Netzlast, Storage-Anbindung, **Automatisierungsgrad**, Monitoring-Anbindung.

**Typische Hindernisse:**
*   **Budgetengpass:** Priorisierung Tier 1 → 3, schrittweise Umsetzung.
*   **Kompetenzlücken:** Schulung oder MSP.
*   **Infrastrukturrestriktionen:** z. B. VDSL statt Glasfaser.
*   **Datenschutzhürden:** US-Hyperscaler vs. CLOUD Act → Schweizer Cloud.
*   **Zeitdruck** durch Parallelprojekte.

**Alternativen:**
*   **Bewertungsmatrix/Nutzwertanalyse** (z. B. Tape: günstig, aber langsam vs. Cloud: teurer, aber schneller).
*   **Kompromisse** mit akzeptiertem Restrisiko.
*   **Phasenplan:** Phase 1 kritische DBs lokal, Phase 2 Offsite, Phase 3 Rest.
*   **Verworfene Alternativen dokumentieren** («Warum keine Tapes mehr?» → «2026 evaluiert, wegen SLA verworfen»).
*   Der Berater **entscheidet nicht**, er liefert die Entscheidungsgrundlage. **Die GL trägt das Restrisiko und gibt das Budget frei.** Danach folgt die Umsetzungsbegleitung.

**Lösungsberatung (Folien Block 8):**
*   **Marktübersicht/Trends:** KI-Anomalieerkennung, Anbieterbewertung, Standardisierung, unabhängige Benchmarks.
*   **Cloud vs. On-Premises:**

| | Cloud | On-Premises |
| :--- | :--- | :--- |
| Kosten | variabel (OPEX) | hohe Anfangsinvestition (CAPEX) |
| Datenhoheit | beim Provider (Vertrag) | volle physische Kontrolle |
| Restore | abhängig von der Internetbandbreite | schnell im LAN |
| Sicherheit | spezialisierte Features, aber Verschlüsselung nötig | eigene Verantwortung |
| **Empfehlung** | **Hybrid** kombiniert beides und verbessert den Desasterschutz | |

*   **Managed Backup Services:** Entlastung der IT, **SLA**, Fixpreis pro TB, Know-how des Providers, Flexibilität.
*   **Lizenzmodelle:** kapazitätsbasiert (nach gesicherter Datenmenge), instanzbasiert (pro VM/Server), **Subscription** statt Kauf, Feature-Bundles, Wartungsverträge (Pflicht für Security-Updates).
*   **Strategische Empfehlungen:** Scale-up vs. Scale-out, **Tool-Standardisierung**, **Datenminimierung** durch Archivierung, Sicherheits-Härtung, **Roadmapping**.
*   **TCO-Betrachtung:** alle direkten und indirekten Kosten (Strom, Kühlung, Fläche, **Administrationsaufwand**, Wertverlust) den **Ausfallkosten** gegenüberstellen.

**Gesamtbeurteilung und Weiterentwicklung (Artikel 8.4):**
*   **Holistische Gesamtbeurteilung** (umsetzbar mit den vorhandenen Ressourcen?), **Stärken** hervorheben (Best Practices), **Schwächen** priorisieren (ohne Schuldzuweisung).
*   **Restrisiko** (Residual Risk) dokumentieren, die GL akzeptiert es formell.
*   **Reifegrad** z. B. nach **CMMI**:
    *   **Level 1 (Initial):** manuelle, unregelmässige Sicherungen.
    *   **Level 3 (Defined):** standardisiert und dokumentiert.
    *   **Level 5 (Optimizing):** automatisierte Verifikation, KI-Anomalieerkennung.
*   **Weiterentwicklung:**
    *   Konzept als **«Living Document»** im **PDCA-Zyklus** (Deming).
    *   Technologiebeobachtung (Cloud-Cold-Storage, DNA-Speicher).
    *   Regulatorische Entwicklung («Recht auf Vergessenwerden» auch in Backups umsetzen).
    *   Bedrohungslage (Double Extortion → Air-Gap/Immutable).
    *   **Jährliches Strategie-Review auf C-Level.**

---

### **XIX. Testverfahren und Validierung**

**Grundsatz:** **«Nicht getestete Backups sind keine Backups.»** Ein Backup gilt erst als funktionsfähig, wenn ein **Restore physisch nachgewiesen** wurde. Die Meldung «Job completed successfully» (grüner Haken) beweist nichts: Silent Failure, fehlende Keys, korrupte Medien, inkompatible Hardware.

**Arten von Restore-Tests:**

| Testart | Was wird geprüft? | Beispiel |
| :--- | :--- | :--- |
| **Datei-Restore** (File-Level) | Granularität, Lesbarkeit | überschriebene Excel-Datei in wenigen Minuten zurückholen |
| **Application-Item-Recovery** | einzelne Objekte aus der Applikation | einzelne E-Mail aus der Exchange-DB |
| **System-/Full-VM-Restore** | Zusammenspiel OS + Backup-Software, Boot | VM nach missglücktem Update im isolierten Netz hochfahren |
| **Datenbank-Restore** | Konsistenz, **Point-in-Time** aus Transaktionslogs | DB auf 14:15 zurückrollen (eine Minute vor dem fehlerhaften Skript) |
| **Bare-Metal-Restore** | Wiederherstellung auf **neuer, «nackter» Hardware** (Hardware Independent Restore, andere Treiber) | Mainboard-Schaden, Image auf Server eines anderen Herstellers |
| **Disaster-Recovery-Test** | ganzes RZ gilt als zerstört: Abhängigkeiten (Netz → DC → DB → Apps), Krisenstab, Kommunikation, externer Standort, Prioritätenliste | Samstagmorgen Zürich virtuell abschalten, in Bern hochfahren |

**Testplanung:**
*   **Jahres-Testplan/Testkalender**, Frequenz nach Kritikalität:

| Frequenz | Test |
| :--- | :--- |
| täglich | automatisierte Verifikation (Sandbox, Logs, Integrität) |
| monatlich | Datei-/granulare Restores (Stichproben) |
| **mind. quartalsweise** | System- und DB-Restores der Tier-1-Systeme, **Tabletop-Übung** des Krisenstabs |
| mind. jährlich | Tier-2/3-Systeme, **vollständiger DR-Test / Teilumschaltung** (oft am Wochenende) |

*   **Isolierte Testumgebung** (Sandbox, Fenced Network, VLAN): sonst entstehen IP-Konflikte, Split-Brain oder ungewollte Mails an Kunden. Die Testumgebung sollte beim Patch-Level der Produktion entsprechen. **Datenmaskierung** sensibler Daten (Datenschutz).
*   **Ressourcenplanung:** Zeitfenster für die Mitarbeitenden, genügend Speicher und Rechenleistung.
*   **Erfolgskriterien vorab** definieren, messbar, nicht «Server läuft wieder». Beispiel: DB wiederhergestellt, Test-Login erfolgreich, **Prüfsummen** der Finanzberichte stimmen byte-genau.
*   **Verantwortlichkeiten** festlegen (Rolle «Backup-Administrator»). Die **Abnahme** erfolgt durch den Fachverantwortlichen.
*   **Realistische Szenarien**, Budget freigeben, gescheiterte Tests als Erkenntnis werten (**Fehlerkultur**: «Ein gescheiterter Test ist kein Versagen, sondern eine wertvolle Erkenntnis»).

**Durchführung und Auswertung:**
*   **Drehbuch** abarbeiten, jeden Schritt und Workaround protokollieren.
*   **Zeitmessung:** reales **RTO** vs. Vorgabe (z. B. 5 h statt 4 h → Optimierung nötig), erreichtes **RPO** (letztes Backup 24 h alt bei Vorgabe 4 h → Konzept überarbeiten).
*   **Datenkonsistenz** prüfen (bootet, aber DB «corrupt» = gescheitert), **Abweichungsanalyse** mit Ursache.
*   **Standardisierter Testbericht** (Vorgehen, Chronologie, Ergebnisse, Abweichungen, Empfehlungen). Der Testzyklus gilt erst mit **Freigabe/Unterschrift** als abgeschlossen.
*   **Fehlerbehebung und Iteration:** Korrekturmassnahmen, **Nachtest** zwingend, Anleitungen und Schulung verbessern, Konfiguration tunen (Timeouts, Puffer), Feedback ins Konzept.
*   **Re-Zertifizierung** der RTO-Werte nach grösseren Infrastrukturänderungen.

**Automatisierte Validierung:** **Auto-Verify** (VM in Sandbox booten), skriptbasierte Funktionstests, tägliche **Readiness-Checks**, Dashboards. So lassen sich mehr Systeme testen als manuell.

**Beispiel Musterlösung 4.3 (SwissMediCare AG, nach Ransomware 3-2-1-1-0):**
*   **Architektur:** Kopie A auf einer Disk-Appliance, Kopie B auf **LTO-9**, wöchentlich per Kurier in einen Tresor einer anderen Gemeinde. Dazu **S3 Object Lock 30 Tage** sowie **SureBackup** für die «0».
*   **Testkalender:**
    *   Täglich: automatische Verifikation.
    *   Monatlich: granularer Restore (max. 15 Min.).
    *   Quartalsweise: Tabletop-Übung.
    *   Jährlich: DR-Teilumschaltung am Wochenende.

---

### **XX. Kontrollen, Monitoring, Audits**

**Automatisierte Kontrollen:**
*   **Backup-Monitoring** (täglich, Dashboard, roter Indikator statt 500 Logfiles lesen).
*   **Jobprotokollierung** (historische Auswertung).
*   **Integritätsprüfung** mit Prüfsummen/Hashes (SHA-256): erkennt z. B. eine schleichende Verschlüsselung, bevor gesunde Backups überschrieben werden.
*   **Kapazitätsüberwachung** mit automatischem Ticket im ITSM.
*   **Alarmierung** über **mehrere Kanäle** (Lessons Learned aus einem Fall: Warnmails landeten im Spamfilter, deshalb zusätzlich Teams/Slack/Pager).
*   **Monitoring-Dashboards** mit Echtzeitstatus, Erfolgsquote, Durchsatz-Trends und Kapazitätswarnungen.

**Manuelle Kontrollen:**
*   **Protokollkontrolle** (Plausibilität: Backup plötzlich 5 Min. statt 2 h → Daten fehlen).
*   **Stichproben-Restore-Tests** (deckten z. B. einen nicht mitgesicherten Verschlüsselungs-Key auf).
*   **Medieninspektion** (Tapes).
*   **Konfigurationsreview.**
*   **Berechtigungsreview** (Account eines Ex-Mitarbeiters mit Löschrechten entdeckt).

**Archivspezifische Kontrollen:**
*   **Archivintegrität** periodisch auf Lesbarkeit prüfen.
*   **Migrationsplanung** vor Technologie-Obsoleszenz (CDs/DVDs von 2005 → WORM-Cloud, «CD-Rot»).
*   **Indexprüfung.**
*   **Aufbewahrungskontrolle.**
*   **Löschkontrolle** mit kryptografischem Zertifikat (Datensparsamkeit).

**Eskalations- und Meldeprozesse:**
*   **Schweregrade mit Reaktionszeiten.** Beispiel: Wiki-Backup fehlgeschlagen = Sev 3, 24 h. Kernbanken-DB = Sev 1, SMS an den Pikettdienst, Start innert 15 Min.
*   **Meldepflicht an die GL** bei kritischen Ausfällen, lückenloses **Tracking**, **Lessons Learned / Post-Mortem**.

**Audits:**
*   **Intern** (interne Revision, unabhängig von der IT) vs. **extern** (Prüfgesellschaft, ISO-27001-Zertifizierer): objektive Aussensicht, z. B. mangelhafte physische Zugangskontrolle zum Bandarchiv.
*   **Auditfrequenz** nach Kritikalität (Kernsysteme jährlich). **Umfang** wird vorab definiert.
*   **Prüfbereiche:** Konzeptaktualität (Beispiel: M365 eingeführt, aber nicht im Konzept), Konfigurationskonformität, Protokollvollständigkeit, **Testnachweise** (z. B. nur 3 von 5 Restore-Tests nachweisbar), Berechtigungen.
*   **Klassifizierung der Findings:**
    *   **Kritisch:** z. B. kein Offline/Immutable-Backup → Sofortmassnahme am selben Tag.
    *   **Wesentlich:** z. B. Tests nur jährlich statt halbjährlich.
    *   **Geringfügig:** z. B. veraltete Abteilungsnamen.
*   **Massnahmenplan (CAPA** = Corrective and Preventive Actions: wer, was, bis wann) und **Umsetzungskontrolle / Follow-up-Audit** (Object Lock aktiv, Modifikation wird abgelehnt → «geschlossen»).

**Reporting an die Geschäftsleitung:** Management-Summary, **SLA-Reporting** (RPO/RTO monatlich), **Compliance-Nachweis** (Prüfer, FINMA), **Risikoberichterstattung**, Langzeitanalysen fürs Budget.

**Change Management für das Backup-System:** Änderungen dokumentieren und von einer zweiten Person kontrollieren lassen, **Impact-Analyse** in einer Testumgebung, **Rollback-Plan**, Wartungsfenster kommunizieren, Freigabe durch das **Change Advisory Board (CAB)**.

**Rollen und Berechtigungen:**
*   **Least Privilege.**
*   **Funktionstrennung:** Backup-Admin ≠ Admin der Produktivsysteme.
*   **MFA** für die Management-Konsole.
*   **Passworthygiene.**
*   **Regelmässige Rezertifizierung**, Rechte bei Austritt sofort entziehen.

**Kontinuierliche Verbesserung (KVP):** Erfahrungen aus dem Betrieb einarbeiten, Lessons Learned nach jedem Restore/Test, Technologie-Updates, Feedback der Anwendungsbetreuer, **Reifegradmodell**.

> **Merksatz Block 8:** «Datensicherung ist kein einmaliges Projekt, sondern ein kontinuierlicher Managementprozess zur Sicherung der Unternehmensexistenz.»

---

### **XXI. Rechtliche und regulatorische Rahmenbedingungen (Schweiz)**

| Regelwerk | Relevanz für Backup und Archivierung |
| :--- | :--- |
| **DSG / nDSG / revDSG** (Bundesgesetz über den Datenschutz, totalrevidiert, **in Kraft seit 1. September 2023**) | angemessene **technische und organisatorische Massnahmen (TOM)** zur Datensicherheit, risikobasierter Schutz von Personendaten, Löschen/Anonymisieren, wenn der Zweck entfällt, Meldepflicht bei Datensicherheitsverletzungen, Rechenschaftspflicht |
| **OR Art. 958f** | Geschäftsbücher, Buchungsbelege, Geschäfts- und Revisionsbericht **10 Jahre** aufbewahren (ab Ende des Geschäftsjahres). Elektronisch zulässig, wenn die Übereinstimmung mit den Geschäftsvorfällen gewährleistet ist und die Daten jederzeit lesbar gemacht werden können |
| **GeBüV** (Geschäftsbücherverordnung) | Anforderungen an ordnungsgemässe Führung und Aufbewahrung (Integrität, Informationsträger, Lesbarkeit) |
| **OR Art. 716a** | unübertragbare Oberleitung des VR, Haftungsrisiko bei vernachlässigter Datenverfügbarkeit |
| **FINMA-Rundschreiben** | Anforderungen an operationelle Risiken, BCM und Cyber-Resilienz im Finanzsektor (Nachweis von DR-Tests, RTO) |
| **Branchenregulierungen** | Gesundheit (kantonale Gesetze, KVG, Patientenakten), Anwälte (**BGFA Art. 13**, Anwaltsgeheimnis), international **PCI-DSS** (Kreditkarten), **HIPAA** (US-Gesundheit) |
| **DSGVO / GDPR** (EU) | gilt bei EU-Bezug. Meldung an die Aufsichtsbehörde **innert 72 Stunden** |
| **US CLOUD Act** | US-Behörden können unter Umständen auf Daten von US-Anbietern im Ausland zugreifen. Deshalb Data Residency CH, Swiss Cloud, BYOK |
| **Normen und Frameworks** | **ISO/IEC 27001** (ISMS), ISO 27005 (IT-Risikomanagement), **ISO 22301** (BCM), ISO 31000, ISO 27031 (ICT Readiness for BC), **BSI IT-Grundschutz CON.3** (Datensicherungskonzept), DER.4 (Notfallmanagement), **NIST** CSF, SP 800-34 (Contingency Planning), SP 800-61 (Incident Handling), **ITIL 4**, **COBIT 2019** |

> 🔎 **Ergänzung (Recherche) – präzisere Rechtslage:**
> *   **Meldepflicht nach Art. 24 DSG:** Meldung an den **EDÖB «so rasch als möglich»**, wenn eine Datensicherheitsverletzung **voraussichtlich zu einem hohen Risiko** für die Persönlichkeit oder die Grundrechte der Betroffenen führt. Inhalt: Art der Verletzung, Folgen, ergriffene/geplante Massnahmen. Betroffene werden informiert, wenn es zu ihrem Schutz nötig ist oder der EDÖB es verlangt. Auftragsbearbeiter melden dem Verantwortlichen.
>     *   ⚠️ **Korrektur zu Artikel 2.2:** Dort steht, eine Meldung müsse «in der Regel innerhalb von 72 Stunden» erfolgen. **Die 72-h-Frist stammt aus der EU-DSGVO.** Das Schweizer DSG kennt keine feste Stundenfrist, sondern «so rasch als möglich».
> *   **Bussen (Art. 60–63 DSG):** bis **CHF 250'000**. Sie treffen **private (natürliche) Personen**, nicht primär das Unternehmen, und setzen **Vorsatz** voraus.
>     *   **Art. 60–62** (Informations-/Auskunfts-, Sorgfalts-, Schweigepflicht) werden nur **auf Antrag** verfolgt. **Art. 63** (vorsätzliches Missachten einer Verfügung des EDÖB) enthält keinen Antragsvorbehalt.
>     *   **Art. 61 lit. c:** Wer vorsätzlich die **Mindestanforderungen an die Datensicherheit** (Art. 8 Abs. 3 DSG, konkretisiert in der DSV) nicht einhält, macht sich strafbar, auch ohne dass ein Data Breach passiert ist (abstraktes Gefährdungsdelikt).
>     *   **Art. 64:** Bei Bussen **bis CHF 50'000** kann statt der verantwortlichen Person der **Geschäftsbetrieb** gebüsst werden, wenn deren Ermittlung unverhältnismässig aufwendig wäre.
> *   **Aus NCSC wurde BACS:** Das Nationale Zentrum für Cybersicherheit (NCSC) ist seit dem **1. Januar 2024** das **Bundesamt für Cybersicherheit (BACS)** im VBS. Die Kursmaterialien verwenden teils noch «NCSC».
> *   **Meldepflicht für Cyberangriffe auf kritische Infrastrukturen:** seit **1. April 2025** in Kraft (Informationssicherheitsgesetz ISG). Betreiber kritischer Infrastrukturen (Energie, Gesundheit, Finanzen, Telekom, Transport u. a.) müssen Cyberangriffe **innert 24 Stunden** nach Entdeckung dem **BACS** melden und die Meldung innert 14 Tagen vervollständigen. Seit 1. Oktober 2025 sind **Bussen bis CHF 100'000** möglich.
> *   **FINMA-RS 2023/1 «Operationelle Risiken und Resilienz – Banken»:** seit **1. Januar 2024** in Kraft, **ersetzt das RS 2008/21**. Es regelt u. a. kritische Daten, IKT- und Cyberrisiken sowie die operationelle Resilienz (Übergangsfristen bis 2 Jahre). Artikel 8.3 nennt noch das alte RS 2008/21.
> *   **Aufbewahrungsfristen – Feinheiten:**
>     *   **Immobilien:** Geschäftsunterlagen zu **unbeweglichen Gegenständen (Immobilien)** müssen nach **MWSTG (Art. 70 Abs. 3)** **20 Jahre** aufbewahrt werden.
>     *   **Geschäftskorrespondenz:** Sie ist seit der Revision des Rechnungslegungsrechts **nur noch aufbewahrungspflichtig, soweit sie Buchungsbelegfunktion hat**. Die pauschale Aussage «Geschäfts-E-Mails 10 Jahre» (Artikel 2.3) ist daher eine vereinfachte, vorsichtige Praxisregel.
> *   **IKT-Minimalstandard:** Vom **BWL** entwickelt (basiert auf dem NIST CSF), seit 2024 beim BACS angesiedelt. Er richtet sich primär an kritische Infrastrukturen (für die Strombranche seit 1. Juli 2024 verbindlich), ist aber für jede Organisation als Leitfaden nutzbar und verlangt u. a. Backup-Strategien (3-2-1), Segmentierung und Zugriffsbeschränkungen.

**Spannungsfeld Aufbewahrung vs. Löschung:** Finanzdaten müssen 10 Jahre **unveränderbar** (WORM) archiviert werden. Gleichzeitig verlangt das DSG, dass Personendaten gelöscht werden, sobald der Zweck entfällt («Recht auf Vergessenwerden»). Das Archivkonzept muss beides abbilden: Finanzdaten ins WORM-Archiv, ein Marketingprofil auf Löschbegehren hin auch aus den operativen Backups entfernen bzw. beim Restore herausfiltern.

---

### **XXII. Fallbeispiele**

#### **1. Fallbeispiel Mobiliar: «Wegen Hacker: Schreinerei steht still» (Mobirama 1/2018)**

**Sachverhalt (Artikel):**
*   Am **1. Dezember 2017 (Freitag)** konnten die Mitarbeitenden der **Schreinerei Baltensperger AG, Bülach** (Raumgestaltung, KMU in zweiter Generation) keine Dateien und keine E-Mails mehr öffnen.
*   Ein **Kryptotrojaner** hatte die Daten auf dem Server verschlüsselt und teilweise gelöscht. Vermutlich hatte ein Mitarbeiter in der Hektik auf einen präparierten E-Mail-Anhang geklickt. Der externe IT-Partner traf den Angreifer noch auf dem Server an.
*   **Auch die drei computergesteuerten CNC-Maschinen** standen still, der Betrieb ebenfalls.
*   **Forderung: 3 Bitcoins.** Der Inhaber **zahlte nicht**, liess das System herunterfahren und alarmierte die **Polizei** (die Anzeige gegen Unbekannt verlief im Sand).
*   **Rettung:** Der interne IT-Verantwortliche erstellte **jede Woche eine Sicherungskassette (Tape)** mit allen Daten. «Nur» die Arbeit **einer Woche** musste nachgeholt werden (z. B. Pläne neu zeichnen). Übers Wochenende wurde die IT neu aufgesetzt, **nach drei Tagen** war alles wieder in Ordnung.
*   **Schaden:** laut Artikel im **unteren fünfstelligen Bereich** (neue Hardware, IT-Spezialist, alle Computer neu programmiert). ⚠️ Die Folie Block 8 spricht von einem «**mittleren** fünfstelligen Betrag», die Musterlösung schätzt CHF 10'000–30'000 pro Ausfalltag.
*   **Folgen:** Firewall, Backups & Co. waren laut Fachleuten für die Betriebsgrösse «verhältnismässig», trotzdem blieb ein Restrisiko. Danach **Cyberversicherung** abgeschlossen und die Sicherheitsstrategie überprüft. Bis dahin galten **Brand und Naturgefahren** als grösste Risiken. Einziger «ultimativer» Schutz wäre der Verzicht auf E-Mail und Internet, was keine Option ist.

**Musterlösung (Kernaussagen nach Analysetagen):**

| Tag | Frage | Musterlösung |
| :--- | :--- | :--- |
| **1** | Relevante Risiken? | Risikomatrix, z. B. **Brand** (EW hoch: Maschinen, Sägemehl, Holz / SA sehr hoch), Wasserschaden (gering / im IT-Raum hoch), Sabotage/Insider (gering / mittel–sehr hoch), **Ransomware** (mittel–hoch / sehr hoch), Stromausfall (mittel / IT gering, Maschinen potenziell hoch), Cyberattacke und Datenverlust allgemein (mittel / gering–sehr hoch) |
| 1 | Eingetretenes Risiko? | **Ransomware** |
| 1 | Im Konzept berücksichtigt? | Wahrscheinlich nicht. Das Konzept war auf **Brand** ausgelegt (Tape-Auslagerung, 1–2 Wochen Datenverlust in Kauf genommen). Mit Ransomware im Fokus wären RPO/RTO tiefer gewesen |
| 1 | Auswirkung / Schaden? | Auftragsdaten fehlten, Maschinen standen, Betrieb still. Unterer fünfstelliger Bereich, 1 Tag ≈ CHF 10–30k |
| **2** | Vorhandene Daten? | Kundendaten, Baupläne, OS/Applikationsdaten (CNC-Steuerung), (Annahme) Buchhaltung |
| 2 | RPO/RTO, Sicherungsart, Verfügbarkeit, Lagerung, 3-2-1? | RPO nicht explizit, bei wöchentlicher Auslagerung **mind. 7 Tage**. Vermutlich wöchentliches Full + inkrementell. Verfügbarkeit Geschäftszeit (08–17). Je eine Sicherung vor Ort und ausgelagert. 3-2-1: «3» und «2» unklar, **«1» ja** (Band ausgelagert) |
| 2 | Datenverlust und SPOF? | **Eine komplette Arbeitswoche.** SPOF: Auslagerung **nur wöchentlich**. Der Vorfall am Freitag bedeutete fast den grösstmöglichen Verlust (4 von 5 Tagen) |
| 2 | Backup- oder DR-Fall? | **DR**: die komplette Umgebung und alle Services waren weg |
| 2 | Überschneidung? | Backup und DR nutzen **dieselben Medien und Datenbestände** |
| **3** | Medium, Vor-/Nachteile? | **Tape.** Vorteil: auslagerbar. Nachteile: **manueller, fehleranfälliger Prozess**, Medium kann beim Transport verloren gehen, keine Auslagerung rund um die Uhr in kurzen Intervallen |
| 3 | 3-2-1-(0) erfüllt? | Wahrscheinlich nur **ein** Tape, Ende Woche ausgelagert → «1» ja, «3» und «2» vermutlich nicht (sonst wären Restores wie Bare-Metal schneller gewesen) |
| 3 | Auswirkung auf RPO/RTO? | **RPO unter 24 h kaum möglich** (tägliche Auslagerung nötig). **RTO kaum unter 1 Tag** (Bänder holen, lesen, einspielen). Liegen die Bänder auf einer Bank, gibt es Fr–So keinen Zugriff, also RTO > 2 Tage |
| 3 | Bessere Alternative? | Für ein kleines KMU eine **Cloud-Lösung** für die Auslagerung: **RPO < 5 Min.** möglich, **RTO ~1–8 h** (abhängig von Datenmenge und Downlink, Annahme 1–2 TB) |
| 3 | Automatisierbarkeit? | Backups und Backup-Tests (wenn primär nicht auf Tape) sind automatisierbar, die **Tape-Auslagerung nicht** (physischer Transport). Lösung: primäre Auslagerung auf ein **«online» Medium**. Mit Ransomware-Schutz praktisch nur über eine **Cloud-Lösung** (mit Immutability) |
| **4** | Technologie? | Wahrscheinlich **agentenbasiert** (CNC-Steuerung, Server, Fokus auf Daten). Mit API-basiertem VM-Backup (OS + Apps + Daten) wäre der Restore viel schneller gewesen |
| 4 | Vor-/Nachteile Agent? | Vorteile: komplettes Abbild des physischen Geräts, zentral/dezentral steuerbar, **Bare-Metal-Recovery** möglich. Herausforderungen: Agents aktuell halten (Wartung wirkt aufs Gerät), **Gerät muss eingeschaltet sein**, lokale Admins können Agent manipulieren (Ausschlüsse), Bare Metal muss **explizit getestet** werden (Treiber, aktuelles Recovery-Image) |
| 4 | Backupart? | Wahrscheinlich **Full + inkrementell**, sinnvoll (Full fürs Tape). Tägliches Full hätte täglich ein Full-Tape ergeben |
| 4 | «Incremental Forever»? | **Nicht direkt auf Tape umsetzbar**. Geht nur, wenn das Backup **zuerst auf Disk** und dann auf Tape geschrieben wird |
| **5** | Datenvolumen? | Annahme ~**2 TB**, Change-Rate ~5 % ≈ 100 GB/Tag. Kompression realistisch **1:2**. **Zu optimistische Reduktion ist kritischer** (Speicher geht aus). Full 2 TB, Inkrement 0.1 TB. Gesamt = Anzahl Fulls × 2 TB + Anzahl Deltas × 0.1 TB (ohne Zusatzkopie/Auslagerung) |
| 5 | Performance? | Annahme 8-h-Fenster: 2 TB / 8 h ≈ **70 MB/s**. Restore analog (Full-Restore / RTO). Beteiligt: CNC-Rechner (Disk, CPU, RAM), Netzwerk, Backup-Server (CPU, RAM, Netz, Disks), Tape-Drive und -Kassette. Indirekt: **produktiver Betrieb** (CNC arbeitet, User am Fileserver, ausgelastete SATA-Disks → Latenz) |
| **6** | Umsetzbarkeit/Komplexität? | **Umsetzbar ja, Komplexität gering** (sehr rudimentär). Umsetzbarkeit ≠ Sinnhaftigkeit |
| 6 | Umgesetzter DR-Plan? | Annahme: 1. Tapes holen, 2. alles neu installieren (1 und 2 parallel), 3. Daten pro Applikation einspielen, 4. testen/verifizieren. Erfolgreich, aber eine Woche Datenverlust und **Abhängigkeit vom IT-Dienstleister**. Mit Bare-Metal wäre es schneller gegangen |
| 6 | SPOF / vergessen? | Komplett vergessen: **Totalverlust am letzten Wochentag** (5 Tage Verlust). Nicht umgesetzt: Ransomware als Risiko, **RTO-Einschätzung** (IT war Fr–So dran; was wäre an einem Mittwoch passiert? → 3 zusätzliche Tage Stillstand), Bare-Metal-Recovery. Proaktiv: **klare Anforderungen mit SLA**, dann z. B. auch mittwochs auslagern, Bare Metal umsetzen |
| 6 | Skalierbarkeit? | Grenze = Kapazität **einer** Kassette bei einem Single Drive (2017 wohl LTO-6 2.5 TB / LTO-7 6 TB). Bei Wachstum ×10/×20/×100 mehrere Tapes, mit einem Laufwerk nicht realistisch, also **Tape-Library** nötig |
| 6 | Architektur-Alternativen? | Jede Lösung ok, **wenn sie enthält:** klare **SLA** (RTO, RPO, Aufbewahrung), Vor-/Nachteile, sinnvolle Skalierung, **3-2-1 inkl. Ransomware-Schutz**, **RPO ≤ 24 h mit automatisierter Auslagerung**, **Backup to Disk first** (Tape nur als zweite Kopie) |

> ⚠️ **Rechenfehler in der Musterlösung (Tag 3):** «Bei 1 Gbit/s wären über 300 GB pro Minute möglich» stimmt nicht. 1 Gbit/s ≈ 125 MB/s ≈ **7.5 GB pro Minute ≈ 450 GB pro Stunde**. Die Schlussfolgerung «1–2 TB → RTO realistisch 1–8 h» passt aber zu ~450 GB/h (≈ 2.2–4.5 h reine Übertragung).

#### **2. DE&C (Digital Education & Consulting GmbH) – Fallbeispiel 1: Handwerksbetrieb**

**Ausgangslage:** KMU-Kunde in Zürich (Wärmepumpen und Steuereinheiten), preissensitiv, 4-jähriger HP/HPE ProLiant noch nicht amortisiert. Der Server steht im Büro in einem Schrank über der Werkhalle.
*   **VSS:** Baupläne auf Stundenbasis **3 Tage** lang wiederherstellbar (Self-Service).
*   **Wöchentlich:** Baupläne + Gruppenshare auf eine **externe USB-HD**, dann ins **Schliessfach in der Werkhalle**. Die Disk wird **jede Woche überschrieben** (zu wenig Platz).
*   Die Werkhalle kann **1–2 Wochen** unabhängig mit ausgedruckten Plänen arbeiten. Ein **Tablet-PoC** (Echtzeit-Zugriff) ist geplant.
*   **Kundenanforderungen:** wöchentliches Backup genügt, Risiken eines Handwerksbetriebs abdecken, Wiederanlauf bei Totalausfall in **3–4 Tagen**.

| Daten | Menge | Änderungsrate | Ort |
| :--- | :--- | :--- | :--- |
| Baupläne/CAD | 350 GB | < 1 %/Tag | Server |
| Mails | 25 GB | < 1 %/Tag | externer Hoster |
| Buchhaltung | 50 GB | 100–250 MB/Tag | Server |
| Persönlicher User-Ordner «Privat» | 1–4 GB | unbekannt | PC lokal |
| Gruppenshare | 250 GB | < 1 %/Tag | Server |

**Lösung (Kernaussagen):**
1.  **Risikomatrix:**
    *   **Feuer = hohe Gefahr**, führt zum Totalschaden, weil das Backup im selben Gebäude liegt.
    *   **Sabotage:** Die Produktion ist im Haus, das Schliessfach kann gewaltsam geöffnet werden.
    *   **Externe HD ungeeignet** (Erschütterung, Schmutz im Betrieb).
    *   **Archivierung nicht revisionssicher.**
    *   **Aufbewahrung zu kurz** (3 Tage VSS, 1 Woche HD).
2.  **Analyse:**
    *   **Archiv:** fehlt, nicht revisionssicher (**WORM fehlt**). Nach **OR 10 Jahre revisionssicher**, idealerweise mit dem neuen Backup-Konzept verbinden (günstiger als nachträglich). Mit dem Kunden klären, was archiviert werden muss: Der **Kunde entscheidet und verantwortet**. Praxistipp: bei kleinen Datenmengen im Zweifel alles Relevante archivieren (sofern DSG-konform).
    *   **Anforderungen genügen nicht:** Mit Tablets steigen die Anforderungen, also sind die Kunden-RPO/RTO zu lasch.
    *   **Empfehlung:** **RPO max. 24 h** (VSS stündlich für 3 Tage + tägliches Backup auf externes Medium), **RTO 2–4 h** (z. B. SLA 06:00–20:00). Offene Frage: Wie lange wird an Plänen gearbeitet, muss die Änderungshistorie nachvollziehbar sein (Retention)?
3.  **3-2-1-(0):**
    *   **«3»:** theoretisch ja (Original, VSS, HD), praktisch nein (Aufbewahrung zu kurz).
    *   **«2»:** diskutabel. Die externe Disk ist ein anderer Typ als die Server-Disks, aber beides sind HDDs, deshalb ein Medium mit besserer Fehlerrate ergänzen.
    *   **«1»:** **nein** (gleiches Gebäude).
    *   **«0»:** **nein** (keine Prüfung).
4.  **Operativer Betrieb:** Backup und Auslagerung **automatisieren** (dann täglich möglich), **keine manuellen Tasks**. Aktuell hängt alles an einer Person.
5.  **Datenmenge:**
    *   **~700 GB** unkomprimiert (alles ausser «Privat», inkl. Mails), Delta max. **10 GB/Tag**, **7 Tage max. ~800 GB**.
    *   **Archiv:** Buchhaltung 50 GB + Gruppenshare 250 GB + Mails 25 GB + CAD, Delta 100–250 MB/Tag, als eigenständiges Full je nach Lösung.
    *   **Private User-Daten** kommen nicht ins Backup (Datenschutz, vom Arbeitgeber geduldet).
    *   **Mails:** Ist der Hoster zuständig? Beim Hoster/O365 ist ein Backup gegen Aufpreis möglich, aber man ist dann abhängig. Deshalb **ins eigene Konzept aufnehmen** (günstige Lösungen am Markt).
6.  **Lösungsvarianten (studentisch, alle 3-2-1-0-konform):**
    *   **V1:** 2 zusätzliche lokale Disks (RAID 1) als Backup + **Cloud (SaaS)** als Auslagerung + Archiv auf **WORM-Tape** + wöchentliche automatische Prüfung.
    *   **V2:** NAS + **Tape-as-a-Service** + **Archive-as-a-Service**.
    *   **V3:** NAS + Cloud-Auslagerung + Cloud-Archiv.
    *   **Vorteil Cloud:** **Medienbruch und Auslagerung in einem**, automatisierbar (**RPO < 15 Min.** möglich).

#### **3. DE&C – Fallbeispiel 2: NGO (Enterprise, 24/7) – ✍️ eigene Lösungsskizze**

*Zu diesem Fall gibt es keine offizielle Lösung. Die Fragen sind dieselben wie bei Fallbeispiel 1.*

**Ausgangslage:**
*   International bekannte NGO. Helfer weltweit (skalierbare externe Dienste), Gönnerportal, stark digitalisiert.
*   **Eigener Serverraum** am Hauptsitz (CH) mit **VMware-Cluster, > 800 VMs**. Ein kleiner **Notfall-Cluster** in einem gemieteten Rack **einige km entfernt**, über redundante dedizierte Glasfaser verbunden.
*   **Backup 1–4× täglich am Hauptsitz**, dann nach DC2 ausgelagert und archiviert. Im DR-Fall **Restore aus dem Backup** in DC2. Restore-Tests **quartalsweise manuell**.

| Daten | Menge | Änderungsrate |
| :--- | :--- | :--- |
| Geschäftskritisch (reguliert) | 30 TB | 5 %/Tag |
| Kritische System-/App-Daten | 5 TB | 1 %/Tag |
| Unkritisch (temp., Logs, Test, automatisch neu aufsetzbar) | 20 TB | 5 %/Tag |
| Mails (Office 365) | 2–4 TB | < 1 %/Tag |
| User-Ordner lokal / Gruppenshare | 1–4 GB / 250 GB | unbekannt / < 1 %/Tag |

**Anforderungen:**
*   2 Wochen lang alle Daten auf **2 unterschiedlichen, unabhängigen Systemen an 2 Standorten**. Produktion in DC1, **Backup und Archiv in DC2** (Georedundanz).
*   **Wöchentliche** Backups ≥ 3 Monate, **monatliche** ≥ 18 Monate, **jährliche** ≥ 5 Jahre.
*   **Geschäftskritische** Daten quartalsweise archivieren, **5–10 Jahre** aufbewahren.
*   Alles **basierend auf Full-Backups** (Unabhängigkeit).
*   **3 SLAs:** 1×, 2×, 4× täglich.

**Mögliche Findings und Empfehlungen:**
*   **DR per Restore auf einen kleinen Cluster widerspricht der 24/7-Anforderung:** 800 VMs aus dem Backup brauchen Stunden bis Tage und die Kapazität von DC2 ist begrenzt.
    *   **Empfehlung:** Tier-0/1-Systeme (AD, DNS, Helferportal, Gönner-DB) **asynchron nach DC2 replizieren** (Warm/Hot Standby) oder **Instant Recovery** einsetzen.
    *   Unkritische Systeme **automatisiert neu aufsetzen** statt restoren.
    *   Eine verbindliche **Wiederanlauf-Reihenfolge** festlegen.
*   **RPO:** Die SLA-Klassen sind klar (24 h / 12 h / 6 h). Das RPO des Offsite-Backups hängt aber zusätzlich von der **Dauer der Auslagerung** nach DC2 ab. Bis zur Auslagerung liegt das Backup nur in DC1, also Auslagerung beschleunigen oder direkt nach DC2 sichern.
*   **Ransomware:** Kein Air-Gap und keine Immutability erwähnt, und die dedizierte Glasfaser macht DC2 aus DC1 erreichbar.
    *   **Empfehlung:** **Immutable Repository** (Hardened Linux / S3 Object Lock) oder **Tape** als Offline-Kopie, Backup-Infrastruktur **nicht im produktiven AD**, MFA, Segmentierung.
*   **Georedundanz:** «Einige Kilometer» kann dieselbe Gefahrenregion sein (Hochwasser, grossflächiger Stromausfall).
    *   **Empfehlung:** eine zusätzliche weiter entfernte Kopie (Schweizer Cloud oder Tape-Vaulting).
*   **Restore-Tests nur quartalsweise manuell** verletzen die «0» der 3-2-1-1-0-Regel. **Automatisierte Verifikation** (SureBackup), dazu jährliche DR-Übung inkl. **Failback**.
*   **Office 365 (2–4 TB):** Shared Responsibility, deshalb eigenes **M365-Backup** (Retention-Lücken 14–30 bzw. 93 Tage). Lokale User-Ordner per Richtlinie auf OneDrive/Share umleiten oder bewusst ausschliessen.
*   **Zielkonflikt «Full-basiert/unabhängig» vs. Deduplizierung:** Auf einer Dedup-Appliance teilen sich alle Fulls dieselben Blöcke, ein defekter Block trifft viele Generationen. Deshalb die Langzeit-Fulls (Monat/Jahr/Archiv) auf ein **separates Medium** (z. B. WORM-Tape oder Cloud-Archiv) schreiben.
*   **Grobe Volumenabschätzung** (Annahme: unkritische 20 TB nur in der 2-Wochen-Kette, nicht in der Langzeit-Retention):
    *   Tägliches Delta ≈ 30 × 5 % + 5 × 1 % + 20 × 5 % ≈ **2.55 TB**.
    *   Langzeit-Fulls (35 TB + ~4 TB Mail): wöchentlich 13 × 39 ≈ 507 TB, monatlich 18 × 39 ≈ 702 TB, jährlich 5 × 39 ≈ 195 TB.
    *   **Archiv** geschäftskritisch 4 × 30 TB pro Jahr × 10 Jahre = **1.2 PB** logisch.
    *   Das ergibt **mehrere PB logisch**, was nur mit Deduplizierung/Kompression und **Tape/Cloud-Archiv** wirtschaftlich ist. Genaue Werte hängen von den Annahmen ab und sind im Konzept zu dokumentieren.

---

### **XXIII. Prüfungsschema für Fallbeispiele**

> Die Fallbeispiele (Mobirama in 6 Analysetagen, DE&C) und die Musterlösungen zeigen den erwarteten Stil: **jede Antwort begründen** (Ja/Nein + kurze Begründung) und **wo Angaben fehlen, eine plausible Annahme treffen und begründen**. Die folgende Checkliste deckt die typischen Fragen ab.

1.  **Risiken:** Risikomatrix mit 3–4 Risiken (EW × SA, begründet). Typisch: Brand, Wasser, Ransomware, Sabotage/Insider, Stromausfall, Hardwaredefekt, Bedienfehler. Pro Risiko eine **Massnahme** (Vermeiden/Mindern/Transferieren/Akzeptieren).
2.  **Was ist eingetreten, war es im Konzept berücksichtigt?** (Ist das Konzept z. B. nur auf Brand ausgelegt?)
3.  **Auswirkungen und Schaden** schätzen (Ausfalltage × Tagesschaden, Finanzen/Betrieb/Recht/Reputation).
4.  **Datenbestände** auflisten, welche werden gesichert (und welche bewusst nicht, z. B. Privatordner)?
5.  **RPO/RTO ableiten** (aus Intervall bzw. Auslagerungsrhythmus) und mit dem Business-Bedarf vergleichen. Sind die Kundenanforderungen ausreichend? **Welche Fragen muss der Kunde beantworten?**
6.  **Sicherungsart** (Full/Inkrementell/Differenziell/Incremental Forever/CDP) und **Periodizität/Retention** (GFS).
7.  **3-2-1-1-0-Check:** jede Ziffer einzeln mit Ja/Nein/unklar und Begründung.
8.  **Archivierung:** revisionssicher (WORM)? OR 10 Jahre? Wer entscheidet, was archiviert wird? (Der Kunde.)
9.  **Medien:** eingesetzte Medien, Vor-/Nachteile, **Grenzen für RPO/RTO** (Tape: RPO ≥ Auslagerungsintervall, RTO ≥ Holzeit + Lesezeit, Wochenende/Bank!), bessere Alternativen (Cloud/Immutable).
10. **Automatisierung:** Was ist automatisierbar, was nicht (physischer Transport), und wie wird es automatisierbar (Online-Medium)?
11. **Technologie:** Agent vs. Agentless/API vs. dateibasiert, Konsistenz (VSS), **Bare-Metal**.
12. **Datenvolumen:** Full-Grösse, Delta (Change-Rate), Retention-Summe, **Reduktion realistisch (~1:2)**, zu optimistisch ist gefährlicher.
13. **Performance:** **MB/s = Datenmenge ÷ Fenster**, Restore = Menge ÷ RTO, beteiligte Komponenten (Quelle, Netz, Server, Ziel), Einfluss des produktiven Betriebs.
14. **Backup- oder DR-Fall?** Überschneidung (dieselben Medien/Daten), **DR-Plan beschreiben** (Reihenfolge, parallelisierbare Schritte), Schwierigkeiten.
15. **Single Point of Failure** (Person, Medium, Standort, Intervall, fehlende Tests) und wie man ihn proaktiv erkennt (**SLA**, Tests).
16. **Skalierbarkeit:** Was passiert bei ×10/×20/×100 Daten? (z. B. Tape-Library statt Single Drive)
17. **Operativer Betrieb:** Verantwortlichkeiten, Stellvertretung, Monitoring, Restore-Tests, Dokumentation.
18. **Zwei Architektur-Alternativen skizzieren** mit Vor-/Nachteilen, minimalem RPO/RTO, Umsetzbarkeit und Komplexität, klarer SLA, 3-2-1 inkl. Ransomware-Schutz und **Backup to Disk first**.
19. **Empfehlung** priorisiert (sofort / mittelfristig / langfristig), begründet in Business-Sprache, **Restrisiko** benennen.

---

### **XXIV. Gruppenaufgaben und Musterlösungen im Überblick**

> Jede Gruppenaufgabe hat eine **Musterlösung A (strukturiert-analytisch)** und meist eine **Musterlösung B (praxisnah-narrativ)**. Die Tabelle fasst die Kernaussagen zusammen.
>
> ⚠️ **Hinweise zu den Dateien:**
> *   In **Block 6** passen die Musterlösungen zu **Aufgabe 6.3** (behandelt «SwissRetail AG», Image/Snapshots) und **6.4** (behandelt «CloudPioneer AG», Cloud/M365) **nicht** zur jeweiligen Aufgabenstellung (BaselCloud AG bzw. ZürichFinance AG).
> *   Die **Übungsdateien in Block 8** sind **identische Kopien** der Block-7-Aufgaben. Die eigentlichen Block-8-Aufgaben stehen nur auf den Folien (ohne Musterlösung, siehe Kapitel XXV).

| Nr. | Szenario | Auftrag | Kernaussage der Musterlösung |
| :--- | :--- | :--- | :--- |
| **1.1** | SwissData AG (IT-Dienstleister, Störungen im nächtlichen Backup) | Risikoübersicht 4 Kategorien + je 2 Massnahmen | Ursachen im **Zusammenspiel** (alte NAS, Update-Inkompatibilität, Admin-Wechsel ohne Einarbeitung, niemand prüft Logs). **Top 3:** Restore-Tests / tägliches Monitoring mit Verantwortlichem, Hardware-Monitoring, Dokumentation, Offline-Kopie |
| **1.2** | AlpinTech GmbH | 5×5-Risikomatrix, Top 5 + Steuerung | Ransomware und fehlende Restore-Tests je **RW 20 (rot)**, siehe Tabelle Kapitel III |
| **1.3** | HelvetiaMed AG (14 Tage Datenverlust) | Vorfallanalyse, Auswirkungen, 5+ Massnahmen | RAID-5-Controller + volles Backup-Volume + kein Monitoring + keine Tests. ~CHF 240k. M1 Alarmierung, M2 Restore-Tests, M7 Notfallplan sofort |
| **1.4** | FinSecure AG (Ransomware, 50 BTC / 72 h) | Angriffsablauf, 5 Anforderungen, Notfallplan | Kill Chain über Wochen, Backup-Server im selben Segment. Offline, Immutable, 3-2-1, Monitoring, Restore-Tests. **Nicht zahlen** |
| **2.1** | CyberShield AG (AV versagte bei 2 Kunden) | Erkennungsmethoden bewerten, 3+ Ebenen | Signatur versagt bei Zero-Day/polymorph/fileless. **4 Ebenen:** Gateway, EDR, SIEM/NDR, Threat Intel |
| **2.2** | LogiTrans AG (kein Notfallplan, 30 BTC / 48 h) | 60-Min.-Sofortmassnahmen, Kommunikation, Wiederherstellung | Trennen → Krisenteam → Inventar → Forensik → Polizei/NCSC → nicht zahlen. Reihenfolge **ERP → Lager → Kunden-DB → Mail → Clients**, 30 Tage Monitoring |
| **2.3** | SwissLegal AG (Kanzlei, alles gleich behandelt) | Schema ≥ 4 Stufen, Zuordnung, Rollen | K1–K4 (öffentlich → streng vertraulich/Anwaltsgeheimnis **BGFA Art. 13**). Schutzmassnahmen pro Stufe, Rollen Managing Partner / Data Owner / IT / alle / Revision |
| **2.4** | PharmaSwiss GmbH (Audit) | 5 Applikationen klassifizieren, RTO/RPO, Schutzbedarf | ERP RPO 1 h/RTO 4 h, LIMS 4/8 h (GMP), DMS 24/24 h, Mail 1/4 h, HR 24/48 h |
| **3.1** | SwissLogistics AG | Matrix Volumen/Periodizität/Sicherheit (1–3) | Logistik-DB 8 → Tier 1 (CDP), HR 5 → Tier 2 (verschlüsselt, RBAC), Webseite 4 → Tier 3 |
| **3.2** | AlpinBank SA («Zero Downtime für alles») | RPO/RTO E-Banking vs. Intranet, Pitch | E-Banking RPO < 1 Min./RTO < 15 Min., Intranet 24 h/12 h, «Zwei-Klassen-Gesellschaft» |
| **3.3** | MedizinTech Zürich GmbH (nur lokales NAS) | 3-2-1-Architektur + Ransomware-Schutz | Prod (Flash) + lokaler Backup-Server (ZFS/ReFS, HDD-RAID) + **S3 in Schweizer Cloud** (Protokollwechsel!) mit **Object Lock 30 Tage** |
| **4.1** | AlpinTech GmbH (Backup reichte nicht) | Abgrenzung Backup/DR, RPO/RTO pro Abteilung | Produktion RTO 1 h/RPO 15 Min. → **DR** (sync + Failover). Buchhaltung 24 h/4 h → Snapshots + Restore. Marketing 48 h/24 h → File-Backup. Entscheidungsmatrix für den Krisenstab |
| **4.2** | HelveticFinance AG (Audit-Mangel) | Datenhaltungskonzept für Kreditdossiers, Flyer, Mails | Kreditdossiers: HA + vertraulich + 10 J. WORM. Mails: Standard, intern, 5 J., DLP. Flyer: Basis, öffentlich, kurz. **Chargeback** gegen Subjektivität, Office-Plugin |
| **4.3** | SwissMediCare AG (Backup mitverschlüsselt) | 3-2-1-1-0 + Jahres-Testkalender | Disk-Appliance + LTO-9 im Tresor + S3 Object Lock + SureBackup. Test täglich / monatlich / quartalsweise Tabletop / jährlich DR |
| **5.1** | AlpinTech GmbH (Ingenieurbüro) | Block vs. File für CAD und ERP | ERP → **SAN/Block** (All-Flash, Multipathing), CAD → **NAS/File** (Tiering). Unified Storage. Backup: Snapshots bzw. **NDMP** |
| **5.2** | SwissData AG (CIO will Tape abschaffen) | Argumentarium für Tape | Air-Gap, 3-2-1-Medienbruch + 10 J. Compliance (30 J. Haltbarkeit), TCO/0 Watt → **D2D2T** |
| **5.3** | MediCare Bern AG (300 VMs, 18 h Backup) | Dedup-Appliance, Inline/Post, Raten | **Source-Dedup + Inline**, VMs 10:1–20:1, Dumps bis 20:1, Fenster 2–4 h, Risiko Rehydrierung |
| **5.4** | HelvetiaCloud Services GmbH (BaaS) | Object Storage + Object Lock | S3, Erasure Coding, **Compliance Mode 30 Tage**. Verkaufsargumente: Pay-as-you-grow + Ransomware-Garantie |
| **6.1** | AlpinLogistik AG (heterogen) | Technologieüberblick + 3 Kriterien | Kriterien: Performance/Skalierbarkeit, Wiederherstellbarkeit (RPO/RTO), Integration. **Agentless für VMware, Agent für Legacy, API für Cloud** |
| **6.2** | HelvetiaMed GmbH (Oracle + Exchange) | Agenten-Konzept Pro/Contra | Agent **alternativlos** für transaktionskonsistente DB (RMAN) und Item-Level-Restore (Exchange/VSS) |
| **6.3** | BaselCloud AG (MSP, VMware + Hyper-V) | agentless Architektur | *(Musterlösung behandelt SwissRetail AG)* Image vs. Snapshot, Snapshots max. ~24 h, Image-Backup mit Offsite-Replikat, RPO/RTO-Matrix |
| **6.4** | ZürichFinance AG (FINMA, NAS) | Entscheidungsmatrix NDMP/Dedup/Object/Tape | *(Musterlösung behandelt CloudPioneer AG)* **Shared Responsibility**, revDSG, SaaS-Backup + Azure Backup + Immutable Object Storage CH |
| **7.1** | SwissLogistics AG (120 TB, +20 %) | Kapazität Ende Jahr 3 | **≈ 840 TB netto, ~1.1 PB brutto** (siehe Kapitel XXV) |
| **7.2** | AlpinMedia GmbH (4 TB/Tag, Fenster 6 h) | Durchsatz + 3 Massnahmen | **222 MB/s**, 10 GbE, Parallelisierung, Snapshots |
| **7.3** | Chronos Precision AG (RPO 15 Min., RTO 2 h) | Technologien | Log-Backups 15 Min. + CDP, Instant VM Recovery + Replikation |
| **7.4** | LuzernBank AG (400 VMs + Mainframes, Air-Gap Pflicht) | Architektur Kurz-/Langzeit/DR | Tier 1 SSD-Backup-Server (SAN/DAS), Tier 2 **S3 Immutable**, Tier 3 **LTO-9 Library**, extern gelagert |

---

### **XXV. Übungsfragen mit Lösungen**

#### **1. Excel-Übung «RPO/RTO» (Block 7, Einzelarbeit 3) – ✍️ eigene Lösung**

*Aufgabe: RPO und RTO in Stunden bestimmen. Vorgabe: 1 Tag = 24 h. RPO = max. tolerierbarer Datenverlust (Sicherungsintervall), RTO = max. tolerierbare Ausfall-/Wiederherstellungszeit.*
*Zusätzliche Annahmen: 1 Woche = 168 h, 1 Monat ≈ 30 Tage = 720 h, «nahtlos» = 0 h, Minuten in Stunden umgerechnet.*

| # | Fall | RPO [h] | RTO [h] | Begründung |
| :---: | :--- | :---: | :---: | :--- |
| 1 | Active Directory: max. halber Tag Ausfall, Änderungen auf 4 h nachweisbar | **4** | **12** | halber Tag = 12 h, «auf 4 h nachweisbar» = Datenverlust max. 4 h |
| 2 | Mailservice: max. 3 h eingeschränkt, stündlich gesichert | **1** | **3** | Sicherungsintervall 1 h |
| 3 | Testserver SRV-XYZ2 innert 2 h als Kopie von XYZ1, Daten des Vortages | **24** | **2** | Stand Vortag = max. 24 h alt |
| 4 | Fileserver: letzte 10 Tage innert 2 h auf stündlicher Basis wiederherstellbar | **1** | **2** | «stündliche Basis» = RPO. Die 10 Tage sind die **Retention** (240 h), nicht das RPO |
| 5 | Zeiterfassung: max. 12 h Datenverlust, Ausfall 2–3 Tage tolerierbar | **12** | **48–72** | konservativ 48 h |
| 6 | Alle Testserver wöchentlich gesichert, innert eines Tages wieder verfügbar | **168** | **24** | 1 Woche = 168 h |
| 7 | Finanzbuchhaltung alle 15 Min. gesichert, max. 1 h Ausfall | **0.25** | **1** | 15 Min. = 0.25 h |
| 8 | Webshop max. 30 Min. offline, Datenverlust max. 5 Min. | **≈ 0.083** | **0.5** | 5 Min. = 1/12 h |
| 9 | CRM alle 6 h gesichert, spätestens nach halbem Arbeitstag (4 h) wieder in Betrieb | **6** | **4** | «halber Arbeitstag» ist in der Aufgabe als 4 h definiert |
| 10 | Produktions-DB synchron repliziert, Failover max. 5 Min. | **0** | **≈ 0.083** | synchron = kein Datenverlust |
| 11 | DMS täglich 22:00 gesichert, Ausfall bis nächsten Werktag (24 h) | **24** | **24** | tägliches Intervall |
| 12 | Druckserver 1× pro Monat, Wiederherstellung innert 3 Tagen | **≈ 720** | **72** | 30 Tage × 24 h |
| 13 | ERP: max. 2 h Datenverlust, innert 8 h produktiv | **2** | **8** | direkt vorgegeben |
| 14 | DNS redundant, nahtloser Betrieb, Konfiguration täglich gesichert | **24** | **0** | Redundanz = RTO 0. Die Konfiguration wird täglich gesichert |
| 15 | VoIP max. 1 h Ausfall, Sprachnachrichten alle 2 h gesichert | **2** | **1** | Intervall 2 h |
| 16 | Backup-Repository wöchentlich auf Band, Wiederherstellung bis 5 Tage | **168** | **120** | 5 × 24 h |
| 17 | Patientendatenbank: kein Datenverlust, spätestens nach 15 Min. verfügbar | **0** | **0.25** | erfordert synchrone Replikation/Hot Standby |
| 18 | Entwicklungsserver alle 3 Tage gesichert, Ausfall bis 1 Woche | **72** | **168** | |
| 19 | Lohnbuchhaltung alle 12 h gesichert, innert 4 h wiederhergestellt | **12** | **4** | |
| 20 | Monitoring max. 6 h Ausfall, Messdaten alle 30 Min. gesichert | **0.5** | **6** | |

#### **2. Excel-Übung «Backup vs. DR» (Block 7, Einzelarbeit 4) – ✍️ eigene Lösung**

*Definition der Aufgabe: **Backup-Restore** = Wiederherstellung einzelner Daten/Objekte. **Disaster Recovery** = Ausweichen/Failover bei (physischem) Totalausfall. **Ausfall** = System physisch beschädigt und **mindestens 3 Arbeitstage** ausser Betrieb. Ergänzt um eine dritte Kategorie **«Keins – Redundanz/HA greift»**, weil einige Fälle weder Restore noch DR brauchen.*

| # | Fall | Einordnung | Begründung |
| :---: | :--- | :---: | :--- |
| 1 | Eines von zwei redundanten Storage-Systemen fällt aus (Cluster trägt den Verlust) | **Keins (HA)** | Redundanz fängt es ab, Hardware tauschen, kein Datenverlust |
| 2 | Beide Storage-Systeme fallen gleichzeitig aus | **DR** | kompletter Speicher weg, physischer Totalausfall ≥ 3 Tage → Ausweichen |
| 3 | Ein einzelner Hypervisor fällt aus (Cluster verträgt 2) | **Keins (HA)** | VMs starten per HA auf den anderen Hosts |
| 4 | Vier Hypervisor gleichzeitig (Cluster verträgt nur 2) | **DR** | Kapazität des Clusters überschritten, physischer Ausfall |
| 5 | Ein DC versehentlich gelöscht (4 DC vorhanden) | **Keins (Redundanz)** | 3 DCs laufen, den gelöschten neu hochstufen. Ein Restore ist nicht nötig |
| 6 | Ein einzelner Benutzer absichtlich aus dem AD gelöscht | **Backup** | Die Löschung repliziert auf alle DCs, deshalb Objekt-Restore (AD-Papierkorb / Backup) |
| 7 | Alle Benutzer versehentlich gelöscht | **Backup** | logischer Fehler, Hardware intakt → **autoritativer AD-Restore**. Gross, aber kein physischer Schaden |
| 8 | Ein DC startet nach Updates nicht (3 weitere laufen) | **Keins / Backup** | Redundanz trägt den Betrieb. DC aus dem Backup zurücksetzen oder neu aufsetzen |
| 9 | Nach Updates startet kein DC mehr | **Backup** | Hardware intakt → System-Restore der DCs (Forest Recovery). Kritisch, aber nach Definition kein DR |
| 10 | Serverraum durch Wasserschaden komplett zerstört | **DR** | physischer Totalausfall des Standorts |
| 11 | Einzelne Datei versehentlich überschrieben | **Backup** | Klassiker: granularer Restore |
| 12 | Ransomware verschlüsselt Produktivdaten, Offline-Backups unversehrt | **Backup** (+ DR-Prozess) | Hardware intakt → Restore aus dem Offline-Backup nach Bereinigung. ⚠️ Folie Block 4: «verlangt oft beide Strategien», Mobirama-Lösung: DR, wenn die ganze Umgebung weg ist |
| 13 | RAID-Controller defekt, RAID-5-Array nicht mehr lesbar | **Backup** | Controller ersetzen, Daten aus dem Backup zurückspielen. DR nur, wenn der Ersatz ≥ 3 Tage dauert |
| 14 | Stromausfall legt das RZ 2 h lahm, Hardware unbeschädigt | **Keins** | kein Schaden, < 3 Tage → USV/Notstrom/Warten, danach geordneter Neustart |
| 15 | Brand zerstört das gesamte RZ Standort 1 | **DR** | physischer Totalausfall |
| 16 | DB-Tabelle durch fehlerhaftes Skript korrumpiert | **Backup** | Point-in-Time-Restore |
| 17 | Einzelner Switch fällt aus (redundant) | **Keins (HA)** | Redundanz |
| 18 | Versehentlich gelöschtes Postfach wiederherstellen | **Backup** | Item-/Postfach-Restore |
| 19 | Erdbeben macht Standort 1 für Wochen unbrauchbar | **DR** | Standortverlust |
| 20 | Logischer Applikationsfehler löscht über Nacht produktive Datensätze | **Backup** | Point-in-Time-Restore. Replikation hilft nicht (repliziert den Fehler) |

#### **3. Kapazitätsberechnung Gruppenaufgabe 7.1 (SwissLogistics AG)**

*Annahmen: 120 TB Start, +20 % p. a., Retention 12 monatliche Fulls + 30 tägliche Inkremente (5 % Change-Rate), Deduplizierung 4:1, Overhead 20 %.*

| Jahr | Primärdaten | 12 Fulls | 30 Dailies (5 %) | logisch gesamt | ÷ 4 (Dedup) | × 1.2 (Overhead) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 120 TB | 1'440 TB | 180 TB | 1'620 TB | 405 TB | 486 TB |
| 1 | 144 TB | 1'728 TB | 216 TB | 1'944 TB | 486 TB | 583.2 TB |
| 2 | 172.8 TB | 2'073.6 TB | 259.2 TB | 2'332.8 TB | 583.2 TB | 699.8 TB |
| **3** | **207.36 TB** | **2'488.3 TB** | **311.0 TB** | **2'799.4 TB** | **699.8 TB** | **≈ 839.8 TB** |

*   **Empfehlung Musterlösung:** mindestens **850 TB netto** nutzbar, **ca. 1.1 PB brutto** (inkl. RAID und Reserve für unvorhergesehenes Wachstum).
*   ⚠️ **Vereinfachung der Musterlösung:** Sie rechnet alle 12 Monats-Fulls mit dem **Endvolumen von Jahr 3** (worst case). Real wären die älteren Fulls etwas kleiner, das Ergebnis ist also bewusst konservativ.

#### **4. Gruppenaufgabe 8.1 (Folie Block 8): SwissBank IT Services, RPO 0 / RTO 30 Min., Zürich–Bern – ✍️ eigene Lösung**

*   **Latenz:** Die Lichtlaufzeit in Glasfaser beträgt ca. 5 µs/km. Bei ~120 km sind das ≈ 0.6 ms pro Richtung und **≈ 1.2 ms Round-Trip** (die reale Faserstrecke ist meist länger als die Luftlinie, dazu kommt der Overhead von Switches/Storage). **Jeder synchrone Schreibvorgang wartet mindestens einen RTT.** Die Faustgrenze für synchrone Replikation liegt bei ~100 km, also an der Grenze.
*   **RPO = 0:** **technisch machbar, aber mit Performance-Risiko** für eine hochfrequente Transaktions-DB → **Gelb**. Wichtig: Bei einer Leitungsstörung muss man entscheiden, ob die Produktion stoppt oder das RPO kurzzeitig ≠ 0 wird.
*   **RTO 30 Min. bei Standort-Totalausfall:** **nur mit Hot Standby und automatisiertem, regelmässig getestetem Failover** realistisch (Cluster mit **Quorum/Witness an einem dritten Standort** gegen Split-Brain, DNS/Netz/Applikationsabhängigkeiten). Mit Restore aus dem Backup ist das unmöglich → **Gelb**.
*   **Finanziell:** doppelte Infrastruktur, HA-Lizenzen, Dark Fiber sind teuer, aber für Kernbanken (FINMA, operationelle Resilienz) begründbar.
*   **Drei grösste Risiken:**
    1.  Latenz/Performance-Einbussen und Leitungsausfall (Split-Brain).
    2.  **RPO 0 schützt nicht vor logischen Fehlern/Ransomware**, die sofort mitrepliziert werden. Zusätzlich immutable Backups oder Snapshots nötig.
    3.  Hohe Kosten, und das RTO von 30 Min. steht und fällt mit Automatisierung und Tests.
*   **Gesamtbewertung: Gelb** (machbar unter Auflagen).

#### **5. Gruppenaufgabe 8.3 (Folie Block 8): MediCare Hospital, Testkonzept (RTO 4 h) – ✍️ eigene Lösung**

| Szenario | Testart | Wer | Wie oft | Erfolgskriterium |
| :--- | :--- | :--- | :--- | :--- |
| «Der versehentlich gelöschte Befund» | Datei-/Item-Restore | Backup-Admin, Abnahme durch Fachverantwortliche (Arzt/Klinik-IT) | monatlich (Stichprobe) | Dokument korrekt und vollständig in < 30 Min. zurück, Inhalt bestätigt |
| «Der verschlüsselte SQL-Server» | DB-Restore (Point-in-Time) aus Immutable/Offline-Kopie in isolierter Sandbox, **inkl. Entschlüsselung mit Key aus HSM/Tresor** | DB-Admin, Security, Applikationsverantwortliche | quartalsweise | Key auffindbar, DB konsistent (Integritätscheck), App-Login ok, Datenstand gemäss RPO, Dauer < 4 h |
| «Das abgebrannte Rechenzentrum» | **Tabletop** (Krisenstab) + technischer **DR-Test / Teilumschaltung** am Ausweichstandort | Krisenstab, Klinikleitung, IT, Kommunikation | Tabletop quartalsweise, DR-Test jährlich (Wochenende, isoliert) | KIS/AD/PACS in **≤ 4 h** am Ausweichstandort nutzbar, Reihenfolge eingehalten, Kommunikationskette funktioniert, Failback geplant |

*   Dazu **täglich** automatische Verifikation (SureBackup), Testprotokolle mit Zeitmessung, Abweichungsanalyse und Nachtest.

#### **6. Kurze Kontrollfragen zum Selbsttest**

1.  *Worin unterscheiden sich Backup und Archivierung?* Backup: kurzfristige Wiederherstellung, kurze Retention. Archiv: unveränderbare, gesetzeskonforme Langzeitaufbewahrung (z. B. 10 Jahre OR, WORM).
2.  *Warum ist RAID kein Backup?* Es schützt nur vor Plattenausfällen, nicht vor Löschung, Ransomware, Korruption oder Brand. Fehler werden sofort gespiegelt.
3.  *Was bedeuten die «1» und die «0» in 3-2-1-1-0?* Eine Offline-/Air-Gapped- oder Immutable-Kopie. Null Fehler durch automatische Verifikation und Restore-Tests.
4.  *Inkrementell vs. differenziell beim Restore?* Inkrementell: Full + alle Inkremente. Differenziell: Full + letztes Differenzielles.
5.  *Warum schützt Replikation nicht vor Ransomware?* Die Verschlüsselung und Löschung wird mitrepliziert.
6.  *Warum sind Snapshots kein Backup?* Sie liegen auf demselben Storage und gehen bei dessen Ausfall mit verloren.
7.  *RPO 15 Min.: Welche Technologien?* Log-Backups alle 15 Min., häufige Snapshots/Inkremente, CDP, Replikation.
8.  *RTO < 1 h: Welche Technologien?* Instant Recovery, Hot Standby, aktive Replikation mit Failover.
9.  *Agentless vs. Agent: Wann was?* VMs agentless (CBT, skalierbar). Physische Server, DBs mit Item-Restore und Endgeräte mit Agent.
10. *Inline vs. Post-Process-Deduplizierung?* Inline: sofort, viel CPU, keine Landing Zone. Post-Process: erst schreiben, später reduzieren, braucht temporären Platz.
11. *Source- vs. Target-Deduplizierung?* Source entlastet das Netzwerk, Target entlastet die Quellsysteme.
12. *Warum kann ein zu optimistischer Dedup-Faktor gefährlich sein?* Es wird zu wenig Speicher beschafft, Backups brechen ab und das RPO wird verletzt.
13. *Vier Strategien der Risikosteuerung?* Vermeiden, Mindern, Transferieren, Akzeptieren (Akzeptanz formell dokumentieren).
14. *Sofortmassnahme Nr. 1 bei Ransomware?* Betroffene Systeme vom Netz trennen (Containment), nicht sofort neu aufsetzen (Forensik).
15. *Wem meldet man in der Schweiz eine Datensicherheitsverletzung mit hohem Risiko?* Dem EDÖB, «so rasch als möglich» (Art. 24 DSG). Betreiber kritischer Infrastrukturen melden Cyberangriffe zusätzlich innert 24 h dem BACS.
16. *Cold, Warm oder Hot Standby für RTO 4 h?* Warm Standby (Stunden). Hot für ≈ 0, Cold für Tage.
17. *Was ist Failback?* Die Rückführung vom DR-Standort ins reparierte Primär-RZ inkl. Rücksynchronisation. Ebenso komplex und testpflichtig.
18. *Was gehört in einen Restore-Testbericht?* Vorgehen, Chronologie, gemessenes RTO/RPO, Konsistenzprüfung, Abweichungen, Massnahmen, Freigabe.

---

### **XXVI. Formelsammlung und Merkzahlen**

| Thema | Formel / Merkzahl |
| :--- | :--- |
| **Risikowert** | RW = Eintrittswahrscheinlichkeit × Schadensausmass (5×5 → 1–25) |
| **Backup-Durchsatz** | Durchsatz = Datenmenge ÷ Backup-Fenster (+ ~20 % Reserve) |
| **Restore-Durchsatz** | Durchsatz = wiederherzustellende Menge ÷ RTO |
| **Backup-Intervall** | Intervall ≤ RPO |
| **Inkrement-Grösse** | Primärvolumen × tägliche Änderungsrate |
| **Rohkapazität** | (#Fulls × Full-Grösse) + (#Inkremente × Inkrement-Grösse) |
| **Reduktionsfaktor** | Deduplizierungsrate × Komprimierungsrate |
| **Effektive Kapazität** | Rohkapazität ÷ Reduktionsfaktor × (1 + Puffer 20–30 %) |
| **Wachstum** | Kapazitätₙ = Kapazität₀ × (1 + Wachstumsrate)ⁿ |
| **Verfügbarkeit** | Ausfallzeit = (1 − Verfügbarkeit) × Zeitraum. 99.9 % ≈ 8.76 h/Jahr, 99.99 % ≈ 52.6 min/Jahr |
| **RAID-Nutzkapazität** | RAID 0: n·C · RAID 1: C (2 Disks) · RAID 5: (n−1)·C · RAID 6: (n−2)·C · RAID 10: n/2·C |
| **Netzwerk** | 1 Gbit/s ≈ 125 MB/s theoretisch (≈ 110 MB/s praktisch) ≈ 450 GB/h. 10 Gbit/s ≈ 1'250 MB/s |
| **Einheiten** | 1 TB = 1'000'000 MB (dezimal). 1 TB/h ≈ 278 MB/s. 1 h = 3'600 s |
| **Transferzeit** | 1 TB über 1 Gbit/s ≈ 2.2 h (theoretisch). 10 TB über 100 Mbit/s ≈ 9 Tage. 50 TB über 1 Gbit/s ≈ 4.6 Tage. 100 TB über 1 Gbit/s ≈ 9–10 Tage |
| **Glasfaser-Latenz** 🔎 | ≈ 5 µs/km. 100 km ≈ 1 ms Round-Trip. Synchrone Replikation bis ~50–100 km |
| **Aufbewahrung CH** | OR 958f: 10 Jahre (Geschäftsbücher, Buchungsbelege, Geschäfts-/Revisionsbericht). MWSTG Immobilien: 20 Jahre 🔎 |
| **Tape** | LTO-9: 18 TB nativ / 45 TB komprimiert. LTO-10: 30 TB / 75 TB, 40-TB-Kassette / 100 TB 🔎. Haltbarkeit bis 30 Jahre |
| **Typische Raten** | Deduplizierung 2:1–20:1 (VMs/VDI bis 20:1+). Kompression 1.2:1–2:1. Realistische Gesamtannahme im Fallbeispiel ~1:2 |
| **Typische Änderungsraten** | Archiv ~0.5 %/Tag, Standard 1–5 %/Tag, ERP ≥ 10 %/Tag. Inkremente ≈ 3–5 % eines Fulls (Acronis) |
| **Planungshorizont** | 3–5 Jahre. Wachstum typischerweise 10–30 % p. a. |
| **Kapazitätsschwellen** | Warnung ~80–85 %, kritisch ~90 %, Reserve ~20 % |
| **Nach Ransomware** | mind. 30 Tage verstärktes Monitoring |
| **Immutability** | typisch 30 Tage Object Lock / WORM |
| **M365** 🔎 | Exchange Recoverable Items 14 Tage (max. 30), SharePoint/OneDrive-Papierkorb 93 Tage |

---

### **XXVII. Glossar**

| Begriff | Erklärung |
| :--- | :--- |
| **Air-Gap** | physische (oder logische) Trennung einer Backup-Kopie vom Netzwerk, z. B. Tape im Tresor |
| **Applikationskonsistent** | Backup, bei dem die Applikation vorher in einen konsistenten Zustand versetzt wurde (VSS/Quiescing) |
| **BACS** | Bundesamt für Cybersicherheit, bis Ende 2023 NCSC |
| **Bare-Metal-Recovery** | Wiederherstellung eines kompletten Systems auf neuer, leerer Hardware |
| **BCM / BCP** | Business Continuity Management / Plan: Aufrechterhaltung des Geschäftsbetriebs, DR ist ein Teil davon |
| **BIA** | Business Impact Analysis: Analyse der Kritikalität von Prozessen/Systemen, Basis für RPO/RTO |
| **BYOK** | Bring Your Own Key: Der Kunde behält die Kontrolle über die Verschlüsselungsschlüssel in der Cloud |
| **CAPEX / OPEX** | Investitions- bzw. Betriebskosten, zusammen die TCO |
| **CBT** | Changed Block Tracking: Der Hypervisor merkt sich geänderte Blöcke, das ermöglicht effiziente Inkremente |
| **CDP** | Continuous Data Protection: jede Schreiboperation wird im Journal erfasst, RPO ≈ 0, Any-Point-in-Time |
| **CIA-Triade / VVI** | Confidentiality, Integrity, Availability / Vertraulichkeit, Verfügbarkeit, Integrität |
| **CLOUD Act** | US-Gesetz, das US-Behörden unter Umständen Zugriff auf Daten von US-Anbietern im Ausland erlaubt |
| **Copy-on-Write / Redirect-on-Write** | Snapshot-Verfahren: alten Block kopieren bzw. neue Schreibvorgänge umleiten |
| **Crash-konsistent** | Zustand wie nach einem Stromausfall: RAM-Inhalte und laufende Transaktionen fehlen |
| **D2D2T / D2D2C** | Disk-to-Disk-to-Tape / -Cloud: zuerst schnell auf Disk, dann auf Tape oder in die Cloud |
| **Data Owner / Custodian** | fachlicher Dateneigentümer / technischer Verwalter (haftet für die Umsetzung) |
| **Deduplizierung** | redundante Blöcke nur einmal speichern (Hash + Pointer). Inline/Post-Process, Source/Target |
| **DLP** | Data Loss Prevention: verhindert den Abfluss sensibler Daten, findet falsch abgelegte Daten |
| **DR / DRaaS** | Disaster Recovery (Wiederherstellung der gesamten IT-Betriebsfähigkeit) / als Cloud-Service |
| **EDÖB** | Eidgenössischer Datenschutz- und Öffentlichkeitsbeauftragter, Meldestelle nach Art. 24 DSG |
| **EDR / XDR / MDR** | Endpoint / Extended / Managed Detection and Response (Verhaltensanalyse statt Signaturen) |
| **Egress-Gebühren** | Kosten für das Herunterladen von Daten aus der Cloud |
| **Failover / Failback** | Umschalten auf das Zweitsystem / Rückführung ins Primärsystem |
| **GFS** | Grossvater-Vater-Sohn-Rotationsschema (monatlich-wöchentlich-täglich) |
| **HSM** | Hardware Security Module für die sichere Schlüsselverwaltung |
| **Immutable Storage** | unveränderbarer Speicher (WORM, Object Lock): keine Löschung/Änderung innerhalb der Frist |
| **Instant Recovery** | VM startet direkt aus dem Backup-Speicher, Daten werden im Hintergrund zurückmigriert |
| **IoC** | Indicator of Compromise: technischer Hinweis auf eine Kompromittierung (Hash, IP, Domain) |
| **IOPS** | Input/Output Operations per Second: Mass für viele kleine Zugriffe |
| **LTO / LTFS** | Linear Tape Open (Bandstandard) / Linear Tape File System |
| **LUN** | Logical Unit Number: Adresse eines Block-Speicherbereichs im SAN |
| **NDMP** | Network Data Management Protocol: performante Sicherung von NAS-Systemen |
| **NAS / SAN / DAS** | Network Attached / Storage Area Network / Direct Attached Storage |
| **Object Lock** | WORM-Funktion für S3-Objektspeicher (Compliance Mode: auch Admins können nicht löschen) |
| **RaaS** | Ransomware-as-a-Service: Entwickler vermieten die Ransomware an Affiliates |
| **RACI** | Responsible, Accountable, Consulted, Informed: Matrix für Verantwortlichkeiten |
| **RBAC** | Role-Based Access Control: rollenbasierte Zugriffsrechte |
| **Rehydrierung** | Zusammensetzen deduplizierter Daten beim Restore (verlängert das RTO) |
| **Retention** | Aufbewahrungsdauer von Backups/Archiven |
| **RPO / RTO** | max. tolerierbarer Datenverlust (zeitlich) / max. tolerierbare Ausfallzeit |
| **Scale-up / Scale-out** | Erweiterung im bestehenden System / durch zusätzliche Knoten |
| **Shared Responsibility** | Cloud-Provider verantwortet die Infrastruktur, der Kunde seine Daten (inkl. Backup) |
| **SIEM** | Security Information and Event Management: korreliert Sicherheitsereignisse zentral |
| **SLA** | Service Level Agreement: vertraglich vereinbarte Service-Ziele (Verfügbarkeit, RTO/RPO) |
| **SPOF** | Single Point of Failure: Komponente, deren Ausfall das Ganze stoppt |
| **SureBackup / Auto-Verify** | automatischer Boot-/Funktionstest des Backups in einer Sandbox |
| **Tabletop-Übung** | theoretisches Durchspielen eines Notfallszenarios am Tisch |
| **TCO** | Total Cost of Ownership: alle Kosten über den Lebenszyklus |
| **Tiering** | Verteilung der Daten auf Speicherklassen nach Nutzung (Hot/Warm/Cold) |
| **TOM** | technische und organisatorische Massnahmen (DSG) |
| **VADP / RCT** | VMware vStorage APIs for Data Protection / Hyper-V Resilient Change Tracking |
| **VSS** | Volume Shadow Copy Service (Windows): applikationskonsistente Snapshots, «Vorherige Versionen» |
| **WORM** | Write Once, Read Many: einmal schreiben, danach nur lesen |
| **Zero Trust** | «Vertraue niemandem, überprüfe alles»: jeder Zugriff wird geprüft |

---

### **XXVIII. Quellen**

**Kursunterlagen (Ordner «Archivierung - Backup- und Restore Loesungen»):**
*   *Kursmaterialien/Block1–8:* Foliensätze `BlockX_ABRL_TA1A*.pdf`, Artikel (`Artikel_1_1` … `Block8_4`), Gruppenaufgaben mit Musterlösungen (`Uebungen/Gruppenaufgabe_*.pdf`), Excel-Übungen `Uebungsfragen_ABRL_RPO_RTO.xlsx` und `Uebungsfragen_ABRL_Backup_DR.xlsx`.
*   *Fallbeispiele/:* `Fallbeispiel-Mobiliar.pdf` (Mobirama 1/2018, gescannt), `Fallbeispiel-Fragen-Mobirama(-Musterlösung-V1.0).pdf`, `Fallbeispiele-DEC_1-2(-Lösungen).pdf`.
*   *Infos/:* `RAID-Übersicht und 3-2-1-1-0 Backup-Strategie.pdf`, `Info_6_2_ABRL_Liste der agenten basierten software.pdf`.
*   *Aufgaben/:* Gruppenpräsentationen (Risikoanalyse SwissData AG, Risikomatrix AlpinTech, CyberShield AG).
*   *Veeam/:* Acronis «Backup für Dummies» (2015), Veeam «Microsoft 365 Backup for Dummies» (2020).
*   *Nicht verarbeitet:* Podcasts (`.m4a`, Audio-Fassungen der Artikel), PNG-Screenshots der Aufgabenfolien.

**🔎 Online-Recherche (Stand September 2026):**
*   Art. 24 DSG – Meldung von Verletzungen der Datensicherheit: [datenschutzpartner.ch](https://www.datenschutzpartner.ch/dsg/dsg-24/), [EDÖB – Leitfaden Data Breach](https://www.edoeb.admin.ch/de/leitfaden-data-breach)
*   Art. 61, 63 und 64 DSG – Strafbestimmungen (Busse bis CHF 250'000 bzw. CHF 50'000 gegen den Betrieb): [datenschutzpartner.ch – Art. 61](https://www.datenschutzpartner.ch/dsg/dsg-61/), [onlinekommentar.ch – Art. 61](https://onlinekommentar.ch/de/kommentare/dsg61), [datenschutzpartner.ch – Art. 63](https://www.datenschutzpartner.ch/dsg/dsg-63/), [datenschutzpartner.ch – Art. 64](https://www.datenschutzpartner.ch/dsg/dsg-64/)
*   Meldepflicht für Cyberangriffe auf kritische Infrastrukturen (BACS): [bacs.admin.ch – Meldepflicht](https://www.bacs.admin.ch/de/meldepflicht), [bacs.admin.ch – Informationen zur Meldepflicht](https://www.bacs.admin.ch/de/informationen-zur-meldepflicht)
*   NCSC wird Bundesamt für Cybersicherheit BACS: [admin.ch – Medienmitteilung](https://www.admin.ch/gov/de/start/dokumentation/medienmitteilungen/rss-feeds/nach-dienststellen/alle-mitteilungen.msg-id-99574.html)
*   FINMA-Rundschreiben 2023/1 «Operationelle Risiken und Resilienz – Banken»: [Redguard – Überblick](https://www.redguard.ch/blog/2024/05/24/finma-rundschreiben-2023-1/), [KPMG – FINMA-Rundschreiben](https://kpmg.com/ch/de/branchen/banking/finanzmarkt-regulierung/finma-rundschreiben.html)
*   Aufbewahrungspflichten Schweiz (OR 958f, GeBüV, MWSTG 20 Jahre Immobilien): [BDO – Aufbewahrungspflichten](https://www.bdo.ch/de-ch/publikationen/aufbewahrungspflichten-und-aufbewahrungsfristen-von-geschaeftsunterlagen-in-der-schweiz), [WEKA – Aufbewahrungsfristen](https://www.weka.ch/themen/finanzen-controlling/rechnungswesen/buchfuehrung/article/aufbewahrungsfristen-compliance-anforderungen-an-die-geschaeftsunterlagen/)
*   LTO-10 (30 TB / 40 TB nativ): [lto.org – LTO-10](https://www.lto.org/lto-10/), [lto.org – 40-TB-Ankündigung](https://www.lto.org/2025/11/lto-program-announces-new-40-tb-lto-10-cartridge-specifications-and-refreshes-its-roadmap-for-ultra-high-density-ai-ready-archival-storage/), [Blocks & Files](https://www.blocksandfiles.com/tape/2025/11/13/lto-10-bumped-to-40-tb-as-future-tape-capacities-get-cut/1711787)
*   Glasfaser-Latenz (5 µs/km) und synchrone Replikation: [MapYourTech – The 5-Microsecond Rule](https://mapyourtech.com/the-5-microsecond-rule-fiber-propagation-latency-per-kilometer/), [Bitkom – Datenspiegelung über grosse Entfernungen](https://www.bitkom.org/sites/main/files/file/import/071218-Wide-Area-Version-10.pdf)
*   Microsoft-365-Retention (Recoverable Items, Papierkorb 93 Tage): [NinjaOne – M365 Recycle Bin and Retention Limits](https://www.ninjaone.com/blog/explain-m365-recycle-bin-and-retention-limits/), [Microsoft Support – Site Collection Recycle Bin](https://support.microsoft.com/en-us/office/restore-deleted-items-from-the-site-collection-recycle-bin-5fa924ee-16d7-487b-9a0a-021b9062d14b)
*   IKT-Minimalstandard: [BWL – IKT-Minimalstandards](https://www.bwl.admin.ch/de/ikt-minimalstandards), [datenrecht.ch – BWL-Minimalstandard](https://datenrecht.ch/en/bwl-minimalstandard-zur-verbesserung-der-it-resilienz/)
