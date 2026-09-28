# SIUS – System-Installation und Störungsbehebung

**Zusammenfassung für die Modulprüfung (Open Book)**
HF Informatik, 5. Semester · Dozent: Pratheep Sinnathurai (Unit 08: Markus Nussbaumer) · Stand: 28.09.2026

> **Grundlage:** alle Dateien im Ordner `Kursmaterialien/`: Foliensätze Unit 00–08 (Unit 05 in zwei Versionen: April 2024 und August 2026), Arbeitsaufträge `aa01a` (Multiple Choice Hyper-V) und `aa01b` (VM erstellen), Übungsauftrag `B5 – Security Experts (Defender & Firewall)` und Selbststudium Bicep. Dazu kommen die Inhalte der **Nachbereitungs-Module auf Microsoft Learn**. Laut Folien können diese in der Modulprüfung abgefragt werden. Ergänzt mit Online-Recherche (Quellen am Schluss).
>
> **Aufbau:** Ein Kapitel pro Unit. Jedes Kapitel enthält die Lernziele, die Kernkonzepte (auch den Inhalt der Diagramm-Folien), die beantworteten Recherchefragen aus den Folien, die Arbeitsaufträge und einen Block zur **Störungsbehebung**. Danach folgen ein Kapitel zu den Vorfächern CSIN/SYSI, Lösungen zu den Aufträgen, ein Fragenkatalog, eine Befehlsreferenz und die Korrekturen.

### Legende

| Symbol | Bedeutung |
|---|---|
| 📚 | Inhalt aus einem **Nachbereitungs-Modul** (Microsoft Learn). Laut Unit 00 prüfungsrelevant. |
| 🔎 | **Ergänzung aus der Recherche**. Steht so nicht in den Folien. |
| ⚠️ | **Korrektur oder Widerspruch**: Die Unterlage enthält einen Fehler, ist veraltet oder missverständlich. Alle Punkte sind in [Kapitel 15](#korrekturen) gesammelt. |
| 🛠️ | **Störungsbehebung**: typische Fehlerbilder, Ursachen und Lösungen |
| ✍️ | **Eigene Lösung** für Aufgaben ohne offizielle Musterlösung |
| 🗂️ | Nur in der **älteren Folienversion** von Unit 05 (April 2024) enthalten |

---

## Inhaltsverzeichnis

1. [Prüfung und Modulüberblick](#pruefung)
2. [Unit 01 – Microsoft Hyper-V](#hyperv)
3. [Unit 02 – Container auf Windows (Docker, Kubernetes)](#container)
4. [Unit 03 – Microsoft Intune](#intune)
5. [Unit 04 – Azure Arc](#arc)
6. [Unit 05 – Windows-Sicherheit: Credential Guard, Defender Antivirus, Firewall](#defender)
7. [Unit 06 – GitHub](#github)
8. [Unit 07 – Generative KI, Microsoft Foundry, Security Copilot](#ki)
9. [Unit 08 – Infrastructure as Code mit Bicep](#bicep)
10. [Repetition der Vorfächer CSIN und SYSI (Räume 1–4)](#vorfaecher)
11. [Lösungen: Arbeitsauftrag aa01a (Multiple Choice Hyper-V)](#aa01a)
12. [Lösungen: Übungsauftrag B5 «Security Experts»](#b5)
13. [Fragenkatalog: alle Repetitions- und Recherchefragen](#fragen)
14. [Befehlsreferenz](#befehle)
15. [Korrekturen zu den Kursunterlagen](#korrekturen)
16. [Hinweise zum Material](#hinweise)
17. [Glossar](#glossar)
18. [Quellen](#quellen)

---

<a id="pruefung"></a>
## 1. Prüfung und Modulüberblick

### Rahmen (Unit 00)

- **Modulprüfung:** 2 Stunden, zählt **100 %** zur Gesamtnote, Ende Semester.
- **Geprüft wird auch Wissen aus den Vorfächern CSIN und SYSI** (siehe [Kapitel 10](#vorfaecher)).
- **Nachbereitung:** Nach jedem Block gibt es MS-Learn-Module (Richtgrösse 2 h pro Block). **Inhalte der Nachbereitung können in der Modulprüfung abgefragt werden.**
- Lehrmittel: **learn.microsoft.com**. Zusätzliches Material ist erlaubt, aber nicht nötig.
- Unterrichtsform: online, 40 Lektionen (8 Blöcke à 5 Lektionen), viele Praxisaufgaben und Diskussionen, starke Zusammenarbeit mit Online-Kursen (MOCs). Kamerapflicht, kein Recording.
- Empfehlung des Dozenten: eine eigene Zusammenfassung führen.
- Ersatztermine für verpasste Blöcke: 11.09.2026 (13:00–17:00) und 25.09.2026 (08:00–12:00).

### Themen und Nachbereitung

| Unit | Thema | Nachbereitung (MS Learn) | Kapitel |
|---|---|---|---|
| 01 | Grundlagen Microsoft Hyper-V | *Configure and manage Hyper-V*, *Configure and manage Hyper-V virtual machines* | [2](#hyperv) |
| 02 | Container auf Windows Server | *Run containers on Windows Server*, optional *Orchestrate containers on Windows Server using Kubernetes* | [3](#container) |
| 03 | Microsoft Intune | *Introduction to Microsoft Intune*, *Understand device management using Microsoft Intune*, *Benefits of Microsoft Intune* | [4](#intune) |
| 04 | Azure Arc | *Manage hybrid workloads with Azure Arc* | [5](#arc) |
| 05 | Microsoft Defender | *MD-102: Manage Microsoft Defender in Windows client* | [6](#defender) |
| 06 | GitHub | *Introduction to GitHub* | [7](#github) |
| 07 | Foundry, Security Copilot, OpenAI | *Introduction to generative AI and agents*, *AI Fluency* (Anthropic Academy), *Get started with AI in Azure*, *Security Copilot getting started / interactive guides*, Foundry-Doku | [8](#ki) |
| 08 | Bicep und Repetition | *Introduction to IaC using Bicep*, *Build your first Bicep file* | [9](#bicep) |

### Worauf die Prüfung zielt (Unit 08, Folie «Repetition & Prüfungsvorbereitung»)

- Begriffe und Zusammenhänge **verständlich erklären**
- Technologien und Konzepte **unterscheiden und einordnen**
- **Vor- und Nachteile begründen**
- Vorgehen **anhand eines Praxisbeispiels** erklären
- Lösungen bzw. Situationen **analysieren und beurteilen**
- Nicht nur «Was ist das?», sondern auch **«Warum und wann wird es eingesetzt?»**

### Die fünf Prüfungsbereiche («Räume» aus Unit 08)

Die Repetition in Unit 08 war in fünf Räume aufgeteilt. Laut Folie «orientieren sich die Themen an den Bereichen der Modulprüfung».

| Raum | Bereich | Inhalte | Wo in dieser Zusammenfassung |
|---|---|---|---|
| 1 | Windows, Server und PowerShell | Windows 10/11, Windows Server, Server Core, Migration, PowerShell-Grundlagen und Cmdlets | [10.1](#raum1) |
| 2 | Active Directory, DNS und DHCP | AD-Rollen, Gruppen, Trust, AGDLP, DNS-Abfragen/Records/TTL, DHCP-Prozess, Relay und Failover | [10.2](#raum2) |
| 3 | Azure, Verfügbarkeit und Business Continuity | Cloud vs. On-Premises, Cloud Service Types, Scaling, SLA, Entra ID, Metrics/Logs, RPO und RTO | [10.3](#raum3) |
| 4 | Security und Identity | TPM/BitLocker, MFA, Conditional Access, Least Privilege, RBAC, PowerShell Security, Security Baselines, LAPS, Defender und Firewall | [10.4](#raum4) und [6](#defender) |
| 5 | Moderne Infrastruktur und Automatisierung | Hyper-V, Container, Intune, Azure Arc, GitHub, Generative KI/LLM, Bicep und IaC | Kapitel [2](#hyperv) bis [9](#bicep) |

**Ablauf jeder Unit:** Repetition der letzten Unit → Lernziele → Recherchefragen (in Gruppen) → Demo → Arbeitsauftrag → Reflexion → Nachbereitung. Die Repetitionsfragen am Anfang jeder Unit sind gute Prüfungsfragen. Sie sind mit Antworten in [Kapitel 13](#fragen) gesammelt.

---

<a id="hyperv"></a>
## 2. Unit 01 – Microsoft Hyper-V

### Lernziele

Die Technikerinnen und Techniker HF können …
- die Funktionalität und Merkmale von Hyper-V auf Windows Server beschreiben,
- Hyper-V auf Windows Server installieren,
- die Optionen zur Verwaltung von Hyper-V-VMs beschreiben,
- die Netzwerkfunktionen von Hyper-V beschreiben,
- virtuelle Switches (vSwitches) erstellen,
- die Verwendung von verschachtelter Virtualisierung (Nested Virtualization) beschreiben.

### 2.1 Virtualisierung und Hypervisor

**Virtualisierung (Folie 5):**

| Physische Umgebung | Virtuelle Umgebung |
|---|---|
| Hardware (NIC, RAM, CPU, Disk) → **ein** Betriebssystem → mehrere Apps | Hardware → **Virtualisierungsschicht (Hypervisor)** → mehrere VMs. Jede VM hat ein eigenes Betriebssystem, eigene Apps und virtuelle Hardware (**vNIC, vRAM, vCPU, vDisk**). |

**Was ist ein Hypervisor?** (Folien 6 und 9, 📚)
- Der Hypervisor ist eine Softwareschicht, die beim Installieren der Hyper-V-Rolle **in den Bootprozess eingefügt** wird. Er steuert den Zugriff auf die physische Hardware.
- **Hardwaretreiber** werden nur im Host-Betriebssystem installiert (auch **übergeordnete Partition / Parent Partition / Root Partition** genannt). Die VMs (Child Partitions) sehen nur virtualisierte Hardware.
- Der Hyper-V-Hypervisor übernimmt die **volle Kontrolle über die Virtualisierungsfunktionen der CPU** (Intel VT-x / AMD-V) und gibt sie **nicht** an die Gastbetriebssysteme weiter. Ausnahme: Nested Virtualization, siehe [2.9](#nested).
- Schichten (Folie 6): **Level 0** = Hyper-V-Hypervisor auf der Hardware (CPU mit Virtualisierungs-Erweiterungen). **Level 1** = Windows-Root-Partition und Gastbetriebssysteme.

🔎 **Typ-1 vs. Typ-2-Hypervisor:**

| Typ | Beschreibung | Beispiele |
|---|---|---|
| Typ 1 (Bare Metal) | läuft direkt auf der Hardware | **Hyper-V**, VMware ESXi, KVM, Xen |
| Typ 2 (Hosted) | läuft als Anwendung auf einem Betriebssystem | VirtualBox, VMware Workstation |

Hyper-V ist auch auf Windows 10/11 ein Typ-1-Hypervisor: Nach dem Aktivieren läuft Windows selbst als Root-Partition **auf** dem Hypervisor.

### 2.2 Funktionen von Hyper-V

📚 Hyper-V gibt es als **Serverrolle** in Windows Server, als **Feature** in 64-Bit-Windows-Clients und früher als eigenständiges Produkt *Microsoft Hyper-V Server*.

| Bereich | Funktionen |
|---|---|
| **Management und Konnektivität** | Hyper-V-Manager, Hyper-V-PowerShell-Modul, VMConnect (Konsole), PowerShell Direct (PowerShell in der VM ohne Netzwerk, direkt vom Host) |
| **Portabilität** | Live Migration (laufende VM ohne Unterbruch auf anderen Host verschieben), Storage Migration, Import/Export |
| **Disaster Recovery und Backup** | **Hyper-V Replica** (Kopien von VMs an einem anderen Standort), Production Checkpoints, VSS-Unterstützung für applikationskonsistente Backups |
| **Sicherheit** | **Secure Boot** (prüft Signaturen beim Start), **Shielded VMs** (verschlüsselte VMs, laufen nur auf geschützten Hosts) |
| **Optimierung** | **Integration Services**: Time Synchronization, Operating System Shutdown, Data Exchange (Key-Value-Pairs), Heartbeat, Backup (VSS), Guest Services (Dateien vom Host in die VM kopieren) |

### 2.3 Gastbetriebssysteme, Anforderungen, Tools, Use Cases

**Unterstützte Gastbetriebssysteme** (Stand Folie Februar 2024):
- alle unterstützten Windows-Versionen
- Linux: Red Hat Enterprise Linux, Debian, Oracle Linux, SUSE, Ubuntu (die Folie nennt zusätzlich CentOS. 🔎 CentOS Linux ist seit dem 30.06.2024 ohne Support und fehlt in der aktuellen MS-Liste.)
- FreeBSD
- **nicht:** macOS
- 📚 Microsoft leistet Support nur für Probleme in Microsoft-Betriebssystemen und in den Integration Services.

**Systemanforderungen Hyper-V-Host** (Folie 11, 📚):
- 64-Bit-Prozessor mit **SLAT** (Second Level Address Translation; Intel EPT bzw. AMD RVI)
- Prozessor mit **VM Monitor Mode Extensions**
- **Intel VT oder AMD-V** im BIOS/UEFI aktiviert
- **Hardware-DEP** aktiviert (Intel XD-Bit, AMD NX-Bit)
- genügend RAM für Host und VMs
- 📚 Prüfen mit `systeminfo.exe` (Abschnitt «Hyper-V-Anforderungen»)

🔎 **Editionen:** Client-Hyper-V gibt es in Windows 10/11 **Pro, Enterprise und Education**, **nicht in Home**. Auf dem Server ist Hyper-V in Standard und Datacenter enthalten (Unterschied: Anzahl lizenzierter Windows-Server-VMs, 2 vs. unbegrenzt).

**Verwaltungstools** (Folie 12):

| Tool | Beschreibung |
|---|---|
| **Hyper-V-Manager** | Natives Windows-Tool (MMC) für lokale und entfernte Hyper-V-Server |
| **System Center Virtual Machine Manager (SCVMM)** | Umfassende Verwaltung grosser virtueller Umgebungen (Cluster, Fabric, Bibliotheken) |
| **Windows Admin Center (WAC)** | **Webbasiertes** Tool zur Serververwaltung, inkl. Hyper-V |
| **PowerShell** | Vollständige Verwaltung per Cmdlets, ideal für Automatisierung |

📚 **Use Cases:** Serverkonsolidierung (weniger physische Server, weniger Platz und Energie), Entwicklungs- und Testumgebungen (schnell erstellen und zurücksetzen), VDI (virtuelle Desktops mit Remote Desktop Services), Private Cloud (z. B. Azure Local mit Storage Spaces Direct und SDN).

### 2.4 Installation

📚 Drei Wege auf Windows Server:

1. **Server-Manager:** Rollen und Features hinzufügen → Rolle *Hyper-V* + Feature *Hyper-V-Verwaltungstools* → Installieren (Neustart).
2. **Windows Admin Center:** Server wählen → Tools → Rollen und Features → Hyper-V.
3. **PowerShell:**

```powershell
Install-WindowsFeature -Name Hyper-V -ComputerName <Servername> -IncludeManagementTools -Restart
Get-WindowsFeature -Name Hyper-V*      # Kontrolle nach dem Neustart
```

Auf **Server Core** installiert `-IncludeManagementTools` nur das PowerShell-Modul (keine GUI).

**Windows-Client** (Arbeitsauftrag aa01b): Systemsteuerung → Programme und Features → *Windows-Features aktivieren oder deaktivieren* → **Hyper-V** (mit *Hyper-V-Plattform* und *Hyper-V-Verwaltungstools*) → Neustart.
🔎 Per PowerShell (als Admin):

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

### 2.5 Virtuelle Maschinen: Konfigurationsversion und Generation

**VM Configuration Version** (Folie 15, 📚)
- Kennzeichnet **Feature-Satz und Kompatibilität** einer VM (Konfiguration, Checkpoints).
- **Bestimmt durch die Hyper-V-Version des Hosts**, auf dem die VM erstellt (oder aktualisiert) wurde.
- Wird beim Verschieben auf einen neueren Host **nicht automatisch** aktualisiert. So kann die VM zurück auf den alten Host.
- Update nur manuell, **VM muss ausgeschaltet sein**, und **kein Downgrade möglich**. Danach startet die VM nicht mehr auf älteren Hosts.

```powershell
Get-VM * | Format-Table Name, Version        # Versionen der VMs
Get-VMHostSupportedVersion                   # vom Host unterstützte Versionen
Get-VMHostSupportedVersion -Default          # Standardversion für neue VMs
Update-VMVersion -Name <VMName>              # auf höchste Version des Hosts anheben
```

| Host | Unterstützte Konfigurationsversionen (Auszug) |
|---|---|
| Windows Server 2012 R2 | 5.0 |
| Windows Server 2016 | bis 8.0 |
| Windows Server 2019 | bis 9.0 |
| Windows 10 20H2 | bis 9.2 |

| Feature | ab Version |
|---|---|
| Production Checkpoints, PowerShell Direct, Hot Add/Remove Memory, Secure Boot für Linux | 6.2 |
| Virtuelles TPM (vTPM) | 7.0 |
| Nested Virtualization, VBS im Gast, grosse VMs | 8.0 |
| Nested Virtualization auf **AMD** 🔎 | 9.3 |
| Hibernation, SMT automatisch | 9.0 |

**VM-Generationen** (Folien 16–17, 📚)

| | **Generation 1** | **Generation 2** |
|---|---|---|
| Firmware | Legacy **BIOS** | **UEFI** |
| Gast-OS | 32- und 64-Bit | nur 64-Bit (ab Windows 8 / Server 2012, aktuelle Linux) |
| Boot von | IDE-Disk, IDE-DVD, Floppy (.vfd), PXE nur mit **Legacy-Netzwerkadapter** | **SCSI**-Disk, SCSI-DVD, PXE mit **Standard-Netzwerkadapter** |
| **Secure Boot** | nein | **ja, standardmässig aktiv** |
| Shielded VMs, vTPM | nein | ja |
| Virtuelle Disk | VHD oder VHDX | **nur VHDX** |
| Max. Bootvolume | 2 TB (VHDX) / 2040 GB (VHD) | **64 TB** |
| Max. vCPU / RAM 🔎 | 64 vCPU / 1 TB | 240 (WS 2019), 1024 (WS 2022), 2048 (WS 2025) / bis 240 TB |
| Hot Add/Remove von Netzwerkadaptern | nein | ja |

- **Für Secure Boot wird Generation 2 benötigt.**
- Die Generation kann **nach dem Erstellen nicht mehr geändert werden**.
- 📚 Im Betrieb gibt es **keinen Leistungsunterschied**. Gen 2 startet und installiert nur etwas schneller. Die Leistung soll nicht das Hauptargument sein.
- Best Practice: **Generation 2 verwenden, wenn das Gast-OS sie unterstützt.**

### 2.6 Virtuelle Festplatten (VHD/VHDX)

Eine **VHD (Virtual Hard Disk)** ist ein Dateiformat, das eine physische Festplatte für eine VM darstellt (mit Partitionen, Dateien und Ordnern).

**Formate** (📚)

| Format | Eigenschaften |
|---|---|
| **VHD** | max. **2040 GB**, kompatibel mit alten Hyper-V-Versionen |
| **VHDX** | max. **64 TB**, robuster bei Stromausfall (Metadaten-Log), grössere Blockgrössen (bessere Leistung), **Vergrössern/Verkleinern im laufenden Betrieb** (an SCSI-Controller) |
| **VHD Set (.vhds)** | nur für **gemeinsam genutzte Disks** (Guest Cluster), unterstützt Backup auf Host-Ebene, Online-Resize und Hyper-V Replica |

**Typen**

| Typ | Beschreibung | Vor- und Nachteile |
|---|---|---|
| **Fixed** (feste Grösse) | reserviert sofort den ganzen Platz | wenig Fragmentierung, beste Leistung, braucht aber sofort viel Speicher |
| **Dynamic** (dynamisch erweiterbar) | wächst bei Bedarf bis zur definierten Maximalgrösse | spart Speicher, Gefahr der Überbuchung des Hostspeichers |
| **Differencing** (differenzierend) | Kind-Disk speichert nur Änderungen gegenüber einer **Parent-Disk** (z. B. sysprep-Image) | spart viel Platz bei vielen ähnlichen VMs. Die Parent-Disk darf nicht verändert werden. |
| **Pass-Through** 🔎 | VM nutzt direkt eine physische Disk oder iSCSI-LUN (muss auf dem Host **offline** sein) | exklusiver Zugriff, keine Checkpoints |

⚠️ Die Folie (und MC-Frage 3) zählt **VHDX als vierten «Typ»** auf. VHDX ist ein **Format**. Fixed, Dynamic und Differencing gibt es als VHD **und** als VHDX.

Werkzeuge: Hyper-V-Manager (Assistent *Datenträger bearbeiten*), Datenträgerverwaltung, `diskpart`, WAC, PowerShell:

```powershell
New-VHD -Path D:\VMs\srv01.vhdx -SizeBytes 60GB -Dynamic
New-VHD -Path D:\VMs\kind.vhdx -ParentPath D:\Images\ws2025-sysprep.vhdx -Differencing
Convert-VHD -Path alt.vhd -DestinationPath neu.vhdx     # erstellt eine Kopie im neuen Format
Resize-VHD -Path D:\VMs\srv01.vhdx -SizeBytes 100GB
```

### 2.7 VM-Einstellungen, Checkpoints und Best Practices

**VM-Einstellungen** (Folien 19–20, ergänzt mit 📚). Im Hyper-V-Manager in zwei Gruppen:

| Gruppe | Einstellung | Inhalt |
|---|---|---|
| **Hardware** | Firmware/BIOS | Startreihenfolge, Secure Boot (Gen 2), TPM |
| | Prozessor | Anzahl vCPUs, NUMA-Topologie, Kompatibilitätsmodus |
| | Arbeitsspeicher | statisch oder **Dynamic Memory** (Startup-, Minimum-, Maximum-RAM, Puffer) |
| | Controller | IDE (nur Gen 1, max. 2 × 2 Geräte), SCSI (max. 4 Controller × 64 Disks) |
| | Netzwerkadapter | vSwitch, VLAN-ID, Bandbreite, MAC-Adresse, erweiterte Features |
| | Weitere | COM-Port, Diskette (Gen 1), Fibre-Channel-Adapter |
| **Verwaltung** | Name | Anzeigename im Hyper-V-Manager (nicht der Computername im Gast) |
| | Integrationsdienste | welche Integration Services aktiv sind |
| | Prüfpunkte (Checkpoints) | aktivieren/deaktivieren, Typ, Speicherort |
| | Smart Paging | Auslagerungsdatei für den Start, wenn das Minimum-RAM kleiner ist als der Bedarf beim Booten |
| | Automatische Start-/Stoppaktion | Verhalten beim Starten/Herunterfahren des Hosts |

- Dateien einer VM: `.vmcx` (Konfiguration), `.vmrs` (Laufzeitzustand), `.vhdx` (Disk), `.avhdx` (Checkpoint-Differenzdisk).
- 📚 Virtual NUMA und Dynamic Memory schliessen sich gegenseitig aus.
- 📚 **Ressourcenmessung:** `Enable-VMResourceMetering -VMName srv01` und danach `Measure-VM -VMName srv01` (CPU, RAM, Disk, Netzwerk).

**Checkpoints** (früher «Snapshots»)

| | **Standard Checkpoint** | **Production Checkpoint** (Standard) |
|---|---|---|
| Was wird gesichert | Disk **und Arbeitsspeicher** (laufende Programme) | nur Disk, **applikationskonsistent** via **VSS** (Windows) bzw. File System Freeze (Linux) |
| Nach dem Zurücksetzen | VM läuft genau wie vorher (z. B. offenes Notepad) | VM ist **ausgeschaltet** und startet sauber neu |
| Einsatz | Test/Entwicklung | produktive Systeme |
| Risiko | Probleme bei replizierenden Systemen (z. B. **Active Directory**, Datenbanken) | geringer |

```powershell
Set-VM -Name srv01 -CheckpointType Production       # oder Standard / ProductionOnly
Checkpoint-VM -Name srv01 -SnapshotName "vor Update"
Get-VMCheckpoint -VMName srv01
Restore-VMCheckpoint -VMName srv01 -Name "vor Update" -Confirm:$false
Remove-VMCheckpoint -VMName srv01 -Name "vor Update"  # führt die .avhdx wieder mit der .vhdx zusammen
```

- Einsatz: **vor Updates oder Softwareinstallationen** einen Checkpoint erstellen, um zurückkehren zu können (MC-Fragen 12 und 17).
- ⚠️ **Ein Checkpoint ist kein Backup.** Er liegt auf demselben Storage wie die VM. Lange Checkpoint-Ketten kosten Leistung und Speicherplatz. **`.avhdx`-Dateien nie von Hand löschen**, sondern den Checkpoint in Hyper-V löschen, damit die Disks zusammengeführt werden.

**Best Practices für Hyper-V-Hosts** (Folie 21, 📚 mit Begründung)

| Best Practice | Begründung |
|---|---|
| Host mit **angemessener Hardware** ausstatten (CPU, RAM, schneller und redundanter Storage, mehrere NICs im Team) | Ein schwacher Host bremst **alle** VMs |
| VMs auf **separaten Disks** oder **Cluster Shared Volumes (CSV)** betreiben (bei HDDs dringend empfohlen, bei SSDs sind mehrere VMs pro SSD möglich) | Weniger I/O-Konkurrenz mit dem Host-OS, das OS-Volume kann nicht vollaufen |
| **Hyper-V als einzige Serverrolle** auf dem Host (kein DC, kein Fileserver) | Alle Ressourcen stehen den VMs zur Verfügung. Andere Rollen gehören in VMs. |
| Hyper-V **remote verwalten** und den Zugriff auf Admins beschränken | Eine lokale Anmeldung verbraucht Ressourcen. Ein Konfigurationsfehler am Host trifft alle VMs. |
| Host als **Server Core** betreiben | Weniger Ressourcenverbrauch, weniger Updates, weniger Neustarts |
| **Best Practices Analyzer** und **Ressourcenmessung** nutzen | Konfigurationsprobleme und «laute Nachbarn» erkennen |
| **Generation-2-VMs** verwenden, wenn das Gast-OS das unterstützt | Secure Boot, UEFI, SCSI-Boot, grössere Disks |

<a id="hyperv-netz"></a>
### 2.8 Hyper-V-Netzwerk

Netzwerk in Hyper-V besteht aus dem **virtuellen Netzwerkadapter** (in der VM) und dem **virtuellen Switch** (auf dem Host). Der Adapter wird mit einem Port des vSwitch verbunden.

**Netzwerkadapter** (Folie 24, 📚)

| Adapter | Eigenschaften |
|---|---|
| **Legacy-Netzwerkadapter** | emuliert eine Intel 21140 Fast-Ethernet-Karte, **nur Generation 1**, kann **PXE-Boot** (Netzwerkinstallation) in Gen-1-VMs, langsamer, braucht keine Integration Services |
| **Netzwerkadapter (synthetisch)** | schneller, Gen 1 und Gen 2. In Gen 1 **kein** PXE-Boot, in Gen 2 schon. Braucht Integration Services. |

**Virtuelle Switches** (Folie 24, 📚)

| Typ | VM ↔ VM | VM ↔ Host | VM ↔ physisches Netz/Internet | Einsatz |
|---|---|---|---|---|
| **Extern** | ✅ | ✅ (wenn der Host den Adapter mitbenutzt) | ✅ | Produktion. Gebunden an eine physische NIC (auch NIC-Team oder WLAN). |
| **Intern** | ✅ | ✅ | ❌ (nur mit NAT/Routing über den Host) | Lab mit Hostzugriff, NAT-Szenarien |
| **Privat** | ✅ | ❌ | ❌ | vollständig isolierte Testnetze |

- Es gibt **keinen** Switch-Typ «Öffentlich» (MC-Frage 15).
- **VLAN-ID** pro Adapter setzbar, um VLANs des physischen Netzes in den Host zu verlängern. Verkehr zwischen VLANs läuft nur über einen Router.
- Verwaltung: **Manager für virtuelle Switches** im Hyper-V-Manager, `New-VMSwitch`, WAC.
- **Switch-Erweiterungen** (von Drittherstellern): Capture, Filtering und Forwarding (NDIS- bzw. WFP-Filtertreiber).

```powershell
New-VMSwitch -Name "Extern" -NetAdapterName "Ethernet" -AllowManagementOS $true
New-VMSwitch -Name "Intern" -SwitchType Internal
New-VMSwitch -Name "Privat" -SwitchType Private
Connect-VMNetworkAdapter -VMName srv01 -SwitchName "Extern"
Set-VMNetworkAdapterVlan -VMName srv01 -Access -VlanId 20
Get-VMSwitch
```

**Erweiterte Netzwerkfunktionen** (📚)

| Funktion | Zweck |
|---|---|
| **DHCP Guard** | verwirft DHCP-Antworten von VMs, die sich als (Rogue-)DHCP-Server ausgeben |
| **Router Guard** | verwirft Router-Advertisements/Redirects von nicht autorisierten VMs |
| **Port Mirroring** | kopiert den Verkehr eines Adapters auf eine Monitoring-VM |
| **Bandbreitenverwaltung** | Minimum- und Maximum-Bandbreite pro virtuellem Adapter |
| **NIC Teaming / SET** (Switch Embedded Teaming) | Ausfallsicherheit und Bündelung. SET ist direkt im vSwitch integriert und unterstützt RDMA. |
| **VMQ / VMMQ / d.VMMQ** | Hardware-Queues liefern Pakete direkt an die VM (weniger CPU-Last) |
| **SR-IOV** | VMs teilen sich direkt die PCIe-Hardware der NIC (sehr schnell, braucht Hardware und Treiber) |
| **IPsec Task Offloading** | IPsec-Berechnung auf der NIC |
| **NAT-Objekt** | `New-NetNat`: interne Adressen auf die Host-Adresse übersetzen (z. B. Lab hinter internem Switch) |
| **Hyper-V Network Virtualization** | virtuelle Netze unabhängig vom physischen Netz (SDN) |

<a id="nested"></a>
### 2.9 Nested Virtualization (verschachtelte Virtualisierung)

**Definition:** Hyper-V **innerhalb einer VM** betreiben. Die VM wird selbst zum Hyper-V-Host und kann eigene VMs ausführen («virtualisierte Umgebung in einer virtualisierten Umgebung»).

**Schichten (Folie 26):** Level 0 = physischer Hypervisor, Level 1 = VM mit eigenem Hyper-V, Level 2 = Gast-VM darin. Der Level-0-Hypervisor gibt die **Virtualisierungs-Erweiterungen der CPU** an die Level-1-VM weiter.

**Einsatz:** Test- und Schulungslabs, Azure-Local-Evaluation, **Hyper-V-isolierte Container in einer VM**, WSL2 in einer VM, Emulatoren. 🔎 Nested auf Hyper-V ist auch produktiv unterstützt, aber **nicht** für Failover-Cluster und leistungskritische Anwendungen. Azure Local nested nur zur Evaluation.

**Voraussetzungen** (📚 und 🔎)

| CPU | Host-Betriebssystem | VM-Konfigurationsversion |
|---|---|---|
| **Intel** mit VT-x und EPT | Windows Server 2016+ / Windows 10+ | **≥ 8.0** |
| **AMD** EPYC/Ryzen 🔎 | Windows Server 2022+ / Windows 11+ | **≥ 9.3** |

Dazu genügend (statischer) RAM auf dem physischen Host. ⚠️ Das MS-Learn-Nachbereitungsmodul nennt nur Intel. Die aktuelle Windows-Server-Doku unterstützt auch AMD.

**Aktivieren** (VM muss **ausgeschaltet** sein, Befehl auf dem physischen Host):

```powershell
Set-VMProcessor -VMName <VMName> -ExposeVirtualizationExtensions $true
# danach VM starten und darin Hyper-V installieren
```

**Netzwerk für nested VMs**
1. **MAC Address Spoofing** auf dem Adapter der Level-1-VM (damit Pakete durch zwei vSwitches geroutet werden):
   ```powershell
   Get-VMNetworkAdapter -VMName <VMName> | Set-VMNetworkAdapter -MacAddressSpoofing On
   ```
   ⚠️ Im MS-Learn-Modul steht fälschlich `Set-VMNetworkAdapter … | Set-VMNetworkAdapter`. Richtig ist `Get-…` am Anfang der Pipeline.
2. **NAT** (z. B. in der Public Cloud, wo Spoofing nicht erlaubt ist): In der Level-1-VM einen internen Switch mit `New-NetNat` einrichten und den nested VMs IP, Gateway und DNS statisch zuweisen. Mehr Aufwand als Spoofing.

**Einschränkungen:** Während Hyper-V in der VM läuft, funktioniert **kein Runtime Memory Resize bzw. Dynamic Memory** (RAM-Änderung nur im ausgeschalteten Zustand). VBS/Device Guard können die Virtualisierungs-Erweiterungen nicht weiterreichen (laut MS Learn vorher deaktivieren). Virtualisierungssoftware von Drittherstellern in Hyper-V-VMs ist nicht unterstützt.

### 2.10 Aktualitäten aus Unit 01: Azure Local, VMware, «Is Hyper-V dead?», WAC

- **Azure Local** (früher *Azure Stack HCI*, Folien 27–28): «Cloud-Infrastruktur für verteilte Standorte, ermöglicht durch Azure Arc». Aufbau:
  - **Unten:** zertifizierte Hardware (*Premier Solutions, Validated Nodes, Integrated Systems*)
  - **Betriebssystem:** Azure Stack HCI OS mit **Hyper-V** und **Storage Spaces Direct**
  - **Workloads:** Windows- und Linux-VMs als **Arc-enabled Servers**, **Azure Virtual Desktop**, Kubernetes-Apps mit **AKS enabled by Azure Arc**, Arc-enabled Services
  - **Oben (Azure):** Entra ID, Azure Policy, Site Recovery, Backup, Monitor, File Sync, Key Vault, Update Manager, Defender for Cloud. Verwaltet über Azure-Portal, ARM/Bicep-Templates und Azure CLI.
- **VMware-Lizenzthematik** (Folie 29): Seit der Übernahme durch **Broadcom** gelten neue Lizenzmodelle. Laut Artikel vom 28.03.2025 **mindestens 72 Cores** statt bisher 16. Das Aus für vSphere Standard ist absehbar (nach dem Ende von Essentials Plus), und Broadcom bündelt alles in der VMware Cloud Foundation (VCF). Dazu kommen Preiserhöhungen und Nachzahlungen. Folge: Viele Firmen prüfen die **Migration zu Hyper-V bzw. Azure Local**.
- **«Is Hyper-V dead?» – Nein** (Folie 30). Hyper-V ist die Basis für **Azure**, die **Azure-Stack-Familie**, **Windows Server/Windows**, **Container mit Hyper-V-Isolation**, **Plattformsicherheit** (VBS, Credential Guard) und **Xbox**.
- **Windows Admin Center – Virtualization Mode** (Folie 31): Der Client (Webbrowser) verbindet sich mit einem **WAC-Virtualization-Mode-Host**, der aus einem **Gateway** und einer **Datenbank** besteht. Dieser verwaltet über **Agents** mehrere Hyper-V-Hosts, einzeln oder im **Failover-Cluster**. Gedacht ist das für grössere Hyper-V-Umgebungen (als Alternative zu vCenter/SCVMM).

### 2.11 Arbeitsaufträge Unit 01

- **aa01a – Multiple-Choice-Fragen** (für alle ohne Möglichkeit, Hyper-V zu installieren): Lösungen in [Kapitel 11](#aa01a).
- **aa01b – Virtuelle Maschine erstellen** (60 Min.): Ziel ist eine VM mit Internetzugang.
  1. Hyper-V aktivieren (Windows-Features) und neu starten.
  2. Hyper-V-Manager → *Aktion* → *Neu* → *Virtueller Computer*: Name, Generation, RAM, Netzwerk, Disk und **ISO als Installationsmedium**.
  3. *Manager für virtuelle Switches* → **Extern** → physischen Netzwerkadapter wählen. Die VM verwendet **DHCP**.
  4. VM starten und das Betriebssystem installieren (Updates brauchen Internet).
  5. Internetzugang testen (Browser, `ping`, `Test-NetConnection`).

✍️ Dasselbe per PowerShell:

```powershell
New-VMSwitch -Name "Extern" -NetAdapterName "Ethernet" -AllowManagementOS $true
New-VM -Name "Win11-Test" -Generation 2 -MemoryStartupBytes 4GB `
       -NewVHDPath "C:\VMs\Win11-Test.vhdx" -NewVHDSizeBytes 64GB -SwitchName "Extern"
Add-VMDvdDrive -VMName "Win11-Test" -Path "C:\ISO\Win11.iso"
Set-VMFirmware -VMName "Win11-Test" -FirstBootDevice (Get-VMDvdDrive -VMName "Win11-Test")
Set-VMKeyProtector -VMName "Win11-Test" -NewLocalKeyProtector   # Voraussetzung für vTPM
Enable-VMTPM -VMName "Win11-Test"                                # Windows 11 braucht TPM 2.0
Set-VMProcessor -VMName "Win11-Test" -Count 2
Start-VM -Name "Win11-Test"; vmconnect localhost "Win11-Test"
```

### 2.12 🛠️ Störungsbehebung Hyper-V

| Fehlerbild | Mögliche Ursache | Lösung / Prüfung |
|---|---|---|
| Hyper-V lässt sich nicht aktivieren, die Option ist ausgegraut | Virtualisierung (VT-x/AMD-V) im UEFI deaktiviert, Windows **Home**, CPU ohne SLAT | UEFI-Einstellung aktivieren, `systeminfo` (Hyper-V-Anforderungen) prüfen, Edition prüfen |
| VM startet nicht: «Hypervisor is not running» | Hypervisor-Start deaktiviert | `bcdedit /set hypervisorlaunchtype auto` und Neustart |
| Gen-2-VM bootet nicht vom ISO/Netz | Boot-Reihenfolge, kein DVD-Laufwerk (Gen 2 hat standardmässig keins), **Secure Boot** blockiert Linux | DVD-Laufwerk hinzufügen, Boot-Reihenfolge anpassen, für Linux Secure-Boot-Vorlage *Microsoft UEFI Certificate Authority* wählen |
| Windows 11 lässt sich in der VM nicht installieren | kein TPM 2.0 / Secure Boot | Gen 2, vTPM aktivieren (Key Protector), Secure Boot an |
| VM hat kein Netzwerk/Internet | falscher Switch-Typ (privat/intern), falsche physische NIC gebunden, VLAN-ID falsch, kein DHCP | Switch-Typ **Extern** prüfen, `Get-VMSwitch`, `Get-VMNetworkAdapter`, im Gast `ipconfig /all` (APIPA 169.254.x.x = kein DHCP) |
| Gen-1-VM: PXE-Boot geht nicht | synthetischer Adapter kann in Gen 1 kein PXE | Legacy-Netzwerkadapter hinzufügen oder Gen 2 verwenden |
| VM startet nach Umzug auf anderen Host nicht | Konfigurationsversion zu neu für den Zielhost | Zielhost aktualisieren (kein Downgrade möglich) |
| Host-Disk läuft voll | wachsende dynamische Disks, vergessene Checkpoints, Smart-Paging-Dateien | Checkpoints in Hyper-V löschen (nicht die `.avhdx`), Speicherplatz überwachen |
| Nested Virtualization funktioniert nicht | VM lief beim Aktivieren, Konfigurationsversion zu alt, CPU/Host nicht unterstützt | VM ausschalten, `Set-VMProcessor … -ExposeVirtualizationExtensions $true`, Version prüfen, MAC-Spoofing für das Netz |
| Keine Zeitsynchronisation, Herunterfahren vom Host geht nicht | Integration Services deaktiviert oder veraltet | `Get-VMIntegrationService -VMName srv01`, Dienste aktivieren |

---

<a id="container"></a>
## 3. Unit 02 – Container auf Windows (Docker, Kubernetes)

### Lernziele

Die Technikerinnen und Techniker HF können …
- Container beschreiben und ihr Funktionsprinzip erläutern,
- den Unterschied zwischen Containern und VMs erklären,
- den Unterschied zwischen **Prozessisolierung** und **Hyper-V-Isolierung** beschreiben,
- Docker beschreiben und erläutern, wie es Windows-Container verwaltet,
- Kubernetes beschreiben und seine Bestandteile nennen.

### 3.1 Was sind Container?

📚 Ein **Container** verpackt eine Anwendung **mit allen Abhängigkeiten** (Bibliotheken, Runtime, Konfiguration) und abstrahiert sie vom Host-Betriebssystem. Container sind vom Host und voneinander isoliert und bieten eine leichtgewichtige Laufzeit- und Entwicklungsumgebung.

**Vorteile** (Recherchefrage «Nenne drei Vorteile»)
1. **Läuft überall** (Portabilität): Laptop, Server im RZ, Cloud, Linux/Windows/macOS
2. **Isolation**: Für die App sieht der Container wie ein eigenes Betriebssystem aus
3. **Effizienz**: startet in Sekunden, braucht wenig Ressourcen, **höhere Dichte** pro Server
4. **Konsistente Entwicklungsumgebung**: läuft beim Entwickler gleich wie in Produktion («works on my machine» entfällt)
5. 🔎 **Schnelle Skalierung und Updates** (neues Image bauen und neu ausrollen)

**Wie funktionieren Container?** (📚)
- Die CPU hat einen **Kernel-Modus** (Kern-OS, Treiber) und einen **User-Modus** (Anwendungen).
- Ein Container **teilt sich den Kernel des Host-Betriebssystems** und bekommt eine **eigene, isolierte Kopie des User-Modus** (Systemdateien, Registry-Sicht, Prozesse).
- Die User-Modus-Dateien stammen aus einem **Container-Base-Image**.
- Images bestehen aus **Schichten (Layers)**, z. B. *Base-OS-Layer → IIS-Layer → ASP.NET-Layer → eigene Website*. Jede Build-Anweisung erzeugt einen neuen Layer. Die Base-Layer werden getrennt gepflegt und nur heruntergeladen, gearbeitet wird in den oberen Layern.

**Architektur (Folien 15–16):**
- **Container:** Hardware → **ein** Betriebssystem mit **einem Kernel** → darauf Apps/Services des Hosts **und** mehrere Container (je eigene Apps/Services, aber gemeinsamer Kernel).
- **VM:** Hardware → Host-OS mit Kernel **und** daneben jede VM mit **eigenem vollständigem OS inklusive eigenem Kernel**.

### 3.2 Microservices vs. monolithische Applikationen

| | **Monolith** | **Microservices** |
|---|---|---|
| Aufbau | eine grosse Anwendung, alle Funktionen in einem Deployment | viele kleine, **lose gekoppelte**, unabhängig deploybare Dienste (z. B. Auth, Warenkorb, Zahlung) |
| Skalierung | nur als Ganzes | jeder Dienst einzeln |
| Deployment | jede Änderung bedeutet ein Deployment der ganzen App | Dienste einzeln aktualisierbar |
| Nachteile | schwerfällig, ein Fehler kann alles treffen | komplexer (Netzwerk, Monitoring, Datenkonsistenz) |

**Diskussion: «Wenn ich Container verwende, habe ich automatisch eine Microservice-Applikation?» – Nein.** 📚 Jeder Microservice kann in einem Container laufen, aber **Container erzwingen keine Microservice-Architektur**. Auch ein Monolith lässt sich containerisieren. Container sind aber nicht dafür gedacht: Docker und Orchestratoren gehen davon aus, dass ein Container **jederzeit gelöscht und ersetzt** werden kann. Deshalb gilt: **Keine Daten und keinen Zustand im Container speichern**, sondern externen persistenten Speicher verwenden.

### 3.3 Container vs. virtuelle Maschinen

📚 (Tabelle aus der MS-Doku, die in der Unit gemeinsam studiert wurde)

| Merkmal | Virtuelle Maschine | Container |
|---|---|---|
| **Isolation** | vollständig, starke Sicherheitsgrenze (z. B. Apps konkurrierender Firmen) | leichtgewichtig, schwächere Grenze (verstärkbar mit Hyper-V-Isolation) |
| **Betriebssystem** | komplettes OS **mit Kernel**, braucht mehr CPU/RAM/Storage | nur der **User-Modus** des OS, weniger Ressourcen |
| **Gast-Kompatibilität** | fast jedes OS | **gleiche OS-Version wie der Host** (ältere nur mit Hyper-V-Isolation) |
| **Deployment** | Hyper-V-Manager/WAC (einzeln), PowerShell/SCVMM (viele) | Docker CLI (einzeln), **Orchestrator** wie AKS (viele) |
| **Updates** | in jeder VM einzeln patchen | Dockerfile auf neues Base-Image zeigen lassen → Image neu bauen → in Registry pushen → neu deployen |
| **Persistenter Speicher** | VHD (lokal), SMB-Share (geteilt) | Azure Disks (ein Node), Azure Files/SMB (mehrere Nodes) |
| **Load Balancing** | laufende VMs werden im Cluster verschoben | Container werden nicht verschoben, der Orchestrator startet und stoppt Instanzen |
| **Fehlertoleranz** | Failover: VM startet auf anderem Knoten neu | Orchestrator erstellt Container auf anderem Knoten sofort neu |
| **Netzwerk** | virtuelle Netzwerkadapter | isolierte Sicht auf einen virtuellen Adapter, **Host-Firewall wird geteilt** |

**Merksatz:** VM = Hardware virtualisieren, Container = Betriebssystem virtualisieren.

### 3.4 Isolationsmodi unter Windows

| | **Prozessisolierung** («Windows Server Container») | **Hyper-V-Isolierung** («Hyper-V Container») |
|---|---|---|
| Kernel | **teilt sich den Kernel** mit Host und anderen Containern | jeder Container läuft in einer **hochoptimierten Utility-VM mit eigenem Kernel** |
| Sicherheit | geringere Isolation, ein Ausbruch aus der Sandbox ist theoretisch möglich | Hardware-Isolation, deutlich sicherer |
| Versionen | **Host- und Image-Version müssen übereinstimmen** | ältere Images auf neuerem Host möglich (z. B. 2019-Image auf 2022-Host) |
| Start/Ressourcen | am schnellsten, am wenigsten Overhead | startet trotzdem in Sekunden, etwas mehr Overhead |
| **Standard auf** | **Windows Server** | **Windows 10/11** (Pro/Enterprise) |
| Voraussetzung | Feature *Containers* | zusätzlich **Hyper-V-Rolle**. Ist der Host selbst eine VM, braucht es **Nested Virtualization**. |

```powershell
docker run -it --isolation=process mcr.microsoft.com/windows/servercore:ltsc2022 cmd
docker run -it --isolation=hyperv  mcr.microsoft.com/windows/servercore:ltsc2022 cmd
```

**Wann Hyper-V-Isolierung?** Wenn eine App einen eigenen Kernel braucht, wenn der Host der App (oder Apps einander) nicht vertrauen (Multi-Tenant, Cloud-Provider), wenn Compliance mehr Isolation verlangt oder wenn Versionen gemischt werden müssen. 📚 Nicht jeder Orchestrator (z. B. Kubernetes) unterstützt Hyper-V-Container. Dann bleibt als Alternative eine vollständige VM.

### 3.5 Docker

**Was ist Docker?** Eine Firma bzw. eine Sammlung von Open-Source-Tools und Diensten, die ein **einheitliches Modell zum Verpacken (Containerisieren)** von Anwendungen bieten. Ein Docker-Container enthält alles, was die App braucht: Code, Runtime, Systemtools, Bibliotheken.

**Docker Engine (Folie 21):**
- **Docker Client** (CLI `docker`) → **REST API** → **Docker Server** (Daemon `dockerd`)
- Der Server verwaltet lokale **Images** (z. B. Ubuntu, Windows, Nginx) und daraus laufende **Container**.
- Images werden aus einer Registry geladen, z. B. **Docker Hub** (öffentliche Registry mit über 100 000 Images).

**Begriffe** (Recherchefragen)

| Begriff | Bedeutung |
|---|---|
| **Container Image** | unveränderliche Vorlage (Schichten) mit App und Abhängigkeiten. Aus einem Image entstehen beliebig viele Container. |
| **Container** | laufende (oder gestoppte) Instanz eines Images mit einer beschreibbaren Schicht (Scratch Space) |
| **Host Operating System** | das Betriebssystem der Maschine, auf der Docker läuft. Es stellt den **Kernel** bereit. |
| **Container Operating System** | das OS **im** Image (Base Image, User-Modus-Dateien), z. B. Nano Server oder Server Core |
| **Dockerfile** | Textdatei mit allen Anweisungen, um ein Image automatisiert zu bauen (Basis-Image, Befehle beim Build, Startbefehl). Wird mit `docker build` verarbeitet. |
| **Registry / Repository** | Ablage für Images: **Docker Hub**, **Microsoft Container Registry** (mcr.microsoft.com, offizielle Microsoft-Images), **Azure Container Registry** (eigene private Registry) |

🔎 **Beispiel-Dockerfile** (Windows, IIS):

```dockerfile
FROM mcr.microsoft.com/windows/servercore/iis:windowsservercore-ltsc2022
COPY ./website/ C:/inetpub/wwwroot/
EXPOSE 80
# Startbefehl erbt das IIS-Image (ServiceMonitor)
```

Wichtige Anweisungen: `FROM` (Basis), `RUN` (Befehl beim Build), `COPY`/`ADD` (Dateien), `WORKDIR`, `ENV`, `EXPOSE` (dokumentiert den Port), `CMD`/`ENTRYPOINT` (Startbefehl).

📚 **Windows-Base-Images (MCR)**

| Image | Inhalt | Einsatz |
|---|---|---|
| **Nano Server** | kleinstes Image, .NET (Core)-APIs, wenige Rollen | neue, dafür geschriebene Apps |
| **Server Core** | Teil der Windows-Server-APIs inkl. **.NET Framework**, die meisten Rollen | bestehende Apps containerisieren («lift and shift») |
| **Windows** | volle Windows-APIs, keine Serverrollen | ab Windows Server 2022 ersetzt durch **Server** |
| **Server** | volle Windows-Server-APIs | wenn Server Core nicht reicht (grösser, dafür kompatibler) |

📚 **Container-Runtimes auf Windows Server:** Unter der CLI liegt die **Container-Runtime** und darunter das Windows-Feature *Containers* mit dem **Host Compute Service (HCS)**.
- **Moby** (Open-Source-Basis von Docker, `dockerd`, gut zum Testen)
- **containerd** (Standard für Kubernetes, ohne eigene CLI, stattdessen `crictl`/`nerdctl`)
- **Mirantis Container Runtime** (ehemals Docker EE, für Docker Swarm)
- **Docker Desktop** nur für Entwicklung auf Windows 10/11

📚 **Sicherheit, Speicher und Netzwerk bei Windows-Containern**
- Container **teilen Firewall und Defender des Hosts**.
- Container werden **nicht gepatcht**, sondern mit dem aktuellen Base-Image **neu gebaut**. Microsoft aktualisiert die Images monatlich am Patch Tuesday.
- Standardkonto im Container ist **ContainerAdministrator**. Besser ist **ContainerUser**, wenn keine Adminrechte nötig sind.
- Image- und Runtime-Scanning mit **Microsoft Defender for Containers**.
- **Speicher:** standardmässig flüchtig (Scratch Space, geht beim Löschen verloren). Persistent über **Bind Mounts** (Host-Ordner), **Named Volumes**, SMB oder bei Kubernetes über Persistent Volumes.
- **Netzwerk-Treiber:** `nat` (Standard, für Entwickler), `transparent` (direkt am physischen Netz), `overlay` (mehrere Hosts, Swarm/Kubernetes, VXLAN), `l2bridge` (Kubernetes/SDN), `l2tunnel` (nur Azure).

### 3.6 Kubernetes

**Was ist Kubernetes?** (📚) Eine Open-Source-Plattform zur **Orchestrierung** von Containern über viele Server: Sie plant, startet, skaliert und überwacht Container **deklarativ** (YAML-Manifeste beschreiben den Soll-Zustand). Abkürzung **K8s** (8 Buchstaben zwischen K und s).

**Was ist AKS?** **Azure Kubernetes Service**: Kubernetes als verwalteter Dienst in Azure. Microsoft betreibt die Control Plane, der Kunde verwaltet nur die Worker Nodes und Workloads. Integriert mit Azure Container Registry und Entra ID.

**Aufgaben eines Orchestrators / Features von Kubernetes** (mindestens drei nennen):

| Feature | Beschreibung |
|---|---|
| Scheduling | entscheidet, auf welchem Node ein Container läuft |
| Self-Healing / Health Monitoring | ersetzt abgestürzte Container automatisch |
| Failover | verschiebt Container von ausgefallenen Nodes |
| Skalierung | mehr/weniger Instanzen, manuell oder automatisch |
| Service Discovery und Load Balancing | Container finden sich per Name, Last wird verteilt |
| Rolling Updates und Rollback | Updates ohne Downtime, bei Fehlern zurück |
| Affinität/Anti-Affinität | Container nah beieinander oder bewusst verteilt |
| Storage-Orchestrierung | Volumes (persistent/ephemeral), z. B. azureDisk, azureFile |

**Architektur (Folie 35):**

| Teil | Komponente | Aufgabe |
|---|---|---|
| **Control Plane** (Master) | **kube-apiserver** | zentrale API, über die alles läuft (auch `kubectl`) |
| | **etcd** | konsistenter Key-Value-Store mit dem gesamten Cluster-Zustand |
| | **kube-scheduler** | weist neue Pods einem passenden Node zu |
| | **kube-controller-manager** | Controller, die den Ist- auf den Soll-Zustand bringen (z. B. ReplicaSet) |
| | **cloud-controller-manager** | Anbindung an die API des Cloud-Providers (Load Balancer, Disks) |
| **Worker Node** | **kubelet** | Agent auf jedem Node, sorgt dafür, dass die Pods laufen |
| | **kube-proxy** | Netzwerkregeln für Services |
| | **Container Runtime (CRI)** | führt die Container aus (z. B. containerd) |
| | **Pods** | kleinste Einheit: ein oder mehrere Container mit gemeinsamer IP und gemeinsamem Speicher |

Weitere Begriffe: **Service** (logische Gruppe von Pods mit stabiler virtueller IP), **Deployment/ReplicaSet** (gewünschte Anzahl Pods), **kubectl** (CLI), **kubeadm** (Cluster aufsetzen), **CNI-Plugin** (Pod-Netzwerk).
📚 **Wichtig für Windows:** Die Control Plane läuft **nur auf Linux**, **Worker Nodes** können Linux oder **Windows Server** sein.
📚 **Andere Orchestratoren:** Docker Swarm (einfacher, weniger erweiterbar), Apache Mesos.

### 3.7 Arbeitsaufträge Unit 02

**Docker (Windows-Client):**

```powershell
# 1. Docker Desktop installieren, 2. Git installieren
git clone https://github.com/docker/welcome-to-docker
cd welcome-to-docker
# 4. Dockerfile prüfen: FROM (Basis-Image), COPY, RUN, EXPOSE (Port), CMD
docker build -t welcome-to-docker .
docker run -d -p 8088:<EXPOSE-Port> --name welcome welcome-to-docker
docker ps                                   # läuft der Container?
# 7. Frontend im Browser: http://localhost:8088
```

Den Containerport für `-p Hostport:Containerport` liest man aus der `EXPOSE`-Zeile des Dockerfiles ab.

**Hyper-V-Container (Windows Server oder Client):**

```powershell
Install-WindowsFeature -Name Hyper-V, Containers -IncludeManagementTools -Restart   # Server
Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -OutFile install-docker-ce.ps1
.\install-docker-ce.ps1
docker pull mcr.microsoft.com/dotnet/samples:aspnetapp
docker run -it --rm -p 8000:8080 --isolation=hyperv mcr.microsoft.com/dotnet/samples:aspnetapp
```

🔎 Das .NET-Beispiel-Image hört ab .NET 8 auf Port **8080** im Container (ältere Versionen auf 80).

### 3.8 🛠️ Störungsbehebung Container

| Fehlerbild | Ursache | Lösung |
|---|---|---|
| `no matching manifest for windows/amd64` bzw. `image operating system "linux" cannot be used on this platform` | Linux-Image auf Windows-Engine oder umgekehrt | Docker Desktop: *Switch to Linux/Windows containers*. Richtiges Image wählen. |
| «The container operating system does not match the host operating system» | Prozessisolierung mit anderer OS-Version als der Host | passenden Tag verwenden (z. B. `ltsc2022` auf Server 2022) oder `--isolation=hyperv` |
| Hyper-V-Isolierung schlägt in einer VM fehl | Nested Virtualization nicht aktiviert | auf dem physischen Host `Set-VMProcessor -ExposeVirtualizationExtensions $true` |
| Container beendet sich sofort | kein Vordergrundprozess, Fehler im Startbefehl | `docker ps -a`, `docker logs <id>`, CMD/ENTRYPOINT prüfen |
| Webseite nicht erreichbar | Port nicht veröffentlicht (`-p` fehlt), falscher Containerport, Firewall, Port belegt | `docker port <id>`, `netstat -ano`, `Test-NetConnection localhost -Port 8088` |
| Daten nach `docker rm` weg | kein Volume, Daten lagen im Scratch Space | Volume oder Bind Mount verwenden (`-v`) |
| Disk voll | alte Images, Container und Layer | `docker system df`, `docker system prune` |
| `docker: command not found` / Daemon nicht erreichbar | Dienst gestoppt, Docker Desktop nicht gestartet | Dienst `docker` starten, `docker version` (zeigt Client **und** Server) |

---

<a id="intune"></a>
## 4. Unit 03 – Microsoft Intune

### Lernziele

Die Technikerinnen und Techniker HF können …
- die Funktionsweise von Microsoft Intune verstehen und Anwendungsszenarien identifizieren,
- **Windows Autopilot** konfigurieren und anwenden,
- Windows-10/11-Geräte mit Intune konfigurieren, um eine effiziente Verwaltung sicherzustellen.

### 4.1 Überblick

📚 **Microsoft Intune** ist eine **Cloud-Lösung** für **Mobile Device Management (MDM)**, **Mobile Application Management (MAM)** und die Verwaltung von PCs. Sie verwaltet Android, iOS/iPadOS, macOS, Windows 10/11 und 🔎 Linux (Ubuntu, RHEL). Eng integriert mit **Microsoft Entra ID** (Identität, Conditional Access), **Microsoft Purview** (Information Protection) und **Microsoft Defender** (Endpoint-Schutz).

**Folie 6 (Microsoft Endpoint Manager):** Eine gemeinsame Konsole (*Unified admin console*, «Cloud-driven intelligence») für **Configuration Manager** (on-prem, u. a. Desktop Analytics) und **Microsoft Intune** (Cloud, u. a. App Protection Policies). Beide teilen sich **Autopilot**, **Endpoint Security** und **Endpoint Analytics**.
🔎 Die Dachmarke «Microsoft Endpoint Manager» wird nicht mehr verwendet. Heute heisst alles **Microsoft Intune** (Admin Center: intune.microsoft.com). *Microsoft Endpoint Configuration Manager* heisst jetzt **Microsoft Configuration Manager**. Desktop Analytics wurde eingestellt, der Nachfolger ist Endpoint Analytics.

### 4.2 Begriffe (Recherchefragen mit Antworten)

| Begriff | Erklärung |
|---|---|
| **MDM** – Mobile Device Management | Zentrale Verwaltung ganzer **Geräte**: Sicherheitsrichtlinien durchsetzen, Apps installieren, Updates steuern, Geräte sperren/löschen. Das Gerät wird in Intune **registriert (enrolled)**. |
| **MAM** – Mobile Application Management | Verwaltung und Schutz **einzelner Apps und der Firmendaten darin**, **unabhängig vom Gerät**, auch auf privaten, nicht registrierten Geräten (BYOD, «MAM without enrollment»). Beispiel: Kopieren von Outlook in private Apps sperren, PIN für Teams verlangen. |
| **Unterstützte Geräte** | Android (Android Enterprise, AOSP), iOS/iPadOS, macOS, Windows 10/11 (inkl. Windows 365/AVD), Linux (Ubuntu Desktop, RHEL) 🔎. Detaillierte Liste unter *supported-devices-browsers*. |
| **Microsoft (Endpoint) Configuration Manager** (MECM/ConfigMgr, ehemals SCCM) | **On-Premises**-Verwaltung von PCs und Servern: Softwareverteilung, Updates, Konfiguration, Betriebssystemverteilung (Task Sequences), Inventar. Zusammen mit Intune lassen sich PCs, Macs und Mobilgeräte in einer Konsole verwalten. |
| **Cloud Attach** | ConfigMgr-Umgebung an die Cloud anbinden, ohne grosse Umstellung. Laut Folie gilt eine Umgebung als «cloud-attached», sobald mindestens **eines der drei Features** genutzt wird: **Tenant Attach**, **Co-Management**, **Endpoint Analytics**. 📚 Das MS-Learn-Modul beschreibt zwei Schritte: 1. *Tenant Attach* (ConfigMgr beim Intune-Tenant registrieren, Geräte in Intune sichtbar und steuerbar, kein Co-Management nötig), 2. *Co-Management*. |
| **Co-Management** | Windows-10/11-Geräte **gleichzeitig** mit ConfigMgr **und** Intune verwalten. Pro **Workload** (z. B. Compliance, Windows Update, Endpoint Protection, Apps, Gerätekonfiguration) entscheidet man, wer die **Verwaltungsautorität** hat, und schiebt Workloads schrittweise in die Cloud. Voraussetzung: Hybrid-Entra-Join (bestehende Clients) oder Entra-Join + ConfigMgr-Client (neue Geräte). Gewinn sofort: Conditional Access mit Compliance, Remote-Aktionen (Neustart, Wipe), Autopilot. |
| **Endpoint Analytics** | Analysiert die **Benutzererfahrung** auf den Geräten: **Startleistung** (Boot/Anmeldung), **Anwendungszuverlässigkeit** (Abstürze), **Work from anywhere** (Cloud-Bereitschaft), Ressourcenleistung, **Remediations** (Skripte, die Probleme erkennen und proaktiv beheben). Ergebnis: **Endpoint Analytics Score** (0–100) mit Empfehlungen. |
| **Windows Autopilot** | Technologien, um neue Geräte **ohne Imaging direkt ab Werk** produktiv bereitzustellen. Der Benutzer verbindet sich nur mit dem Netz und meldet sich an, der Rest läuft automatisch (Entra-Join, Intune-Enrollment, Apps, Richtlinien, angepasstes OOBE). Auch zum **Zurücksetzen, Umwidmen und Wiederherstellen** (Autopilot Reset). Unterstützt Windows-PCs und HoloLens 2. |

🔎 **Autopilot-Szenarien:** *User-driven* (Benutzer richtet ein), *Self-deploying* (Kiosk, ohne Benutzer), *Pre-provisioning* (IT/Händler bereitet vor, früher «White Glove»), *Existing devices* (bestehende Geräte). Voraussetzung ist der registrierte **Hardware-Hash** des Geräts (vom Händler/OEM oder per `Get-WindowsAutopilotInfo`) und ein zugewiesenes **Deployment-Profil**. Neuere Variante: **Autopilot device preparation** (ohne vorherige Registrierung des Hashes).

**Intune vs. Configuration Manager** (Repetitionsfrage Unit 04)

| | **Intune** | **Configuration Manager** |
|---|---|---|
| Betrieb | Cloud (SaaS), keine eigene Infrastruktur | On-Premises-Server (Site-Server, SQL, Distribution Points) |
| Geräte | Mobile, Windows, macOS, Linux, auch ausserhalb des Firmennetzes | vor allem Windows-PCs und -Server im Firmennetz |
| Stärken | MDM/MAM, Compliance mit Conditional Access, Autopilot, moderne Verwaltung | komplexe Softwareverteilung, OS-Deployment, Serververwaltung, Offline-Netze |
| Kombination | Co-Management / Tenant Attach | |

### 4.3 Geräte-Lebenszyklus und Registrierung

📚 **Lebenszyklus:** **Enroll** (registrieren) → **Configure** (konfigurieren) → **Protect** (schützen: Compliance, Endpoint Security) → **Retire** (ausmustern: Retire/Wipe).

📚 **Registrierungsmethoden**

| Plattform | Methoden |
|---|---|
| **Windows** | **BYOD** (Company Portal oder *Arbeits- oder Schulkonto hinzufügen*), **automatische Registrierung** (bei Entra-Join), **Autopilot**, **Bulk Enrollment** (Provisioning-Paket mit Windows Configuration Designer), Co-Management, Gruppenrichtlinie (Hybrid-Join), **DEM** |
| **iOS/iPadOS, macOS** | BYOD mit Company Portal (**Apple MDM Push Certificate** nötig), **Automated Device Enrollment (ADE)** über Apple Business Manager, Apple Configurator, DEM |
| **Android** | Android Enterprise **Work Profile** (privates Gerät, Trennung privat/geschäftlich), **Fully Managed** (Firmengerät), Dedicated (Kiosk), Corporate-Owned Work Profile |

- **DEM (Device Enrollment Manager):** spezielles Konto, das bis zu **1000 Geräte** registrieren darf (max. 150 DEM-Konten). Für benutzerlose Geräte wie Kassen oder Kiosk.
- **Registrierungsoptionen:** Nutzungsbedingungen, **Registrierungsbeschränkungen** (Plattform, Anzahl pro Benutzer, private Geräte blockieren), Unternehmens-IDs (IMEI/Seriennummer), MFA bei der Registrierung, Gerätekategorien.

### 4.4 Praxis: Arbeitsaufträge Unit 03 (Schritte)

1. **Intune-Testversion** erstellen (*free-trial-sign-up*, 30 Tage).
2. **Benutzer erstellen und Lizenz zuweisen**: Microsoft 365 Admin Center oder Entra → Benutzer → Lizenzen → Intune (bzw. EMS/M365 E3/E5/Business Premium).
3. **Automatische Registrierung prüfen**: Entra Admin Center (oder Intune) → *Mobility (MDM and WIP)* → *Microsoft Intune* → **MDM-Benutzerbereich = Alle** (oder eine Gruppe). Dann registriert sich ein Windows-Gerät beim Entra-Join automatisch in Intune.
4. **Gruppe erstellen** und Benutzer hinzufügen: Typ *Sicherheit*, Mitgliedschaft **zugewiesen** (statisch) oder **dynamisch** (Regel, z. B. `(user.department -eq "IT")`). Dynamische Gruppen brauchen Entra ID P1.
5. **App hinzufügen und zuweisen**: Intune → Apps → Windows → Hinzufügen (Microsoft-365-Apps, Microsoft-Store-App, **Win32-App** als `.intunewin`, MSI). Zuweisung als **Required** (erforderlich), **Available** (im Company Portal) oder **Uninstall**.
6. **Gerätekonfiguration (Settings Management)**, z. B. Windows Update, Anmeldebeschränkungen:
   - **Welche Profiltypen gibt es?** **Settings Catalog** (alle Einstellungen an einem Ort, ähnlich GPO) oder **Templates**: *Administrative Templates*, *Custom* (OMA-URI), *Device restrictions*, *Endpoint protection* (veraltet), *Wi-Fi*, *VPN*, *E-Mail*, *Zertifikate* (Trusted/SCEP/PKCS), *Domain Join* (Hybrid-Autopilot), *Kiosk*, *Delivery Optimization*, *Edition Upgrade*, *Windows Health Monitoring*, *Imported Administrative Templates (ADMX)*, *Wired Networks* u. a. Dazu kommen Update-Ringe/Feature-Updates, PowerShell-Skripte und Endpoint-Security-Richtlinien.
   - **Wie füge ich ADMX-Dateien hinzu?** Intune → Geräte → Konfiguration → Reiter **Import ADMX** → Import: ADMX- und zugehörige ADML-Datei hochladen. Danach Profil **Templates → Imported Administrative templates** erstellen und zuweisen. Grenzen: max. **20 ADMX-Dateien**, je **≤ 1 MB**, **eine ADML pro ADMX**, **nur en-us**. **Abhängigkeiten zuerst** importieren (z. B. `mozilla.admx` vor `firefox.admx`, oft `Windows.admx`). Keine Combo-Box-Einstellungen. Rolle: *Policy and Profile Manager*. Tipp: Viele Einstellungen (z. B. Chrome) sind bereits im Settings Catalog.
7. **Device Compliance Policy** (Konformitätsrichtlinie), siehe 4.5.
8. **MAM-Richtlinie** (*App Protection Policy*): Intune → Apps → App-Schutzrichtlinien → iOS/Android/Windows.
   - *Datenschutz*: Speichern unter, Kopieren/Einfügen nur in verwaltete Apps, Backup verhindern
   - *Zugriffsanforderungen*: PIN, Biometrie, Firmenanmeldedaten
   - *Bedingter Start*: z. B. min. OS-Version, kein Jailbreak/Root, sonst blockieren oder Firmendaten löschen

### 4.5 Compliance und Conditional Access

📚 **Compliance-Richtlinien** sind Regeln, die ein Gerät erfüllen muss, um als **konform** zu gelten. Beispiele für Windows: BitLocker aktiv, Secure Boot, min./max. OS-Version, Firewall/Antivirus aktiv, Passwortanforderungen, **Defender-for-Endpoint-Risikostufe** ≤ X.
- **Aktionen bei Nichtkonformität:** als nicht konform markieren (immer, mit **Kulanzzeit**), E-Mail an den Benutzer, Remote-Sperre, zur Ausmusterung (Retire) markieren.
- **Tenant-weite Einstellungen:** *Geräte ohne zugewiesene Compliance-Richtlinie markieren als* **konform** (Standard!) oder **nicht konform** (empfohlen mit Conditional Access). *Gültigkeitsdauer des Compliance-Status*: Standard **30 Tage** (1–120).
- **Mit welchem Entra-Tool kombiniert man Compliance Policies?** Mit **Microsoft Entra Conditional Access** (bedingter Zugriff). Das Gerät meldet seinen Compliance-Status an Entra ID. Eine CA-Richtlinie mit der Gewährung **«Gerät muss als konform markiert sein»** (*Require device to be marked as compliant*) blockiert nicht konforme Geräte, z. B. beim Zugriff auf Exchange Online oder SharePoint. Conditional Access braucht **Entra ID P1**.

### 4.6 🛠️ Störungsbehebung Intune

| Fehlerbild | Ursache | Prüfung / Lösung |
|---|---|---|
| Gerät registriert sich nicht | keine Intune-Lizenz, **MDM-Benutzerbereich** nicht gesetzt, Registrierungsbeschränkung (Plattform/privat/Anzahl), Gerät schon anderweitig verwaltet | Lizenz und MDM-Scope prüfen, *Registrierungsbeschränkungen*, Fehlercode auf dem Gerät |
| Autopilot-Profil greift nicht (normales OOBE) | Hardware-Hash nicht importiert, Profil nicht der Gerätegruppe zugewiesen, kein Internet im OOBE | Autopilot-Geräte-Liste, Profilstatus «Assigned», Netzwerk |
| Richtlinie kommt nicht an | falsche Gruppe (Benutzer- vs. Gerätegruppe), Filter, Gerät hat noch nicht synchronisiert | Zuweisung prüfen, Sync auslösen: Einstellungen → Konten → Auf Arbeits- oder Schulkonto zugreifen → Info → **Synchronisieren** (oder Company Portal) |
| Status «Konflikt» | zwei Profile setzen dieselbe Einstellung unterschiedlich | Profile konsolidieren, *Per-setting status* ansehen |
| App-Installation schlägt fehl | Erkennungsregel falsch (Win32), Installationsbefehl, Abhängigkeiten | Logs `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs\IntuneManagementExtension.log` |
| Gerät «nicht konform» ohne Grund | Compliance-Status nicht innerhalb der Gültigkeitsdauer gemeldet, «keine Richtlinie = nicht konform» | Gerät synchronisieren, Compliance-Einstellungen des Tenants prüfen |
| Join-Status unklar | Entra-Join/Hybrid/registriert? | `dsregcmd /status` (AzureAdJoined, DomainJoined), `mdmdiagnosticstool.exe -out C:\temp` (MDM-Diagnosebericht) |

---

<a id="arc"></a>
## 5. Unit 04 – Azure Arc

### Lernziele

Die Technikerinnen und Techniker HF können …
- Azure Arc beschreiben und seine Funktionen erläutern,
- erklären, wie man lokale Windows-Server-Instanzen in Azure Arc integriert,
- hybride Maschinen vom Azure-Portal aus mit Azure verbinden,
- Azure Arc zur Verwaltung von Geräten verwenden,
- den Zugriff mit **rollenbasierter Zugriffssteuerung (RBAC)** einschränken.

### 5.1 Hybrid Cloud und Azure Arc

**Hybrid Cloud** (Folie 11): Kombination aus **lokalen Ressourcen/Private Cloud** und **Public Cloud**. Workloads lassen sich je nach Leistung, Sicherheit und Kosten verteilen: Sensible Daten und kritische Apps bleiben intern, dazu kommen Skalierbarkeit und globale Reichweite der Public Cloud. Man ist nicht an eine einzige Umgebung gebunden. 🔎 Abgrenzung: **Multi-Cloud** = mehrere Public-Cloud-Anbieter (z. B. Azure + AWS).

**Azure Arc** (📚) ist ein Set von Technologien, das **Azure-Management, -Sicherheit und -Dienste auf Ressourcen ausserhalb von Azure** bringt (on-prem, Edge, andere Clouds). Verwaltet werden können:
- **Windows- und Linux-Server** (physisch oder VM, z. B. auf Hyper-V, VMware, AWS, GCP)
- **Kubernetes-Cluster**
- **SQL Server**
- **Azure Data Services**, App Services, Machine Learning (auf Arc-enabled Kubernetes)
- VMware vSphere, System Center VMM, Azure Local

**Übersicht (Folie 6):** Unten stehen die Ressourcen on-prem (Azure Stack HCI, VMware) und in anderen Clouds (AWS, GCP). Über **Azure Arc** erscheinen sie im **Azure Resource Manager** als *Arc-enabled infrastructure resources* (Server, SQL, Kubernetes) oder *Arc-enabled services*. Oben liegen einheitlicher Betrieb, Verwaltung, Compliance, Sicherheit und Governance, gleich wie für native Azure-Ressourcen.

**Kernidee:** Jede Maschine bekommt eine **Azure-Ressourcen-ID** (Typ `Microsoft.HybridCompute/machines`) in einer **Ressourcengruppe**. Damit funktionieren Tags, RBAC, Policy, Resource Graph und Monitoring wie bei Azure-VMs.

### 5.2 Funktionen von Azure Arc für Server

| Funktion | Beschreibung |
|---|---|
| **Inventar und Organisation** | Server in Ressourcengruppen/Abos, **Tags**, Abfrage mit **Azure Resource Graph** (kostenlos) |
| **Governance** | **Azure Policy** mit **Machine Configuration** (früher *Guest Configuration*): Einstellungen **im Betriebssystem** prüfen (z. B. Passwortrichtlinie, installierte Software) |
| **Sicherheit** | **Microsoft Defender for Cloud / Defender for Servers** (inkl. Defender for Endpoint, Schwachstellen), **Microsoft Sentinel** |
| **Überwachung** | **Azure Monitor** (Azure Monitor Agent, Log Analytics, VM Insights, Abhängigkeiten) |
| **Updates** | **Azure Update Manager** (Bewertung, geplante Updates über Wartungskonfigurationen) |
| **VM-Erweiterungen** | Custom Script Extension, Monitoring-Agent, Defender, Key Vault, WAC u. a. |
| **Zugriff** | **Azure RBAC** auf Serverebene, **SSH über Arc**, **Windows Admin Center im Azure-Portal**, Run Command |
| **Log-Zugriff** | Log-Analytics-Daten im Ressourcenkontext (Rechte des Servers gelten auch für seine Logs) |
| **Lizenzen** | 🔎 Extended Security Updates (ESU) für Windows Server 2012/R2 und SQL 2012/2014 über Arc, Windows Server Pay-as-you-go |

Laut Folie 12: Arc bietet eine **konsistente Bestands-, Verwaltungs-, Governance- und Sicherheitslösung** für alle Server und ermöglicht **VM-Erweiterungen** für Überwachung, Schutz und Updates.

### 5.3 Azure Connected Machine Agent

Der Agent wird auf dem Server installiert. Er besteht aus drei Komponenten (Folie 8):

| Komponente | Aufgabe | Kommuniziert mit (HTTPS/443) |
|---|---|---|
| **Hybrid Instance Metadata Service (HIMDS)** | **Managed Identity** des Servers, Metadaten, **Heartbeat** | Entra ID, *Hybrid Compute Resource Provider* (ARM) |
| **Guest Configuration** (Machine Configuration) | In-Guest-Policy: prüft, ob die Maschine die zugewiesenen Richtlinien erfüllt | *Guest Configuration Resource Provider* |
| **Extension Manager** | installiert, aktualisiert und entfernt **VM-Erweiterungen** (Custom Script, Defender/ASC, MMA/AMA) | ARM, Log Analytics |

Beim Onboarding bekommt der Agent: **Abo und Ressourcengruppe**, **Azure-Region** (wo die Metadaten gespeichert werden), **Netzwerkoption** (direkt, Proxy, Private Link) und die **Anmeldeinformation** (Device Login interaktiv, Entra-Token oder **Service Principal**).
Der Admin verwaltet danach alles über Azure-Portal, Azure CLI/PowerShell/SDK oder die REST-API → **ARM**.

**Über welches Protokoll kommuniziert der Agent mit der Azure Management Plane?** → **HTTPS, TCP 443, nur ausgehend** (Folie 17). 🔎 Es braucht **keine eingehenden Ports**. TLS 1.2/1.3.

### 5.4 Netzwerk (Folie 7)

Vier Verbindungswege zum *Azure Arc Service Endpoint*:
1. **Direkt übers Internet** zum Public Endpoint
2. **Über einen Proxy** (Internet). 🔎 Ein Proxy macht es nicht sicherer, der Verkehr ist schon verschlüsselt.
3. **Service Tag** über Site-to-Site-VPN oder ExpressRoute (Public Endpoint)
4. **Private Link** (Private Endpoint im Azure-VNet) über S2S-VPN/ExpressRoute

🔎 In der Firewall zu erlaubende **Service Tags**: `AzureActiveDirectory`, `AzureTrafficManager`, `AzureResourceManager`, `AzureArcInfrastructure`, `Storage`, `AzureFrontDoor.Frontend` (seit April 2026), optional `WindowsAdminCenter`. Wichtige URLs: `login.microsoftonline.com`, `*.login.microsoft.com`, `management.azure.com` (nur beim Verbinden/Trennen), `*.his.arc.azure.com`, `*.guestconfiguration.azure.com`, `*.servicebus.windows.net`, `download.microsoft.com` (Installation). Mit **Azure Arc Gateway** lässt sich die Anzahl nötiger Endpunkte reduzieren.
🔎 Bandbreite: Heartbeat alle 5 Minuten (< 64 KB), Status-Checks für Extensions und Machine Configuration.

### 5.5 Unterstützte Betriebssysteme

🔎 (Folie verweist auf die Doku, Stand 09/2026)
- **Windows Server 2016, 2019, 2022, 2025** (Desktop und Server Core). 2012/2012 R2 nur noch bis November 2026 (typisch für ESU).
- **Windows 10/11** nur in «serverähnlichen» Szenarien (immer online und eingeschaltet, z. B. Digital Signage, Kassen). Für normale Arbeitsplätze **Intune/ConfigMgr** verwenden.
- **Linux:** Ubuntu 22.04/24.04/26.04, RHEL 8/9/10, SLES 15 SP7, Debian 13, Rocky, AlmaLinux, Oracle Linux, Amazon Linux 2023
- nur **64-Bit** (x86-64, teilweise ARM64)
- **Nicht auf Azure-VMs** installieren (das Skript bricht ab), nicht für kurzlebige Server/VDI. Bei **geklonten Maschinen/Golden Images** erst nach dem Klonen onboarden (sonst doppelte Identität).

### 5.6 Onboarding

**Onboarding-Methoden** (Folie 14, ergänzt 🔎)

| Methode | Umfang | Beschreibung |
|---|---|---|
| **Interaktives Skript** aus dem Portal | einzeln/wenige | Portal generiert ein PowerShell-/Bash-Skript, das man auf dem Server ausführt (Anmeldung per Device Code) |
| **PowerShell** (einzelner Server) | einzeln | `Connect-AzConnectedMachine` bzw. Skript |
| **PowerShell mit Service Principal** | viele | nicht interaktiv, das SPN hat die Rolle *Azure Connected Machine Onboarding* |
| **Configuration Manager** | viele | per PowerShell-Skript oder **Task Sequence** |
| **Group Policy (GPO)** | viele | geplanter Task installiert und verbindet den Agent (aus einem Netzwerkshare) |
| 🔎 **Windows Admin Center** | einzeln | Onboarding direkt aus WAC |
| 🔎 **Azure Arc Setup** (Windows Server 2022/2025) | einzeln | integrierter Assistent im Server |
| 🔎 **Ansible**, Arc-enabled **VMware vSphere/SCVMM**, **Multicloud Connector** (AWS) | viele | automatisierte Verteilung |

**Vorbereitungen** (Arbeitsauftrag «Server zu Azure Arc hinzufügen»):
1. Azure-Abo und **Ressourcengruppe** und **Region** festlegen
2. **Resource Provider registrieren**: `Microsoft.HybridCompute`, `Microsoft.GuestConfiguration`, `Microsoft.HybridConnectivity` (+ `Microsoft.AzureArcData` für SQL, `Microsoft.Compute` für Update Manager)
3. **Berechtigungen** in Azure prüfen (siehe 5.7) und **lokale Adminrechte** auf dem Server
4. **Netzwerk**: ausgehend TCP 443 zu den URLs/Service Tags, allenfalls Proxy konfigurieren
5. Unterstütztes OS, 64-Bit, **Zeit synchron** (Tokens), nicht in Azure
6. Tags/Namenskonvention planen, Onboarding-Methode wählen

```powershell
# Provider registrieren
Register-AzResourceProvider -ProviderNamespace Microsoft.HybridCompute
Register-AzResourceProvider -ProviderNamespace Microsoft.GuestConfiguration
Register-AzResourceProvider -ProviderNamespace Microsoft.HybridConnectivity

# Auf dem Server (Agent installiert): verbinden
azcmagent connect --resource-group "rg-arc" --tenant-id "<TenantID>" `
  --location "switzerlandnorth" --subscription-id "<SubID>"
azcmagent show        # Status: Connected?
azcmagent check       # Netzwerk-Konnektivität zu allen Endpunkten prüfen
```

### 5.7 Berechtigungen und RBAC

**Welche Berechtigungen braucht man?** (Arbeitsaufträge)

| Aufgabe | Rolle (Azure RBAC, auf der Ressourcengruppe) |
|---|---|
| Server **onboarden** | **Azure Connected Machine Onboarding** (oder Contributor) |
| Arc-Server **lesen, ändern, löschen** und verwalten | **Azure Connected Machine Resource Administrator** (oder Contributor) |
| Ressourcengruppe im Portal-Skript auswählen | zusätzlich **Reader** |
| Nur ansehen | Reader |
| 🔎 Per Windows Admin Center aus dem Portal anmelden | *Windows Admin Center Administrator Login* |

**Antwort auf «Gebt eurem Benutzer Berechtigung, Arc-Server zu verwalten – welche Rolle?»** → **Azure Connected Machine Resource Administrator** auf der Ressourcengruppe (Least Privilege statt Owner/Contributor).

**Azure RBAC in Kürze** 🔎:
- **Security Principal** (wer: Benutzer, Gruppe, Service Principal, Managed Identity)
- **Rollendefinition** (was: Sammlung von Actions, z. B. Reader, Contributor, Owner)
- **Scope** (wo: Management Group → Abo → Ressourcengruppe → Ressource, Rechte vererben sich nach unten)
- → ergibt eine **Rollenzuweisung**

📚 Im Portal: Arc → Server → **Access control (IAM)** mit den Reitern *Check access*, *Role assignments*, *Deny assignments*, *Classic administrators*, *Roles*.
📚 Weil Arc jedem On-Prem-Server eine Ressourcen-ID gibt, gilt der **Ressourcenkontext** auch für Log-Analytics-Daten. Wer Rechte auf den Server hat, sieht dessen Logs, ohne Zugriff auf den ganzen Workspace.

### 5.8 Azure Policy

**Azure Policy** (Folie 15) definiert und erzwingt **Regeln und Compliance-Anforderungen** für Azure-Ressourcen (Sicherheit, Compliance, Kosten, z. B. «nur Region Switzerland North», «Tag *Kostenstelle* Pflicht»). Die Konfigurationen werden laufend überwacht, bei Abweichungen greift Policy ein.
🔎 **Effekte:** `Audit` (nur melden), `Deny` (verhindern), `Modify`/`Append` (anpassen), `DeployIfNotExists` (fehlende Konfiguration nachliefern, z. B. Monitoring-Agent), `AuditIfNotExists`. Mehrere Policies werden zu einer **Initiative** gebündelt. Zuweisung auf einen Scope. Nicht konforme Ressourcen lassen sich mit **Remediation Tasks** korrigieren. Für Arc-Server prüft **Machine Configuration** Einstellungen **innerhalb** des OS.

### 5.9 Azure Resource Graph, WAC-Extension, Update Manager

**Azure Resource Graph** 🔎: Dienst, um Ressourcen über viele Abos hinweg schnell abzufragen. Die Sprache basiert auf **KQL** (Kusto Query Language). Nutzbar im Portal (**Resource Graph Explorer**), mit `az graph query` oder `Search-AzGraph`. Man braucht mindestens **Read**-Rechte auf die Ressourcen. Der Dienst ist kostenlos (gedrosselt).

✍️ Lösungen für den Arbeitsauftrag «KQL-Query für Arc-Server»:

```kusto
// alle Arc-Server
resources
| where type =~ 'microsoft.hybridcompute/machines'

// Name und Location der Server
resources
| where type =~ 'microsoft.hybridcompute/machines'
| project name, location, resourceGroup, os = tostring(properties.osName), status = tostring(properties.status)

// Anzahl Server pro Status (Connected/Disconnected)
resources
| where type =~ 'microsoft.hybridcompute/machines'
| summarize Anzahl = count() by status = tostring(properties.status)
```

**Windows Admin Center Extension:** Arc-Server → *Windows Admin Center* → Installieren. Danach lässt sich der Server **direkt aus dem Azure-Portal** mit WAC verwalten (ohne VPN und ohne eingehende Ports, Verbindung über Arc). Voraussetzung ist die passende RBAC-Rolle.

**Azure Update Manager** (🔎): verwaltet Windows- und Linux-Updates für Azure-VMs **und Arc-Server** zentral, ohne Log Analytics oder Automation Account.
- periodische Bewertung (alle 24 h)
- **Einmal-Update** oder **geplantes Patching** über eine **Wartungskonfiguration** (*Maintenance Configuration*: Zeitfenster, Wiederholung, Klassifikationen wie Critical/Security, Neustartverhalten, dynamische Scopes)
- Vorgehen im Arbeitsauftrag: Update Manager → *Maintenance Configurations* → Erstellen (Scope: Guest, Zeitplan, Update-Klassifikationen) → Arc-Server zuweisen → nach dem Lauf den Verlauf prüfen

### 5.10 Kosten

(Folie 16 verweist auf die Preisseite, 🔎 Stand 09/2026)
- **Kostenlos (Control Plane):** Inventar, Ressourcengruppen/Tags, Resource Graph, RBAC, Templates, SSH/Run Command/Custom Script Extension
- **Kostenpflichtig pro Server und Monat:** Azure Policy **Machine Configuration** + Change Tracking (ca. **USD 6 pro Server/Monat**), **Defender for Servers** (Plan 1/2), **Azure Update Manager**
- **Nach Verbrauch:** Azure Monitor/Log Analytics und Sentinel (pro GB)
- Mit **Windows Server Software Assurance** oder Pay-as-you-go-Lizenz über Arc sind Update Manager, Change Tracking, Machine Configuration u. a. **inklusive**

### 5.11 🛠️ Störungsbehebung Azure Arc

| Fehlerbild | Ursache | Prüfung / Lösung |
|---|---|---|
| Server im Portal «**Disconnected**» | kein Heartbeat: Firewall/Proxy blockiert 443, Dienst gestoppt, Server aus | `azcmagent show`, `azcmagent check`, Dienste *himds*, *GCArcService*, *ExtensionService* |
| Onboarding schlägt fehl: Netzwerk | Endpunkte/Service Tags blockiert, TLS-Problem, Proxy nicht gesetzt | `azcmagent check`, `azcmagent config set proxy.url "http://proxy:8080"` |
| Onboarding schlägt fehl: `AuthorizationFailed` / 403 | fehlende Rolle (*Onboarding*), Resource Provider nicht registriert | Rolle zuweisen, `Register-AzResourceProvider …` |
| Installation bricht ab | Server läuft in Azure (nicht erlaubt), 32-Bit-OS, nicht unterstütztes OS | Voraussetzungen prüfen |
| Zwei Server überschreiben sich gegenseitig | Klon/Golden Image mit bereits verbundenem Agent | `azcmagent disconnect` auf dem Klon, neu onboarden |
| Token-Fehler | Uhrzeit weicht ab | Zeitsynchronisation (NTP) |
| HIMDS-Dienst startet nicht | GPO entzieht `NT SERVICE\himds` das Recht «Anmelden als Dienst» | GPO anpassen |
| Extension-Installation schlägt fehl | Extension-Endpunkte blockiert, Speicherplatz | Logs unter `%ProgramData%\GuestConfig\` und `azcmagent logs` (sammelt alles in ein ZIP) |

---

<a id="defender"></a>
## 6. Unit 05 – Windows-Sicherheit: Credential Guard, Defender Antivirus, Firewall

> Es gibt zwei Folienversionen. Die **neue Version (August 2026)** arbeitet mit Gruppen- und Expertenaufträgen und zeigt die Summary-Folien der Gruppen. Die **ältere Version (April 2024, 🗂️)** enthält die Musterantworten zu Defender Antivirus und Firewall, die in der neuen fehlen. Beide sind hier zusammengeführt.

### Lernziele

Die Technikerinnen und Techniker HF können …
- die Sicherheitsfähigkeiten von Windows beschreiben,
- **Windows Defender Credential Guard** beschreiben und sein Funktionsprinzip erklären,
- **Microsoft Defender Antivirus** verwalten,
- die **Windows Defender Firewall** verwalten.

### 6.1 Einordnung: Microsoft Cybersecurity Reference Architecture (MCRA)

Folie 6 zeigt die MCRA (Zero Trust, Dezember 2023). Die wichtigsten Bausteine:

| Bereich | Produkte/Funktionen |
|---|---|
| **Identität und Zugriff** | Microsoft Entra ID, **Conditional Access** (Zero-Trust-Zugriffsentscheidung aufgrund von Benutzer und Geräte-Zustand), Entra ID Protection (geleakte Anmeldedaten, Verhaltensanalyse), PIM, Passwordless/MFA, Authenticator, Windows Hello for Business, FIDO2, Defender for Identity |
| **Endpoints und Geräte** | Intune und Configuration Manager (UEM), **Microsoft Defender for Endpoint** (EDR, Threat & Vulnerability Management, Web Content Filtering, Endpoint DLP). **Windows 11/10 Security:** App Control, Exploit Protection, Behavior Monitoring, Next-Generation Protection, Network Protection, **Credential Protection**, Full Disk Encryption, Attack Surface Reduction |
| **Hybride Infrastruktur** | **Defender for Cloud** (CSPM + XDR für IaaS/PaaS/on-prem), **Azure Arc**, Azure Firewall/Firewall Manager, WAF, DDoS Protection, Key Vault, Bastion, Backup, Private Link |
| **SaaS / Daten** | Defender for Cloud Apps (Shadow IT, Session Control, DLP), **Microsoft Purview** (Information Protection, Klassifizierung, Data Governance, Insider Risk, eDiscovery) |
| **Security Operations (SOC)** | **Microsoft Defender XDR** (Incident Response, Automation, Threat Hunting), **Microsoft Sentinel** (Cloud-SIEM/SOAR/UEBA), **Security Copilot**, Threat Intelligence |
| **Weitere** | Defender for IoT/OT, Secure Score/Compliance Score, Privileged Access Workstations (PAW), GitHub Advanced Security |

📚 **Windows-Sicherheit-App (Windows Security Center)**, Bereiche:
- **Viren- und Bedrohungsschutz** (Antivirus, Schutzverlauf)
- **Kontoschutz** (Windows Hello, dynamische Sperre)
- **Firewall- und Netzwerkschutz**
- **App- und Browsersteuerung** (SmartScreen)
- **Gerätesicherheit** (Kernisolierung/VBS, Sicherheitsprozessor/TPM, Secure Boot)
- **Geräteleistung und -integrität**
- **Familienoptionen**

### 6.2 Windows Defender Credential Guard

Gruppenauftrag (neue Version): 5 Gruppen mit je einer Leitfrage (Betriebssysteme, Angriffsmethoden, Voraussetzungen, Funktionsweise, Domain Controller). Pro Gruppe gab es 20 Minuten Vorbereitung und eine Kurzpräsentation von 3–5 Minuten mit vier Elementen: **Antwort – Technik – Praxis – Security-Fazit** (welches Risiko sinkt, welches bleibt?).

**Was ist Credential Guard?** Credential Guard **isoliert Anmeldeinformationen** mit **Virtualization-Based Security (VBS)**, sodass nur privilegierte Systemsoftware darauf zugreifen kann. Geschützt werden:
- **NTLM-Passwort-Hashes**
- **Kerberos Ticket Granting Tickets (TGTs)**
- von Anwendungen als Domänen-Anmeldedaten gespeicherte Anmeldeinformationen

**Merksatz der Folie:** Credential Guard schützt Credentials **durch Isolation, nicht durch einen weiteren Virenscanner**.

**1 – Betriebssysteme**

| Quelle | Aussage |
|---|---|
| Folie alt 🗂️ | Windows 11 (ab 22H2 automatisch aktiviert), Windows 10, Windows Server 2016/2019/2022 |
| Folie neu | Windows 10/11, Windows Server ab 2016, benötigt VBS, auf neueren Systemen teilweise standardmässig aktiv |
| 🔎 MS-Doku | **Editionen: nur Enterprise und Education** (nicht Pro/Pro Education). Lizenzen: Windows Enterprise E3/E5, Education A3/A5. **Standardmässig aktiv** ab **Windows 11 22H2** und **Windows Server 2025** auf **domänengebundenen Nicht-DC-Systemen**, welche die Anforderungen erfüllen (ohne UEFI-Lock, also remote deaktivierbar). |

- **Wo sinnvoll?** Unternehmens-Clients, **Admin-Workstations**, Member Server, Systeme mit privilegierten Konten. «Je wertvoller die verwendeten Credentials, desto wichtiger deren Schutz.»
- **Unterschied Client/Server:** Auf Clients ist Credential Guard seit 22H2 standardmässig aktiv, auf Servern erst ab 2025 und dort nur auf Member Servern (nicht auf DCs).

**2 – Angriffsmethoden: Pass-the-Hash und Pass-the-Ticket**

| | **Pass-the-Hash (PtH)** | **Pass-the-Ticket (PtT)** |
|---|---|---|
| Protokoll | **NTLM** | **Kerberos** |
| Was wird gestohlen | **NTLM-Hash** des Passworts (aus dem Speicher von LSASS) | **Kerberos-Ticket** (TGT oder Service-Ticket) |
| Idee | Der Hash **ersetzt das Passwort**. Das Klartextpasswort muss nicht bekannt sein, Brute-Force entfällt. | Das TGT beweist die Identität. Wer es hat, erhält weitere Tickets, ohne das Passwort zu kennen. |

**Beispielhafter Ablauf (Lateral Movement):** Phishing-Mail → Malware auf einem PC → Angreifer erlangt lokale Adminrechte → liest den Speicher von LSASS aus (Hashes/Tickets eines Admins, der sich angemeldet hatte) → meldet sich mit dem Hash/Ticket an weiteren Systemen an → arbeitet sich bis zum Domain Controller hoch.
«PC kompromittiert → Credentials → weitere Systeme → Lateral Movement». Merksatz: **PtH = NTLM | PtT = Kerberos**.

**3 – Voraussetzungen**
- Technische Kette: **Hardwarevirtualisierung → VBS → Credential Guard**
- **64-Bit-CPU** mit Virtualisierungserweiterungen (VT-x/AMD-V) und **SLAT**
- **UEFI** und **Secure Boot**
- **VBS** aktiv, unterstützte Windows-Version/-Edition
- 🔎 empfohlen: **TPM** 1.2/2.0 (Bindung an Hardware), **UEFI Lock** (verhindert Deaktivieren per Registry)
- **In VMs:** Der Hyper-V-Host braucht eine **IOMMU**, und die VM muss **Generation 2** sein (Gen 1 wird nicht unterstützt). Credential Guard in der VM schützt gegen Angriffe **innerhalb** der VM, nicht gegen einen kompromittierten Host.
- **Fehlt eine Voraussetzung**, startet Credential Guard nicht. Windows läuft normal weiter, aber die Credentials liegen **ungeschützt** in LSASS. In `msinfo32` erscheint Credential Guard dann nicht unter «Ausgeführte Dienste für virtualisierungsbasierte Sicherheit».

**4 – Funktionsweise**

| Ohne Credential Guard | Mit Credential Guard |
|---|---|
| Windows → **LSASS** (`lsass.exe`) → Credentials im Prozessspeicher. Ein Admin/SYSTEM-Prozess (z. B. Mimikatz) kann sie auslesen. | Windows → LSASS → per **RPC** → **LSAIso** (`LSAIso.exe`, *isolierter LSA-Prozess*) in einem **von VBS geschützten Bereich** (Virtual Secure Mode) → geschützte Secrets («Tresor») |

- Der Hypervisor trennt die normale Windows-Welt vom isolierten Bereich. **Selbst mit Kernel-/Admin-Rechten** kommt man nicht an die Secrets.
- LSAIso enthält nur wenige, von VBS **signierte** Binaries und keine Treiber.
- 🔎 Mit TPM 2.0 wird ein persistierter VSM-Masterschlüssel durch das TPM geschützt. NTLM-Hash und TGT werden ohnehin nicht über Neustarts gespeichert.

**5 – Domain Controller und Grenzen**

| Quelle | Aussage |
|---|---|
| Folie alt 🗂️ | «Das Aktivieren auf Domänencontrollern wird **nicht empfohlen**. Kein Sicherheitsgewinn, mögliche Kompatibilitätsprobleme.» |
| Folie neu | «Domain Controller: NEIN – Credential Guard wird auf Domain Controllern **nicht unterstützt**.» |
| 🔎 MS-Doku | «Enabling Credential Guard on domain controllers **isn't recommended**» – kein zusätzlicher Schutz (die **AD-Datenbank** selbst wird nicht geschützt), mögliche Kompatibilitätsprobleme. Bei der Standardaktivierung sind DCs ausgenommen. |

⚠️ Genau genommen ist es «nicht empfohlen / ohne Nutzen» und nicht «nicht unterstützt». Die Prüfungsantwort ist in beiden Fällen: **Nein, nicht auf DCs aktivieren.**

**Andere Schutzmassnahmen für DCs:** Least Privilege, separate Admin-Konten (Tiering), sichere Admin-Workstations (PAW), Patch-Management, Netzwerksegmentierung, Monitoring. 🔎 Weitere: Gruppe *Protected Users*, **LSA-Schutz** (`RunAsPPL`), Windows LAPS für das DSRM-Passwort, keine Internetnutzung auf DCs, Defender for Identity.

**Was Credential Guard nicht schützt** (Folie + 🔎): **Phishing**, **gestohlene Passwörter** (Keylogger, eingegebene Passwörter), **nicht jede Malware**, **Fehlkonfigurationen**. Dazu die AD-Datenbank und die **SAM** (lokale Konten), Microsoft-Konten, **Kerberos-Service-Tickets** (nur das TGT ist geschützt), physische Angriffe. Mit aktivem Credential Guard funktionieren **NTLMv1, MS-CHAPv2, Digest, CredSSP** nicht mehr mit Single Sign-on, und Kerberos-**DES** und **unconstrained Delegation** gehen nicht mehr (Anwendungen testen!).
**Merksatz:** Credential Guard ist **eine Schutzschicht innerhalb von «Defense in Depth»**.

🗂️ **Arbeitsauftrag (alte Version):** Prüfen, ob Credential Guard aktiv ist. Wenn nicht, mit Mimikatz den Passwort-Hash auslesen. Dann Credential Guard aktivieren und erneut versuchen. Erwartung: Ohne Credential Guard zeigt das Tool NTLM-Hashes aus dem LSASS-Speicher, mit Credential Guard sieht es nur noch isolierte, verschlüsselte Daten (LSA Isolated Data).

```powershell
# Status prüfen (1 = Credential Guard konfiguriert/läuft)
Get-CimInstance -ClassName Win32_DeviceGuard -Namespace root\Microsoft\Windows\DeviceGuard |
  Select-Object SecurityServicesConfigured, SecurityServicesRunning, VirtualizationBasedSecurityStatus
# oder: msinfo32 → «Virtualisierungsbasierte Sicherheit: Ausgeführte Dienste»
```

🔎 **Aktivieren:** GPO *Computerkonfiguration → Administrative Vorlagen → System → Device Guard → Virtualisierungsbasierte Sicherheit aktivieren* → Credential-Guard-Konfiguration «Mit UEFI-Sperre aktiviert» oder «Ohne Sperre», **oder** Intune (Settings Catalog / Endpoint Security → Kontoschutz), dann Neustart.

### 6.3 «Sicher genug?» – Security richtig betreiben

**Szenario (Folie 19):** Ein Unternehmen mit 100 Windows-11-Geräten: Windows aktuell, Defender aktiv, Firewall eingeschaltet. **Reicht das?** Nein. Möglich bleiben Malware, Ransomware, offene Ports, Fehlkonfiguration und gestohlene Credentials.

**«Einschalten reicht nicht» (Folie 20):**
- **Defender** = Erkennen → Blockieren → Reagieren
- **Firewall** = Verkehr → Prüfen → Erlauben/Blockieren
- Typische Schwachstellen: **falsche Ausnahmen**, **zu offene Firewall-Regeln**, **fehlendes Monitoring**, **keine zentrale Verwaltung**
- **Security = Technologie + Konfiguration + Betrieb**

**Drei Schutzbereiche, drei Aufgaben (Abschluss):**

| Komponente | Aufgabe |
|---|---|
| **Credential Guard** | schützt **Anmeldeinformationen** |
| **Defender Antivirus** | **erkennt und blockiert** Bedrohungen/Malware |
| **Firewall** | **kontrolliert den Netzwerkverkehr** |

«Gute Security entsteht durch mehrere Schutzschichten und deren richtige Konfiguration und Betrieb.» Eine einzelne Massnahme reicht nicht, weil jede nur einen Angriffsweg abdeckt (Defense in Depth).

### 6.4 Microsoft Defender Antivirus

📚 Defender Antivirus schützt vor Spyware, Malware und Viren, ist Hyper-V-bewusst und aktualisiert seine **Definitionen (Security Intelligence)** automatisch.

**Unterstützte Windows-Versionen** 🔎: **Windows 10 und 11**, **Windows Server 2016 und neuer** (sowie Server-Version 1803+), **Windows Server 2012 R2** nur über die «modern unified solution» von Defender for Endpoint, **Azure Stack HCI OS 23H2+**. Auf Windows Server ist Defender ein Feature (`Windows-Defender`), das deinstalliert werden kann. Funktionen: **Echtzeitschutz** (Always-on), **Cloud-basierter Schutz** (inkl. **Block at First Sight**: neue Malware in Sekunden per Cloud-Analyse blockieren), Verhaltensüberwachung, Heuristik/ML, **PUA-Schutz** (potenziell unerwünschte Apps), 🔎 **Manipulationsschutz** (Tamper Protection).

**Welche Lizenz wird benötigt?**
- 🗂️ Folie: Privatpersonen brauchen ein Microsoft-365-Single/Family-Abo (für die Consumer-App *Microsoft Defender*). **Unternehmen mindestens Microsoft Defender for Endpoint P1.**
- 🔎 Präzisierung ⚠️: **Defender Antivirus ist in Windows 10/11 und Windows Server integriert und kostenlos.** Lizenzen braucht es für die **zentrale Unternehmensverwaltung und erweiterte Funktionen**:

| Lizenz | Inhalt | enthalten in |
|---|---|---|
| **Defender for Endpoint P1** | Next-Gen-Protection, ASR, Device Control, zentrale Verwaltung | Microsoft 365 **E3**/A3 |
| **Defender for Endpoint P2** | + **EDR**, automatische Untersuchung, Threat & Vulnerability Management, **Advanced Hunting** | Microsoft 365 **E5**/A5 |
| **Defender for Business** | KMU-Variante (**bis 300 Benutzer**) mit EDR und automatischer Behebung | **Microsoft 365 Business Premium** |
| **Defender for Servers** | Server-Schutz über Defender for Cloud (inkl. MDE für Server) | Azure (auch für Arc-Server) |

**Scan-Typen** (📚)

| Scan | Was wird geprüft | Einsatz |
|---|---|---|
| **Echtzeitschutz** | jede Datei beim Öffnen/Ausführen/Herunterladen, laufend | immer aktiv |
| **Quick Scan** (Schnellüberprüfung) | Orte, an denen sich Malware typischerweise einnistet (Autostart, Systemordner, laufende Prozesse, Registry) | **täglich geplant** (Best Practice) |
| **Full Scan** (vollständig) | **alle Dateien** auf allen Laufwerken und alle laufenden Programme, dauert lange | bei Verdacht auf Infektion |
| **Custom Scan** (benutzerdefiniert) | ausgewählte Laufwerke/Ordner | gezielt (z. B. USB-Stick) |
| **Microsoft Defender Offline** | Scan aus einer vertrauenswürdigen Umgebung **vor dem Windows-Start** | Rootkits, MBR-Malware, hartnäckige Infektionen |

```powershell
Start-MpScan -ScanType QuickScan      # FullScan / CustomScan -ScanPath D:\
Start-MpWDOScan                        # Defender Offline (Neustart)
Update-MpSignature                     # Definitionen aktualisieren
Get-MpComputerStatus | Select AMRunningMode, AntivirusEnabled, RealTimeProtectionEnabled, AntivirusSignatureLastUpdated, IsTamperProtected
Get-MpThreatDetection                  # erkannte Bedrohungen / Verlauf
```

**Was passiert bei einem Fund?** Bedrohung → **Erkennung** → **Blockierung/Quarantäne** → **Information** (Benachrichtigung, Schutzverlauf, Event-Log, Meldung ans Portal) → **Bereinigung** (entfernen/wiederherstellen) → **Kontrolle** (erneuter Scan, Ursache klären).
**Quarantäne:** Die Datei wird in einen geschützten Bereich verschoben und verschlüsselt/unschädlich abgelegt. Sie kann nicht ausgeführt werden. Im **Schutzverlauf** kann man sie **entfernen** oder **wiederherstellen**. 📚 Software mit Warnstufe «Schwerwiegend/Hoch» nie wiederherstellen.

**Drittanbieter-Antivirus installiert?** 🔎
- **Windows 10/11:** Defender geht automatisch in den **deaktivierten Modus** (mit Smart App Control teils passiv).
- **Windows Server:** **kein** automatischer Wechsel, Defender muss **manuell** deaktiviert/deinstalliert oder in den passiven Modus gesetzt werden (`ForceDefenderPassiveMode = 1`).
- Mit **Defender for Endpoint** läuft Defender im **passiven Modus** weiter (scannt und meldet, behebt aber nicht). **EDR im Blockmodus** kann trotzdem eingreifen.
- Fällt der Drittanbieter weg (Lizenz abgelaufen, deinstalliert), aktiviert sich Defender auf Clients automatisch wieder.
- Status: `Get-MpComputerStatus | Select AMRunningMode` → *Normal*, *Passive* oder *EDR Block Mode*.

**Ausschlüsse (Exclusions)**
- **Arten:** **Datei**, **Ordner** (inkl. Unterordner), **Dateityp** (Erweiterung), **Prozess**. 🔎 Dazu IP-Adressen (für Network Protection).
- 🗂️ **GUI:** Windows-Sicherheit → Viren- & Bedrohungsschutz → *Einstellungen verwalten* → *Ausschlüsse hinzufügen oder entfernen* → *Ausschluss hinzufügen* → Datei/Ordner/Dateityp/**Prozess**
- **PowerShell** 🔎:
  ```powershell
  Add-MpPreference -ExclusionPath "D:\App\Data"           # Add- ergänzt die Liste
  Add-MpPreference -ExclusionExtension ".log"
  Add-MpPreference -ExclusionProcess "C:\App\app.exe"
  Get-MpPreference | Select-Object ExclusionPath, ExclusionExtension, ExclusionProcess   # prüfen
  Remove-MpPreference -ExclusionPath "D:\App\Data"
  ```
  ⚠️ `Set-MpPreference -Exclusion…` **überschreibt** die bestehende Liste, `Add-MpPreference` **ergänzt**. Ein **Prozess-Ausschluss** schliesst die **Dateien aus, die dieser Prozess öffnet**, nicht die EXE selbst. Die EXE schliesst man mit `-ExclusionPath` aus.
- Zentral per **Intune** (Endpoint Security → Antivirus), **GPO** oder ConfigMgr. Zentral gesetzte Ausschlüsse sind im Client meist nur eingeschränkt sichtbar.
- **Risiken:** Malware kann sich gezielt in ausgeschlossenen Ordnern verstecken oder als ausgeschlossener Prozess laufen. Angreifer suchen aktiv nach Ausschlusslisten. Zu breite Ausschlüsse (ganze Laufwerke, `C:\Temp`, `*.exe`) sind gefährlich. Vergessene Ausschlüsse bleiben jahrelang bestehen.

**Mit welchen Tools lässt sich Defender Antivirus konfigurieren?** 🗂️ **Microsoft Intune**, **Configuration Manager**, **Gruppenrichtlinien**, **PowerShell-Cmdlets**, **WMI**. Dazu die Windows-Sicherheit-App (lokal) und 🔎 das Microsoft-Defender-Portal (Security Settings Management).
📚 Mit Microsoft 365 ist **Intune** empfohlen (Endpoint Security → Antivirus bzw. Konfigurationsprofil).

**Demonstration/Gruppenarbeit: Einstellungen per PowerShell** ✍️

```powershell
Set-MpPreference -SignaturesUpdatesChannel Broad    # in neueren Versionen: -DefinitionUpdatesChannel Broad
Set-MpPreference -DisableCatchupQuickScan $false     # «Disable» der Folie = Catch-up NICHT mehr deaktivieren
Set-MpPreference -SignatureDefinitionUpdateFileSharesSources "\\test\istgarkeinpfad"
Get-MpPreference | Select-Object *UpdatesChannel*, DisableCatchupQuickScan, SignatureDefinitionUpdateFileSharesSources, SignatureFallbackOrder
```

| Einstellung | Auswirkung |
|---|---|
| **DefinitionUpdatesChannel = Broad** | Signatur-Updates (Security Intelligence) kommen erst **nach Abschluss des gestaffelten Rollouts** von Microsoft. Stabiler (Fehler fallen zuerst bei anderen auf), aber etwas später geschützt. Empfohlen für die breite Produktion (ca. 10–100 % der Geräte). Andere Kanäle: *Staged* (ca. 10 % Pilot, früher), *NotConfigured* (Microsoft wählt), für Engine/Plattform auch *Beta* und *Preview*. 🔎 Der Parameter heisst in der aktuellen Doku `-SignaturesUpdatesChannel` («wird zu DefinitionUpdatesChannel umbenannt»). |
| **DisableCatchupQuickScan = False** | Standard ist **True** (keine Nachhol-Scans). Mit `$false` gilt: Hat der PC **zwei geplante Quick Scans verpasst** (z. B. weil er aus war), läuft bei der nächsten Anmeldung ein **Catch-up-Scan**. Mehr Schutz, dafür kurz mehr Last beim Anmelden. |
| **SignatureDefinitionUpdateFileSharesSources = \\test\istgarkeinpfad** | Definiert **UNC-Freigaben als Update-Quelle** (Liste mit `\|` getrennt). Der Pfad existiert nicht. Solange `FileShares` nicht in der **SignatureFallbackOrder** steht (Standard: `MicrosoftUpdateServer \| MMPC`), passiert nichts. Wird die Freigabe als einzige Quelle genutzt, **veralten die Signaturen**. Lehre: Update-Quellen testen und die Signaturaktualität überwachen. |

**Advanced Hunting** (Verifikation im Defender-Portal): security.microsoft.com → *Hunting* → *Advanced Hunting*. Abfragen in **KQL** über Tabellen wie `DeviceInfo`, `DeviceEvents`, `DeviceProcessEvents`, `DeviceTvmSecureConfigurationAssessment` oder `DeviceTvmInfoGathering`. Voraussetzung: Das Gerät ist in **Defender for Endpoint (P2)** onboarded.

```kusto
// Konfigurations- und AV-Infos eines Geräts ansehen (AdditionalFields enthält die AV-Details)
DeviceTvmInfoGathering
| where DeviceName startswith "srv01"
| project Timestamp, DeviceName, AdditionalFields
| evaluate bag_unpack(AdditionalFields)
```

🔎 Die genauen Feldnamen für den Update-Kanal in `AdditionalFields` sind in der Doku nicht einzeln aufgeführt. Mit `bag_unpack` die Felder anzeigen und die Spalte mit dem Kanal/Ring suchen. **Lokal** geht die Prüfung einfacher mit `Get-MpPreference`.

### 6.5 Windows Defender Firewall

**Was ist eine Firewall und was macht sie?** 🗂️ Eine Sicherheitsvorrichtung, die den **Datenverkehr zwischen Netzwerken bzw. zu/von einem Gerät überwacht und kontrolliert**: Sie blockiert unerlaubten Zugriff und lässt autorisierten Verkehr zu.

**Warum ist eine Firewall wichtig?** 🗂️ Sie
1. schützt vor unautorisierten Zugriffen und Cyberangriffen,
2. filtert schädlichen Verkehr und verhindert Malware-Infektionen,
3. überwacht und kontrolliert ein- und ausgehenden Verkehr,
4. unterstützt die Einhaltung von Richtlinien und Gesetzen,
5. schützt sensible Daten und Ressourcen.

**Warum trotz Antivirus eine Firewall?** Antivirus prüft **Dateien und Prozesse** auf dem Gerät. Die Firewall kontrolliert **Netzwerkverbindungen**, z. B. Angriffe auf offene Dienste (Exploits, Brute-Force auf RDP, Wurmverbreitung) ohne Datei oder die Kommunikation von Malware mit ihrem C2-Server. Die beiden decken unterschiedliche Angriffswege ab.

**Was muss eine Firewall-Regel definieren?** 🗂️
1. **Quelladresse** (IP/Bereich)
2. **Zieladresse**
3. **Protokoll** (TCP, UDP, ICMP)
4. **Quellport**
5. **Zielport**
6. **Aktion** (Allow/Block)
7. **Richtung** (Inbound/Outbound)

🔎 Bei der Windows-Firewall zusätzlich: **Programm/Dienst**, **Profil** (Domäne/Privat/Öffentlich), Schnittstellentyp, Benutzer/Computer (bei IPsec).

| Begriff | Erklärung |
|---|---|
| **Firewall-Exception** (Ausnahme) | Regel, die bestimmten Verkehr **ausdrücklich erlaubt**, obwohl er sonst blockiert würde, damit vertrauenswürdige Apps/Dienste funktionieren (definiert über IP, Port, Protokoll, Programm). 📚 Jede Ausnahme ist ein «Loch». Eine **Programm-Ausnahme** ist sicherer als ein **offener Port**, weil das Loch nur offen ist, wenn das Programm läuft. |
| **Inbound-Regel** | kontrolliert **eingehenden** Verkehr zum Gerät (wer darf sich verbinden?). Ziel: unautorisierten Zugriff von aussen verhindern. |
| **Outbound-Regel** | kontrolliert **ausgehenden** Verkehr vom Gerät. Ziel: verhindern, dass Daten unkontrolliert abfliessen oder Malware nach aussen kommuniziert. |
| **Allow / Block** | Verkehr zulassen oder verwerfen. 🔎 Bei der Windows-Firewall hat **Block Vorrang vor Allow** (Ausnahme: authentifizierte IPsec-Umgehung). |

📚 **Standardverhalten:** **Eingehend: alles blockiert**, was nicht per Regel erlaubt ist. **Ausgehend: alles erlaubt**, was nicht per Regel blockiert ist.

📚 **Netzwerkprofile** (über Network Location Awareness):

| Profil | Wann | Verhalten |
|---|---|---|
| **Domäne** | Gerät erreicht einen DC seiner Domäne | Firmenregeln, Netzwerkerkennung an |
| **Privat** | vertrauenswürdiges Heim-/Firmennetz | Netzwerkerkennung an |
| **Öffentlich** | Café, Hotel, unbekannt (Standard bei neuen Netzen) | am restriktivsten, Netzwerkerkennung aus |

📚 **Windows Defender Firewall mit erweiterter Sicherheit (WFAS)** (`wf.msc`):
- Pro Profil: Status, Standardaktion eingehend/ausgehend, geschützte Adapter, Benachrichtigungen, **Protokollierung** (`%windir%\System32\LogFiles\Firewall\pfirewall.log`, Standard **4096 KB**, loggt erst, wenn «verworfene Pakete protokollieren» bzw. «erfolgreiche Verbindungen» aktiviert ist)
- **Regeltypen:** **Programm**, **Port**, **Vordefiniert** (z. B. Remotedesktop, Datei- und Druckerfreigabe), **Benutzerdefiniert**
- **Verbindungssicherheitsregeln (IPsec):** Isolierung (Domänen-/Serverisolierung), Authentifizierungsausnahme (z. B. DCs, DHCP), Server-zu-Server, Tunnel, Benutzerdefiniert. Sie **authentifizieren/verschlüsseln**, erlauben aber selbst keinen Verkehr.
- **Überwachung:** aktive Profile, Regeln, Sicherheitszuordnungen. Ereignisanzeige (z. B. ConnectionSecurity-Log).

**Verwaltung:** lokal (Systemsteuerung, `wf.msc`), **GPO**, **Intune** (Endpoint Security → Firewall), **PowerShell** (`NetSecurity`-Modul), `netsh advfirewall`.

```powershell
Get-NetFirewallProfile | Select Name, Enabled, DefaultInboundAction, DefaultOutboundAction, LogFileName
New-NetFirewallRule -DisplayName "RDP nur aus Admin-Netz" -Direction Inbound -Protocol TCP `
  -LocalPort 3389 -RemoteAddress 10.10.99.0/24 -Profile Domain -Action Allow
New-NetFirewallRule -DisplayName "Block Telnet out" -Direction Outbound -Protocol TCP -RemotePort 23 -Action Block
Get-NetFirewallRule -DisplayName "RDP*" | Get-NetFirewallAddressFilter
Set-NetFirewallProfile -Profile Domain,Private,Public -LogBlocked True
```

### 6.6 Aktualitäten: CrowdStrike und Security Baselines

**CrowdStrike-Vorfall (19.07.2024)** 🔎: Ein fehlerhaftes Inhaltsupdate für den **Kernel-Treiber** des CrowdStrike-Falcon-Sensors liess weltweit rund 8,5 Mio. Windows-Geräte mit einem Bluescreen abstürzen (Flughäfen, Banken, Spitäler). Die Behebung war oft nur **manuell** möglich (Safe Mode/WinRE, Datei löschen, BitLocker-Schlüssel nötig).
**«Wie kann man solche Probleme heute lösen?»**
- **Gestaffelte Rollouts** (Ringe: Pilot → breit) auch für Security-Updates. Genau das steuern die Defender-**Update-Kanäle** (*Staged*, *Broad*, *Critical – Time Delay*).
- Microsofts **Windows Resiliency Initiative**: **Quick Machine Recovery** (Fehlerbehebung über die Windows-Wiederherstellungsumgebung per Windows Update, auch wenn der PC nicht mehr startet) und Security-Produkte schrittweise **aus dem Kernel in den User-Modus** verlagern.
- Organisatorisch: BitLocker-Wiederherstellungsschlüssel zentral verfügbar (Entra ID/AD), Notfallpläne, Backups, Abhängigkeit von einem Anbieter prüfen.

**Security Baseline Windows 11 24H2** (Link in der Folie) 🔎: Eine **Security Baseline** ist eine von Microsoft empfohlene Sammlung sicherheitsrelevanter **Gruppenrichtlinien-Einstellungen**. Sie wird mit dem **Security Compliance Toolkit (SCT)** geliefert: GPO-Backups, *Policy Analyzer* zum Vergleichen, *LGPO.exe* zum lokalen Anwenden. In Intune gibt es entsprechende **Security Baselines** als Profile. Vorgehen: Baseline testen, Abweichungen dokumentieren, dann ausrollen.

### 6.7 Übungsauftrag «Security Experts» (B5)

Vier Expertengruppen (je 3–4 Personen, ca. 45–60 Min.): **1 Defender – Schutz & Erkennung**, **2 Defender – Administration & Exclusions**, **3 Endpoint Security – Unternehmenslösung**, **4 Firewall – Security Design**. Leitfrage: *«Wie setzen wir diese Technologie sicher und sinnvoll in einem Unternehmen ein?»* Präsentation 5–8 Min.: Leitfragen beantworten (3–4 Min.), eigene Einschätzung (1 Min.), Diskussionsfrage an die Klasse (2–3 Min.; nicht mit Ja/Nein beantwortbar). Beurteilt werden auch Risiken, Kosten, Betriebsaufwand, Fehlkonfigurationen und Alternativen.
→ **Ausgearbeitete Lösungen in [Kapitel 12](#b5).**

### 6.8 🛠️ Störungsbehebung Defender, Firewall, Credential Guard

| Fehlerbild | Ursache | Prüfung / Lösung |
|---|---|---|
| Defender ist «aus» | Drittanbieter-AV aktiv, GPO *Microsoft Defender Antivirus deaktivieren*, Server ohne Defender-Feature | `Get-MpComputerStatus` (AMRunningMode), Windows-Sicherheit → *Anbieter verwalten*, `gpresult /h report.html` |
| Signaturen veraltet | keine Verbindung zur Update-Quelle, falsche Fallback-Reihenfolge, WSUS genehmigt nicht | `Update-MpSignature`, `Get-MpComputerStatus` (AntivirusSignatureLastUpdated), `Get-MpPreference` (SignatureFallbackOrder) |
| Lokale Änderung wird zurückgesetzt | **Manipulationsschutz** aktiv oder Richtlinie (Intune/GPO) überschreibt | zentral ändern, nicht lokal |
| Fehlalarm (False Positive) blockiert eine Business-App | Heuristik/Cloud-Erkennung | Datei an Microsoft einreichen, **eng begrenzten** Ausschluss dokumentieren, aus der Quarantäne nur nach Prüfung wiederherstellen |
| Wo sehe ich Funde? | – | Windows-Sicherheit → Schutzverlauf, `Get-MpThreatDetection`, Ereignisanzeige *Microsoft-Windows-Windows Defender/Operational* (🔎 Event **1116** = erkannt, **1117** = Aktion ausgeführt) |
| Dienst von aussen nicht erreichbar | Inbound-Regel fehlt, falsches **Profil** (Netz als *Öffentlich* erkannt, Regel nur für *Domäne*), Dienst hört nicht | `Get-NetConnectionProfile`, `Test-NetConnection srv01 -Port 443`, `netstat -ano`, Firewall-Log (verworfene Pakete) |
| Netz fälschlich «Öffentlich» | NLA erkennt die Domäne nicht (DNS/DC nicht erreichbar) | DNS prüfen, Dienst *Network Location Awareness* neu starten, notfalls `Set-NetConnectionProfile -NetworkCategory Private` (nicht bei Domänennetz) |
| Credential Guard läuft nicht | Edition Pro, Gen-1-VM, kein Secure Boot/VBS, Hypervisor aus | `msinfo32`, `Win32_DeviceGuard`, Voraussetzungen und Edition prüfen |
| Anwendung bricht nach Credential Guard ab | nutzt NTLMv1, Digest, CredSSP, Kerberos-DES oder unconstrained Delegation | Anwendung/Protokoll modernisieren, vorher testen |

---

<a id="github"></a>
## 7. Unit 06 – GitHub

### Lernziele

Die Technikerinnen und Techniker HF …
- können die grundlegenden Funktionen von GitHub verstehen,
- verstehen das Management von Repositories,
- können das **GitHub-Flow**-Konzept verstehen (Branches, Commits),
- verstehen die kollaborativen Funktionen von GitHub.

### 7.1 Git und GitHub

📚 **Git** ist ein **verteiltes Versionskontrollsystem**: Änderungen nachverfolgen, zusammenarbeiten, Versionen verwalten. Jeder Klon enthält die ganze Historie.
**GitHub** ist eine **Cloud-Plattform auf Basis von Git**. Sie ergänzt Git um Weboberfläche, Zusammenarbeit (Pull Requests, Issues), Automatisierung (Actions), Sicherheit und KI.

**GitHub-Plattform – fünf Säulen (Folie 6):**

| Säule | Inhalt |
|---|---|
| **AI** (Powered by AI) | **GitHub Copilot** (KI-Codeassistent), Copilot Chat, Copilot Agents, KI in Pull Requests und Issues |
| **Collaboration** | Repositories, Issues, Pull Requests, Discussions, Projects, Code Review |
| **Productivity** | **GitHub Actions** (CI/CD), **Codespaces** (Cloud-Entwicklungsumgebung), Automatisierung |
| **Security** | **CodeQL** (Code-Scanning), **Secret Scanning**, **Dependabot** (verwundbare Abhängigkeiten), Security Overview (GitHub Advanced Security) |
| **Scale** | grösste Entwickler-Community (über 100 Mio. Entwickler, 420 Mio. Repositories), Integrationen & APIs |

### 7.2 Begriffe (Recherchefragen mit Antworten)

| Begriff | Erklärung |
|---|---|
| **Repository** | Speicherort eines Projekts mit **allen Dateien und der gesamten Versionshistorie**. Grundlage für Zusammenarbeit, Änderungsverfolgung und Code-Review. Öffentlich (public) oder privat (private). |
| **Branch** | eigenständiger Entwicklungszweig innerhalb eines Repos. Man arbeitet an Features/Bugfixes, **ohne den Haupt-Branch** (`main`, früher `master`) zu beeinflussen. Später wird er **gemergt**. |
| **Commit** | **Momentaufnahme** von Änderungen an einer oder mehreren Dateien, mit **Commit-Message**, Autor, Zeitstempel und eindeutiger **ID (SHA-Hash)**. Ergibt eine nachvollziehbare Historie (Audit-Trail). |
| **Pull Request (PR)** | Anfrage, die Commits eines Branches in einen anderen (meist `main`) zu übernehmen. Ermöglicht **Code-Review**, Diskussion, Kommentare, Änderungswünsche und automatische Checks **vor** dem Merge. Es gibt auch **Draft-PRs** (noch nicht bereit für Review). |
| **GitHub Flow** | leichtgewichtiger, branch-basierter Workflow für Continuous Delivery (siehe 7.3) |
| **Gists** | Funktion zum Teilen von **Code-Schnipseln** oder Notizen. Eigentlich kleine Git-Repos (versioniert, forkbar, einbettbar). **Public** (auffindbar) oder **Secret** (nicht gelistet, aber **jeder mit dem Link** sieht ihn, also **nicht privat**). Nie Passwörter oder Keys in Gists! |
| 🔎 **Issue** | Aufgabe, Bug oder Idee verfolgen (Labels, Zuweisung, Meilensteine, Verknüpfung mit PRs) |
| 🔎 **Discussion** | Forum für Fragen, Ideen und Ankündigungen, nicht an Code gebunden (Kategorien: Q&A, Ideas, Polls …). Kann in ein Issue überführt werden. |
| 🔎 **Wiki / README / Pages** | Projektdokumentation (Wiki), Kurzbeschreibung (README.md), statische Website direkt aus dem Repo (GitHub Pages) |
| 🔎 **Fork** | eigene Kopie eines fremden Repos (Beitrag via PR ans Original) |

📚 **Dateizustände in Git:** *Untracked* (Git kennt die Datei nicht) → *Tracked*: *Unmodified* → *Modified* → *Staged* (`git add`) → *Committed* (`git commit`).

### 7.3 GitHub Flow

1. **Branch erstellen** vom `main` für jedes Feature/jeden Bugfix
2. **Commits** auf dem Branch (regelmässig, mit aussagekräftigen Messages)
3. **Pull Request öffnen**, um Änderungen zur Prüfung vorzuschlagen
4. **Code-Review**: Teammitglieder kommentieren, fordern Änderungen an oder genehmigen
5. **Mergen** in `main` nach erfolgreicher Prüfung
6. **Bereitstellen (Deploy)**: `main` ist **immer deploybar** (automatisch/manuell). 📚 Danach den Branch löschen.

📚 **Abgrenzung Git Flow:** strukturierteres Modell mit langlebigen Branches `master` (Produktion), `develop` sowie `feature/*`, `release/*` und `hotfix/*`. Geeignet für geplante Releases und mehrere parallel gepflegte Versionen, aber schwergewichtiger. GitHub Flow ist einfacher und schneller.

### 7.4 Arbeitsaufträge Unit 06

**Grundlagen** (Web-UI, ✍️ mit CLI-Entsprechung):

| Schritt | Web-UI | Git-CLI |
|---|---|---|
| Account und Repo `IPSO_2024_XxYy` | *New repository* (mit README) | `gh repo create` bzw. `git init` |
| README erstellen | *Add a README* | `echo "# Titel" > README.md` |
| Branch erstellen | Branch-Dropdown → *Create branch* | `git switch -c feature/test` |
| Leere Datei im Branch | *Add file → Create new file* → Commit auf Branch | `New-Item leer.txt; git add .; git commit -m "Leere Datei"; git push -u origin feature/test` |
| Branch in `main` mergen | *Compare & pull request* → *Merge pull request* | `git switch main; git merge feature/test; git push` |

**Pull Request erzwingen: Was muss konfiguriert werden?**
- *Settings → Branches → Add branch protection rule* (oder neuer: *Settings → Rules → **Rulesets***) für das Muster `main`:
  - ☑ **Require a pull request before merging**
  - ☑ **Require approvals** (z. B. 1). Optional: bestehende Approvals bei neuen Commits verwerfen, Review durch Code Owners, alle Konversationen aufgelöst, Status Checks (CI) grün.
  - ☑ **Do not allow bypassing** (gilt auch für Admins)
- 🔎 ⚠️ **Wichtig:** Branch-Schutz/Rulesets werden bei **privaten Repos auf GitHub Free** (persönliches Konto) **nicht durchgesetzt**. Das funktioniert nur bei **öffentlichen** Repos oder mit GitHub **Pro/Team/Enterprise**. Ausserdem kann der Autor seinen **eigenen PR nicht selbst genehmigen**, es braucht also einen zweiten Collaborator.

**Kollegen einladen: Welche Berechtigungen?**
- Bei einem **persönlichen Repo** kann **nur der Owner** Collaborators einladen: *Settings → Collaborators → Add people*. Eingeladene bekommen **Lese- und Schreibrechte (Push)**: Sie können Issues/PRs erstellen, mergen, Releases anlegen. Admin-Funktionen (Sichtbarkeit, Löschen, Branch-Schutz) bleiben beim Owner.
- 🔎 In **Organisationen** gibt es feinere Rollen: **Read**, **Triage**, **Write**, **Maintain**, **Admin**.

**Pull Request mit Kommentaren:** PR öffnen → Reviewer im Tab *Files changed* → Zeilenkommentare oder *Suggestions* → *Review changes* → **Request changes** (Änderungen gewünscht) / *Comment* / **Approve**. Neue Commits auf dem Branch aktualisieren den PR automatisch.

**GitHub-Skills-Übungen** (Folie 18): *hello-github-actions*, *code-with-codespaces*, *copilot-codespaces-vscode*, *deploy-to-azure*.

🔎 **GitHub Actions** = CI/CD direkt in GitHub. **Workflows** sind YAML-Dateien in `.github/workflows/`, ausgelöst durch **Events** (`push`, `pull_request`, Zeitplan, manuell). Sie bestehen aus **Jobs** mit **Steps** und laufen auf **Runnern** (von GitHub gehostet oder selbst gehostet).

```yaml
name: Bicep prüfen
on: [pull_request]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: az bicep build --file main.bicep
```

🔎 **Codespaces** = vollständige Entwicklungsumgebung (VS Code) in der Cloud, definiert per `devcontainer.json`. **Copilot** = KI-Paarprogrammierer in der IDE, im Chat und als Agent.

**Einsatz im Unternehmen (Diskussion):**
- **Pro:** Standard der Branche, Zusammenarbeit und Reviews, CI/CD integriert, Security-Scanning, Copilot, IaC-Versionierung (Bicep, Skripte)
- **Contra/Abklärungen:** Cloud-Dienst (Datenstandort, Compliance, Schutz von Geheimnissen), Kosten pro Benutzer, Know-how. Alternativen: Azure DevOps, GitLab (auch selbst gehostet), GitHub Enterprise Server (on-prem).

### 7.5 🛠️ Störungsbehebung GitHub/Git

| Fehlerbild | Ursache | Lösung |
|---|---|---|
| `! [rejected] … (fetch first)` / non-fast-forward | Remote hat neuere Commits | `git pull --rebase`, dann `git push` |
| `protected branch hook declined` | direkter Push auf geschützten `main` | Branch erstellen und PR öffnen |
| Merge-Konflikt | dieselben Zeilen in beiden Branches geändert | Konfliktmarker (`<<<<<<<`, `=======`, `>>>>>>>`) bereinigen, `git add`, `git commit` (bzw. im Web-Editor lösen) |
| Authentifizierung scheitert (HTTPS) | Passwort-Login für Git wird nicht mehr akzeptiert (seit 2021) | **Personal Access Token**, **SSH-Key** oder Git Credential Manager |
| PR kann nicht selbst genehmigt werden | Autor ≠ Reviewer | zweite Person als Collaborator einladen |
| Branch-Schutz greift nicht | privates Repo auf GitHub Free | Repo öffentlich machen oder Pro/Team verwenden |
| Geheimnis (Passwort/Key) committet | – | **Secret sofort rotieren**. Das Löschen aus der Historie allein reicht nicht. Push Protection/Secret Scanning aktivieren. |
| Commits mit falschem Autor | lokale Git-Konfiguration | `git config --global user.name/user.email` |

---

<a id="ki"></a>
## 8. Unit 07 – Generative KI, Microsoft Foundry, Security Copilot

### Lernziele

Die Technikerinnen und Techniker HF …
- verstehen, was **generative KI** und **Sprachmodelle** sind und welche Rolle OpenAI-Modelle in Anwendungen spielen,
- kennen **Microsoft Foundry** als Plattform, um KI-Modelle bereitzustellen, zu testen und Agenten zu bauen,
- kennen **Microsoft Security Copilot** und können erklären, wie KI den IT- und Security-Betrieb unterstützt,
- können in Foundry ein Modell bereitstellen, im **Playground** testen und die wichtigsten **Fehlerquellen** benennen.

### 8.1 Grundlagen generative KI

**Whiteboard-Übersicht (Folie 6):**
- **KI** imitiert menschliches Verhalten. **Generative KI** erzeugt **neue Originalinhalte**: natürliche Sprache, Code, Bilder.
- **LLM:** Prompt in natürlicher Sprache → LLM sagt das nächste Wort voraus (**Inferenz**), wiederholt bis zur fertigen Antwort.
- **Training:** Daten + GPUs + Zeit → neuronales Netz mit **Milliarden/Billionen Parametern** (mehr Parameter bedeuten mehr Fähigkeiten) → **Transformer-Modell**. Es kann Text zusammenfassen, erzeugen und vergleichen.
- **Verarbeitung:** Prompt (Text) → **Tokens** → **Embedding-Modell** (z. B. ada-002, 1536 Dimensionen) → **Vektoren** → **Positional Encoding** → **Self-Attention** (Query/Key/Value) → Feed Forward (N-mal wiederholt) → Repräsentation.
- **Prompt Engineering:** explizit sein, sagen wie die KI agieren soll, **Zero-Shot** (ohne Beispiele) vs. **Few-Shot** (mit Beispielen), **Grounding** mit eigenen Daten.
- **Verantwortungsvolle KI:** **Identify → Measure → Mitigate → Operate** (Risiken identifizieren, messen, mindern, im Betrieb überwachen).
- **OpenAI/Microsoft:** **GPT** = *Generative Pre-trained Transformer* (Kontext: GPT-3.5 4K/16K, GPT-4 8K/32K, GPT-4 Turbo 128K Tokens). ChatGPT = GPT + Training auf Interaktion. **Azure OpenAI** bietet GPT, Embeddings und DALL·E mit **RBAC** und **privatem Netzwerk**, dazu ein Studio (Playground: ausprobieren, Deploy) → API → App. Anbindung eigener Daten über Azure AI Search (Blob, DB, Data Lake), Semantic Kernel. **Copilot** ist der **Orchestrator** mit Grounding in Microsoft Graph (M365), Bing oder Security-Daten (Sentinel).

**Recherchefragen (Folien 12–15)**

| Frage | Antwort |
|---|---|
| **Was ist generative KI? 3 Beispiele mit OpenAI-Modell** | KI, die **neue Inhalte erzeugt** (Text, Bild, Audio, Video, Code), indem sie Muster aus grossen Datenmengen lernt. Beispiele: 1. **Text/Chat/Code**: GPT-5-Familie (ChatGPT, GitHub Copilot, M365 Copilot), 2. **Bilder**: gpt-image / DALL·E, 3. **Sprache→Text**: Whisper, **Video**: Sora |
| **Was ist ein LLM, was ein Token?** | **LLM** (Large Language Model): neuronales Netz, mit sehr viel Text trainiert, sagt das **wahrscheinlichste nächste Token** voraus. Kann verstehen, zusammenfassen, übersetzen, erzeugen. **Token**: kleinste Einheit, mit der das Modell arbeitet (Wortteil, Wort, Satzzeichen). Englisch ca. 4 Zeichen pro Token, Deutsch meist mehr Tokens pro Wort. Tokens begrenzen das **Kontextfenster** und bestimmen die **Abrechnung**. |
| **ChatGPT vs. Azure OpenAI in Foundry** | **ChatGPT** = Endnutzer-Dienst von OpenAI (Web/App), Daten bei OpenAI, OpenAI-Konten. **Azure OpenAI in Foundry Models** = dieselben Modelle als **Azure-Dienst im eigenen Abo**: **Entra ID + RBAC**, **Private Endpoints**, **Datenresidenz** (z. B. Switzerland North), Azure-Verträge/Compliance. **Eingaben werden nicht zum Training verwendet.** Zugriff per API/SDK oder Foundry-Portal. Gedacht für eigene Firmenanwendungen. |
| **Copilot vs. KI-Agent** | **Copilot** = KI-Assistent, der **unterstützt** (Chat, Vorschläge, Inhalte), der Mensch bleibt am Steuer (M365 Copilot, GitHub Copilot, Security Copilot). **Agent** = erhält ein **Ziel**, **plant mehrere Schritte**, nutzt **Tools und Daten** (Suche, APIs, Ticketsystem) und führt Aufgaben **teil- oder vollautonom** aus, innerhalb von Leitplanken (Foundry Agent Service, Security Copilot Agents). **Merksatz: Copilot = assistiert, Agent = erledigt.** |

**Sprachmodelle: Encoder und Decoder (Folie 7, 📚)**
1. Trainingsdaten (viel Text) → 2. **Encoder** erzeugt **Embeddings** (Vektoren mit semantischer Bedeutung) → 3. Vokabular mit Vektoren (dog [10,3,2], cat [10,3,1], puppy [5,2,1], skateboard [-3,3,2]) → 4. **Decoder** nutzt die Embeddings, um das **nächste Token** vorherzusagen → 5. «When my dog was …» → «… a puppy».
- **Encoder** (Repetitionsfrage Unit 08): wandelt Tokens mithilfe von **Attention** in **Embeddings** um, also Vektoren, die Bedeutung und Kontext eines Tokens enthalten.
- **Decoder**: erzeugt aus dem Kontext (Prompt + bisher erzeugte Tokens) **Token für Token die Ausgabe**. Er nutzt **Masked Attention** (sieht nur vorangehende Tokens) und ein Feed-Forward-Netz, um das wahrscheinlichste nächste Token zu bestimmen.
- 🔎 Das ist das vereinfachte Lernmodell aus MS Learn. GPT-Modelle sind in der Praxis **reine Decoder-Modelle** («decoder-only»).

**Embeddings (Folie 8):** Tokens werden als Punkte in einem **Vektorraum** dargestellt. Semantisch ähnliche Begriffe liegen **nahe beieinander** (Dog, Cat, Bark, Meow), unähnliche weit weg (Skateboard). Die Ähnlichkeit misst man mit der **Kosinus-Ähnlichkeit** (📚). Grundlage für Vektorsuche und RAG. ⚠️ Die Vektorwerte für «Skateboard» unterscheiden sich zwischen Folie 7 und 8. Die Zahlen sind nur illustrativ.

**Attention (Folie 9, 📚):** Für jedes Token wird gewichtet, **wie stark die umgebenden Tokens es beeinflussen**. Beispiel «I heard a dog **bark**»: «heard» und «dog» bekommen mehr Gewicht als «I» oder «a». **Multi-Head Attention** betrachtet mehrere Aspekte parallel. **Positional Encoding** bringt die Reihenfolge der Tokens ein.

### 8.2 OpenAI und Microsoft (Folie 10)

- **OpenAI** (gegründet 2015) entwickelt GPT, DALL·E, Whisper und Sora. **ChatGPT** (2022) hat generative KI für alle zugänglich gemacht.
- **Microsoft** ist seit **2019** strategischer Partner und Investor. Die OpenAI-Modelle laufen auf Azure.
- **«Azure OpenAI in Foundry Models»:** dieselben Modelle im eigenen Azure-Abo, mit Entra ID, RBAC, privaten Netzwerken und Datenresidenz.
- **Modellfamilien:** GPT-5 (Chat und Reasoning), gpt-image (Bilder), Whisper/gpt-audio (Sprache), text-embedding (Vektoren für Suche/RAG).
- **Abrechnung pro Token** (Eingabe + Ausgabe). **Deployment-Typen:** Standard, Global Standard, **Provisioned** (reservierte Kapazität, PTU).
- **Datenschutz:** Ein- und Ausgaben in Azure werden **nicht zum Trainieren** verwendet. Das ist der wichtige Unterschied zu ChatGPT Free/Plus.

🔎 **Deployment-Typen und Datenverarbeitung** (wichtig für Schweizer Firmen):

| Typ | Verarbeitung | Abrechnung |
|---|---|---|
| **Global Standard** (Standardempfehlung) | in **beliebiger** Azure-Region | pro Token |
| **Data Zone Standard/Provisioned** | nur innerhalb der Datenzone (**EU**, US, APAC). Die EU-Zone folgt der EU Data Boundary und kann die Schweiz einschliessen. | Token bzw. PTU |
| **Standard / Regional Provisioned** | innerhalb der gewählten **Azure-Geografie** (z. B. Schweiz) | Token bzw. PTU |
| **Global/Data Zone Batch** | asynchron, Ziel 24 h, **50 % günstiger** | pro Token |

Daten *at rest* bleiben immer in der gewählten Geografie.

### 8.3 Prompting und das 4D-Framework

**Gute Prompts (Folie 16, 📚):** Beispiel *«Summarize the key considerations for adopting Copilot¹ described in this document² for a corporate executive³. Format the summary as no more than six bullet points with a professional tone⁴.»* Es enthält ¹ Aufgabe/Thema, ² Quelle/Kontext, ³ Zielgruppe, ⁴ Format und Ton.
Der Copilot schickt dem Sprachmodell die **System Message** («You are a helpful assistant …») + den **Gesprächsverlauf**⁵ + den **aktuellen Prompt**.
- **System-Prompt:** legt Rolle, Verhalten, Ton und Grenzen fest (von der App gesetzt)
- **User-Prompt:** konkrete Frage/Anweisung
- **RAG** (Retrieval-Augmented Generation): passende Dokumente suchen und dem Prompt mitgeben → Antwort ist **gegroundet**
- **Tipps:** klar und spezifisch, **Kontext** (Thema, Publikum), **Beispiele**, **Struktur** verlangen (Liste, Tabelle)

**4D-Framework – AI Fluency (Anthropic, Folie 17):** AI Fluency heisst, KI **effektiv, effizient, ethisch und sicher** einsetzen, nicht nur «einen Prompt schreiben».

| D | Frage | Inhalt |
|---|---|---|
| **1. Delegation** | Was mache ich selbst, was gebe ich der KI? | Problem, Plattform und Eignung der Aufgabe kennen |
| **2. Description** | Ziel, Kontext, Format klar beschreiben | Produkt, Prozess und Performance-Erwartungen formulieren |
| **3. Discernment** | Ergebnis kritisch prüfen: Stimmt das? | Output bewerten, iterativ verbessern (Feedback-Schlaufe mit Description) |
| **4. Diligence** | Verantwortung, Datenschutz, Transparenz | für das Ergebnis geradestehen, offenlegen, sorgfältig einsetzen |

**Drei Arten der Zusammenarbeit:** **Automation** (KI führt einen Auftrag aus), **Augmentation** (Mensch und KI denken gemeinsam), **Agency** (KI arbeitet selbstständig im gesetzten Rahmen, z. B. Agents). Die 4D gelten für alle drei und für ChatGPT, Foundry-Agenten und Security Copilot gleichermassen.

✍️ **Arbeitsauftrag «Prompt erstellen» – Beispiel:**
- *Schlechter Prompt:* «Schreib mir ein PowerShell-Skript für Benutzer.»
- *Guter Prompt nach 4D:*
  - **Delegation/Rolle:** «Du bist erfahrener Windows-Server-Administrator.»
  - **Description (Ziel, Kontext, Format):** «Erstelle ein PowerShell-7-Skript, das aus `users.csv` (Spalten Vorname, Nachname, Abteilung) AD-Benutzer in der OU `OU=Staff,DC=contoso,DC=local` anlegt. Mit Fehlerbehandlung (try/catch) und Logdatei. Kommentare auf Deutsch. Ausgabe als ein Codeblock plus kurze Erklärung.»
  - **Discernment:** «Weise auf Annahmen hin und nenne, wie ich das Skript zuerst gefahrlos teste (`-WhatIf`).»
  - **Diligence:** keine echten Namen oder Passwörter im Prompt, das Ergebnis vor dem Einsatz reviewen

🔎 **Microsofts Prinzipien für verantwortungsvolle KI:** Fairness, Zuverlässigkeit und Sicherheit, Datenschutz und Sicherheit, Inklusion, Transparenz, Verantwortlichkeit.

### 8.4 Microsoft Foundry

**Was ist Microsoft Foundry?** (Folie 20)
- Microsofts Plattform, um **KI-Anwendungen und Agenten in Azure zu bauen, bereitzustellen und zu betreiben**. Namenshistorie: **Azure AI Studio → Azure AI Foundry → Microsoft Foundry** (laut Folie seit Nov. 2025). 🔎 Die Azure AI Services heissen jetzt *Foundry Tools*, das alte Portal *Foundry (classic)*.
- Zugriff über das Portal **ai.azure.com**, SDKs (Python, .NET, JavaScript, Java), CLI und die Foundry-Erweiterung für VS Code
- **Modellkatalog** mit laut Folie über 11 000 Modellen (🔎 MS-Doku: «mehr als 10 000»): OpenAI (GPT-5), Anthropic (Claude), Meta (Llama), Mistral, DeepSeek, Microsoft (Phi, MAI). Ein Portal, ein Vertrag, eine Abrechnung.
- **Bausteine:** Modell-Deployments, **Playground**, **Foundry Agent Service**, **Foundry IQ** (Wissen/RAG), Evaluations & Observability, **Content Safety**
- **Foundry Local:** ausgewählte Modelle **lokal** auf Windows, macOS oder Azure Local ausführen, auch ohne Internet
- **Kosten:** Azure-Verbrauch (Tokens, Compute, Speicher), **keine Plattformgebühr**

**Aufbau (Folie 21):** **Azure-Abo → Foundry-Ressource → Projekt → Modell-Deployment → Endpoint + Entra ID/Key → App/Agent**

| Begriff | Erklärung |
|---|---|
| **Foundry-Ressource** | Azure-Ressource (Ressourcengruppe, Region): liefert Modelle, Netzwerkeinstellungen (Private Endpoint), Abrechnung und RBAC-Basis. **Nachfolgerin der Azure-OpenAI-Ressource.** |
| **Projekt** | Arbeitsbereich **innerhalb** der Ressource: bündelt Deployments, Agenten, Daten, Verbindungen (z. B. Azure AI Search, Storage) und Evaluations eines Vorhabens. Zugriff und Kosten pro Projekt (Team/Anwendung) nachvollziehbar. |
| **Modell** | trainiertes KI-Modell aus dem Katalog (z. B. *gpt-5-mini*, Version xyz), gehört dem Anbieter, von Microsoft gehostet |
| **Deployment** | **bereitgestellte Instanz** eines Modells in meiner Ressource: eigener **Name**, fixe **Version**, **Deployment-Typ**, **Quota** (Tokens pro Minute, TPM), Content-Filter. **Apps rufen den Deployment-Namen auf, nicht das Modell.** So lässt sich die Modellversion wechseln, ohne die App anzupassen. |
| **Zugriff** | Endpoint-URL + **API-Key** oder (empfohlen) **Entra ID** mit Rolle **«Azure AI User»**. **Content-Filter** prüfen Ein- und Ausgabe. |
| **Agent** | Modell + **Anweisungen** (System-Prompt) + **Tools** (Dateisuche, Websuche, Code Interpreter, eigene APIs/**MCP**) + optional **Wissen** (Foundry IQ) und **Memory** |
| **Foundry Agent Service** | verwalteter Dienst, der Agenten **hostet und ausführt**: Sitzungen, Tool-Aufrufe, Sicherheit (Entra Agent ID), Monitoring, Skalierung. Kein eigener Server nötig. Veröffentlichung in Apps, Teams oder M365 Copilot. 🔎 *Prompt Agents* (deklarativ, im Portal) vs. *Hosted Agents* (eigener Code im Container, z. B. mit Microsoft Agent Framework oder LangGraph). |
| **RAG** | Retrieval-Augmented Generation: vor der Antwort **passende Dokumente aus eigenen Daten suchen** (Embeddings/Vektorsuche) und dem Prompt mitgeben → Antwort mit Firmenwissen |
| **Foundry IQ** | Wissensschicht: Quellen (SharePoint, Blob Storage, Azure AI Search, Web) als **Knowledge Base** anbinden. Suche **und Berechtigungen** übernimmt der Dienst, keine eigene RAG-Pipeline nötig. Nutzen: aktuelle, firmenspezifische, **nachvollziehbare** Antworten (mit Quellen), **weniger Halluzinationen**, ohne das Modell neu zu trainieren. |

**Arbeitsauftrag Foundry** (MS-Learn-Übung *Get started with AI in Azure*, 45 Min.): Foundry-Projekt erstellen → Modell bereitstellen (z. B. gpt-5-mini) → im Playground testen → als **Agent** speichern (Anweisungen auf Deutsch, Rolle «IT-Helpdesk», ein Tool) → notieren: **Deployment-Name, Endpoint, verwendete Rolle** und einen **provozierten und behobenen Fehler**. Optional: Deployment per Python-/.NET-Beispiel aufrufen.

**🛠️ Typische Störungen (Folie 21 + 🔎)**

| Fehler | Ursache | Lösung |
|---|---|---|
| **429** Too Many Requests | **Quota/TPM erschöpft**, Rate Limit | warten/Retry mit Backoff, Quota erhöhen, anderer Deployment-Typ/andere Region, Provisioned |
| **401** Unauthorized | falscher/abgelaufener **API-Key** oder Token | Key/Token prüfen |
| **403** Forbidden | **fehlende RBAC-Rolle** (z. B. *Azure AI User*), Netzwerkregeln/Private Endpoint blockieren | Rolle zuweisen, Netzwerkzugriff prüfen |
| **404** Not Found | **falscher Deployment-Name**, falscher Endpoint oder API-Pfad/-Version | Deployment-Namen (nicht Modellnamen) verwenden, Endpoint prüfen |
| Antwort blockiert (`content_filter`) | **Content-Filter** schlägt bei Ein- oder Ausgabe an | Prompt anpassen, Filterkonfiguration prüfen (verantwortungsvoll) |
| Modell/Typ nicht wählbar | **Modell in der Region nicht verfügbar**, Typ nicht unterstützt | andere Region oder anderen Deployment-Typ wählen |

### 8.5 Microsoft Security Copilot

**Was ist Security Copilot und für wen?** (Folien 30, 33)
- **Generative KI für Security- und IT-Teams**: Vorfälle untersuchen, Signale zusammenfassen, **Skripte erklären**, **KQL-Abfragen schreiben**, Berichte erstellen, in natürlicher Sprache. Wiederkehrende Aufgaben werden über **Agents** automatisiert.
- **Zielgruppen:** SOC-Analysten (Defender, Sentinel), Identitäts-Admins (Entra), Endpoint-Admins (Intune), Compliance-Teams (Purview)
- **Technische Basis:** OpenAI-Modelle in Azure + **Microsoft Threat Intelligence** + **Daten des eigenen Tenants**

**Standalone vs. Embedded**

| | **Standalone** | **Embedded** |
|---|---|---|
| Wo | eigenes Portal **securitycopilot.microsoft.com** | **direkt in den Admin-Portalen**: Defender XDR, Entra, Intune, Purview, Sentinel |
| Was | Chat, **Promptbooks**, Agent-Übersicht, **Agent Builder**, produktübergreifende Sicht (Defender, Entra, Intune, Purview und Drittanbieter-Plugins in einer Sitzung) | z. B. Incident-Zusammenfassung in Defender XDR, **Skript-Analyse** in Intune, Risiko-Zusammenfassung in Entra, Agents im jeweiligen Produkt |
| Gemeinsam | gleiche Kapazität (SCU) und gleiche Berechtigungen. Embedded ist im Alltag meist der schnellere Einstieg. | |

**Bausteine**

| Baustein | Erklärung |
|---|---|
| **Prompts** | einzelne Anfragen in natürlicher Sprache |
| **Promptbooks** | gespeicherte, **wiederverwendbare Abfolgen von Prompts** für einen Anwendungsfall (z. B. «Incident untersuchen», «verdächtiges Skript analysieren»), von Microsoft oder selbst erstellt |
| **Plugins** | **Verbindungen zu Datenquellen/Diensten**: Microsoft (Defender, Entra, Intune, Purview, Sentinel) und Drittanbieter (z. B. ServiceNow). Sie bestimmen, **welche Informationen** Copilot abfragen kann. |
| **Agents** | KI-Workflows, die eine Aufgabe **mehrschrittig und (teil-)autonom** bearbeiten. Sie laufen im Produkt, haben eine **eigene Identität (Entra)**, **schlagen vor bzw. bereiten vor**. Freigabe und Verantwortung bleiben beim Menschen. |

**Agents (Folie 31):**
- **Defender:** Phishing Triage Agent (bewertet gemeldete Mails), Alert Triage, Threat Intelligence Briefing Agent
- **Entra:** Conditional Access Optimization Agent (findet Lücken in CA-Richtlinien), Access Review Agent
- **Intune:** Policy Configuration Agent (Baseline-Dokument → Richtlinie), Vulnerability Remediation Agent, Device Offboarding Agent, Change Review Agent
- **Purview:** Alert Triage Agents für DLP und Insider Risk
- **Eigene Agents:** No-Code **Agent Builder** oder Entwicklung über **MCP/Graph APIs**, dazu Partner-Agents aus dem Katalog
- **Betrieb:** Agent-Identität in Entra, Empfehlungen überwachen, **SCU-Verbrauch** im Blick behalten

**Berechtigungen:** Security Copilot handelt **«on behalf of»**: Er sieht nur, was die angemeldete Person in den Quellprodukten sehen darf. Eigene Rollen: **Copilot Owner** und **Copilot Contributor**. **Es gibt keine Benutzerlizenz.**

**Lizenzierung – Security Compute Units (SCU):**
- **SCU** = Recheneinheit. Jeder Prompt, jedes Promptbook und jeder Agent-Lauf verbraucht SCUs. Die Kapazität gilt pro Tenant bzw. Arbeitsbereich, der Verbrauch wird überwacht.
- **Mit Microsoft 365 E5/E7 inklusive** (Folie: «seit 2026»; 🔎 Rollout ab **18.11.2025**, gestaffelt): **400 SCU pro Monat pro 1000 bezahlte Benutzerlizenzen**, max. **10 000 SCU/Monat**. Beispiel: 400 Lizenzen → 160 SCU/Monat. Die Menge verfällt monatlich (kein Übertrag). Die Bereitstellung erfolgt automatisch.
- **Ohne E5/E7:** SCU-Kapazität als **Azure-Ressource stundenweise** buchen (provisioniert, 🔎 ca. USD 4 pro SCU-Stunde) bzw. Overage.

**Arbeitsauftrag Security Copilot** (MS Learn *security-copilot-interactive-guides*, 45 Min.): interaktive Simulationen durcharbeiten (Standalone, Defender XDR Incident, Purview, Agents), drei sinnvolle Prompts/Promptbooks mit Begründung notieren, einen Agent beschreiben (Was macht er? Welche Daten? Wer gibt frei?).

✍️ **Beispielantwort «Welche Aufgabe würdet ihr einem Agent übergeben?»** Die **Triage von Phishing-Meldungen** durch Benutzer.
- **Darf:** Mails lesen und klassifizieren, Header/URLs/Anhänge analysieren, ähnliche Mails suchen, eine Empfehlung mit Begründung erstellen, Ticket aktualisieren.
- **Darf auf keinen Fall ohne Freigabe:** Mails tenantweit löschen, Konten sperren, Passwörter zurücksetzen, Regeln ändern. Freigabe durch den SOC-Analysten, Protokollierung aller Aktionen, Least Privilege für die Agent-Identität.

---

<a id="bicep"></a>
## 9. Unit 08 – Infrastructure as Code mit Bicep

**Agenda Unit 08:** Repetition IaC → IaC & Bicep → Bicep-Crashkurs (YouTube-Video) → Bicep-Template verstehen → Selbststudium «Bicep ausprobieren» → Repetition/Prüfungsvorbereitung in 5 Gruppen → Abschluss.

### 9.1 Infrastructure as Code (IaC)

**Definition (Folie 6):** Infrastruktur wird **als Code beschrieben** statt manuell über eine Oberfläche eingerichtet. Beispiele: VMs, Netzwerke, Storage Accounts, Datenbanken, Berechtigungen.
Grundidee: **Code → Azure → Infrastruktur**. «Wir beschreiben den **gewünschten Zustand**, Azure setzt ihn um.»

**Folie 5:** Das Template liegt in **GitHub** oder **Azure DevOps** und erzeugt z. B. einen **App Service Plan**, eine **App Service App** und **Application Insights**.

**Manuell vs. IaC (Folie 7):**
- Manuell: Azure-Portal → Ressource wählen → Einstellungen → Erstellen (für jede Ressource, jedes Mal)
- IaC: **Bicep-Datei → Deployment starten → Azure erstellt die Ressourcen**

| **Vorteile von IaC** (Folie + 🔎) | **Nachteile / Herausforderungen** (✍️/🔎) |
|---|---|
| **wiederholbar** und **reproduzierbar** (gleiches Ergebnis bei jedem Deployment, auch für DR) | **Lernaufwand** (Sprache, Tools, Git, Pipelines) |
| **automatisierbar** (CI/CD-Pipelines) | **Initialaufwand** höher als ein schneller Klick im Portal |
| **dokumentiert** (der Code ist die Doku) | Fehler im Template werden **multipliziert** (in allen Umgebungen) |
| **Änderungen nachvollziehbar** (Git-Historie, Reviews per PR) | **Drift**: Manuelle Änderungen im Portal weichen vom Code ab |
| **im Team nutzbar** | Umgang mit **Geheimnissen** braucht Disziplin (Key Vault, `@secure`) |
| **weniger manuelle Fehler**, einheitliche Standards | Tool-/API-Versionen müssen gepflegt werden |
| 🔎 mehrere Umgebungen (Dev/Test/Prod) gleich aufbauen, Konfigurationsdrift vermeiden | Debugging von Deployments manchmal aufwendig |

### 9.2 Imperativ vs. deklarativ

| | **Imperativer Code** | **Deklarativer Code** |
|---|---|---|
| Was? | beschreibt Schritt für Schritt, **WIE** etwas gemacht wird | beschreibt, **WAS** am Ende vorhanden sein soll (Soll-Zustand) |
| Beispiel | «Erstelle Ordner → installiere Software → ändere Konfiguration.» | «Ich möchte einen Webserver mit diesen Eigenschaften.» |
| Wo verwendet? | **Python, PowerShell, Bash, Java, C#** | **Bicep, Terraform, ARM-Templates, Kubernetes-YAML, SQL** (auch PowerShell DSC) |
| Typischer Einsatz | Skripte, Programme, Automatisierung von Abläufen | IaC, Cloud-Infrastruktur, Konfigurationen |

✍️ Beispiel für denselben Storage Account:

```powershell
# imperativ (Azure PowerShell): Befehle der Reihe nach, Logik für "existiert schon?" selbst schreiben
New-AzResourceGroup -Name rg-demo -Location switzerlandnorth
New-AzStorageAccount -ResourceGroupName rg-demo -Name hfinfdemo12345 `
  -Location switzerlandnorth -SkuName Standard_LRS -Kind StorageV2
```

```bicep
// deklarativ (Bicep): Soll-Zustand beschreiben, beliebig oft ausführbar (idempotent)
resource storage 'Microsoft.Storage/storageAccounts@2023-05-01' = {
  name: 'hfinfdemo12345'
  location: 'switzerlandnorth'
  sku: { name: 'Standard_LRS' }
  kind: 'StorageV2'
}
```

### 9.3 Azure Resource Manager (ARM), Templates, Provider, Ressourcen-IDs

**ARM (Folie 33):** Die **Verwaltungsschicht (Control Plane) von Azure**. **Alle** Werkzeuge (Azure-Portal, Azure PowerShell, Azure CLI, REST-Clients, über SDKs) senden ihre Anfragen an ARM. ARM **authentifiziert/autorisiert** (Entra ID, RBAC) und leitet an die **Resource Provider** weiter (Storage, Web App, VM, …). Dadurch sind Ergebnisse unabhängig vom Tool gleich. Dazu kommen RBAC, Tags, Locks und Policy.
🔎 **Control Plane** (Ressourcen verwalten, über `management.azure.com` = ARM) vs. **Data Plane** (Daten in der Ressource nutzen, z. B. Blob lesen).

**Recherchefragen Bicep (Folie 36):**

| Frage | Antwort |
|---|---|
| **Was ist ARM im Kontext von Azure?** | Azure Resource Manager: der Bereitstellungs- und Verwaltungsdienst, über den alle Ressourcen erstellt, geändert und gelöscht werden (siehe oben) |
| **Was sind ARM-Templates, in welcher Sprache?** | Dateien, die Azure-Ressourcen **deklarativ** beschreiben, in **JSON** (Aufbau: `$schema`, `contentVersion`, `parameters`, `variables`, `functions`, `resources`, `outputs`). Bicep ist eine einfachere Sprache, die zu ARM-JSON **transpiliert** wird. |
| **Was sind Resource Providers?** | Sammlungen von REST-Operationen für einen Azure-Dienst, z. B. **`Microsoft.Storage`**, `Microsoft.Compute`, `Microsoft.KeyVault`. Sie definieren die Ressourcentypen (**`{Provider}/{Typ}`**, z. B. `Microsoft.Storage/storageAccounts`). Ein Provider muss im Abo **registriert** sein (`Register-AzResourceProvider`, `az provider register`; Recht `/register/action`, in Contributor/Owner enthalten). Bei Bicep/ARM-Deployments werden die Provider aus dem Template automatisch registriert. |
| **Was ist die eindeutige Identifikation einer Ressource?** | die **Ressourcen-ID** |
| **Aus welchen Teilen besteht sie?** | `/subscriptions/{Abo-ID}/resourceGroups/{Ressourcengruppe}/providers/{Provider-Namespace}/{Ressourcentyp}/{Ressourcenname}` |
| **Was sind Child Resources?** | Ressourcen, die **nur im Kontext einer übergeordneten Ressource** existieren, z. B. **Subnetz** im VNet, **Blob-Container** bzw. **File Share** im Storage Account, **Datenbank** auf einem SQL-Server, VM-Extension an einer VM. Name: `{parent}/{child}`, Typ: `{Provider}/{parentTyp}/{childTyp}`. |

Beispiel-ID eines Storage Accounts und eines Child:

```
/subscriptions/1111-…/resourceGroups/rg-demo/providers/Microsoft.Storage/storageAccounts/hfinfdemo12345
/subscriptions/1111-…/resourceGroups/rg-demo/providers/Microsoft.Storage/storageAccounts/hfinfdemo12345/blobServices/default/containers/logs
```

🔎 Child Resources in Bicep: **verschachtelt** im Parent, **mit `parent:`-Eigenschaft** (empfohlen) oder mit vollem Namen und `dependsOn` (nicht empfohlen):

```bicep
resource blobService 'Microsoft.Storage/storageAccounts/blobServices@2023-05-01' = {
  parent: storage
  name: 'default'
}
resource container 'Microsoft.Storage/storageAccounts/blobServices/containers@2023-05-01' = {
  parent: blobService
  name: 'logs'
}
```

### 9.4 Bicep

**Was ist Bicep?** (Folien 8–9, 📚) Eine **domänenspezifische Sprache für IaC in Azure**. Man beschreibt, **welche** Ressourcen benötigt werden, und Azure übernimmt die Bereitstellung. Ein Bicep-Template ist wie ein **Bauplan** und beschreibt: **Wo?** (Region), **Was?** (Speicher, Netzwerk, Server), **Wie?** (Grösse, Eigenschaften), **Welche Bezeichnung?** (Namen).
📚 Beim Deployment wird die `.bicep`-Datei in ein **ARM-JSON-Template transpiliert** und an ARM übergeben. Bicep ist also eng mit ARM verbunden.
Ablauf (Folie 15): `main.bicep` erstellen → Infrastruktur beschreiben → Bicep wird verarbeitet (transpiliert) → **ARM** → Ressourcen werden erstellt **oder angepasst**.

**Erkenntnisse aus dem Crashkurs (Folie 11):** Bicep = IaC für Azure. Es ist **deklarativ**. Wichtige Elemente: `resource`, `name`, `location`, `properties` sowie Parameter und Variablen. Abhängigkeiten zwischen Ressourcen werden erkannt. **Module** teilen grosse Templates auf und machen Teile wiederverwendbar. Das Template kann **erneut ausgeführt** werden, die Infrastruktur ist damit reproduzierbar und standardisiert.

**Aufbau eines Bicep-Templates (Folie 14):**

| Element | Zweck | Beispiel |
|---|---|---|
| **Parameter** (`param`) | Werte, die **beim Deployment** verändert werden können (Namen, Region, SKU, Umgebung, Credentials) | `param location string = 'switzerlandnorth'` |
| **Variablen** (`var`) | **interne** Werte/Berechnungen im Template (kein Typ nötig) | `var storageName = 'hfinfdemo12345'` |
| **Ressourcen** (`resource`) | die Infrastruktur: **symbolischer Name**, **Typ@API-Version**, Eigenschaften | `resource storage 'Microsoft.Storage/storageAccounts@2023-05-01' = { … }` |
| **Outputs** (`output`) | Werte, die **nach dem Deployment** zurückgegeben werden (keine Secrets!) | `output storageId string = storage.id` |
| **Module** (`module`) | andere Bicep-Datei als wiederverwendbaren Baustein einbinden | `module net 'modules/network.bicep' = { name: 'net', params: { … } }` |

📚 Details:
- **Symbolischer Name** (`storage`) gilt nur im Bicep-File. Der **Ressourcenname** (`name:`) erscheint in Azure.
- **Implizite Abhängigkeit:** Referenziert eine Ressource eine andere (`serverFarmId: appPlan.id`), deployt Bicep in der richtigen Reihenfolge. Explizit geht es mit `dependsOn`.
- **Decorators:** `@allowed([...])`, `@secure()` (Passwörter nicht loggen/ausgeben), `@minLength()`/`@maxLength()`, `@description()`
- **Funktionen/Ausdrücke:** `resourceGroup().location`, `uniqueString(resourceGroup().id)` (deterministisch eindeutig), String-Interpolation `'toylaunch${uniqueString(resourceGroup().id)}'`, Ternär-Operator `(env == 'prod') ? 'Standard_GRS' : 'Standard_LRS'`
- **Module:** Jedes Bicep-File kann ein Modul sein. Ein Modul braucht einen `name` (eigenes Deployment) und `params`. Outputs eines Moduls können Parameter eines anderen sein. Vorteile (Folie 12): übersichtlich und **wiederverwendbar** (z. B. Gesamtlösung → Netzwerk, Speicher, Server, Datenbank). Gute Module haben einen klaren Zweck, sinnvolle Parameter/Outputs, sind möglichst in sich geschlossen und geben **keine Secrets** aus.
- **Azure Verified Modules (AVM)** (Demo): von Microsoft gepflegte, geprüfte Bicep-Module in der öffentlichen Registry, einzubinden mit `module … 'br/public:avm/res/<dienst>/<ressource>:<version>'`. Das spart eigene Module und folgt Best Practices.

**Gute Praxis (Folie 13):** verständlich aufgebaut, **wiederverwendbar**, Änderungen nachvollziehbar (Git), grosse Lösungen in **kleinere Bausteine** (Module), **keine Passwörter im Code** (🔎 `@secure()`-Parameter, Key-Vault-Referenzen), für **verschiedene Umgebungen** einsetzbar (Parameter/Parameterdateien `.bicepparam`). Ziel: Infrastruktur einfach, reproduzierbar und nachvollziehbar bereitstellen.

### 9.5 Beispiel Web-App (Folie 25) und korrigierter Code

Auftrag: «Unsere Firma braucht eine neue Web-App in Azure. Zusätzlich soll überwacht werden, ob die Anwendung funktioniert.» Ohne Bicep legt man die Ressourcen manuell im Portal an. Mit Bicep stehen sie im Code.

⚠️ Der Code auf den Folien 14 und 25 lässt sich so **nicht kompilieren**: Er enthält **typografische Anführungszeichen** (`’` statt `'`, beim Kopieren aus PowerPoint) und auf Folie 25 eine **überzählige schliessende Klammer `}`**. Ausserdem ist `meine-webapp` ein fixer Name, obwohl Web-App-Namen **global eindeutig** sein müssen. Korrigierte und erweiterte Fassung (✍️, inkl. Überwachung mit Application Insights):

```bicep
@description('Azure-Region für alle Ressourcen')
param location string = 'switzerlandnorth'

@allowed([
  'nonprod'
  'prod'
])
param environmentType string = 'nonprod'

var appName = 'webapp-${uniqueString(resourceGroup().id)}'
var appServicePlanSku = (environmentType == 'prod') ? 'P1v3' : 'B1'

resource appPlan 'Microsoft.Web/serverfarms@2023-12-01' = {
  name: 'plan-${appName}'
  location: location
  sku: {
    name: appServicePlanSku
  }
}

resource appInsights 'Microsoft.Insights/components@2020-02-02' = {
  name: 'appi-${appName}'
  location: location
  kind: 'web'
  properties: {
    Application_Type: 'web'
  }
}

resource webApp 'Microsoft.Web/sites@2023-12-01' = {
  name: appName
  location: location
  properties: {
    serverFarmId: appPlan.id            // implizite Abhängigkeit: Plan wird zuerst erstellt
    httpsOnly: true
    siteConfig: {
      appSettings: [
        {
          name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
          value: appInsights.properties.ConnectionString
        }
      ]
    }
  }
}

output webAppUrl string = 'https://${webApp.properties.defaultHostName}'
```

**Deployment** 🔎:

```powershell
# Azure CLI (installiert Bicep automatisch)
az login
az group create --name rg-demo --location switzerlandnorth
az deployment group what-if --resource-group rg-demo --template-file main.bicep    # Vorschau der Änderungen
az deployment group create  --resource-group rg-demo --template-file main.bicep --parameters environmentType=nonprod

# Azure PowerShell (Bicep CLI separat installieren)
Connect-AzAccount
New-AzResourceGroup -Name rg-demo -Location switzerlandnorth
New-AzResourceGroupDeployment -ResourceGroupName rg-demo -TemplateFile main.bicep -environmentType nonprod -WhatIf
New-AzResourceGroupDeployment -ResourceGroupName rg-demo -TemplateFile main.bicep -environmentType nonprod

az bicep build --file main.bicep     # nur transpilieren → main.json (ARM-Template ansehen)
```

🔎 **Deployment-Modi:** *Incremental* (Standard: Ressourcen hinzufügen/ändern, andere in der RG bleiben) vs. *Complete* (was nicht im Template steht, wird **gelöscht**). **Scopes:** Ressourcengruppe (Standard), Abo, Management Group, Tenant (`targetScope = 'subscription'`).

### 9.6 Selbststudium «Bicep einfach ausprobieren»

Schritte: VS Code → Extension **Bicep (Microsoft)** installieren (`Ctrl+Shift+X`) → Ordner `bicep-demo` öffnen → Datei **`main.bicep`** (Endung `.bicep` ist wichtig) → Storage-Account-Ressource einfügen → speichern.

| Zeile | Bedeutung |
|---|---|
| `resource storage` | Wir definieren eine **Ressource** mit dem symbolischen Namen `storage` (nur im Template) |
| `'Microsoft.Storage/storageAccounts@2023-05-01'` | **Ressourcentyp** (Storage Account) und **API-Version** |
| `name: 'hfinfdemo12345'` | Name in Azure. 🔎 Storage-Namen: **3–24 Zeichen, nur Kleinbuchstaben und Ziffern, global eindeutig** |
| `location: 'switzerlandnorth'` | Azure-Region Switzerland North (Zürich) |
| `sku: { name: 'Standard_LRS' }` | Leistungs- und **Redundanzstufe** (LRS = 3 Kopien in einem RZ. 🔎 Weitere: ZRS, GRS, GZRS) |
| `kind: 'StorageV2'` | Kontotyp General Purpose v2 |

- **Region ändern** (`westeurope`) zeigt: Die Infrastruktur wird durch Code beschrieben und lässt sich einfach verändern.
- **Letzte `}` entfernen** → VS Code zeigt sofort einen **Fehler** (Linter). Die Entwicklungsumgebung unterstützt also schon beim Schreiben.
- **Manuell vs. Bicep:** Im Portal sind es rund 8 Klicks (Portal → Storage Account → Create → RG → Name → Region → Redundanz → prüfen → erstellen). Mit Bicep steht die gewünschte Konfiguration direkt im Code.

**Abschlussfragen:**
1. **Was wird mit `resource` beschrieben?** Eine Azure-Ressource (Typ, API-Version, Name, Region, Eigenschaften), die Azure bereitstellen soll.
2. **Warum ist Bicep deklarativ und nicht imperativ?** Man beschreibt den **gewünschten Endzustand**, nicht die Schritte. ARM ermittelt selbst, was zu tun ist (erstellen, ändern, nichts tun). Mehrfaches Ausführen ergibt dasselbe Ergebnis (idempotent).
3. **Vorteil gegenüber dem Portal?** Wiederholbar, versionierbar (Git), dokumentiert, im Team prüfbar (PR), weniger Klickfehler, identisch in mehreren Umgebungen, automatisierbar.

**Weitere Übungen** (MS Learn *Build your first Bicep file*, Folien 43–47): Storage Account + App Service definieren → Parameter und Variablen ergänzen → in **Module** refaktorieren.

### 9.7 🛠️ Störungsbehebung Bicep/ARM

| Fehler | Ursache | Lösung |
|---|---|---|
| Rote Unterstreichung / `BCP…`-Fehler in VS Code | Syntaxfehler, **typografische Anführungszeichen** aus Word/PowerPoint, fehlende Klammer | Linter-Meldung lesen, gerade Hochkommas `'` verwenden, `az bicep build` |
| `StorageAccountAlreadyTaken` / `AccountNameInvalid` | Name schon global vergeben bzw. Grossbuchstaben/Bindestrich/Länge | `uniqueString()` + Präfix, Namensregeln beachten |
| `MissingSubscriptionRegistration` | Resource Provider nicht registriert | `az provider register --namespace Microsoft.X` |
| `AuthorizationFailed` | fehlende RBAC-Rechte auf RG/Abo | Rolle (z. B. Contributor) zuweisen |
| `LocationNotAvailableForResourceType` / SKU nicht verfügbar | Region unterstützt Typ/SKU nicht, Quota | andere Region/SKU, Quota erhöhen |
| `InvalidTemplateDeployment` / API-Version ungültig | falsche Eigenschaften für die API-Version | IntelliSense der Bicep-Extension, Resource-Referenz prüfen |
| Unerwartete Änderungen/Löschungen | Complete-Modus, Drift durch manuelle Änderungen | vorher `what-if`, Incremental verwenden, keine Portaländerungen an IaC-Ressourcen |
| Wo sehe ich Details? | – | Portal → Ressourcengruppe → **Deployments** (Operationen, Fehlermeldung), `az deployment operation group list` |

---

<a id="vorfaecher"></a>
## 10. Repetition der Vorfächer CSIN und SYSI (Räume 1–4)

> Laut Unit 00 wird Wissen aus **CSIN** (Client-/Server-Installation) und **SYSI** (Systemsicherheit) geprüft. Dazu liegt in `Kursmaterialien/` **kein Material**. Dieses Kapitel ist deshalb eine **kompakte Repetition aus Recherche und Grundlagenwissen** (grösstenteils 🔎) entlang der Raum-Themen aus Unit 08.
> Ausführlicher zu CSIN: [CSIN-Zusammenfassung (3. Semester)](<../../../3. Semester/CSIN/CSIN_Client_Server_Installation.md>). Zu SYSI gibt es im Repository noch keine Zusammenfassung.

<a id="raum1"></a>
### 10.1 Raum 1 – Windows, Server und PowerShell

**Windows 10/11**
- **Editionen:** Home, **Pro** (Domänenbeitritt, BitLocker, Gruppenrichtlinien, Hyper-V, RDP-Host), **Enterprise** (u. a. Credential Guard, AppLocker/App Control, LTSC-Varianten), **Education**.
- **Windows 11 – Anforderungen:** 64-Bit-CPU (unterstützte Generation), 4 GB RAM, 64 GB Speicher, **UEFI mit Secure Boot**, **TPM 2.0**.
- **Windows 10 – Supportende 14.10.2025.** Danach Updates nur noch über das kostenpflichtige **Extended Security Updates (ESU)**-Programm (Unternehmen bis max. 3 Jahre, also bis Oktober 2028).
- **Servicing-Kanäle:** *General Availability Channel* (jährliches Feature-Update, monatliche Qualitätsupdates) vs. **LTSC** (Long-Term Servicing Channel, 5–10 Jahre ohne Feature-Updates, für Spezialsysteme). Dazu das Windows Insider Program.
- **Bereitstellung/Migration:** In-Place-Upgrade (Daten und Apps bleiben), Wipe-and-Load/Neuinstallation (Imaging mit MDT/WDS/ConfigMgr, Windows PE), **Autopilot** (ohne Imaging, siehe [4.2](#intune)), Benutzerdaten mit USMT oder OneDrive migrieren. Upgrade = gleiches Gerät, neue Version. Migration = Umzug auf neues Gerät/neue Umgebung.

**Windows Server**
- **Editionen:** **Standard** (2 VMs pro lizenziertem Host) und **Datacenter** (unbegrenzt VMs, zusätzlich z. B. Storage Spaces Direct, SDN). **Lizenzierung pro Core** (min. 8 pro CPU, 16 pro Server) plus **CALs** (Benutzer oder Gerät).
- **Server Core vs. Desktop Experience:** Core ohne GUI, **kleinere Angriffsfläche**, weniger Updates/Neustarts und Ressourcen. Verwaltung remote (WAC, PowerShell, RSAT, `sconfig`). Desktop Experience mit voller GUI. Die Wahl ist bei der Installation zu treffen (kein nachträglicher Wechsel).
- **Aktivierung:** KMS (ab 25 Clients / 5 Servern), MAK, **AVMA** (automatische VM-Aktivierung auf Datacenter-Hyper-V-Hosts), Active-Directory-basierte Aktivierung.
- **Migration:** In-Place-Upgrade (nur unterstützte Pfade), **Rollenmigration** auf neuen Server (z. B. Storage Migration Service für Fileserver, AD per neuem DC + FSMO-Transfer, DHCP-Export/-Import).

**PowerShell**
- **Cmdlets** im Schema **Verb-Nomen** (`Get-Service`, `Set-Item`). Hilfe: `Get-Help <cmd> -Examples`, `Get-Command *dns*`, `Get-Member` (zeigt Eigenschaften/Methoden eines Objekts).
- **Pipeline** `|` übergibt **Objekte** (nicht Text): `Get-Process | Where-Object CPU -gt 100 | Sort-Object CPU -Descending | Select-Object -First 5`
- **Variablen** `$name`, Arrays `@()`, Hashtables `@{}`, automatische Variablen (`$_`, `$PSVersionTable`, `$Error`)
- **Kontrollstrukturen:** `if/elseif/else`, `foreach`, `switch`, Fehlerbehandlung mit `try/catch/finally`
- **Versionen:** Windows PowerShell 5.1 (.NET Framework, nur Windows) vs. **PowerShell 7.x** (`pwsh`, .NET, plattformübergreifend)
- **Remoting:** `Enter-PSSession srv01` (interaktiv), `Invoke-Command -ComputerName srv01,srv02 -ScriptBlock {…}` (1:n), über WinRM (5985/5986) oder SSH
- **Execution Policy** (siehe [10.4](#raum4)): Restricted, AllSigned, **RemoteSigned** (Standard auf Servern), Unrestricted, Bypass

<a id="raum2"></a>
### 10.2 Raum 2 – Active Directory, DNS und DHCP

**AD DS – Aufbau**
- **Forest** (Gesamtstruktur, gemeinsames Schema und globaler Katalog) → **Domänen** (Verwaltungs- und Replikationsgrenze) → **OUs** (Organisation, GPO-Verknüpfung, Delegation). Physisch: **Sites** (Standorte/Subnetze für die Replikation).
- **Domain Controller** hosten die AD-Datenbank (`NTDS.dit`), **Multimaster-Replikation**. **Global Catalog** = Teilkopie aller Objekte des Forests (Suche, Anmeldung, universelle Gruppen).
- **FSMO-Rollen (5):** pro Forest **Schema Master** und **Domain Naming Master**, pro Domäne **RID Master**, **PDC Emulator** (Zeit, Passwortänderungen, Sperrungen, GPO-Bearbeitung) und **Infrastructure Master**. Anzeige: `netdom query fsmo`.
- **Gruppen:** Typ **Sicherheit** vs. **Verteilung**. Bereich **Domänenlokal** (Berechtigungen auf Ressourcen der eigenen Domäne), **Global** (Benutzer der eigenen Domäne bündeln), **Universal** (forestweit, im GC).
- **AGDLP** (Best Practice für Berechtigungen): **A**ccounts → **G**lobale Gruppen (nach Rolle/Abteilung) → **D**omänen**L**okale Gruppen (nach Ressource/Recht) → **P**ermissions. Beispiel: `Anna` → `GG_Buchhaltung` → `DL_Share_Finanzen_RW` → NTFS/Share «Ändern». Vorteil: Personalwechsel = nur Gruppenmitgliedschaft ändern. (Mehrere Domänen: AGUDLP mit universellen Gruppen.)
- **Trusts:** ermöglichen den Zugriff auf Ressourcen einer anderen Domäne ohne neue Anmeldung. Richtung **einseitig/zweiseitig**, **transitiv/nicht transitiv**. Typen: Parent-Child und Tree-Root (automatisch, transitiv, zweiseitig), **Forest Trust**, **External Trust**, Shortcut, Realm. Die vertrauende Domäne stellt Ressourcen bereit, die vertraute Domäne liefert die Konten.
- **GPO-Verarbeitung LSDOU:** **L**okal → **S**ite → **D**omäne → **O**U (die zuletzt angewendete gewinnt). Dazu Vererbung blockieren, «Erzwungen», Sicherheitsfilterung, WMI-Filter. Prüfen mit `gpresult /r` bzw. `/h`, aktualisieren mit `gpupdate /force`.
- **Authentifizierung:** **Kerberos** (Standard, Tickets vom KDC auf dem DC, Zeitabweichung max. 5 Min.) vs. NTLM (Legacy, anfällig für Pass-the-Hash, siehe [6.2](#defender)).

**DNS**
- Aufgabe: Namen ↔ IP-Adressen auflösen. AD **braucht DNS** (DCs finden über SRV-Records).
- **Records:** A (IPv4), AAAA (IPv6), **CNAME** (Alias), **MX** (Mailserver), **PTR** (Reverse), **SRV** (Dienste, z. B. `_ldap._tcp.dc._msdcs`), **NS** (Nameserver), **SOA** (Zonen-Infos, Seriennummer, Timer), TXT (z. B. SPF).
- **Zonen:** Forward-/Reverse-Lookup, **Primär**, **Sekundär** (schreibgeschützte Kopie via Zonentransfer), **Stub**, **AD-integriert** (Replikation über AD, sichere dynamische Updates).
- **Abfragen:** **rekursiv** (Client → DNS-Server: «Gib mir die fertige Antwort») vs. **iterativ** (DNS-Server fragt Root → TLD → autoritativen Server und erhält Verweise). **Forwarder** / **Conditional Forwarder** (bestimmte Domänen an bestimmte Server).
- **TTL** (Time to Live): Wie lange ein Resolver eine Antwort **cachen** darf. Tiefe TTL = Änderungen schneller sichtbar, aber mehr Abfragen. Vor Migrationen TTL senken.
- **Aging/Scavenging:** veraltete dynamische Einträge automatisch entfernen.
- **Diagnose:** `nslookup`, `Resolve-DnsName srv01.contoso.local -Type A`, `ipconfig /flushdns`, `ipconfig /displaydns`, `Clear-DnsClientCache`.

**DHCP**
- **DORA-Prozess:** **D**iscover (Client, Broadcast) → **O**ffer (Server) → **R**equest (Client, Broadcast) → **A**cknowledge (Server). Ports **UDP 67 (Server) / 68 (Client)**.
- **Lease-Erneuerung:** nach **50 %** der Lease-Dauer (T1) Unicast-Request an den eigenen Server, ab **87,5 %** (T2) Broadcast an alle Server.
- **Bereich (Scope)**, Ausschlüsse, **Reservierungen** (fixe IP per MAC), **Optionen**: **003 Router** (Gateway), **006 DNS-Server**, **015 DNS-Domänenname** (Ebenen: Server, Bereich, Richtlinie, Reservierung).
- **Autorisierung** in AD (`Add-DhcpServerInDC`): Nur autorisierte Windows-DHCP-Server verteilen Adressen.
- **DHCP Relay / IP Helper:** Broadcasts werden nicht geroutet. Ein Relay-Agent (Router: `ip helper-address <DHCP-IP>`) leitet DHCP-Anfragen aus anderen Subnetzen per Unicast an den Server weiter (inkl. Kennung des Subnetzes, *giaddr*).
- **DHCP Failover** (eingeführt mit Server 2012. 🔎 Laut aktueller Doku müssen beide Partner mindestens **Windows Server 2016** ausführen):
  - genau **zwei** Server pro Failover-Beziehung, nur **IPv4**, Leases werden synchronisiert (TCP **647**)
  - **Load Balance** (Standard, **50:50**, beide Server verteilen, gleicher Standort)
  - **Hot Standby** (ein aktiver Server, Standby übernimmt nur bei Ausfall, Standardreserve **5 %**, z. B. zentraler Backup-Server für Aussenstellen)
  - **MCLT** (Maximum Client Lead Time): Zeit, bevor der Partner den ganzen Pool übernimmt
  - Zeit auf beiden Servern synchron (max. 1 Minute Abweichung). Bei Relay **beide** Server als Helper eintragen.
  - Alternative: Split-Scope (z. B. 80/20).

<a id="raum3"></a>
### 10.3 Raum 3 – Azure, Verfügbarkeit und Business Continuity

**Cloud vs. On-Premises**

| | Cloud | On-Premises |
|---|---|---|
| Kosten | **OpEx**, Pay-as-you-go | **CapEx** (Hardware, Lizenzen) + Betrieb |
| Skalierung | schnell, elastisch | Beschaffung dauert |
| Verantwortung | geteilt (**Shared Responsibility**) | vollständig selbst |
| Kontrolle/Datenstandort | eingeschränkt, Region wählbar | volle Kontrolle |
| Verfügbarkeit | SLA des Anbieters, Zonen/Regionen | eigene Redundanz nötig |

**Cloud Service Types und Shared Responsibility**

| Modell | Anbieter verwaltet | Kunde verwaltet | Beispiel |
|---|---|---|---|
| **IaaS** | Hardware, Netzwerk, Virtualisierung | **OS**, Middleware, Apps, Daten | Azure VM |
| **PaaS** | + OS, Runtime | **Apps, Daten** | Azure App Service, Azure SQL |
| **SaaS** | alles bis zur App | **Daten, Identitäten, Zugriffe, Geräte** | Microsoft 365 |

Immer beim Kunden: **Daten, Konten/Identitäten, Endgeräte**. Bereitstellungsmodelle: Public, Private, **Hybrid**, Multi-Cloud.

**Skalierung:** **vertikal (Scale up/down)** = grössere Maschine (mehr CPU/RAM), oft mit Neustart. **Horizontal (Scale out/in)** = mehr Instanzen (Load Balancer, **Autoscale** nach Metriken). **Elastizität** = automatisch an die Last anpassen.

**SLA und Downtime:**

| Verfügbarkeit | Ausfall pro Jahr | pro Monat (30 Tage) |
|---|---|---|
| 99 % | 3,65 Tage | 7,2 h |
| 99,9 % | 8,76 h | 43,2 min |
| 99,95 % | 4,38 h | 21,6 min |
| 99,99 % | 52,6 min | 4,3 min |
| 99,999 % | 5,26 min | 26 s |

- **Zusammengesetztes SLA** (seriell abhängige Dienste): Verfügbarkeiten **multiplizieren**, z. B. Web-App 99,95 % × SQL 99,99 % = **99,94 %**.
- Höhere Verfügbarkeit durch **Availability Zones** (getrennte RZ in einer Region) und **Regionspaare**.

**Microsoft Entra ID** (früher Azure AD): cloudbasierter **Identitäts- und Zugriffsdienst** (SSO, MFA, Conditional Access, App-Registrierungen). Unterschied zu AD DS: flach (keine OUs/GPOs/Kerberos-Domäne), Protokolle **OAuth 2.0/OIDC/SAML** statt Kerberos/LDAP. Synchronisation mit **Entra Connect** (Hybrid-Identität). Lizenzen: **Free**, **P1** (Conditional Access, dynamische Gruppen, Hybrid), **P2** (Identity Protection, PIM). Gerätezustände: **Entra joined**, **Hybrid joined**, **Entra registered** (BYOD).

**Monitoring – Metrics vs. Logs (Azure Monitor)**

| | **Metrics** | **Logs** |
|---|---|---|
| Inhalt | numerische Zeitreihen (CPU %, Requests/s) | Ereignisse und Datensätze (Text/strukturiert) |
| Eigenschaften | leichtgewichtig, fast in Echtzeit, ideal für Alarme und Autoscale | detailliert, **Log-Analytics-Workspace**, Abfrage mit **KQL** |
| Beispiel | Alarm bei CPU > 90 % während 5 Min. | «Welche Anmeldungen schlugen gestern fehl?» |

**RPO und RTO**
- **RPO** (Recovery Point Objective): **maximal tolerierter Datenverlust**, gemessen als Zeit zurück bis zum letzten Wiederherstellungspunkt. Bestimmt die **Backup-/Replikationsfrequenz**. Beispiel: RPO 4 h → mindestens alle 4 h sichern.
- **RTO** (Recovery Time Objective): **maximal tolerierte Ausfallzeit** bis der Dienst wieder läuft. Bestimmt die **Wiederherstellungstechnik** (Restore vom Band vs. Replica/Failover).
- Je kleiner RPO/RTO, desto teurer (z. B. Hyper-V Replica, Azure Site Recovery, Geo-Redundanz).

<a id="raum4"></a>
### 10.4 Raum 4 – Security und Identity

**TPM und BitLocker**
- **TPM** (Trusted Platform Module, v2.0): Sicherheitschip für Schlüssel, **Messung des Bootvorgangs** (Measured Boot) und Attestierung. Voraussetzung für Windows 11, BitLocker (empfohlen), Windows Hello, Credential Guard (empfohlen).
- **BitLocker** verschlüsselt **ganze Volumes** (Schutz bei Diebstahl/Verlust). Protektoren: **TPM** (transparent), **TPM + PIN** (Pre-Boot-Authentifizierung, stärker), TPM + USB-Key, Kennwort (Datenlaufwerke), **Wiederherstellungsschlüssel** (48-stellig).
- Wiederherstellungsschlüssel **zentral sichern**: AD DS, **Entra ID/Intune**. BitLocker To Go für USB.
- Befehle: `manage-bde -status`, `Get-BitLockerVolume`, `Enable-BitLocker -MountPoint C: -TpmProtector`, `BackupToAAD-BitLockerKeyProtector`.

**MFA** – mindestens zwei **unterschiedliche** Faktoren: **Wissen** (Passwort, PIN), **Besitz** (Smartphone-App, FIDO2-Key, Smartcard), **Inhärenz** (Fingerabdruck, Gesicht). Stark und phishing-resistent: **FIDO2/Passkeys**, **Windows Hello for Business**, zertifikatsbasiert. SMS/Anruf gelten als schwächer.

**Conditional Access (Entra ID P1)** – «Wenn-Dann»-Richtlinien:
- **Signale** (wer, welche App, welches Gerät, Standort/IP, Risiko, Plattform) → **Entscheidung** → **Durchsetzung**: blockieren **oder** gewähren mit Bedingungen (**MFA**, **konformes Gerät** (Intune), Hybrid-joined, App-Schutzrichtlinie, Passwortänderung). Dazu Sitzungssteuerung.
- Beispiele: MFA für alle Admins, Legacy-Authentifizierung blockieren, Zugriff auf M365 nur von konformen Geräten, Anmeldungen aus bestimmten Ländern blockieren.
- Best Practices: erst im **Report-only**-Modus testen, **Notfallkonten (Break-Glass)** ausschliessen.

**Least Privilege:** jedem Konto/Dienst **nur die minimal nötigen Rechte**, nur so lange wie nötig (Just-in-Time mit **PIM**, Just-Enough-Administration). Trennung von Alltags- und Admin-Konten, Tiering (Tier 0 = DCs/Identität).

**RBAC (rollenbasierte Zugriffskontrolle):** Rechte werden **Rollen** zugewiesen, Benutzer erhalten Rollen (statt einzelner Rechte). Zu unterscheiden: **Azure RBAC** (Ressourcen: Owner, Contributor, Reader, spezifische Rollen; Scope MG/Abo/RG/Ressource, siehe [5.7](#arc)) vs. **Entra-Rollen** (Verzeichnis: Global Administrator, User Administrator, Intune Administrator …). Auch AD-Gruppen nach AGDLP sind RBAC.

**PowerShell Security**
- **Execution Policy** ist **keine Sicherheitsgrenze**, nur ein Schutz vor versehentlichem Ausführen (umgehbar mit `-ExecutionPolicy Bypass`). `AllSigned` + **Code-Signing** (`Set-AuthenticodeSignature`) für kontrollierte Umgebungen. Scopes: MachinePolicy, UserPolicy, Process, CurrentUser, LocalMachine.
- **Logging:** **Script Block Logging** und Module Logging (Ereignisanzeige *Microsoft-Windows-PowerShell/Operational*, Event 4104), **Transcription**
- **Constrained Language Mode** (mit App Control/AppLocker), **AMSI** (Antimalware Scan Interface: Defender prüft Skriptinhalt zur Laufzeit), **JEA** (Just Enough Administration: eingeschränkte Remoting-Endpunkte), PowerShell 2.0 entfernen (kein Logging/AMSI)
- Remoting nur über HTTPS/Kerberos, keine Klartext-Credentials in Skripten (`Get-Credential`, SecretManagement, Key Vault)

**Security Baselines:** von Microsoft empfohlene Sicherheitseinstellungen (GPO) pro Windows-/Office-/Edge-Version. Werkzeuge: **Security Compliance Toolkit** (Baselines, **Policy Analyzer**, **LGPO.exe**), in Intune als *Security Baselines*-Profile. Vorgehen: Ist-Zustand vergleichen → testen → Abweichungen begründen → ausrollen → überwachen (z. B. Defender Vulnerability Management, Secure Score). Siehe auch [6.6](#defender).

**LAPS (Windows Local Administrator Password Solution)**
- verwaltet das **Passwort des lokalen Admin-Kontos**: automatisch **eindeutig, komplex und regelmässig rotiert**, gesichert in **AD DS** oder **Entra ID** (nicht beides). Auch das **DSRM-Passwort** von DCs.
- Schützt gegen **Lateral Movement/Pass-the-Hash** mit überall gleichem lokalem Admin-Passwort.
- **Windows LAPS** ist seit dem **Update vom 11.04.2023** in Windows 10/11 und Server 2019+ **eingebaut** (keine Installation, kostenlos). Mit AD optional **verschlüsselt** und mit **Passwort-Historie**, Aktion nach Verwendung (Passwort zurücksetzen/abmelden). Das alte «Legacy Microsoft LAPS» (MSI) ist abgekündigt.
- Konfiguration per **GPO** oder **Intune** (Endpoint Security → Kontoschutz/LAPS). Befehle: `Update-LapsADSchema`, `Set-LapsADComputerSelfPermission`, `Get-LapsADPassword -Identity PC01 -AsPlainText`, `Reset-LapsPassword`, `Invoke-LapsPolicyProcessing`.

**Defender und Firewall:** siehe [Kapitel 6](#defender).

---

<a id="aa01a"></a>
## 11. Lösungen: Arbeitsauftrag aa01a (Multiple Choice Hyper-V)

✍️ Eigene Lösungen (keine offizielle Musterlösung vorhanden), geprüft an der MS-Doku.

| Nr. | Frage (gekürzt) | Lösung | Begründung / Hinweis |
|---|---|---|---|
| 1 | Welche Windows-Versionen unterstützen die Installation von Hyper-V? | **C** Windows 10 Pro, Enterprise, Education | Client-Hyper-V gibt es ab Pro, nicht in Home. ⚠️ Die Frage vermischt Host und Gast («Gastbetriebssysteme»). Als Gast laufen alle unterstützten Windows-Versionen. |
| 2 | VM-Generation für Secure Boot | **B** Generation 2 | UEFI-Firmware |
| 3 | Unterstützte VHD-Typen | **C** Fixed, Dynamic, Differencing und VHDX | erwartete Antwort. ⚠️ VHDX ist ein Format, kein Typ |
| 4 | Zweck eines vSwitch | **A** Kommunikation zwischen physischen und virtuellen Netzwerken | und zwischen VMs |
| 5 | Was ist ein Snapshot? | **C** Punkt-in-Zeit-Zustand der VM | heute «Checkpoint» |
| 6 | Verschachtelte Virtualisierung | **B** VMs innerhalb anderer VMs | Hyper-V in einer VM |
| 7 | Rolle der Integration Services | **A** Kommunikation zwischen Host und Gast | Heartbeat, Zeit, Shutdown, KVP, VSS, Guest Services |
| 8 | Welche Windows-Funktion muss aktiviert sein? | **D** Hyper-V-Plattform | Unterfeature von «Hyper-V» (neben den Verwaltungstools) |
| 9 | Dynamische Grössenanpassung | **B** Dynamic VHD | wächst bei Bedarf |
| 10 | NICHT unterstütztes Gast-OS | **C** macOS | |
| 11 | Werkzeug zur VM-Verwaltung | **B** Hyper-V Manager | die anderen gehören zu VMware/VirtualBox/Proxmox |
| 12 | Zustand zu einem Zeitpunkt wiederherstellen | **B** Checkpoints | |
| 13 | Unterschied Gen 1 / Gen 2 | **B** Gen 2 unterstützt Secure Boot | ⚠️ A ist technisch **auch richtig**: Gen 1 max. 64 vCPU, Gen 2 bis 240/1024/2048. C ist falsch (kein Leistungsunterschied im Betrieb). |
| 14 | Rolle des Hyper-V-Managers | **B** Verwaltung von VMs auf entfernten Hyper-V-Servern | lokal und remote |
| 15 | NICHT verfügbarer Netzwerktyp | **C** Öffentlich | es gibt nur Extern, Intern, Privat |
| 16 | Dynamische Ressourcenzuweisung | **B** Dynamische Speicherverwaltung | Dynamic Memory |
| 17 | Zustand vor Updates sichern | **C** Checkpoints | |
| 18 | Konfiguration des vSwitch | **D** Hyper-V-Manager | Manager für virtuelle Switches. (SCVMM könnte es auch, erwartet ist D.) |
| 19 | VMs ohne Unterbrechung zwischen Hosts verschieben | **B** Live-Migration | |
| 20 | Webbasierte Verwaltung | **B** Windows Admin Center | |
| 21 | Max. vCPUs einer Gen-1-VM | **A** 64 | MS-Doku «Maximum Scale Limits» (WS 2016–2025) |
| 22 | Sicherheit durch Ausführung in isolierten «Containern» | **B** Shielded VMs | ⚠️ Formulierung ungenau: Shielded VMs sind **verschlüsselte VMs** (vTPM/BitLocker), die nur auf **vom Host Guardian Service freigegebenen Hosts** starten, keine Container |
| 23 | UEFI-Bootarchitektur | **B** Generation 2 | |
| 24 | Edition **ohne** Hyper-V | **C** Windows 11 Home | Home hat kein Client-Hyper-V. Pro/Enterprise (8.1, 10, 11) haben es. 🔎 B ist falsch: Server 2019 Essentials darf die Hyper-V-Rolle ausführen (Host nur mit Hyper-V-Rolle plus eine Essentials-VM). |

---

<a id="b5"></a>
## 12. Lösungen: Übungsauftrag B5 «Security Experts – Defender & Firewall»

✍️ Ausgearbeitete Musterantworten (eigene Lösungen auf Basis von Folien und Recherche). Die Leitfragen, die schon in [Kapitel 6](#defender) beantwortet sind, werden hier nur verlinkt.

### Gruppe 1 – Defender Antivirus: Schutz & Erkennung

- **Was, Windows-Versionen, Lizenz, Scan-Typen, Echtzeit/Quick/Full, Quarantäne, Drittanbieter-AV:** siehe [6.4](#defender).
- **Praxisauftrag:** Status mit `Get-MpComputerStatus` bzw. Windows-Sicherheit → Viren- & Bedrohungsschutz prüfen. Quick und Full Scan ausführen (`Start-MpScan`). Funde unter **Schutzverlauf** und in der Ereignisanzeige (*Windows Defender/Operational*). 🔎 Mit der harmlosen **EICAR-Testdatei** lässt sich eine Erkennung sicher auslösen.
- **Ablauf nach einem Fund:** Bedrohung → Erkennung → Blockierung/Quarantäne → Information → Bereinigung → Kontrolle.
- **Reicht «Threat removed»? – Nein.** Weitere Massnahmen im Unternehmen:
  1. **Ursache klären:** Wie kam die Datei auf das Gerät (Mail, Download, USB)? Wurde sie ausgeführt?
  2. **Ausmass prüfen:** betroffene Benutzer/Geräte, ähnliche Funde im Tenant (Defender-Portal, Advanced Hunting), Persistenz (Autostart, geplante Tasks)
  3. **Gerät isolieren** (MDE) bei Verdacht auf aktive Kompromittierung, **Full Scan** oder Offline-Scan
  4. **Anmeldedaten zurücksetzen**, falls Credentials betroffen sein könnten
  5. **Lücke schliessen** (Patch, Makros, ASR-Regel, Mailfilter), **Benutzer sensibilisieren**
  6. **Dokumentieren** (Incident-Ticket), ggf. Meldepflichten prüfen
- **Bewertung: Ist Defender Antivirus allein ausreichend? – Nein.** Er ist eine gute, integrierte Basis. Für Unternehmen braucht es mehrere Schichten: **EDR** (Erkennung von Angriffsverhalten und Reaktion, z. B. MDE P2/Defender for Business), **Attack Surface Reduction**, Patch-Management, **MFA** und Conditional Access, Least Privilege/LAPS, E-Mail-/Web-Filter, **Backups**, Monitoring und Awareness (Defense in Depth).
- 💬 Mögliche Diskussionsfrage: «Ein Mitarbeiter meldet, dass Defender eine Datei entfernt hat, und will sie wiederherstellen, weil er sie braucht. Wie entscheidet ihr?»

### Gruppe 2 – Defender Administration & Exclusions

- **Tools:** Windows-Sicherheit (lokal, einzelne Geräte, für Benutzer), **PowerShell** (`Set-/Add-/Get-MpPreference`, Skripte, Automatisierung), **Gruppenrichtlinien** (AD-Umgebungen, *Administrative Vorlagen → Windows-Komponenten → Microsoft Defender Antivirus*), **zentrale Managementlösungen** (Intune Endpoint Security, Configuration Manager, Defender-Portal: einheitlich, mit Reporting). Dazu WMI.
- **Exclusion:** Ausnahme, bei der Defender bestimmte Dateien/Ordner/Dateitypen/Prozesse **nicht scannt**. Arten, Erstellen, Prüfen und Risiken: siehe [6.4](#defender).
- **Praxisauftrag:** Ausgangszustand dokumentieren (`Get-MpPreference | Select Exclusion*`) → Test-Ausnahme erstellen (`Add-MpPreference -ExclusionPath C:\Test`) → kontrollieren → wieder entfernen (`Remove-MpPreference -ExclusionPath C:\Test`).
- **Spezialauftrag: Hersteller verlangt, den kompletten Installationsordner auszuschliessen.**
  - **Nicht ungeprüft umsetzen.** Risiko: Ein ganzer Ordner ist ein **blinder Fleck**. Malware, die dort landet oder als Programm dieses Ordners läuft, wird nicht erkannt. Schreibbare Ordner sind besonders gefährlich.
  - **Abklärungen zuerst:** Offizielle Herstellerdoku bzw. KB lesen: welche Dateien/Prozesse genau, warum (Performance? Datei-Locks? Fehlalarm?). Tritt das Problem überhaupt auf? Test auf einem Pilotgerät. Mit Performance-Analyse (🔎 `New-MpPerformanceRecording`) prüfen, welche Dateien bremsen.
  - **Sicherere Lösung:** möglichst **eng** ausschliessen (einzelne Datenbank-/Logdateien oder Dateitypen, konkreter Prozess statt ganzer Ordner). Ordner per **NTFS-Rechte** für normale Benutzer schreibschützen. Ausnahme **zentral** (Intune/GPO) statt lokal setzen. Fehlalarme an Microsoft melden statt ausschliessen. Andere Schutzschichten (EDR, ASR) aktiv lassen.
  - **Dokumentation und Überwachung:** Change-Antrag mit Begründung, Umfang, Verantwortlichem (Owner), Datum und **Ablauf-/Review-Datum**. Regelmässige Überprüfung (z. B. quartalsweise), Monitoring/Alerts auf Aktivitäten in diesem Pfad, Liste aller Ausnahmen führen.
- **Bewertung Security vs. Betrieb:** Risikobasiert entscheiden: So wenig Ausnahmen wie möglich, so viele wie nötig. Jede Ausnahme ist befristet, begründet, genehmigt (Change-Management) und überwacht. Security und Betrieb entscheiden gemeinsam und nicht der Softwarehersteller allein.

### Gruppe 3 – Endpoint Security im Unternehmen

**Ausgangslage:** 100 Mitarbeitende, Windows 11, Microsoft 365, **2 IT-Mitarbeitende**, begrenztes Security-Know-how.

| Begriff | Bedeutung |
|---|---|
| **Antivirus (AV)** | erkennt und entfernt bekannte Schadsoftware (Signaturen, Heuristik), primär **präventiv, dateibasiert** |
| **Endpoint Protection (EPP)** | Plattform um den AV herum: Firewall, Web-/Gerätekontrolle, Exploit-Schutz, ASR, zentrale Verwaltung und Richtlinien |
| **EDR** (Endpoint Detection & Response) | zeichnet **Verhalten/Telemetrie** auf (Prozesse, Netzwerk, Registry), erkennt **Angriffsketten** (auch ohne Malware-Datei), ermöglicht **Untersuchung und Reaktion** (Gerät isolieren, Prozess beenden, Timeline) |
| 🔎 **XDR / MDR** | XDR: Korrelation über Endpoint, Identität, Mail, Cloud (z. B. Defender XDR). MDR: externer Dienst, der rund um die Uhr überwacht und reagiert |

- **Zentrale Administration:** Konsole für Richtlinien, Updates, Ausnahmen (bei Microsoft: Intune + Defender-Portal).
- **Security Events:** Alarme → Incidents im Portal → Triage → automatische Untersuchung/Behebung → Eskalation.
- **Reporting/Monitoring:** Geräte-Status, veraltete Signaturen, Schwachstellen, Secure Score, E-Mail-Benachrichtigungen, SIEM-Anbindung.
- **Lizenzen und Kosten:** pro Benutzer oder Gerät und Monat. Bei Microsoft z. B. Defender for Business (in **M365 Business Premium**) oder MDE P1/P2. Dazu Aufwand für Einführung, Betrieb und evtl. MDR-Dienst.
- **Personeller Aufwand:** Richtlinien pflegen, Alarme täglich sichten, Incidents behandeln, Updates und Ausnahmen verwalten. Mit 2 IT-Personen ohne Security-Spezialisten ist ein **24/7-Betrieb nicht möglich**, deshalb Automatisierung und externe Unterstützung.

**Vergleich (qualitativ)** ✍️

| Kriterium | **Microsoft Defender for Business** (in M365 Business Premium) | **Drittanbieter-EDR** (z. B. CrowdStrike Falcon, SentinelOne, ESET PROTECT) |
|---|---|---|
| Schutzfunktionen | Next-Gen-AV, ASR, Web-Schutz, Firewall-Management | vergleichbar, teils sehr stark bei Erkennung |
| EDR | ja, inkl. automatischer Untersuchung/Behebung | ja (je nach Paket) |
| Zentrale Verwaltung | Intune + Defender-Portal, **gleiche Konsole wie M365** | eigene Konsole |
| Monitoring | Defender-Portal, Incidents, Secure Score | eigenes Portal, oft MDR optional |
| Integration | **nahtlos** mit Entra ID, Intune, Conditional Access (Geräterisiko), M365 | über Schnittstellen/Connectoren |
| Lizenzierung | bereits in Business Premium enthalten (bis 300 Benutzer) | zusätzliche Lizenz pro Endpunkt |
| Kosten | kein Zusatzprodukt, wenn Business Premium vorhanden | Zusatzkosten + Integration |
| Betriebsaufwand | tief bis mittel (eine Umgebung, bekannte Tools) | mittel (zweite Konsole, Know-how) |
| Skalierbarkeit | bis 300 Benutzer, dann MDE P1/P2 | hoch |

**Managemententscheidung (Empfehlung):** Für dieses KMU **Microsoft 365 Business Premium** mit **Defender for Business** und **Intune**. Begründung:
- nutzt die vorhandene M365-Umgebung
- **eine** Verwaltungsoberfläche und integrierte Identität/Compliance (Conditional Access mit Geräterisiko)
- kein zusätzlicher Agent, geringe Zusatzkosten
- für 2 IT-Mitarbeitende mit begrenztem Know-how am einfachsten zu betreiben

Ergänzen mit sauberer Konfiguration (Baselines, ASR, Tamper Protection), MFA/Conditional Access, Patch-Management, Backups und idealerweise einem **externen MDR/SOC-Partner** für die 24/7-Überwachung. Nicht nur der Kaufpreis zählt, sondern auch **Betrieb, Know-how und Integration**.

### Gruppe 4 – Firewall & Security Design

- **Was, Funktion, warum trotz Antivirus, Regel, Inbound/Outbound, Allow/Block, Exception, Angaben einer Regel:** siehe [6.5](#defender).
- **Risiken zu offener Regeln:** Dienste sind für Angreifer aus beliebigen Netzen erreichbar (Brute-Force auf RDP, Exploits auf ungepatchte Dienste, z. B. SQL). Das erleichtert Lateral Movement im internen Netz und Datenabfluss. «Any/Any»-Regeln verstecken Fehlkonfigurationen, vergessene Regeln bleiben offen.

**Spezialauftrag «Firewall Designer»** ✍️ (Prinzip: **Default Deny**, nur explizit Nötiges erlauben):

| Dienst | Wer (Quelle) | → darf auf welches System (Ziel) | Port | Aktion | Begründung |
|---|---|---|---|---|---|
| **HTTPS-Webserver** | **Internet (Any)** | Webserver in der **DMZ** | **TCP 443** | Allow | öffentlicher Dienst, muss von überall erreichbar sein. Nur 443 (80 höchstens als Redirect). Dazu WAF/Reverse Proxy, Server gehärtet und gepatcht. |
| **Remote Desktop** | **Admin-Netz** bzw. **Jump-Host/PAW** (z. B. 10.10.99.0/24), nur Admin-Gruppe | Server (intern) | **TCP 3389** | Allow | Administration nur von vertrauenswürdigen Admin-Geräten. **Nie aus dem Internet** (stattdessen VPN mit MFA, RD Gateway, Azure Bastion). NLA aktiv. |
| | alle anderen | Server | TCP 3389 | **Block** | Brute-Force und Lateral Movement verhindern |
| **SQL-Datenbank** | **nur App-/Webserver** (feste IP) + optional DB-Admin-Netz | **SQL-Server** (internes Netz, nicht DMZ) | **TCP 1433** | Allow | Die Datenbank braucht nur die Anwendung. Kein Zugriff aus Internet oder Client-Netz. |
| | alle anderen | SQL-Server | TCP 1433 | **Block** | Datenbank als Kronjuwel schützen |
| Rest | Any | Any | Any | **Block** (eingehend) | Default Deny |

- Also nicht «TCP 3389 → Allow», sondern **«Admin-Netzwerk → Server → TCP 3389 → Allow»**.
- **Least Privilege:** Jede Regel erlaubt **nur die nötige Quelle, das nötige Ziel, den nötigen Port, das nötige Protokoll und die nötige Richtung**. Auch ausgehend beschränken (Server brauchen selten beliebigen Internetzugang).
- **Bewertung: Warum ist «Port öffnen» allein keine Strategie?**
  - Ein offener Port ohne **Quell-/Zielbeschränkung** öffnet den Dienst für alle.
  - Er ist nicht an ein Programm gebunden, bleibt offen, auch wenn niemand ihn braucht, und ist nicht dokumentiert.
  - Eine gute Strategie umfasst **Default Deny**, **Segmentierung** (DMZ, Server-, Client-, Admin-Netz), **Scoping** der Regeln, zentrale Verwaltung (GPO/Intune), **Protokollierung und Monitoring**, **regelmässige Reviews** und Dokumentation. Dazu andere Schichten (Patchen, MFA, EDR).
- 💬 Mögliche Diskussionsfrage: «Braucht es auf Clients eine Outbound-Filterung, oder ist der Aufwand grösser als der Nutzen?»

---

<a id="fragen"></a>
## 13. Fragenkatalog: alle Repetitions- und Recherchefragen

Alle Fragen aus den Folien mit Kurzantwort. Details im verlinkten Kapitel.

### Hyper-V (Unit 01, Repetition Unit 02)

| Frage | Kurzantwort | Kap. |
|---|---|---|
| Welche Funktionalitäten besitzt Hyper-V? | Management (Manager, PowerShell), Portabilität (Live/Storage Migration, Export), DR/Backup (Replica, Checkpoints), Sicherheit (Secure Boot, Shielded VMs), Optimierung (Integration Services) | [2.2](#hyperv) |
| Was ist ein Hypervisor? | Softwareschicht zwischen Hardware und Betriebssystemen, steuert den Hardwarezugriff. Treiber nur im Host (Parent Partition), VMs sehen virtuelle Hardware. | [2.1](#hyperv) |
| Welche Gast-OS werden unterstützt? | alle unterstützten Windows, Linux (RHEL, Debian, Oracle, SUSE, Ubuntu), FreeBSD. Kein macOS. | [2.3](#hyperv) |
| System Requirements? | 64-Bit-CPU mit SLAT, VM Monitor Mode Extensions, VT-x/AMD-V aktiv, Hardware-DEP, genug RAM | [2.3](#hyperv) |
| Mit welchen Tools verwalten? | Hyper-V-Manager, SCVMM, Windows Admin Center, PowerShell | [2.3](#hyperv) |
| Use Cases? | Serverkonsolidierung, Dev/Test, VDI, Private Cloud | [2.3](#hyperv) |
| Was ist die VM Configuration Version? | Kennzeichnung von Feature-Satz/Kompatibilität einer VM, bestimmt durch die Hyper-V-Version des Hosts. Nur manuelles Update, kein Downgrade. | [2.5](#hyperv) |
| Was ist eine VM-Generation, welche gibt es? | Art der virtuellen Hardware: Gen 1 (BIOS, IDE, Legacy) und Gen 2 (UEFI, SCSI, Secure Boot) | [2.5](#hyperv) |
| Welche Generation für Secure Boot? | **Generation 2** | [2.5](#hyperv) |
| Was ist eine VHD, welche Typen? | Datei, die eine Festplatte darstellt. Typen: Fixed, Dynamic, Differencing (+ Pass-Through). Formate VHD/VHDX/VHDS. | [2.6](#hyperv) |
| Welche VM-Settings gibt es? | Hardware (Firmware, CPU, RAM, Controller, NIC) und Verwaltung (Name, Integration Services, Checkpoints, Smart Paging, Start-/Stoppaktion) | [2.7](#hyperv) |
| Nenne 2 Best Practices | z. B. Hyper-V als einzige Rolle, Server Core, VMs auf separaten Disks, Gen-2-VMs, remote verwalten | [2.7](#hyperv) |
| Welche Netzwerkadapter? | Legacy (Gen 1, PXE) und synthetischer Netzwerkadapter | [2.8](#hyperv-netz) |
| Welche virtuellen Switches? | **Extern, Intern, Privat** | [2.8](#hyperv-netz) |
| Was ist Nested Virtualization? | Hyper-V in einer VM betreiben (`Set-VMProcessor -ExposeVirtualizationExtensions $true`) | [2.9](#nested) |

### Container (Unit 02, Repetition Unit 03)

| Frage | Kurzantwort | Kap. |
|---|---|---|
| Was sind Container? | isolierte, leichtgewichtige Laufzeitumgebung für eine App mit ihren Abhängigkeiten. Teilt den Kernel des Hosts. | [3.1](#container) |
| Drei Vorteile? | portabel, isoliert, effizient (schnell, hohe Dichte), konsistente Entwicklungsumgebung | [3.1](#container) |
| Wie funktionieren Container? | eigener isolierter User-Modus aus einem geschichteten Base-Image, gemeinsamer Kernel | [3.1](#container) |
| Was sind Microservices-Applikationen? | App aus vielen kleinen, lose gekoppelten, unabhängig deploybaren Diensten | [3.2](#container) |
| Was sind monolithische Applikationen? | eine grosse App, alle Funktionen in einem Deployment | [3.2](#container) |
| Container = automatisch Microservices? | **Nein**, Container erzwingen keine Microservice-Architektur | [3.2](#container) |
| Zwei Isolierungsmodi unter Windows? | **Prozessisolierung** (geteilter Kernel) und **Hyper-V-Isolierung** (eigener Kernel in Utility-VM) | [3.4](#container) |
| Was ist Docker? | Tool-/Plattform-Sammlung, um Apps als Container zu verpacken und auszuführen (Client → REST API → Daemon) | [3.5](#container) |
| Was ist ein Container-Image? | unveränderliche, geschichtete Vorlage, aus der Container gestartet werden | [3.5](#container) |
| Host OS vs. Container OS? | Host OS liefert den Kernel. Container OS = Base Image (User-Modus) im Container. | [3.5](#container) |
| Was ist ein Dockerfile? | Textdatei mit den Build-Anweisungen für ein Image (`FROM`, `RUN`, `COPY`, `CMD` …) | [3.5](#container) |
| Was ist Kubernetes? | Open-Source-Orchestrator für Container über viele Server (deklarativ, YAML) | [3.6](#container) |
| Was ist AKS? | Azure Kubernetes Service, verwaltetes Kubernetes in Azure | [3.6](#container) |
| Drei Features von Kubernetes? | Scheduling, Self-Healing, Skalierung, Load Balancing/Service Discovery, Rolling Updates | [3.6](#container) |

### Intune (Unit 03, Repetition Unit 04)

| Frage | Kurzantwort | Kap. |
|---|---|---|
| Was ist MDM? | Verwaltung ganzer Geräte (Richtlinien, Apps, Updates, Wipe) | [4.2](#intune) |
| Was ist MAM? | Verwaltung/Schutz von Apps und Firmendaten, unabhängig vom Gerät (auch BYOD ohne Enrollment) | [4.2](#intune) |
| Welche Geräte unterstützt Intune? | Windows, macOS, iOS/iPadOS, Android, Linux | [4.2](#intune) |
| Was ist MECM (Configuration Manager)? | On-Prem-Verwaltung von PCs/Servern (Software, Updates, OS-Deployment) | [4.2](#intune) |
| Unterschied Intune vs. MECM? | Cloud/MDM/MAM vs. On-Prem/klassische PC- und Serververwaltung. Kombinierbar über Co-Management. | [4.2](#intune) |
| Was ist Cloud Attach? | ConfigMgr an die Cloud anbinden (Tenant Attach, Co-Management, Endpoint Analytics) | [4.2](#intune) |
| Was ist Co-Management? | Windows-Geräte gleichzeitig mit ConfigMgr und Intune verwalten, Autorität pro Workload | [4.2](#intune) |
| Was ist Endpoint Analytics? | Analyse der Benutzererfahrung (Startzeit, App-Abstürze, Work from anywhere) + Remediations | [4.2](#intune) |
| Was ist Windows Autopilot? | Geräte ohne Imaging ab Werk bereitstellen, zurücksetzen, umwidmen | [4.2](#intune) |
| Welche Profiltypen gibt es? | Settings Catalog, Templates (Admin Templates, Custom, Device Restrictions, Wi-Fi, VPN, Zertifikate, Imported ADMX …) | [4.4](#intune) |
| Kann ich ADMX-Dateien in Intune hinzufügen? | **Ja**: Geräte → Konfiguration → Import ADMX (max. 20, en-us, Abhängigkeiten zuerst) → Profil «Imported Administrative templates» | [4.4](#intune) |
| Was ist eine Device Compliance Policy? | Regeln, die ein Gerät erfüllen muss, um als konform zu gelten (BitLocker, OS-Version …), mit Aktionen bei Nichtkonformität | [4.5](#intune) |
| Mit welchem Entra-Tool kombinieren? | **Conditional Access** («Gerät muss als konform markiert sein») | [4.5](#intune) |

### Azure Arc (Unit 04, Repetition Unit 05)

| Frage | Kurzantwort | Kap. |
|---|---|---|
| Was ist eine Hybrid Cloud? | Kombination aus lokaler/privater Infrastruktur und Public Cloud | [5.1](#arc) |
| Welche Funktionen bietet Arc für Server? | Inventar, Policy/Machine Configuration, Defender, Monitor, Update Manager, Extensions, RBAC, WAC/SSH | [5.2](#arc) |
| Was muss auf dem Server installiert werden? | der **Azure Connected Machine Agent** | [5.3](#arc) |
| Welche Betriebssysteme? | Windows Server 2016–2025 (2012/R2 auslaufend), Linux-Distros, Windows 10/11 nur serverähnlich, 64-Bit | [5.5](#arc) |
| Welche Onboarding-Methoden? | Skript/PowerShell (einzeln), PowerShell mit Service Principal, ConfigMgr, GPO (+ WAC, Arc Setup, Ansible) | [5.6](#arc) |
| Wie verbindet sich ein Arc-Server mit Azure? | direkt übers Internet, via Proxy, via Service Tag über VPN/ExpressRoute, via Private Link | [5.4](#arc) |
| Welches Protokoll? | **HTTPS, TCP 443 ausgehend** | [5.3](#arc) |
| Was ist Azure Policy? | Dienst zum Definieren und Durchsetzen von Regeln/Compliance für Ressourcen | [5.8](#arc) |
| Was ist Azure Resource Graph? | schnelle Abfrage von Ressourcen über Abos hinweg mit KQL | [5.9](#arc) |
| Was kostet Arc? | Control Plane gratis. Policy/Machine Configuration, Defender, Update Manager, Monitor kostenpflichtig. | [5.10](#arc) |
| Welche Rolle zum Verwalten? | **Azure Connected Machine Resource Administrator** (Onboarding: *Azure Connected Machine Onboarding*) | [5.7](#arc) |

### Defender (Unit 05, Repetition Unit 06)

| Frage | Kurzantwort | Kap. |
|---|---|---|
| Welche OS unterstützen Credential Guard? | Windows 10/11 **Enterprise/Education**, Windows Server 2016+. Standard ab Win 11 22H2 / Server 2025 (domänengebunden, nicht DC). | [6.2](#defender) |
| Was ist Pass-the-Hash / Pass-the-Ticket? | Anmeldung mit gestohlenem NTLM-Hash bzw. Kerberos-Ticket, ohne das Passwort zu kennen | [6.2](#defender) |
| Voraussetzungen für Credential Guard? | 64-Bit-CPU mit Virtualisierung, UEFI, Secure Boot, VBS (TPM empfohlen). VM: Gen 2 + IOMMU. | [6.2](#defender) |
| Wie funktioniert Credential Guard? | Secrets liegen im isolierten Prozess **LSAIso** in einem von VBS geschützten Bereich statt in LSASS | [6.2](#defender) |
| Credential Guard auf dem DC? | **Nein** (nicht empfohlen, kein Zusatznutzen) | [6.2](#defender) |
| Lizenz für Defender Antivirus? | AV ist in Windows enthalten. Zentral für Unternehmen: MDE P1 (E3), P2 (E5) oder Defender for Business | [6.4](#defender) |
| Scan-Typen? | Quick, Full, Custom (+ Echtzeit, Offline) | [6.4](#defender) |
| Wie Prozesse ausschliessen? | Windows-Sicherheit → Ausschlüsse → Prozess, oder `Add-MpPreference -ExclusionProcess` | [6.4](#defender) |
| Tools zur Konfiguration? | Intune, Configuration Manager, GPO, PowerShell, WMI | [6.4](#defender) |
| Was ist eine Firewall, wozu? | kontrolliert Netzwerkverkehr, blockiert Unerlaubtes, erlaubt Autorisiertes | [6.5](#defender) |
| Was muss eine Regel definieren? | Quelle, Ziel, Protokoll, Quellport, Zielport, Aktion, Richtung | [6.5](#defender) |
| Exception, Inbound, Outbound? | explizite Erlaubnis / eingehender / ausgehender Verkehr | [6.5](#defender) |

### GitHub (Unit 06, Repetition Unit 07)

| Frage | Kurzantwort | Kap. |
|---|---|---|
| Repository? Branch? Commit? | Projektablage mit Historie / paralleler Entwicklungszweig / Momentaufnahme mit Message und Hash | [7.2](#github) |
| Was ist ein Pull Request? | Anfrage, Änderungen eines Branches zu übernehmen, mit Review/Diskussion vor dem Merge | [7.2](#github) |
| Was ist der GitHub Flow? | Branch → Commits → PR → Review → Merge → Deploy (`main` immer deploybar) | [7.3](#github) |
| Was sind Gists? | Code-Schnipsel teilen (public/secret, versioniert). Secret ≠ privat. | [7.2](#github) |
| Was ist GitHub Copilot? | KI-Codeassistent (Vorschläge, Chat, Agent) in IDE und GitHub | [7.1](#github) |
| Kollaborationsfunktionen? | Pull Requests/Reviews, Issues, Discussions, Projects, Wiki, Collaborators/Teams, Mentions | [7.2](#github) |
| Vorteile von GitHub? | Versionierung, Zusammenarbeit, CI/CD (Actions), Security-Scanning, Copilot, grosse Community | [7.1](#github) |

### KI / Foundry / Security Copilot (Unit 07, Repetition Unit 08)

| Frage | Kurzantwort | Kap. |
|---|---|---|
| Was ist generative KI? 3 Beispiele | KI, die neue Inhalte erzeugt. GPT-5 (Text/Code), gpt-image/DALL·E (Bilder), Whisper (Sprache), Sora (Video) | [8.1](#ki) |
| Was ist ein Sprachmodell (LLM), was ein Token? | neuronales Netz, das das nächste Token vorhersagt. Token = Wortteil/Wort/Satzzeichen. | [8.1](#ki) |
| Was ist ein Encoder / Decoder? | Encoder: Tokens → Embeddings (mit Attention). Decoder: erzeugt daraus Token für Token die Ausgabe. | [8.1](#ki) |
| ChatGPT vs. Azure OpenAI in Foundry? | Endnutzerdienst bei OpenAI vs. Azure-Dienst im eigenen Abo (Entra ID, RBAC, Private Endpoint, Datenresidenz, kein Training mit Kundendaten) | [8.1](#ki) |
| Copilot vs. KI-Agent? | Copilot assistiert, Agent erledigt (plant, nutzt Tools, handelt) | [8.1](#ki) |
| Modell vs. Deployment? | Modell = trainiertes KI-Modell im Katalog. Deployment = bereitgestellte Instanz mit Name, Version, Typ, Quota. | [8.4](#ki) |
| Foundry-Projekt vs. -Ressource? | Ressource = Azure-Ressource (Region, Netz, RBAC, Abrechnung). Projekt = Arbeitsbereich darin. | [8.4](#ki) |
| KI-Agent in Foundry / Agent Service? | Modell + Anweisungen + Tools (+ Wissen/Memory). Der Service hostet und betreibt Agenten. | [8.4](#ki) |
| RAG / Foundry IQ? | eigene Dokumente suchen und dem Prompt mitgeben. Foundry IQ = verwaltete Wissensschicht. | [8.4](#ki) |
| Was ist Security Copilot? | generative KI für Security-/IT-Teams (Vorfälle, KQL, Skripte, Agents) | [8.5](#ki) |
| Standalone vs. Embedded? | eigenes Portal vs. direkt in Defender/Entra/Intune/Purview | [8.5](#ki) |
| Promptbooks, Plugins, Agents? | gespeicherte Prompt-Abläufe / Datenquellen-Anbindungen / (teil-)autonome Workflows | [8.5](#ki) |
| SCU und Lizenzierung? | Recheneinheit. In M365 E5/E7 inklusive (400 SCU/1000 Lizenzen/Monat), sonst stundenweise über Azure | [8.5](#ki) |

### Bicep / IaC (Unit 08)

| Frage | Kurzantwort | Kap. |
|---|---|---|
| Was ist IaC? | Infrastruktur als Code beschreiben statt manuell klicken | [9.1](#bicep) |
| Vor- und Nachteile von IaC? | wiederholbar, automatisierbar, dokumentiert, nachvollziehbar vs. Lernaufwand, Initialaufwand, Drift, Secrets-Handling | [9.1](#bicep) |
| Imperativ vs. deklarativ? Wo? | WIE (PowerShell, Python, Bash) vs. WAS (Bicep, Terraform, ARM, K8s-YAML, SQL) | [9.2](#bicep) |
| Was ist ARM? | Azure Resource Manager, die Verwaltungsschicht für alle Ressourcen | [9.3](#bicep) |
| ARM-Templates, welche Sprache? | deklarative Templates in **JSON** | [9.3](#bicep) |
| Resource Providers? | Dienste-Namespaces wie `Microsoft.Storage`, im Abo zu registrieren | [9.3](#bicep) |
| Eindeutige Identifikation einer Ressource? Teile? | Ressourcen-ID: `/subscriptions/…/resourceGroups/…/providers/{Namespace}/{Typ}/{Name}` | [9.3](#bicep) |
| Child Resources? | existieren nur in einer Parent-Ressource (Subnetz, Blob-Container, SQL-DB) | [9.3](#bicep) |
| Was ist Bicep? | deklarative IaC-Sprache für Azure, wird zu ARM-JSON transpiliert | [9.4](#bicep) |
| Wozu Module? | grosse Templates aufteilen, Bausteine wiederverwenden | [9.4](#bicep) |

---

<a id="befehle"></a>
## 14. Befehlsreferenz

### Hyper-V (PowerShell)

| Befehl | Zweck |
|---|---|
| `Install-WindowsFeature Hyper-V -IncludeManagementTools -Restart` | Rolle installieren (Server) |
| `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All` | Feature aktivieren (Client) |
| `Get-VM`, `Start-VM`, `Stop-VM`, `Restart-VM`, `Suspend-VM` | VMs anzeigen/steuern |
| `New-VM -Name X -Generation 2 -MemoryStartupBytes 4GB -NewVHDPath … -NewVHDSizeBytes 60GB -SwitchName …` | VM erstellen |
| `Set-VMMemory -VMName X -DynamicMemoryEnabled $true -MinimumBytes 1GB -MaximumBytes 8GB` | Dynamic Memory |
| `Set-VMProcessor -VMName X -Count 4` / `-ExposeVirtualizationExtensions $true` | vCPUs / Nested Virtualization |
| `New-VHD`, `Convert-VHD`, `Resize-VHD`, `Mount-VHD` | virtuelle Disks |
| `New-VMSwitch -Name X -SwitchType Internal\|Private` / `-NetAdapterName` (extern) | vSwitch erstellen |
| `Connect-VMNetworkAdapter -VMName X -SwitchName Y` | Adapter verbinden |
| `Get-VMNetworkAdapter -VMName X \| Set-VMNetworkAdapter -MacAddressSpoofing On` | MAC-Spoofing (nested) |
| `Checkpoint-VM`, `Get-VMCheckpoint`, `Restore-VMCheckpoint`, `Remove-VMCheckpoint` | Checkpoints |
| `Set-VM -Name X -CheckpointType Production` | Checkpoint-Typ |
| `Get-VMHostSupportedVersion`, `Update-VMVersion` | Konfigurationsversion |
| `Enable-VMResourceMetering`, `Measure-VM` | Ressourcenmessung |
| `Enable-VMTPM`, `Set-VMKeyProtector -NewLocalKeyProtector` | vTPM |
| `Get-VMIntegrationService -VMName X` | Integration Services |
| `Enter-PSSession -VMName X` / `Invoke-Command -VMName X {…}` | PowerShell Direct |
| `Move-VM`, `Export-VM`, `Import-VM` | Migration/Export |

### Docker / Kubernetes

| Befehl | Zweck |
|---|---|
| `docker version` / `docker info` | Client/Server-Version, Modus |
| `docker pull <image>:<tag>` | Image laden |
| `docker images` / `docker ps -a` | Images / Container anzeigen |
| `docker run -d -p 8080:80 --name web --isolation=hyperv <image>` | Container starten (detached, Port, Name, Isolation) |
| `docker run -it <image> powershell` | interaktiv |
| `docker build -t name:tag .` | Image aus Dockerfile bauen |
| `docker logs <id>` / `docker exec -it <id> powershell` | Logs / in Container einsteigen |
| `docker stop <id>` / `docker rm <id>` / `docker rmi <image>` | stoppen / Container / Image löschen |
| `docker volume create data` / `-v data:C:\data` | persistenter Speicher |
| `docker network ls` | Netzwerke (nat, transparent …) |
| `docker system df` / `docker system prune` | Speicherverbrauch / aufräumen |
| `kubectl get nodes` / `kubectl get pods -o wide` | Cluster-Status |
| `kubectl apply -f deployment.yaml` | Manifest anwenden (deklarativ) |
| `kubectl describe pod <name>` / `kubectl logs <pod>` | Diagnose |
| `kubectl scale deployment web --replicas=3` | skalieren |

### Intune / Entra / Windows-Diagnose

| Befehl | Zweck |
|---|---|
| `dsregcmd /status` | Join-Status (Entra/Hybrid/Domäne), PRT |
| `mdmdiagnosticstool.exe -area Autopilot;DeviceEnrollment -cab C:\temp\diag.cab` | MDM-/Autopilot-Diagnose |
| `Get-WindowsAutopilotInfo -OutputFile hash.csv` (Skript aus PSGallery) | Hardware-Hash auslesen |
| `gpresult /r` bzw. `/h report.html`, `gpupdate /force` | GPO-Auswertung / Aktualisierung |
| `msinfo32` | VBS/Credential-Guard-Status, Secure Boot, BIOS-Modus |
| `systeminfo` | u. a. Hyper-V-Anforderungen |
| `Get-Tpm`, `Get-BitLockerVolume`, `manage-bde -status` | TPM/BitLocker |

### Azure Arc

| Befehl | Zweck |
|---|---|
| `azcmagent connect --resource-group … --tenant-id … --location … --subscription-id …` | Server verbinden |
| `azcmagent disconnect` | trennen |
| `azcmagent show` | Status (Connected/Disconnected), Ressourcen-ID |
| `azcmagent check` | Netzwerktest zu allen Endpunkten |
| `azcmagent config set proxy.url "http://proxy:8080"` | Proxy setzen |
| `azcmagent logs` | Logs als ZIP sammeln |
| `azcmagent version` / `azcmagent upgrade` | Version / Update |
| `Register-AzResourceProvider -ProviderNamespace Microsoft.HybridCompute` | Provider registrieren |
| `az graph query -q "resources \| where type =~ 'microsoft.hybridcompute/machines'"` | Resource-Graph-Abfrage |

### Defender Antivirus, Firewall, Credential Guard

| Befehl | Zweck |
|---|---|
| `Get-MpComputerStatus` | Schutzstatus, Modus (AMRunningMode), Signaturalter |
| `Get-MpPreference` / `Set-MpPreference` | Einstellungen lesen / setzen (überschreibt Listen) |
| `Add-MpPreference -ExclusionPath\|-ExclusionProcess\|-ExclusionExtension` | Ausschluss hinzufügen |
| `Remove-MpPreference -ExclusionPath …` | Ausschluss entfernen |
| `Start-MpScan -ScanType QuickScan\|FullScan\|CustomScan` | Scan |
| `Start-MpWDOScan` | Defender Offline Scan |
| `Update-MpSignature` | Signaturen aktualisieren |
| `Get-MpThreat` / `Get-MpThreatDetection` | Bedrohungen / Funde |
| `Get-NetFirewallProfile` / `Set-NetFirewallProfile` | Profile, Standardaktionen, Logging |
| `New-NetFirewallRule -DisplayName … -Direction Inbound -Protocol TCP -LocalPort 443 -RemoteAddress … -Action Allow` | Regel erstellen |
| `Get-NetFirewallRule`, `Enable-/Disable-/Remove-NetFirewallRule` | Regeln verwalten |
| `Get-NetConnectionProfile` / `Set-NetConnectionProfile -NetworkCategory Private` | Netzwerkprofil |
| `Test-NetConnection srv01 -Port 3389` | Port-Erreichbarkeit testen |
| `netsh advfirewall show allprofiles` | Firewall-Status (klassisch) |
| `Get-CimInstance -Namespace root\Microsoft\Windows\DeviceGuard -ClassName Win32_DeviceGuard` | VBS/Credential Guard |

### Git / GitHub

| Befehl | Zweck |
|---|---|
| `git clone <url>` | Repo lokal kopieren |
| `git status` / `git log --oneline --graph` | Zustand / Historie |
| `git switch -c feature/x` (oder `git checkout -b`) | Branch erstellen und wechseln |
| `git add .` / `git commit -m "Nachricht"` | stagen / committen |
| `git push -u origin feature/x` / `git pull --rebase` | hochladen / aktualisieren |
| `git merge feature/x` | Branch einmergen |
| `gh pr create` / `gh pr review --approve` | PR per GitHub CLI |

### Bicep / Azure CLI / Azure PowerShell

| Befehl | Zweck |
|---|---|
| `az login` / `Connect-AzAccount` | anmelden |
| `az group create -n rg-demo -l switzerlandnorth` / `New-AzResourceGroup` | Ressourcengruppe |
| `az deployment group what-if -g rg-demo -f main.bicep` | Vorschau |
| `az deployment group create -g rg-demo -f main.bicep -p environmentType=prod` | bereitstellen |
| `New-AzResourceGroupDeployment -ResourceGroupName rg-demo -TemplateFile main.bicep [-WhatIf]` | bereitstellen (PowerShell) |
| `az bicep build -f main.bicep` / `az bicep decompile -f main.json` | Bicep → JSON / JSON → Bicep |
| `az provider register --namespace Microsoft.Web` | Provider registrieren |
| `az deployment operation group list -g rg-demo -n <deployment>` | Fehler eines Deployments |

---

<a id="korrekturen"></a>
## 15. Korrekturen zu den Kursunterlagen

| Nr. | Ort | Aussage in der Unterlage | Korrektur / Präzisierung |
|---|---|---|---|
| 1 | Unit 01, Folie 18; aa01a Frage 3 | VHDX als vierter «VHD-Typ» neben Fixed/Dynamic/Differencing | VHDX ist ein **Format** (wie VHD, VHDS). Fixed/Dynamic/Differencing gibt es in beiden Formaten. |
| 2 | Unit 01, Folie 8 | «Snapshots werden unterstützt» | Heute **Checkpoints** (Standard und Production, Standard ist Production). Ein Checkpoint ist **kein Backup**. |
| 3 | Unit 01, Folie 10 | Gast-OS inkl. CentOS | Stand Feb. 2024 korrekt. CentOS Linux ist seit 30.06.2024 ohne Support und in der aktuellen MS-Liste nicht mehr aufgeführt. |
| 4 | MS-Learn-Nachbereitung Hyper-V (Nested) | `Set-VMNetworkAdapter -VMName X \| Set-VMNetworkAdapter -MacAddressSpoofing On` | Richtig: `Get-VMNetworkAdapter -VMName X \| Set-VMNetworkAdapter -MacAddressSpoofing On` |
| 5 | MS-Learn-Nachbereitung Hyper-V (Nested) | nur Intel-CPUs (VT-x + EPT) | Aktuelle Doku: auch **AMD EPYC/Ryzen** ab Windows Server 2022/Windows 11, Konfigurationsversion ≥ 9.3 |
| 6 | Unit 05 neu, Folie 11 | «Credential Guard wird auf Domain Controllern **nicht unterstützt**» | MS: auf DCs **nicht empfohlen** (kein Zusatzschutz, Kompatibilitätsprobleme). Die alte Folie war hier genauer. |
| 7 | Unit 05, Folien 8/9 | Credential Guard «Windows 10/11» | nur **Enterprise und Education** (nicht Pro). Lizenz Windows E3/E5 bzw. A3/A5. |
| 8 | Unit 05 alt, Folie 17 | «Unternehmensbenutzer benötigen mindestens Defender for Endpoint P1» | **Defender Antivirus ist in Windows kostenlos enthalten.** P1/P2 bzw. Defender for Business sind für die **zentrale Verwaltung** und erweiterte Funktionen (EDR) nötig. |
| 9 | Unit 05, Demo PowerShell | `DefinitionUpdatesChannel = Broad`, `DisableCatchupQuickScan = Disable` | Der Parameter heisst in der aktuellen Doku `-SignaturesUpdatesChannel` (Umbenennung angekündigt). `DisableCatchupQuickScan` ist ein **Boolean** (`$false` = Catch-up-Scans aktiv). |
| 10 | Unit 05 alt, Folie 19 | Prozess ausschliessen = Prozess wird nicht gescannt | Ein **Prozess-Ausschluss** schliesst die **Dateien aus, die der Prozess öffnet**, nicht die EXE selbst. `Set-MpPreference` überschreibt Listen, `Add-MpPreference` ergänzt sie. |
| 11 | Unit 07, Folien 7/8 | Vektor «Skateboard» = [-3,3,2] bzw. [3,3,1] | widersprüchlich, aber nur illustrativ. Wichtig ist das Prinzip: Ähnliche Begriffe liegen nahe beieinander. |
| 12 | Unit 07, Folie 20 | «über 11'000 Modelle» | MS-Doku (09/2026): «mehr als 10 000 Modelle». Die Zahl ändert sich laufend. |
| 13 | Unit 07, Folien 30/36 | Security Copilot «seit 2026» in M365 E5/E7 | Rollout startete am **18.11.2025** (Ignite 2025) und lief gestaffelt bis 2026. |
| 14 | Unit 08, Folien 14 und 25 | Bicep-Codebeispiele | enthalten **typografische Anführungszeichen** (`’`) und auf Folie 25 eine **überzählige `}`**, würden also nicht kompilieren. Korrigierte Fassung in [9.5](#bicep). |
| 15 | Unit 06, Arbeitsauftrag Pull Request | Branch-Schutz im eigenen Repo einrichten | Wird bei **privaten Repos auf GitHub Free nicht durchgesetzt** (nur öffentlich oder Pro/Team). Eigene PRs kann man nicht selbst genehmigen. |
| 16 | aa01a Frage 1 | «Windows-Versionen … Installation von Hyper-V (**Gastbetriebssysteme**)» | Die Frage vermischt Host und Gast. Die erwartete Antwort (Win 10 Pro/Enterprise/Education) betrifft den **Host**. |
| 17 | aa01a Frage 13 | nur B (Secure Boot) richtig | A ist ebenfalls korrekt: Gen 2 unterstützt mehr vCPUs (Gen 1 max. 64). |
| 18 | aa01a Frage 22 | Shielded VMs = «Ausführung in isolierten Containern» | Shielded VMs sind **verschlüsselte VMs**, die nur auf durch den Host Guardian Service freigegebenen Hosts laufen, keine Container. |

---

<a id="hinweise"></a>
## 16. Hinweise zum Material

- **Zwei Versionen von Unit 05:** `SIUS_Unit_05_GrundlagenDefender.pdf` (April 2024, mit Musterantworten) und `SIUS_Unit_05_GrundlagenDefender 25.8.26.pdf` (August 2026, mit Gruppenaufträgen). Die neue Version ist die aktuelle. Die Antworten der alten sind mit 🗂️ markiert.
- **Folienstände:** Mehrere Foliensätze tragen alte Daten (Feb.–Juni 2024), wurden aber 2026 verwendet. Unit 07 (Sept. 2026) und Unit 08 (Sept. 2026, Markus Nussbaumer) sind neu erstellt.
- **Umbenannte Nachbereitungs-Module (Stand 28.09.2026):**
  - `intro-to-endpoint-manager` → *Introduction to Microsoft Intune*
  - `manage-devices-with-microsoft-endpoint-manager` → *Understand device management using Microsoft Intune*
  - `benefits-microsoft-endpoint-manager` → *Benefits of Microsoft Intune*
  - `manage-defender-windows-client` → *MD-102: Manage Microsoft Defender in Windows client*
  - `fundamentals-generative-ai` → *Introduction to generative AI and agents* (die deutsche Fassung heisst noch *Einführung in generative KI-Konzepte* und hat andere Einheiten)
  - `build-first-bicep-template` → *Build your first Bicep file* (URL `build-first-bicep-file`, die Übungslinks aus den Folien werden umgeleitet)
  - `introduction-to-infrastructure-as-code-using-bicep` wurde beim Abruf umgeleitet. Der Inhalt findet sich im Lernpfad *Fundamentals of Bicep*.
- **Nicht in den Unterlagen enthalten:** die **Demos** (Hyper-V-Installation, Docker/Kubernetes-Installation, Intune, Arc, RBAC, Resource Graph, Advanced Hunting, Firewall, Foundry, Security Copilot, Bicep). Sie sind nur als Titelfolien vorhanden, ihr Inhalt ist hier aus den MS-Learn-Modulen rekonstruiert. Ebenso das **YouTube-Video** «Azure Bicep Crashkurs» (nur die Erkenntnisse-Folie ist dabei).
- **Leere bzw. Bild-Folien:** Unit 07 Folie 5 (leer) und 9 (animierte Attention-Grafik ohne Inhalt im PDF). Unit 08 Folien 22–24 (im PDF leer, vermutlich Aktivierungs-Elemente der Repetition). Der Inhalt der Diagramm-Folien (Hypervisor, Nested, Azure Local, Container/VM-Architektur, Isolation, Docker Engine, Kubernetes, Intune, Arc, MCRA, KI-Whiteboard, ARM) ist in den Kapiteln textlich beschrieben.
- **Foliennummern:** Angaben wie «Folie 21» beziehen sich auf die **auf der Folie gedruckte Nummer**. Diese weicht in einigen PDFs von der Seitenzahl ab (z. B. Unit 02, Unit 05 neu).
- **SYSI-Material fehlt** im Repository. Kapitel 10.4 basiert auf Recherche und Grundlagenwissen.

---

<a id="glossar"></a>
## 17. Glossar

| Begriff | Erklärung |
|---|---|
| **ACR** | Azure Container Registry, private Registry für Container-Images |
| **AGDLP** | Accounts → Global Groups → Domain Local Groups → Permissions |
| **AKS** | Azure Kubernetes Service, verwaltetes Kubernetes |
| **ARM** | Azure Resource Manager, Verwaltungsschicht (Control Plane) von Azure |
| **ASR** | Attack Surface Reduction, Regeln gegen typische Angriffstechniken (z. B. Makros, die Prozesse starten) |
| **Autopilot** | Bereitstellung von Windows-Geräten ab Werk ohne Imaging |
| **AVM** | Azure Verified Modules, geprüfte Bicep-/Terraform-Module von Microsoft |
| **Azure Local** | früher Azure Stack HCI, hyperkonvergente On-Prem-Plattform (Hyper-V + S2D), verwaltet über Arc |
| **Bicep** | deklarative IaC-Sprache für Azure (→ ARM-JSON) |
| **BYOD** | Bring Your Own Device, private Geräte im Firmeneinsatz |
| **Checkpoint** | Zustand einer VM zu einem Zeitpunkt (Standard/Production), früher Snapshot |
| **CI/CD** | Continuous Integration / Continuous Delivery (z. B. GitHub Actions) |
| **Co-Management** | gleichzeitige Verwaltung mit ConfigMgr und Intune |
| **Conditional Access** | Entra-Richtlinien «wenn Signal, dann Zugriff mit Bedingung/Block» |
| **Connected Machine Agent** | Agent von Azure Arc auf dem Server (HIMDS, Guest Config, Extension Manager) |
| **Container** | isolierte App-Laufzeitumgebung, teilt den Kernel des Hosts |
| **Credential Guard** | isoliert NTLM-Hashes/Kerberos-TGTs mit VBS im Prozess LSAIso |
| **CSV** | Cluster Shared Volume, gemeinsam genutztes Volume im Failover-Cluster |
| **DEM** | Device Enrollment Manager, Konto für die Massenregistrierung (bis 1000 Geräte) |
| **Deployment (Foundry)** | bereitgestellte Instanz eines Modells mit Name, Version, Typ, Quota |
| **Dockerfile** | Bauanleitung für ein Container-Image |
| **Dynamic Memory** | RAM einer VM dynamisch zwischen Minimum und Maximum |
| **EDR** | Endpoint Detection & Response, Verhaltensanalyse und Reaktion auf Endpunkten |
| **Embedding** | Vektor, der die Bedeutung eines Tokens/Texts darstellt |
| **Entra ID** | Cloud-Identitätsdienst von Microsoft (früher Azure AD) |
| **Foundry** | Microsoft Foundry, Plattform für KI-Apps und Agenten in Azure |
| **Generation 1/2** | VM-Hardwaretyp: BIOS/IDE vs. UEFI/SCSI/Secure Boot |
| **GitHub Flow** | Branch → Commit → PR → Review → Merge → Deploy |
| **HCS** | Host Compute Service, Windows-API unter Containern und VMs |
| **HIMDS** | Hybrid Instance Metadata Service (Arc-Agent: Identität, Heartbeat) |
| **Hypervisor** | Virtualisierungsschicht zwischen Hardware und VMs (Hyper-V = Typ 1) |
| **IaC** | Infrastructure as Code |
| **Integration Services** | Dienste für die Host-Gast-Kommunikation (Heartbeat, Zeit, Shutdown, KVP, VSS) |
| **KQL** | Kusto Query Language (Resource Graph, Log Analytics, Advanced Hunting, Sentinel) |
| **kubelet / kube-proxy** | Kubernetes-Node-Agent / Netzwerkregeln für Services |
| **LAPS** | Local Administrator Password Solution, rotiert lokale Admin-Passwörter |
| **Lateral Movement** | seitliche Ausbreitung eines Angreifers von System zu System |
| **LLM** | Large Language Model |
| **LSASS / LSAIso** | Local Security Authority (Prozess mit Credentials) / isolierte Variante unter Credential Guard |
| **MAM / MDM** | Mobile Application / Device Management |
| **MCR** | Microsoft Container Registry (mcr.microsoft.com) |
| **MDE** | Microsoft Defender for Endpoint (P1/P2) |
| **Nested Virtualization** | Hyper-V in einer VM |
| **Pod** | kleinste Kubernetes-Einheit (ein oder mehrere Container) |
| **Promptbook** | gespeicherte Prompt-Abfolge in Security Copilot |
| **Pull Request** | Vorschlag, Änderungen eines Branches zu übernehmen, mit Review |
| **RAG** | Retrieval-Augmented Generation, Antworten mit eigenen Dokumenten anreichern |
| **RBAC** | Role-Based Access Control |
| **Resource Provider** | Namespace eines Azure-Dienstes (z. B. `Microsoft.Storage`) |
| **SCU** | Security Compute Unit, Recheneinheit von Security Copilot |
| **Secure Boot** | UEFI-Funktion: nur signierte Bootloader/Treiber starten |
| **SLAT** | Second Level Address Translation (Intel EPT / AMD RVI), Voraussetzung für Hyper-V |
| **Tenant Attach** | ConfigMgr-Geräte in Intune sichtbar machen |
| **Token** | kleinste Texteinheit eines Sprachmodells, Basis für Kontextfenster und Abrechnung |
| **VBS** | Virtualization-Based Security, per Hypervisor isolierter Speicherbereich |
| **VHD / VHDX** | Formate für virtuelle Festplatten (2040 GB / 64 TB) |
| **vSwitch** | virtueller Switch (extern, intern, privat) |
| **WAC** | Windows Admin Center, webbasiertes Verwaltungstool |
| **WFAS** | Windows Defender Firewall with Advanced Security |

---

<a id="quellen"></a>
## 18. Quellen

**Kursunterlagen** (Ordner `Kursmaterialien/`):
- `SIUS_Unit_00_Vorstellung.pdf`, `SIUS_Unit_01_GrundlagenMicrosoftHyperV.pdf`, `SIUS_Unit_02_GrundlagenContainer.pdf`, `SIUS_Unit_03_GrundlagenMicrosoftIntune.pdf`, `SIUS_Unit_04_GrundlagenAzureArc.pdf`, `SIUS_Unit_05_GrundlagenDefender.pdf` (April 2024), `SIUS_Unit_05_GrundlagenDefender 25.8.26.pdf` (August 2026), `SIUS_Unit_06_GrundlagenGitHub.pdf`, `SIUS_Unit_07_Foundry_SecurityCopilot_OpenAI.pdf`, `SIUS_Unit_08_GrundlagenBicep & Repetition.pdf`
- `aa01a_HyperV_MultipleChoiceFragen.docx`, `aa01b_HyperV_VirtuelleMaschineErstellen.docx`, `B5 - Auftrag Security Experts – Defender & Firewall.pdf`, `Übungsauftrag Selbststudium – Bicep.pdf`
- Ergänzend: `3. Semester/CSIN/CSIN_Client_Server_Installation.md` (eigene Zusammenfassung Vorfach)

**🔎 Online-Recherche (abgerufen am 28.09.2026):**

*Hyper-V*
- MS Learn: [Configure and manage Hyper-V](https://learn.microsoft.com/en-us/training/modules/configure-manage-hyper-v/), [Configure and manage Hyper-V virtual machines](https://learn.microsoft.com/en-us/training/modules/configure-manage-hyper-v-virtual-machines/)
- [Using checkpoints](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/checkpoints), [Hyper-V Maximum Scale Limits](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/maximum-scale-limits)
- [What is Nested Virtualization](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/nested-virtualization), [Run Hyper-V in a VM with Nested Virtualization](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/enable-nested-virtualization)
- Microsoft Q&A: [Windows Server 2019 Essentials Hyper-V Licensing](https://learn.microsoft.com/en-us/answers/questions/60156/windows-server-2019-essentials-hyper-v-licensing) (zu aa01a Frage 24)

*Container*
- MS Learn: [Run containers on Windows Server](https://learn.microsoft.com/en-us/training/modules/run-containers-windows-server/), [Orchestrate containers on Windows Server using Kubernetes](https://learn.microsoft.com/en-us/training/modules/orchestrate-containers-windows-server-using-kubernetes/)
- [Containers vs. virtual machines](https://learn.microsoft.com/en-us/virtualization/windowscontainers/about/containers-vs-vm), [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)

*Intune*
- MS Learn: [Introduction to Microsoft Intune](https://learn.microsoft.com/en-us/training/modules/intro-to-endpoint-manager/), [Understand device management using Microsoft Intune](https://learn.microsoft.com/en-us/training/modules/manage-devices-with-microsoft-endpoint-manager/), [Benefits of Microsoft Intune](https://learn.microsoft.com/en-us/training/modules/benefits-microsoft-endpoint-manager/)
- [Device features and settings (Profiltypen)](https://learn.microsoft.com/en-us/intune/intune-service/configuration/device-profiles), [Import custom ADMX templates](https://learn.microsoft.com/en-us/intune/intune-service/configuration/administrative-templates-import-custom), [Device compliance policies](https://learn.microsoft.com/en-us/intune/intune-service/protect/device-compliance-get-started), [Endpoint analytics overview](https://learn.microsoft.com/en-us/intune/endpoint-analytics/)

*Azure Arc*
- MS Learn: [Manage hybrid workloads with Azure Arc](https://learn.microsoft.com/en-us/training/modules/manage-hybrid-workloads-azure-arc/)
- [Deployment options](https://learn.microsoft.com/en-us/azure/azure-arc/servers/deployment-options), [Prerequisites](https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites), [Network requirements](https://learn.microsoft.com/en-us/azure/azure-arc/servers/network-requirements), [azcmagent CLI](https://learn.microsoft.com/en-us/azure/azure-arc/servers/azcmagent)
- [Azure Arc pricing](https://azure.microsoft.com/en-us/pricing/details/azure-arc/core-control-plane/), [Azure Update Manager](https://learn.microsoft.com/en-us/azure/update-manager/overview), [Azure Resource Graph](https://learn.microsoft.com/en-us/azure/governance/resource-graph/overview)

*Defender, Credential Guard, Firewall*
- MS Learn: [MD-102 Manage Microsoft Defender in Windows client](https://learn.microsoft.com/en-us/training/modules/manage-defender-windows-client/)
- [Credential Guard overview](https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/), [How Credential Guard works](https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/how-it-works)
- [Set-MpPreference](https://learn.microsoft.com/en-us/powershell/module/defender/set-mppreference), [Gradual rollout / update channels](https://learn.microsoft.com/en-us/defender-endpoint/manage-gradual-rollout), [Defender AV compatibility (active/passive)](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-compatibility)
- [DeviceTvmInfoGathering table](https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-devicetvminfogathering-table), [Microsoft Defender service description](https://learn.microsoft.com/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-defender-service-description)
- [Windows Resiliency Initiative](https://www.microsoft.com/en-us/windows/business/windows-resiliency-initiative), [Windows 11 24H2 Security Baseline](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/windows-11-version-24h2-security-baseline/ba-p/4252801)

*GitHub*
- MS Learn: [Introduction to GitHub](https://learn.microsoft.com/en-us/training/modules/introduction-to-github/)
- GitHub Docs: [About protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches), [Permission levels for a personal account repository](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-personal-account-settings/permission-levels-for-a-personal-account-repository)

*KI, Foundry, Security Copilot*
- MS Learn: [Introduction to generative AI and agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/) (Units LLMs, Prompts, Agents), [Responsible AI](https://learn.microsoft.com/en-us/training/modules/get-started-ai-fundamentals/7-responsible-ai)
- [Microsoft Foundry documentation](https://learn.microsoft.com/en-us/azure/foundry/), [What is Microsoft Foundry?](https://learn.microsoft.com/en-us/azure/foundry/what-is-foundry), [Deployment types](https://learn.microsoft.com/en-us/azure/foundry/foundry-models/concepts/deployment-types)
- [Security Copilot for Microsoft 365 E5 and E7](https://learn.microsoft.com/en-us/copilot/security/security-copilot-inclusion), [Security Compute Units and capacity](https://learn.microsoft.com/en-us/copilot/security/security-compute-units-capacity)
- Anthropic Academy: [AI Fluency: Framework & Foundations](https://academy.claude.com/courses/ai-fluency-framework-foundations/)

*Bicep / ARM*
- MS Learn: [Build your first Bicep file](https://learn.microsoft.com/en-us/training/modules/build-first-bicep-file/), [Fundamentals of Bicep (Lernpfad)](https://learn.microsoft.com/en-us/training/paths/fundamentals-bicep/)
- [Child resources in Bicep](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/child-resource-name-type), [Resource providers and types](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/resource-providers-and-types)

*Vorfächer*
- [Windows LAPS overview](https://learn.microsoft.com/en-us/windows-server/identity/laps/laps-overview), [DHCP failover](https://learn.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-failover), [Windows 10 support has ended](https://support.microsoft.com/en-us/windows/deployment/updates-lifecycle/windows-10-support-has-ended-on-october-14-2025), [Windows 10 ESU](https://learn.microsoft.com/en-us/windows/whats-new/extended-security-updates)
