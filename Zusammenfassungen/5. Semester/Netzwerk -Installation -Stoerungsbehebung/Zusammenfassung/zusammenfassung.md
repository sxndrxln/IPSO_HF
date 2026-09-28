# NIUS – Netzwerk-Installation & Störungsbehebung

**Zusammenfassung für die Modulprüfung (Open Book)**
HF Informatik – Plattformentwicklung, 5. Semester · Fachcode NIUS.TA1A · Stand: 28.09.2026

> Grundlage: alle Unterlagen im Ordner `Kursmaterialien/` (NIUS-Foliensatz V1.2, NPDO-Foliensatz V1.0 als Vorgängermodul, Skripte «Einführung in BGP» und «Wireshark, eine Einführung», Aufgabenblätter B1/B3/B7, Selbststudium-Aufgaben, WLC-Tutorial, Troubleshooting-Labs und LAB-Lösungen, CCNA 200-301 Portable Command Guide). Ergänzt mit Online-Recherche (Quellen am Schluss).

### Legende

| Symbol | Bedeutung |
|---|---|
| 🧪 | In den Kursfolien mit dem Symbol **`LAB>_`** markiert. Laut Folien musst du diese Befehle **anwenden und die Ausgaben interpretieren** können (prüfungsrelevant). |
| 🔎 | **Ergänzung aus der Recherche** oder aus dem CCNA Command Guide. Steht nicht so in den Folien. |
| ⚠️ | **Korrektur**: Die Kursunterlage enthält hier einen Fehler oder eine missverständliche Angabe. Alle Korrekturen sind in [Kapitel 10](#korrekturen) gesammelt. |

---

## Inhaltsverzeichnis

1. [Prüfung und Modulüberblick](#pruefung)
2. [Block 1 – WAN, MPLS, BGP, hierarchische Netze](#b1)
3. [Block 2 – Device Management, Netzwerkmanagement, Wireshark und TCP-Analyse](#b2)
4. [Block 3 – WLAN planen](#b3)
5. [Block 4 – CLI, VLANs, redundante L2/L3-Netze](#b4)
6. [Block 5 – Routing in IPv4 und IPv6](#b5)
7. [Block 6 – ACLs, NAT und Kombination der Technologien](#b6)
8. [Block 7 und 8 – Strukturierte Störungsbehebung](#b7)
9. [Praxistransfer-Aufgaben (Selbststudium)](#praxistransfer)
10. [Korrekturen zu den Kursunterlagen](#korrekturen)
11. [Hinweise zum Material und Lücken](#hinweise)
12. [Quellen](#quellen)

---

<a id="pruefung"></a>
## 1. Prüfung und Modulüberblick

### Prüfungsform (laut Folien)

- **Modulprüfung NIUS.** (Die älteren Folien von 2022 nennen eine gemeinsame Prüfung mit dem Fach MOCO über 3 Lektionen; im aktuellen Unterrichtsplan ist nur NIUS enthalten.)
- **Open Book:** Alle Offline-Unterlagen sind erlaubt. **Kein Internet.**
- Du brauchst den **Cisco Packet Tracer (PT)** auf deinem Notebook.
- Für die Lösungsblätter: **blauer oder schwarzer Kugelschreiber**, kein Bleistift.
- **Stoffumfang:** alle Folien, alle LABs, der Lesestoff aus den Büchern und **alle Cisco-Commands aus allen Unterlagen**. Die Netzwerkmodule bauen aufeinander auf, deshalb wird der **gesamte Netzwerkstoff** abgefragt, vor allem die Installation von Cisco-Geräten (also auch NPDO-Stoff wie VLAN, STP, ACL, NAT, OSPF).
- Tipps aus den Folien: viel mit PT üben, eigenes Wiki bzw. eigene Command-Sammlung führen.

### Kompetenzen und Taxonomie

Ziel des Fachs: IP-basierte Netzwerke **installieren, Störungen analysieren und beheben**. Die Prüfung ist stark anwendungsorientiert:

| K-Stufe | Bedeutung | Anteil |
|---|---|---|
| K3 | Anwenden (Wissen problemlösend transferieren) | 18 % |
| K4 | Analysieren (Zusammenhänge und Widersprüche erkennen) | 5 % |
| K5 | Synthese (Lösungswege vorschlagen, Schemata entwerfen) | 77 % |

Handlungskompetenzen aus dem Fachplan: B4.6 (Werkzeuge einsetzen), B9.1/B9.3 (Sicherheitskonzepte, Schutzmassnahmen), B12.1–B12.3 (Architektur und Konfigurationen analysieren, Soll-Zustand entwickeln), B14.2 (Probleme im Betrieb überwachen, identifizieren, beheben oder eskalieren).

### Die 8 Modulblöcke («roter Faden»)

| Block | Thema | Du kannst … | Vertiefung (Buch) |
|---|---|---|---|
| 1 | Grundlagen WAN, MPLS und BGP | WAN-Protokolle wie MPLS einordnen, BGP in der Planung einordnen, hierarchische Netze entwerfen | CCNA2 Kap. 13, 14 |
| 2 | Device Management, SNMP, TCP-Analyse | Geräte sichern, wiederherstellen, zurücksetzen; SNMP und Syslog planen; TCP-Probleme analysieren (Retransmission, Fast Retransmission, Zero Window) | CCNA2 Kap. 5, 9, 12 |
| 3 | WLAN planen | WLAN-Installationen planen, Störquellen erkennen und vermeiden | CCNA1 Kap. 26, 28 |
| 4 | Redundante Netzwerke | mehrere Netzsegmente, Redundanz, L2/L3-Switches und Router, VLANs für KMU | CCNA1 Kap. 8, 17 |
| 5 | IPv4- und IPv6-Routing | statische und dynamische Routen planen, Routingkonzept (connected, static, dynamic), OSPF/EIGRP für IPv6 | CCNA1 Kap. 16, 19–21, 25 |
| 6 | LABs Installation und Fehlersuche | IPv4, IPv6, VLAN, VTP, STP, ACL, NAT, FHRP konfigurieren und kombinieren | CCNA1 Kap. 10, 18 |
| 7 | LABs Fehlersuche | durch VLANs (802.1Q) und STP verursachte Störungen lösen | CCNA1 Kap. 9 |
| 8 | LABs Fehlersuche | durch Routing und ACLs verursachte Störungen lösen, strukturiert vorgehen | CCNA2 Kap. 2, 3 |

Pflichtlehrmittel: Wendell Odom, *Cisco CCNA 200-301 Official Cert Guide*, Volume 1 (CCNA1) und Volume 2 (CCNA2). Hilfsmittel: Notebook, Packet Tracer, Wireshark, netacad.com.

### Dokumentations-Adressen 🧪

Für Beispiele und Labs werden reservierte Adressbereiche verwendet (nie im Internet geroutet):

| Bereich | Norm | Zweck |
|---|---|---|
| `192.0.2.0/24` (TEST-NET-1), `198.51.100.0/24` (TEST-NET-2), `203.0.113.0/24` (TEST-NET-3) | RFC 5737 | «öffentliche» IPv4-Adressen in Dokumentationen |
| `2001:db8::/32` | RFC 3849 | IPv6-Dokumentationspräfix |
| `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16` | RFC 1918 | private IPv4-Adressen (brauchen NAT ins Internet) |

---

<a id="b1"></a>
## 2. Block 1 – WAN, MPLS, BGP, hierarchische Netze

### 2.1 WAN-Grundlagen

**Bandbreitennutzung**

- **Basisbandübertragung:** Die ganze Bandbreite steht einem Signal zur Verfügung (typisch LAN, z. B. Ethernet).
- **Breitbandübertragung:** Das Medium wird in Kanäle aufgeteilt, eine Verbindung nutzt nur einen Kanal (typisch WAN, z. B. Kabel-TV).

**Klassische WAN-Begriffe**

| Begriff | Bedeutung |
|---|---|
| CPE | Customer Premises Equipment: Geräte beim Kunden (Router, serielle Karte). |
| CSU/DSU | Channel/Data Service Unit: Abschluss der physischen WAN-Leitung (extern oder im Router). |
| Point-to-Point / Standleitung | Feste Verbindung zwischen zwei Standorten. |
| DTE / DCE | Data Terminal Equipment (Kunde) / Data Communication Equipment (Provider). Das DCE gibt den Takt vor (`clock rate`). |
| HDLC | High-Level Data Link Control. L2-Protokoll für serielle Punkt-zu-Punkt-Links (Cisco-Default). |
| PPP | Point-to-Point Protocol. L2 für Punkt-zu-Punkt mit Authentifizierung (PAP/CHAP). |

**WAN-Anbindungen**

| Technologie | Eigenschaften |
|---|---|
| Modem (analog/ISDN) | Nur noch für Wartung und Fernüberwachung. |
| DSL (ADSL/VDSL) | Nutzt Telefonleitung. Günstig, aber ohne SLA (Business-DSL) nicht ausfallsicher. |
| Kabel (Cable) | Nutzt TV-Kabel. Günstig, meist schneller als DSL. |
| FTTH | Glasfaser bis ins Gebäude. Auch hier auf SLA achten. |
| Standleitung «Dark Fiber / Dark Copper» | Nur die Leitung wird gemietet, die aktiven Geräte betreibt man selbst («dunkle», unbeleuchtete Faser). |

**Evaluation einer WAN-Anbindung (Aufgabe B1):** Pro Provider (Swisscom, Sunrise/UPC, Quickline, Init7 …) abklären: Angebote und Kosten für KMU-Internet und Standleitung zwischen zwei Standorten (z. B. Bern–Zürich), **SLA** (Verfügbarkeit, Reaktions- und Entstörzeiten), öffentliche IPv4/IPv6-Adressen, Zusatzdienste (z. B. Reverse-DNS/PTR für Mailserver), Homeoffice-Anbindung, Fazit und Empfehlung.

### 2.2 Hierarchisches Netzwerkdesign

| Schicht | Aufgabe |
|---|---|
| **Access Layer** (Zugangsschicht) | Anschluss der Endgeräte (PCs, Drucker, IP-Telefone, APs). Access-Switches, Port-Security, PoE. |
| **Distribution Layer** (Verteilerschicht) | Steuert den Datenfluss, **Routing zwischen VLANs**, Policies (ACLs). Leistungsfähige, redundante L3-Switches. |
| **Core Layer** (Kernschicht) | Hochgeschwindigkeits-Backbone. Muss schnell und hochverfügbar sein, keine aufwendigen Policies. |

In kleineren Netzen werden Distribution und Core zusammengefasst (**Collapsed Core**, 2-Schichten-Modell).

🔎 **Redundanz im Design:** doppelte Uplinks von jedem Access-Switch zu zwei Distribution-Switches (STP bzw. EtherChannel), FHRP (z. B. HSRP) für ein ausfallsicheres Default-Gateway, redundante Internetanbindung am Hauptstandort. Mehr dazu in [Block 4](#b4).

### 2.3 MPLS (Multiprotocol Label Switching)

- MPLS ist eine erste technische Umsetzung von **NGN (Next Generation Network)**: Die früheren leitungsvermittelten Dienste werden über **ein** IP-Netz ersetzt.
- Im Providernetz wird meist **OSPF oder IS-IS** als IGP verwendet, dazu BGP und Erweiterungen wie CSPF (Traffic Engineering).
- Über das MPLS-Netz kann der Kunde **eigene Routingprotokolle** betreiben.
- Vorteil: Router leiten anhand eines kurzen **Labels** weiter statt anhand eines vollständigen Routing-Lookups (Label Switched Routers, weniger Aufwand).
- Einordnung im TCP/IP-Modell: MPLS liegt **zwischen Netzzugang (L2) und IP (L3)**, deshalb oft «Layer 2,5».

| Rolle | Beschreibung |
|---|---|
| **CE** – Customer Edge Router | Router des Kunden. Spricht **kein** MPLS, nur statisches Routing oder ein Routingprotokoll zum PE. |
| **PE** – Provider Edge Router | Rand des Providernetzes, hier wird das MPLS-VPN konfiguriert (Label wird aufgesetzt bzw. entfernt). |
| **P** – Provider Router | Kernrouter im Providernetz, leitet nur anhand der Labels weiter. |

- **Layer-3-MPLS-VPN:** Jeder Standort hat ein eigenes Subnetz, der Provider routet dazwischen.
- **Layer-2-MPLS-VPN** (🔎 z. B. VPLS): Beide Standorte liegen im **gleichen Subnetz**. Praktisch für Redundanz zwischen Rechenzentren.

CE-Konfiguration bei L3-MPLS (das MPLS selbst konfiguriert der Provider auf dem PE):

```
R1(config)# interface GigabitEthernet0/0
R1(config-if)# ip address 10.0.1.2 255.255.255.252
R1(config)# ip route 10.0.2.0 255.255.255.0 10.0.1.1
```

Ob auf dem CE statisch oder mit einem Routingprotokoll gearbeitet wird, klärst du mit dem MPLS-Provider.

🔎 **Technische Details:**
- Der MPLS-Header (Shim Header) ist **32 Bit** lang: **20 Bit Label**, **3 Bit Traffic Class** (QoS), **1 Bit Bottom of Stack** (S, mehrere Labels können gestapelt werden) und **8 Bit TTL**.
- Operationen: **Push** (Label aufsetzen, am Eingangs-PE/LER), **Swap** (Label tauschen, auf P-Routern/LSR), **Pop** (Label entfernen, am Ausgangs-PE).
- Labels werden meist über **LDP** (Label Distribution Protocol) verteilt, der Pfad heisst **LSP** (Label Switched Path).

### 2.4 BGP (Border Gateway Protocol)

**Warum BGP?** IGPs wie OSPF skalieren nicht für das Internet (fast 1 Mio. IPv4-Routen, jeder Router müsste bei jeder Änderung die ganze Topologie neu berechnen). Deshalb die Trennung:

| | IGP (Interior Gateway Protocol) | EGP (Exterior Gateway Protocol) |
|---|---|---|
| Einsatz | Routing **innerhalb** eines AS (Intra-Domain) | Routing **zwischen** AS (Inter-Domain) |
| Fokus | schnelle Konvergenz, kürzester Weg | Skalierbarkeit, Stabilität, **Kontrolle (Routing Policies)** |
| Beispiele | OSPF, EIGRP, IS-IS (alt: RIP, IGRP) | **BGP-4** (einziger Standard im Internet, seit 1994, unterstützt CIDR) |

Geschichte: 1989 von Kirk Lougheed (Cisco) und Yakov Rekhter (IBM) auf drei Servietten skizziert («Three-Napkin Protocol»), erster Standard RFC 1105.

**Autonome Systeme (AS)**

- Ein AS ist eine Gruppe von IP-Netzen unter **einer** administrativen Instanz mit einheitlicher Routing-Policy (ISP, Cloud-Anbieter, Hochschule, Grossunternehmen). Metapher: ein **Land**; innen OSPF (Strassen), an der Grenze BGP (Grenzübergänge).
- **ASN** (AS-Nummer): Vergabe durch **IANA** an die regionalen Registries; für Europa und die Schweiz **RIPE NCC** (Amsterdam).
- **16 Bit** (1–65535, alt) und **32 Bit** (über 4 Mrd., heute Standard).
- **Private ASNs:** 64512–65534 (16 Bit) und 🔎 4200000000–4294967294 (32 Bit, RFC 6996). Dürfen nie im Internet auftauchen; der Provider entfernt sie.
- Schweizer Beispiele: **AS3303** Swisscom, **AS6730** Sunrise, **AS13030** Init7, **AS559** SWITCH (Hochschulen, älteste ASN der Schweiz). Nachschlagen z. B. mit bgp.he.net.

| AS-Rolle | Beschreibung |
|---|---|
| **Stub AS** | Nur an **einen** Provider angebunden, Sackgasse. |
| **Multihomed AS** | An **zwei oder mehr** Provider angebunden (Redundanz), lässt aber keinen fremden Transitverkehr durch. |
| **Transit AS** | ISP: leitet Verkehr fremder AS weiter («Autobahnen» des Internets). |

**Grundprinzipien**

- BGP ist ein **Path-Vector-Protokoll**: Es kennt keine Links, sondern nur die Liste der AS, durch die eine Route führt (**AS_PATH**).
- **BGP findet Nachbarn nicht automatisch.** Jeder Peer wird manuell mit IP und AS konfiguriert. Transport über **TCP Port 179** (kein Multicast). Die Peers müssen also nicht direkt verbunden sein, sondern nur per IP erreichbar.
- **Loop Prevention (eBGP):** Ein Router verwirft jedes Update, in dessen AS_PATH seine **eigene ASN** steht.

| | eBGP (external) | iBGP (internal) |
|---|---|---|
| Nachbar | in **anderem** AS | im **gleichen** AS |
| TTL | **1** → Peers meist direkt verbunden (Ausnahme `ebgp-multihop`) | **255** → Peers können weit entfernt sein, IGP stellt Erreichbarkeit sicher |
| Administrative Distanz (Cisco) | **20** | **200** |
| AS_PATH | eigene ASN wird vorangestellt | unverändert |
| Next Hop | wird auf eigene IP gesetzt | wird standardmässig **nicht** geändert (häufige Fehlerquelle) |

**iBGP Split Horizon:** Eine von einem iBGP-Nachbarn gelernte Route wird **nie** an einen anderen iBGP-Nachbarn weitergegeben. Folge: **Full Mesh** nötig, also n·(n−1)/2 Sessions (10 Router = 45, 100 Router ≈ 5000).
**Lösung Route Reflector (RR):** Clients peeren nur noch mit dem RR, der die Regel kontrolliert bricht und Routen an alle Clients «reflektiert». Loop-Schutz im AS über die Attribute **ORIGINATOR_ID** (Router-ID des Ursprungsrouters) und **CLUSTER_LIST** (IDs der durchlaufenen RRs).

🔎 **BGP-Nachbarzustände:** Idle → Connect → Active → OpenSent → OpenConfirm → **Established** (erst jetzt werden Routen ausgetauscht). Hängt ein Peer in **Active**, klappt der TCP-Aufbau nicht (falsche Neighbor-IP, falsches `remote-as`, keine Erreichbarkeit, ACL blockiert TCP 179).

🔎 **Best-Path-Auswahl (Cisco, vereinfacht):** höchstes Weight → höchste Local Preference → lokal erzeugt → **kürzester AS_PATH** → Origin (IGP < EGP < incomplete) → tiefster MED → eBGP vor iBGP → nächster IGP-Next-Hop → … → tiefste Router-ID. Die Folie «Metrik = Anzahl AS» beschreibt also nur ein Kriterium.

#### BGP konfigurieren 🧪

Topologie aus den Folien: R1 (AS 10) – R2 (AS 20) – R3 (AS 30); Transfernetze 192.0.2.0/30 und 192.0.2.4/30; LANs 192.168.1.0/24 (R1) und 192.168.2.0/24 (R3).

```
R1(config)# router bgp 10
R1(config-router)# neighbor 192.0.2.2 remote-as 20
R1(config-router)# network 192.0.2.0 mask 255.255.255.252
R1(config-router)# network 192.168.1.0 mask 255.255.255.0

R2(config)# router bgp 20
R2(config-router)# neighbor 192.0.2.1 remote-as 10
R2(config-router)# neighbor 192.0.2.6 remote-as 30
R2(config-router)# network 192.0.2.0 mask 255.255.255.252
R2(config-router)# network 192.0.2.4 mask 255.255.255.252

R3(config)# router bgp 30
R3(config-router)# neighbor 192.0.2.5 remote-as 20
R3(config-router)# network 192.0.2.4 mask 255.255.255.252
R3(config-router)# network 192.168.2.0 mask 255.255.255.0
```

- Wichtig: `network … mask …` kündigt ein Netz nur an, wenn es **exakt so** (Netz und Maske) in der Routingtabelle steht.
- **Summarisation-Trick:** Statt der einzelnen /30 wird das ganze /24 angekündigt. Die Null-Route sorgt dafür, dass das /24 in der Routingtabelle existiert:
  ```
  R2(config)# ip route 192.0.2.0 255.255.255.0 null0
  R2(config)# router bgp 20
  R2(config-router)# network 192.0.2.0 mask 255.255.255.0
  ```
  ⚠️ Auf der Folie fehlt das `network`-Statement für das /24. Ohne dieses wird nichts angekündigt.

**iBGP im selben AS** (Peering über Loopbacks, weil diese nicht ausfallen, solange irgendein Pfad besteht):

```
R1(config)# interface loopback 0
R1(config-if)# ip address 10.0.2.1 255.255.255.255     (kein no shutdown nötig)
R1(config)# router bgp 100
R1(config-router)# neighbor 10.0.2.2 remote-as 100
R1(config-router)# neighbor 10.0.2.2 update-source loopback 0

R2(config)# interface loopback 0
R2(config-if)# ip address 10.0.2.2 255.255.255.255
R2(config)# router bgp 100
R2(config-router)# neighbor 10.0.2.1 remote-as 100
R2(config-router)# neighbor 10.0.2.1 update-source loopback 0
```

🔎 Die Loopbacks müssen sich gegenseitig über ein IGP (z. B. OSPF) oder statische Routen erreichen, sonst bleibt die Session in **Active**.

**Überprüfen:**

| Befehl | Zeigt |
|---|---|
| `show ip bgp summary` | Übersicht aller Peers. Spalte **State/PfxRcd**: eine **Zahl** = Established mit so vielen empfangenen Präfixen; `Idle`/`Active` = Session nicht aufgebaut. |
| `show ip bgp neighbors` | Details pro Peer (Zustand, Timer, Nachrichten). |
| `show ip bgp` | BGP-Tabelle; `*>` = gültige beste Route, Spalte Path = AS_PATH. |
| `show ip route bgp` | In die Routingtabelle übernommene BGP-Routen (Code **B**). |
| `show run \| section bgp` | BGP-Konfiguration. |
| `show ip protocols` | u. a. Router-ID. |

### 2.5 Alte WAN-Technologien: HDLC, PPP, PPPoE 🧪

**Serielle Schnittstelle:** Die **Clock Rate** (bit/s) wird nur auf dem **DCE** gesetzt (beim Provider bzw. im Lab auf der Seite mit dem DCE-Kabel). `bandwidth` (kbit/s) ändert die physische Rate **nicht**, beeinflusst aber die Metrikberechnung der Routingprotokolle (Standard 1544 kbit/s = T1). Sinnvoll: gleich wie die Clock Rate.

```
! HDLC (DCE-Seite)
R1(config)# interface s1/0
R1(config-if)# clock rate 128000          (bit/s, nur DCE)
R1(config-if)# bandwidth 128              (kbit/s)
R1(config-if)# encapsulation hdlc         (Cisco-Default)
R1(config-if)# ip address 10.0.1.1 255.255.255.252
R1(config-if)# no shutdown
! DTE-Seite gleich, aber ohne clock rate. Für PPP: encapsulation ppp (beide Seiten!)
```

**PPP-Authentifizierung**

| Verfahren | Eigenschaft | Konfiguration |
|---|---|---|
| **PAP** | Passwort im **Klartext**, 2-Way-Handshake | Authenticator: `username USER password CISCO` + `ppp authentication pap`. Client: `ppp pap sent-username USER password CISCO`. Gegenseitig: beide Seiten beides. |
| **CHAP** | Challenge-Response mit Hash (MD5), Passwort wird nie übertragen, periodische Re-Authentifizierung | `ppp authentication chap` auf dem Authenticator, `username <Hostname-des-Peers> password <gleiches PW>` auf beiden Seiten. |

⚠️ Bei CHAP verwendet IOS standardmässig den **Hostnamen des Gegenübers** als Benutzernamen. Die Folien nutzen auf beiden Seiten `username USER`, das funktioniert nur zusammen mit `ppp chap hostname USER`. Sicherer Weg in PT: auf R1 `username R2 password CISCO`, auf R2 `username R1 password CISCO`.

**PPPoE-Client (DSL):**

```
R1(config)# interface dialer1
R1(config-if)# dialer pool 1
R1(config-if)# encapsulation ppp
R1(config-if)# ppp chap password CISCO
R1(config-if)# ip address negotiated        (IP vom Provider)
R1(config)# interface f0/0
R1(config-if)# no ip address
R1(config-if)# pppoe-client dial-pool-number 1
R1(config-if)# no shutdown
```

Prüfen: `show ip interface brief` (Dialer1 hat IP?), `show pppoe session`, `show interface serial 1/0` (Encapsulation, «up/up»), `show ppp all` (LCP-Zustand), `show run interface s1/0`.

### 2.6 QoS-Werte und Messwerkzeuge 🧪

**Dienstgüte (QoS):** Zeitkritische Kommunikation (VoIP, Video) hat Priorität vor zeitunkritischer (Mail, Web, FTP); organisatorisch Wichtiges (Produktion, Webshop) ebenfalls; Unerwünschtes (P2P, Streaming) kann gesperrt werden.

| Grösse | Bedeutung | Richtwert (max.) |
|---|---|---|
| Latenz | Verzögerung Sender → Empfänger (z. B. mit ping) | **< 150 ms** |
| Jitter | Schwankung der Latenz, verursacht Aussetzer | **< 30 ms** |
| Paketverlust | Anteil verlorener Pakete | **< 1 %** |
| Übertragungsrate | Mbit/s (oft fälschlich «Bandbreite» genannt) | – |

**Werkzeuge (Linux)**

```bash
# Layer 7: Latenz-Aufschlüsselung einer Webseite (DNS, TCP-Connect, TLS, Time to First Byte, Total)
curl -k -o /dev/null -s -w "dns:%{time_namelookup} connect:%{time_connect} tls:%{time_appconnect} ttfb:%{time_starttransfer} total:%{time_total}\n" https://www.example.ch
# Layer 7: HTTP-"Ping"
httping -c1 www.example.ch
# Durchsatz im eigenen Netz messen (immer Server UND Client nötig)
iperf3 -s                          # auf dem Server
iperf3 -c 10.0.0.10                # Client, TCP ohne Limit
iperf3 -c 10.0.0.10 -b 200M        # TCP mit 200 Mbit/s
iperf3 -c 10.0.0.10 -u -b 200M     # UDP mit 200 Mbit/s (zeigt Jitter und Loss)
```

Internet-Anschluss prüfen: mehrere Speedtests verwenden, auch den des Providers (speedtest.net, speed.cloudflare.com, fast.com, speedof.me).

Weitere Konnektivitätstools aus NPDO: `ping`, `traceroute -n` / `tracert`, `tracepath`, `mtr -r -n` (Ping und Traceroute kombiniert), `fping -a -g 192.168.1.0/24` (aktive Hosts finden), `nmap -sS -p80 <IP>` (Port offen?), `nc -vv <IP> 25` bzw. `telnet <IP> 80` (Banner).

### 2.7 DNS abfragen (Fehlersuche im DNS) 🧪

```bash
host www.google.ch              # A-Record
host -t MX google.ch            # Mailserver
host 8.8.8.8                    # Reverse Lookup (in-addr.arpa)
dig google.ch +noall +answer    # nur Antworten
dig -t aaaa google.ch           # IPv6-Record (auch: a, ns, soa, txt/SPF, mx)
dig -x 8.8.8.8                  # Reverse Lookup
dig @9.9.9.9 www.google.ch      # bestimmten DNS-Server fragen
dig +trace www.google.ch        # iterative Auflösung ab Root anzeigen
nslookup -q=mx google.ch 9.9.9.10
whois <Domain|IP>
ipcalc 192.168.1.0/24           # Subnetzrechner
```

Unter Windows: `nslookup`, `ipconfig /all`, `ipconfig /flushdns`, `route print`, `tracert`.

---

<a id="b2"></a>
## 3. Block 2 – Device Management, Netzwerkmanagement, Wireshark und TCP-Analyse

### 3.1 Speicher und Konfigurationsdateien 🧪

| Speicher | Inhalt |
|---|---|
| **ROM** | Bootstrap: startet das Gerät und sucht das IOS. Enthält ROMMON. |
| **Flash** | **IOS-Image** (`.bin`), ausserdem Backups und auf Switches `vlan.dat`. |
| **NVRAM** | **startup-config**: wird beim Start geladen. |
| **RAM** | **running-config**: aktuell aktive Konfiguration. Geht beim Neustart verloren, wenn nicht gespeichert. |

```
show running-config   | show run              (aktive Konfiguration)
show startup-config   | show start            (gespeicherte Konfiguration)
write                                          (= copy run start, speichern)
copy running-config startup-config             (RAM → NVRAM)
copy startup-config running-config             (NVRAM → RAM, wird ZUSAMMENGEFÜHRT, nicht ersetzt)
copy running-config tftp | copy tftp running-config
copy startup-config tftp | copy tftp startup-config
```

### 3.2 Backup und Wiederherstellung 🧪

```
R1# copy running-config tftp          (Konfiguration auf TFTP-Server)
R1# copy flash tftp                   (IOS-Image sichern)
R1# copy startup-config usb           (auf USB-Stick, falls vorhanden)

! Backup im Flash ablegen und zurückspielen
R1# copy run flash:                   → Dateiname eingeben, z. B. backup_name
R1# show flash:                       (Inhalt des Flash)
R1# write erase                       (startup-config löschen)
R1# reload
R1# copy flash: start                 → backup_name
R1# delete flash:backup_name          (Backup löschen)
```

🔎 **Automatische Backups** (CCNA Command Guide, Kap. 22):

```
R1(config)# archive
R1(config-archive)# path tftp://192.168.10.3/$h-$t.cfg     ($h = Hostname, $t = Zeitstempel)
R1(config-archive)# time-period 1440                         (alle 1440 Min. = täglich)
R1(config-archive)# write-memory                             (Backup bei jedem "write")
R1# show archive
```

**Konfigurationsproblem, schnelle Rettung:** Gerät **ohne Speichern neu starten** (`reload`, bei der Frage «Save?» mit *no* antworten). Es wird die letzte startup-config geladen.

### 3.3 Recovery, Factory Reset und Passwort-Recovery 🧪

```
R1# reload                    (Neustart, IOS wird entpackt und ins RAM geladen)
R1# show version              (IOS-Version, Uptime, Image-Datei, Config-Register)
R1# dir flash:  |  show flash:
R1# delete flash:c2900-universalk9-mz.SPA.151-4.M4.bin   (Vorsicht: Gerät bootet danach ins ROMMON!)
```

Ohne IOS-Image landet das Gerät im **ROMMON**. Dann Anleitung «<Modell> rommon recovery» suchen (Image z. B. per TFTP aus ROMMON laden). In PT gibt es dazu ein Recovery-Lab mit TFTP-Server.

**Factory Reset:**

```
S1# write erase               (= erase startup-config)
S1# delete flash:vlan.dat     🔎 nur Switch: VLAN-Datenbank liegt separat im Flash!
S1# reload                    (bei "Save?" mit no antworten)
```

**Config-Register**

| Wert | Wirkung |
|---|---|
| **0x2102** | Normaler Boot (Default): IOS aus Flash, startup-config aus NVRAM. |
| **0x2142** | **startup-config wird ignoriert** (Bit 6) → Passwort-Recovery. |
| 🔎 **0x2100** | Boot ins **ROMMON** (Boot-Feld = 0). ⚠️ Die Folie nennt 0x2120. Das bootet zwar auch ins ROMMON, setzt aber zusätzlich Bit 5 und damit eine andere Konsolen-Baudrate (19200 statt 9600). |

Setzen: im laufenden IOS `R1(config)# config-register 0x2102`, im ROMMON `rommon 1 > confreg 0x2142`. Aktueller Wert: letzte Zeile von `show version`.

**Passwort-Recovery (Router in PT)**

1. Mit Konsolenkabel verbinden, Router neu starten und während des Bootens **Ctrl+C** (Break) drücken → ROMMON.
2. `rommon 1 > confreg 0x2142`
3. `rommon 2 > reset` → Router startet mit leerer Konfiguration (Setup-Dialog mit *no* abbrechen).
4. `Router> enable`
5. `Router# copy startup-config running-config` (alte Konfiguration zurückholen, **nicht** umgekehrt!)
6. `R1(config)# enable secret NEUES_PASSWORT` (Folie: `no enable secret`)
7. `R1(config)# config-register 0x2102` (**nicht vergessen**, sonst wird die Konfiguration beim nächsten Start wieder ignoriert)
8. 🔎 `show ip interface brief`: Interfaces, die «administratively down» sind, mit `no shutdown` wieder aktivieren.
9. `R1# copy running-config startup-config`

### 3.4 Debugging 🧪

Nur im Lab oder mit grosser Vorsicht verwenden, weil Debugging die CPU stark belastet.

```
R1# debug ip packet          (dann z. B. ping → detaillierte Ausgabe)
R1# debug ip ospf  |  debug ip ospf hello  |  debug ip rip  |  debug ip nat
R1# show debugging           (was ist aktiv?)
R1# no debug ip packet
R1# undebug all              (Kurzform: u all)
R1(config)# logging synchronous   (unter line con 0: Meldungen unterbrechen die Eingabe nicht)
```

### 3.5 Netzwerkmanagement

- **Aufgaben:** **Konfiguration** (Einstellungen, via CLI, Web-GUI, SNMP) und **Überwachung** (Leistung, Fehler, Abrechnung, via SNMP, RMON, Syslog).
- **FCAPS** (ISO/OSI-Managementmodell): **F**ault (Fehler erkennen und melden), **C**onfiguration (System beschreiben und ändern), **A**ccounting (Ressourcen autorisieren und verrechnen), **P**erformance (Dienstgüte sicherstellen), **S**ecurity (Schutz vor Angriffen).
- **Homogenes Netz** (gleiche Hersteller pro Schicht) ist einfacher zu verwalten (Garantien, SLAs, einheitliche Tools) als ein heterogenes.
- **Protokolle:** ICMP (ping, traceroute, RFC 792), SNMP v1/v2c/v3, RMON/RMON2 (RFC 2819/2021), Syslog, NTP.
- **Aktuelle, korrekte Dokumentation** ist die Voraussetzung, um ein Netz zu betreiben und bei Ausfällen schnell zu reagieren.
- Sicheres Netzmanagement = Netzwerkmanagement + Informationssicherheitsmanagement (Schutzziele **CIA**: Vertraulichkeit, Integrität, Verfügbarkeit).

### 3.6 SNMP (Simple Network Management Protocol)

🔎 **Aufbau:** Ein **Manager** (NMS, z. B. PRTG, Zabbix, LibreNMS) fragt **Agents** auf den Geräten ab (Get/Set, **UDP 161**). Agents senden bei Ereignissen **Traps/Informs** an den Manager (**UDP 162**). Die Werte sind in der **MIB** über **OIDs** adressiert.

| Version | Sicherheit |
|---|---|
| **SNMPv1** | Unverschlüsselt, Community-String («Passwort») im **Klartext** mitlesbar. |
| **SNMPv2c** | Sicherheitstechnisch so schlecht wie v1 (Community im Klartext), aber heute noch häufig. (Die Varianten v2p/v2u mit mehr Sicherheit haben sich nicht durchgesetzt.) |
| **SNMPv3** | **Empfohlen.** Authentifizierung (Benutzer, Hash), Verschlüsselung (Privacy) und Autorisierung. In Cisco IOS seit 12.0(3)T. |

**SNMPv2c konfigurieren 🧪**

```
R1(config)# snmp-server community password1 ro        (nur lesen)
R1(config)# snmp-server community password2 rw        (lesen und schreiben, vermeiden!)
R1(config)# snmp-server host 10.0.0.10 version 2c password1   (Trap-Empfänger)
R1(config)# snmp-server enable traps config           (optional)
R1(config)# snmp-server contact name@domain.ch
R1(config)# snmp-server location Bern
```

⚠️ Auf der Folie steht `snmp-server host 10.0.0.10 snmpsrv01`. Das letzte Argument ist der **Community-String**, und ohne `version 2c` sendet IOS Traps in **Version 1**.
🔎 Absichern: Community per ACL auf den NMS beschränken, z. B. `snmp-server community password1 ro 10` mit `access-list 10 permit host 10.0.0.10`.

**🔎 SNMPv3 konfigurieren**

| Security Level | Authentifizierung | Verschlüsselung |
|---|---|---|
| `noAuthNoPriv` | nein (nur Benutzername) | nein |
| `authNoPriv` | ja (SHA/MD5) | nein |
| `authPriv` | ja | **ja (AES)** → verwenden |

```
R1(config)# snmp-server group SNMPGROUP v3 priv
R1(config)# snmp-server user snmpadmin SNMPGROUP v3 auth sha AuthPass123 priv aes 128 PrivPass123
R1(config)# snmp-server host 10.0.0.10 version 3 priv snmpadmin
R1# show snmp user  |  show snmp group
```

Planungspunkte für das SNMP-Konzept (Praxistransfer Block 2): welche Geräte, welche Version (v3), Benutzer und Gruppen, Zugriff nur aus dem Management-Netz (eigenes Management-VLAN), welche Traps, welches NMS, Schwellwerte und Alarmierung, Dokumentenversionierung.

### 3.7 Syslog, Zeitstempel und NTP

**NTP und Zeit** (aus NPDO; ohne korrekte Zeit sind Logs wertlos):

```
R1# clock set 20:00:00 Oct 23 2025
R1# show clock detail                      (Zeit und Quelle)
R1(config)# ntp server 192.168.10.5        (IP verwenden, siehe Hinweis)
R1# show ntp status  |  show ntp associations
```

⚠️ `feature ntp` auf der NPDO-Folie ist ein **NX-OS**-Befehl (Nexus), im klassischen IOS nicht nötig. Und `ntp server ch.pool.ntp.org` funktioniert nur mit DNS-Auflösung (`ip domain-lookup` + `ip name-server`). Nach `no ip domain-lookup` deshalb die NTP-Server-IP angeben.

**Logging und Zeitstempel:**

```
R1(config)# service timestamps log datetime msec show-timezone year
R1(config)# service sequence-numbers
R1(config)# logging host 192.168.10.53     🔎 an Syslog-Server senden (UDP 514)
R1(config)# logging trap warnings          🔎 Level für den Syslog-Server (0–7 oder Name)
R1# show logging
```

**Syslog-Severity-Levels** («Setzt du Level X, erhältst du X und alle tieferen Nummern»):

| Level | Name | Bedeutung |
|---|---|---|
| 0 | Emergencies | System unbrauchbar |
| 1 | Alerts | sofortiges Handeln nötig |
| 2 | Critical | kritischer Zustand |
| 3 | Errors | Fehler |
| 4 | Warnings | Warnungen |
| 5 | Notifications | normal, aber wichtig (z. B. Link up/down, `%SYS-5-CONFIG_I`) |
| 6 | Informational | Info (Default für `logging trap`) |
| 7 | Debugging | Debug-Ausgaben |

Merksatz: **«Every Awesome Cisco Engineer Will Need Ice cream Daily»**.
Aufbau einer Meldung: `seq: timestamp: %FACILITY-SEVERITY-MNEMONIC: Beschreibung`, z. B. `%LINEPROTO-5-UPDOWN: Line protocol on Interface Gi0/1, changed state to down`.

### 3.8 BSI IT-Grundschutz: NET.1.1 und NET.1.2

In Block 2 wurden die BSI-Bausteine als Checkliste für das eigene Netzdesign verwendet. 🔎 Kernpunkte:

- **NET.1.1 Netzarchitektur und -design:** Netz anhand einer Sicherheitsrichtlinie in **Zonen und Segmente** aufteilen (internes Netz, DMZ, Aussenanbindungen, Management-Netz), Übergänge über Firewalls/Paketfilter kontrollieren, Netz **dokumentieren**, ausreichend dimensionieren und **Redundanz** für kritische Verbindungen einplanen. Gefährdungen: unzureichende Dimensionierung, fehlende Segmentierung, Ausfall einzelner Komponenten (Single Point of Failure), DoS.
- **NET.1.2 Netzmanagement:** Planung und Richtlinie für das Netzmanagement, **eigenes Management-Netz bzw. -VLAN**, sichere Protokolle (SSH statt Telnet, **SNMPv3** statt v1/v2c, HTTPS), zentrale Protokollierung (Syslog) mit **Zeitsynchronisation (NTP)**, regelmässige **Konfigurationssicherung**, Überwachung und Alarmierung, Zugriffskontrolle für Administratoren.

### 3.9 Wireshark

**Einsatz:** Troubleshooting (Latenz, Paketverlust, Verbindungsabbrüche), Sicherheitsanalyse (Malware-Traffic, Klartextpasswörter), Protokolle lernen. Wireshark **analysiert**, es manipuliert nicht. Entstanden 1998 als «Ethereal» (Gerald Combs), seit 2006 Wireshark, GPL.

**Rechtliches (Schweiz):** Mitschneiden nur mit **ausdrücklicher Erlaubnis** bzw. im Auftrag (Wartung, Störungsbehebung).
- Relevante Artikel: Art. 179bis ff. StGB (unbefugtes Abhören), Art. 143bis StGB (unbefugtes Eindringen), Art. 143 StGB (unbefugte Datenbeschaffung).
- **nDSG:** Zweckbindung, Verhältnismässigkeit (Capture-Filter nutzen, Daten nach der Analyse löschen), Vertraulichkeit.

**Voraussetzungen für einen Mitschnitt**

- **Promiscuous Mode:** Die NIC reicht auch Frames weiter, die nicht an ihre MAC adressiert sind.
- **Aber:** Ein **Switch** leitet Unicasts nur an den Zielport weiter. Um fremden Verkehr zu sehen, brauchst du **Port Mirroring (SPAN)** oder einen **TAP**.
  🔎 Cisco-SPAN: `monitor session 1 source interface Gi0/5` und `monitor session 1 destination interface Gi0/10`.
- **WLAN:** Das Äquivalent heisst **Monitor Mode**. Pakete lassen sich mitschneiden, ohne mit dem AP verbunden zu sein (Luft ist ein geteiltes Medium).
- Treiber: **Npcap** (Windows, früher WinPcap), **libpcap** (Linux/macOS). Unter Linux ohne sudo: `sudo usermod -aG wireshark $USER`.
- Interface wählen: das mit **ausschlagender Sparkline**. Virtuelle Adapter (VMnet, docker0, VPN) ignorieren, wenn nicht gezielt benötigt. Localhost-Traffic nur über das Loopback-Interface.
- Speichern immer als **.pcapng** (mit Metadaten und Kommentaren), sprechende Dateinamen (z. B. `20260928-DruckerVLAN20.pcapng`).

**Oberfläche:** **Packet List** (eine Zeile pro Paket) → **Packet Details** (Baum nach Schichten: Frame = Metadaten/L1, Ethernet II = L2, IP = L3, TCP/UDP = L4, HTTP/TLS = L7) → **Packet Bytes** (Hex und ASCII). Hinweis: Der Eintrag «Frame» enthält nur Metadaten, der eigentliche Frame beginnt bei «Ethernet II».

Nützliche Einstellungen: Transport-Namensauflösung ausschalten (echte Portnummern sehen), Spalten **Delta time displayed** und **Cumulative Bytes** hinzufügen (sortieren nach Delta Time zeigt langsame Antworten), eigene **Profile** (Ctrl+Shift+A), z. B. mit absoluten Sequenznummern.

**Capture-Filter vs. Display-Filter**

| | Capture-Filter | Display-Filter |
|---|---|---|
| Wann | **vor** dem Mitschnitt | während oder nach dem Mitschnitt |
| Wirkung | Nicht passende Pakete werden **verworfen** (endgültig weg) | Pakete werden nur **ausgeblendet** |
| Syntax | **BPF**, Wörter: `host 10.0.0.1 and port 80` | Felder mit Punkt: `ip.addr == 10.0.0.1 && tcp.port == 80` |
| Einsatz | Langzeitmitschnitte, volle Leitungen, Datenschutz | Standard für die Fehlersuche |

Filterleiste: **grün** = gültig, **rot** = Syntaxfehler, **gelb** = gültig mit Warnung.

**Capture-Filter (BPF)**

```
host 192.168.1.2            src host 192.168.1.2          dst host 192.168.1.2
net 192.168.1.0/24          port 53                        tcp port 80
portrange 1000-2000         not port 22   (eigene SSH-Sitzung ausblenden)
not port 3389               not broadcast                  not arp        not ip6
ether host 00:02:a3:bb:00:01
host 10.0.0.1 and port 80   host 10.0.0.1 or host 10.0.0.2
```

**Display-Filter**

| Filter | Zweck |
|---|---|
| `ip.addr == 192.168.1.5` / `ip.src ==` / `ip.dst ==` | Host (beide Richtungen / Quelle / Ziel) |
| `ip.addr == 192.168.1.0/24` | ganzes Subnetz |
| `eth.addr == 00:02:a3:bb:00:01` | MAC-Adresse |
| `!(ip.addr == 192.168.1.1)` | alles ausser diesem Host (🔎 besser als `ip.addr != …`, das zeigt jedes Paket, bei dem *eine* der beiden Adressen abweicht) |
| `tcp.port == 443`, `udp.port == 53` | Port (Quelle oder Ziel) |
| `dns \|\| http \|\| dhcp` | mehrere Protokolle (🔎 `bootp` heisst seit Wireshark 3.0 `dhcp`) |
| `!arp`, `!ip6` | Rauschen ausblenden |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Verbindungsaufbau (SYN) |
| `tcp.flags.syn == 1 && tcp.flags.ack == 1` | SYN-ACK |
| `tcp.flags.reset == 1` | abgewiesene/abgebrochene Verbindungen (RST) |
| `tcp.stream == 5` | ein TCP-Stream |
| `dns.flags == 0x0100` / `dns.flags == 0x8180` | DNS-Query / Standard-Response (🔎 allgemeiner: `dns.flags.response == 0/1`) |
| `dns.flags.rcode != 0` | fehlgeschlagene DNS-Auflösungen (z. B. NXDOMAIN) |
| `arp.opcode == 1` / `arp.opcode == 2` | ARP-Request / ARP-Reply |
| `http.response.code >= 400` | HTTP-Fehler |
| `frame contains "passwort"` | Inhaltssuche (case-sensitive) |
| `ip.host == www.google.ch` | Host nach Name |
| **`tcp.analysis.flags`** | **alle TCP-Auffälligkeiten** (wichtigster Troubleshooting-Filter) |

Operatoren: `==` `!=` `<` `>` `<=` `>=`, `&&`/`and`, `||`/`or`, `xor`, `!`/`not`.
Profi-Trick: Rechtsklick auf ein Feld → **Apply as Filter → Selected**. Filter lassen sich speichern.

**Analysefunktionen**

- **Follow → TCP Stream:** setzt eine Sitzung zusammen (rot = Client, blau = Server). Achtung: Danach ist ein Filter `tcp.stream eq X` aktiv, zum Zurücksetzen die Filterleiste leeren. Dateien finden: im Stream nach `.pdf` suchen, Beginn beim `GET`, Ende bei `HTTP/1.1 200 OK`.
- **Farbregeln:** grün = TCP/HTTP, blau = UDP/DNS, **schwarz mit roter Schrift = Problem** (Retransmission, Dup ACK, Zero Window). Beim Scrollen bei schwarzen Zeilen stoppen.
- **Statistics → Endpoints** (Top Talker nach Bytes/Pakete), **Statistics → Conversations** (wer mit wem, z. B. Datenabfluss erkennen), Rechtsklick → als Filter anwenden (A↔B).
- **Analyze → Expert Information:** Probleme schnell finden (wirkt nur auf Display-Filterung).
- **Statistics → Flow Graph:** Ablauf grafisch darstellen.
- Hilfe: wiki.wireshark.org, Rechtsklick auf Protokoll → Wiki Protocol Page.

**Kommandozeile:** `tshark -i eth0 -Y "ip.addr==192.168.1.1 && tcp.port==443"`, `tshark -r scan.pcap -T fields -e ip.src -e ip.dst`, `tcpdump -i eth0 -c 20 port 80 -vv`, `tcpdump -XX` (Hex und ASCII).

### 3.10 TCP-Analyse: typische TCP-Probleme

**TCP-Grundlagen (Repetition)**

- **3-Way-Handshake:** Client → `SYN` (Seq=x) · Server → `SYN, ACK` (Seq=y, Ack=x+1) · Client → `ACK` (Ack=y+1).
- **Ordentlicher Abbau:** `FIN/ACK` → `ACK`, dann in der Gegenrichtung `FIN/ACK` → `ACK`.
- **Abbruch/Ablehnung:** `RST` (z. B. `SYN` → `RST, ACK` = Port geschlossen).
- Multiplexing über Ports: Client mit dynamischem Quellport (z. B. 52398) → Server-Port (80, 443, 25). Anzeigen mit `netstat -an` bzw. `ss -tan`.

| Problem | Was passiert | Display-Filter | Hinweis auf |
|---|---|---|---|
| **Retransmission** | Der Sender erhält innerhalb des **RTO** (Retransmission Timeout) kein ACK und sendet das Segment erneut. Der RTO wird dabei jeweils erhöht. **RTT** = Zeit zwischen Senden und Erhalt des ACK. | `tcp.analysis.retransmission` | Paketverlust, Überlast, Duplex-Mismatch, fehlerhafte Leitung, Empfänger nicht erreichbar |
| **Duplicate ACK + Fast Retransmission** | Der Empfänger merkt eine Lücke (fehlendes Segment) und bestätigt mehrfach dieselbe Sequenznummer (**Dup ACKs**). Nach **3 Dup ACKs** sendet der Sender sofort erneut, ohne den RTO abzuwarten. | `tcp.analysis.duplicate_ack`, `tcp.analysis.fast_retransmission` | einzelne verlorene Pakete, Out-of-Order |
| **Lost Segment** | Wireshark sieht eine Lücke in den Sequenznummern. | `tcp.analysis.lost_segment` | Verlust vor dem Messpunkt |
| **Zero Window** | Der Empfänger meldet **Window Size = 0**: Sein Empfangspuffer ist voll. Der Sender pausiert und schickt **Zero Window Probes**, bis ein **Window Update** kommt. | `tcp.analysis.zero_window`, `tcp.window_size == 0` | **überlasteter Empfänger oder langsame Applikation** (Endgerät, nicht das Netz!) |
| Alle zusammen | | `tcp.analysis.flags` | |

🔎 Faustregel: Retransmissions und Dup ACKs deuten auf ein **Netzproblem** (Verlust) hin, Zero Window auf ein **Endgeräte- bzw. Applikationsproblem**. Wo gemessen wird, ist entscheidend (nahe beim Client oder beim Server mitschneiden).

---

<a id="b3"></a>
## 4. Block 3 – WLAN planen

### 4.1 Grundbegriffe

| Begriff | Bedeutung |
|---|---|
| **WLAN** | Wireless LAN, Implementierung von **IEEE 802.11**. |
| **Wi-Fi** | Herstellerkonsortium (Wi-Fi Alliance), das 802.11-Produkte zertifiziert; umgangssprachlich = WLAN. |
| **AP** | Access Point (Basisstation): Übergang zwischen Funk- und Kabelnetz. |
| **Ad-hoc** | Direkte Verbindung zwischen Clients ohne AP. |
| **SSID** | Service Set Identifier = Name des WLANs. |
| **ESS / ESSID** | Gleiche SSID auf mehreren APs (Extended Service Set, Voraussetzung für Roaming). |
| **BSS / BSSID** | Basic Service Set: ein AP mit seinen Clients. BSSID = meist die MAC-Adresse des AP-Radios. (Die Folie beschreibt BSS als «Paket» – gemeint sind die **Beacons**, die der AP periodisch aussendet.) |
| **WDS** | Wireless Distribution System: APs verbinden sich per Funk (Bridging oder Repeating). Im Single-Radio-Betrieb **halbiert** sich die Datenrate. |
| **Handover** | Wechsel der Funkzelle **im eigenen Netz** (von AP zu AP, gleiche SSID). |
| **Roaming** | Wechsel in ein **anderes Netz** (andere SSID, anderes Band, oder auf LAN/Mobilfunk). |

### 4.2 WLAN-Standards

| Standard | Wi-Fi-Name | Jahr | Band | Brutto-Datenrate (max.) |
|---|---|---|---|---|
| 802.11 | – | 1997 | 2,4 GHz | 1–2 Mbit/s |
| 802.11b | – | 1999 | 2,4 GHz | 11 Mbit/s |
| 802.11a | – | 1999 | 5 GHz | 54 Mbit/s |
| 802.11g | – | 2003 | 2,4 GHz | 54 Mbit/s (Fallback auf b) |
| 802.11n | **Wi-Fi 4** | 2009 | 2,4 + 5 GHz | 150 Mbit/s pro Stream bei 40 MHz, theoretisch 600 Mbit/s (MIMO) |
| 802.11ac | **Wi-Fi 5** | 2013 | 5 GHz | bis 867 Mbit/s pro Stream bei 160 MHz, theoretisch ca. 6,9 Gbit/s |
| 🔎 802.11ax | **Wi-Fi 6** | 2019/21 | 2,4 + 5 GHz | ca. 9,6 Gbit/s; OFDMA, MU-MIMO, BSS Coloring, Target Wake Time → für **hohe Clientdichte** |
| 🔎 802.11ax | **Wi-Fi 6E** | ab 2021 | + **6 GHz** | wie Wi-Fi 6, zusätzlich 6-GHz-Band (viele saubere Kanäle) |
| 🔎 802.11be | **Wi-Fi 7** | 2024 | 2,4 + 5 + 6 GHz | theoretisch > 40 Gbit/s; **Multi-Link Operation (MLO)**, 320-MHz-Kanäle (nur 6 GHz), 4096-QAM |

Spezialstandards: 802.11p (Car-to-Car, 5,9 GHz), ⚠️ **802.11ad** (WiGig, Multi-Gigabit auf wenige Meter) arbeitet im **60-GHz-Band**, nicht wie auf der Folie angegeben im 5-GHz-Band. 802.11ah (Wi-Fi HaLow, unter 1 GHz, für IoT und Smart Home).

### 4.3 Frequenzbänder und Kanäle

| | 2,4 GHz | 5 GHz | 🔎 6 GHz (Wi-Fi 6E/7) |
|---|---|---|---|
| Reichweite | hoch, durchdringt Wände gut | geringer, stärker gedämpft | noch geringer |
| Kanäle | 13 Kanäle im 5-MHz-Raster (Kanal 1 = 2412 MHz), aber nur **3–4 überlappungsfrei** | viele überlappungsfreie 20-MHz-Kanäle (36, 40, 44, 48, 52 … 140) | in CH/EU **5945–6425 MHz** (480 MHz, 24 × 20 MHz) |
| Störungen | Band geteilt mit Bluetooth, Mikrowellen, Babyphones, Funkkameras | weniger belegt | kaum belegt, nur WPA3-Geräte |
| Einsatz | Reichweite, IoT, alte Clients | **Standard für Unternehmens-WLAN** | hohe Dichte, hoher Durchsatz |

**2,4 GHz überlappungsfrei:** Die Folie empfiehlt **1, 5, 9, 13** (bei 20 MHz in Europa möglich). 🔎 Weit verbreitet ist auch das Schema **1, 6, 11** (grösserer Abstand, kompatibel mit Clients aus Nordamerika, wo Kanal 12/13 fehlen). Im 2,4-GHz-Band immer **20 MHz** Kanalbreite verwenden.

🔎 **5 GHz in der Schweiz (BAKOM):**
- Kanäle **36–48**: nur in Gebäuden, max. 200 mW EIRP.
- Kanäle **52–64**: nur in Gebäuden, 200 mW mit TPC (sonst 100 mW), **DFS Pflicht**.
- Kanäle **100–140**: auch im Freien, bis 1 W EIRP mit TPC, **DFS Pflicht**.

⚠️ Die Folie «darf nur in geschlossenen Räumen verwendet werden» gilt also nur für einen Teil der Kanäle. **DFS** (Dynamic Frequency Selection) bedeutet: Der AP muss Radar erkennen und dann den Kanal wechseln. Das kann kurze Unterbrüche verursachen, ein möglicher Grund für sporadische WLAN-Aussetzer.

🔎 **6 GHz in der Schweiz:** seit 2021/2022 freigegeben (5945–6425 MHz, Indoor, Low Power). Geräte für den US-Markt nutzen teils andere Frequenzen und sind nicht automatisch zugelassen.

### 4.4 WLAN-Sicherheit

WLAN kann jeder in Reichweite **passiv mitschneiden** (kein ARP-Spoofing nötig wie im geswitchten LAN) → **immer verschlüsseln**.

| Verfahren | Bewertung |
|---|---|
| **WEP** | RC4 mit schwachem Initialisierungsvektor (IV), in Minuten geknackt. **Nicht mehr verwenden.** |
| **WPA** | Übergangslösung mit TKIP (dynamische Schlüssel, Per-Packet-Key-Mixing). **Nicht mehr verwenden.** |
| **WPA2** (IEEE 802.11i) | **AES-CCMP**. **Personal** mit Pre-Shared Key (PSK, **mind. 24 Zeichen** laut Folie) für Private, **Enterprise** mit 802.1X/EAP und RADIUS-Server für Firmen. Schwachstelle von PSK: Der 4-Way-Handshake kann (z. B. nach einem Deauth-Angriff) mitgeschnitten und offline per Wörterbuch angegriffen werden. |
| 🔎 **WPA3** | **Personal:** **SAE** (Simultaneous Authentication of Equals) statt PSK-Handshake → schützt vor Offline-Wörterbuchangriffen, Forward Secrecy. **Enterprise:** optional **192-Bit-Modus** (CNSA). **PMF** (802.11w, geschützte Management-Frames gegen Deauth-Angriffe) ist Pflicht. **Enhanced Open (OWE):** Verschlüsselung ohne Passwort für offene Gäste-WLANs. Im 6-GHz-Band und für Wi-Fi 7 ist WPA3 **Pflicht**. |

**Empfehlung Unternehmen:** WPA2/WPA3-**Enterprise** mit **802.1X** (Supplicant = Client, Authenticator = AP/WLC, Authentication Server = RADIUS, z. B. Microsoft NPS). Pro SSID ein eigenes VLAN; das Gäste-WLAN nur mit Internetzugang (Client Isolation, eigenes VLAN, Captive Portal oder OWE).

### 4.5 Störquellen und Probleme

- **Physik:** Funkwellen werden gedämpft, reflektiert und gebeugt (**Mehrwegeausbreitung**). Wände (Beton, Stahl, Metallbedampfung von Glas), Wasser (Menschen, Aquarien, Pflanzen), Möbel und Metallregale schwächen das Signal.
- **Fremde Funkquellen im 2,4-GHz-Band:** Mikrowellen, Bluetooth, Babyphones, schnurlose Kameras, Motoren, Küchengeräte.
- **Kanalüberschneidung** mit eigenen oder fremden WLANs (Nachbarfirma) → Co-Channel- und Adjacent-Channel-Interference.
- **Funklöcher** (nicht abgedeckte Bereiche), zu grosse oder zu kleine Zellen.
- Vorbeifahrende WLANs (Handys, Postauto, Zug), elektrische Störungen durch Bahn, Tram und Bus.
- **Handover-Probleme:** «Sticky Clients» halten die schwache Verbindung zu lange.
- Zu viele Clients pro AP, alte langsame Clients (bremsen die ganze Zelle), falsche Kanalbreite, DFS-Kanalwechsel.

### 4.6 WLAN-Planung (Konzept)

**Aufgabe B3 (Alters- und Pflegeheim) und Praxistransfer Block 3**. Bei der Planung festlegen:

1. **Anforderungen klären:** Einsatzzweck (Daten, **VoIP**/zeitkritisch, Pflegedokumentation, Rufsysteme, Gäste), **CIA** (kritische und sensible Kommunikation), **Roaming**-Anforderungen, **Anzahl gleichzeitiger Clients pro AP**, Bausubstanz und **Gebäudepläne**, Standards (Empfehlung heute: mind. Wi-Fi 6).
2. **Anzahl und Standorte der APs** (mit Begründung): Montageort und Ausrichtung (Decke, Antennencharakteristik), Kapazität statt nur Abdeckung planen. 🔎 Grober Richtwert (herstellerabhängig): für Datenverkehr etwa **25–50 gleichzeitig aktive Clients pro Radio**, für Sprache deutlich weniger. Massgebend ist die gleichzeitige Last, nicht die Zahl verbundener Geräte.
3. **Netze:** SSIDs ↔ VLANs (z. B. Intern, VoIP, IoT/Medizingeräte, Gäste, Management), **Verschlüsselung pro SSID**, Gäste-WLAN getrennt. Möglichst **wenige SSIDs** (jede SSID erzeugt Beacon-Overhead).
4. **Stromversorgung:** **PoE/PoE+** (802.3af/at/bt) am Access-Switch einplanen, Switch-PoE-Budget prüfen, USV.
5. **Weitere Komponenten:** WLC oder Cloud-Management, RADIUS, DHCP, Firewall für das Gäste-Netz.
6. **Störquellen** am Standort erheben und bei der Kanal- und AP-Planung berücksichtigen.
7. **Messverfahren** festlegen:
   - 🔎 **Predictive Survey:** Planung am Gebäudeplan mit Software (z. B. Ekahau, Hamina, NetSpot), Wände mit Dämpfungswerten erfassen. Liefert je nach Eingabequalität ca. 75–85 % Genauigkeit, deshalb vorher begehen.
   - 🔎 **Passive Survey:** vor Ort mitlauschen (Signalstärke, Rauschen, fremde APs), ohne sich zu verbinden.
   - 🔎 **Active Survey:** mit AP verbunden messen (Durchsatz, RTT, Paketverlust, Roaming). Dient der Abnahme nach der Installation.
   - Ablauf: Predictive → Vor-Ort-Messung («AP on a Stick») → Installation → **Validierungsmessung**.
8. 🔎 **Zielwerte** (Cisco-Empfehlung für Sprache): Signal am Zellrand mindestens **−67 dBm**, **SNR ≥ 25 dB**, ca. **15–20 % Zellüberlappung** für nahtloses Roaming, benachbarte APs auf **unterschiedlichen, überlappungsfreien Kanälen**.

**Handover-/Roaming-Varianten**

| Variante | Eigenschaften |
|---|---|
| **Heimbereich (günstig)** | Gleiche SSID und Verschlüsselung auf allen APs, jeder AP am LAN, verschiedene überlappungsfreie Kanäle. Der **Client** entscheidet und wechselt oft erst, wenn die Verbindung abbricht. |
| **WDS / Repeater** | Zentraler AP mit LAN, Repeater ohne LAN, gleicher Hersteller, gleiche SSID, Verschlüsselung und Kanal → Datenrate halbiert (oder Backhaul auf zweitem Kanal = möglicher Flaschenhals). |
| **Enterprise (zentrales Management)** | Gleicher Hersteller, **Controller** kann Clients in andere Zellen verschieben, zentrale Authentifizierung, Wechsel von Kanal/Band (2,4 → 5 GHz) oder Medium möglich, **IP-Adresse bleibt gleich**. 🔎 Schnelles Roaming mit 802.11r/k/v. |

### 4.7 Managed WiFi mit Cisco Wireless LAN Controller (PT-Tutorial)

**Aufbau:** 1 × WLC-2504, 3 × Lightweight-AP 3702i, 1 × Multilayer-Switch 3560 (liefert **PoE** und **DHCP**), Laptop mit WLAN-Modul.

| Gerät | Interface | IP |
|---|---|---|
| WLC | Gi0/1 (Management) | 192.168.1.254/24 (statisch, **zuerst** konfigurieren, um IP-Konflikte zu vermeiden) |
| 3560 | VLAN 1 | 192.168.1.1/24 |
| LAPs | Fa0/1–0/3 | per DHCP |

```
Switch(config)# line console 0
Switch(config-line)# privilege level 15         (Konsole startet direkt im privilegierten Modus)
Switch(config)# no ip domain-lookup
Switch(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.9
Switch(config)# ip dhcp pool MGMT
Switch(dhcp-config)# network 192.168.1.0 255.255.255.0
Switch(dhcp-config)# default-router 192.168.1.1
Switch(dhcp-config)# option 150 ip 192.168.1.254     (zeigt den APs den Weg zum Controller)
Switch(config)# interface vlan 1
Switch(config-if)# ip address 192.168.1.1 255.255.255.0
Switch(config-if)# no shutdown
Switch# write
```

Danach die APs im PT-Dialog auf DHCP stellen und den WLC per Browser vom Laptop aus konfigurieren (nach dem Neustart des WLC über `https://`): WLANs/SSIDs, Sicherheit, Zuordnung zu Interfaces bzw. VLANs.

🔎 **Praxis vs. PT:** Das Tutorial verwendet DHCP-**Option 150** (eigentlich die TFTP-Server-Option, u. a. für Cisco-IP-Telefone). In realen Cisco-Umgebungen finden Lightweight-APs den Controller über
- **DHCP-Option 43** (herstellerspezifisch, enthält die WLC-IP),
- den **DNS-Eintrag `CISCO-CAPWAP-CONTROLLER.<domain>`**, oder
- einen L2-Broadcast im gleichen Subnetz.

AP und WLC kommunizieren über **CAPWAP** (UDP 5246 Steuerung, UDP 5247 Daten).

### 4.8 WLAN-Traffic in Wireshark

- Unter «IEEE 802.11» Source, Destination, Transmitter Address und **BSS Id** ansehen.
- `wlan.fc.type_subtype == 0x04` → Probe Requests (welche SSIDs suchen Geräte?)
- `!(wlan.fc.type == 0 && wlan.fc.subtype == 8)` → Beacons ausblenden
- `wlan.fc.protected == 0` → nur **unverschlüsselte** Frames
- SSID filtern: `wlan.ssid == "Name"` (Folie: `wlan_mgmt.tag.interpretation eq "SSID"`, ältere Syntax)
- Monitor Mode unter Linux: `airmon-ng start wlan0`, Überblick über APs und Clients: `airodump-ng wlan0mon` (nur im eigenen Lab bzw. mit Erlaubnis!)

---

<a id="b4"></a>
## 5. Block 4 – CLI, VLANs, redundante L2/L3-Netze

### 5.1 CLI-Grundlagen 🧪

**Modi:** `R1>` User EXEC → `enable` → `R1#` Privileged EXEC → `configure terminal` → `R1(config)#` Global Config → z. B. `interface g0/0` → `R1(config-if)#`. Zurück mit `exit` (eine Ebene), `end` oder **Ctrl+Z** (direkt nach `#`), `disable` (nach `>`).

| Zugriff | Eigenschaften |
|---|---|
| **Konsole** | Physischer Port mit Konsolenkabel, Terminalprogramm (PuTTY, PT-Terminal). Braucht keine IP. |
| **Telnet** | Über das Netz (VTY-Lines), **TCP 23**, **unverschlüsselt** → nicht mehr verwenden. |
| **SSH** | Über das Netz (VTY-Lines), **TCP 22**, verschlüsselt → **immer verwenden** (SSHv2, RSA ≥ 2048 Bit). |

**Nützliche Befehle**

```
R1# show ?                          (Hilfe, mögliche Ergänzungen; TAB vervollständigt)
R1# show running-config | begin hostname    (Filter sind case-sensitive)
R1# show running-config | include interface     (Kurzform: | in int)
R1# show running-config | section ospf
R1(config)# do show ip interface brief     ("do" = Show-Befehle im Config-Modus)
R1(config)# no ip domain-lookup            (Tippfehler werden nicht als Hostname per DNS aufgelöst)
R1# reload | write | write erase           (Neustart | speichern | Werkzustand – Vorsicht!)
```

**Grundabsicherung (Praxistransfer Block 2)**

```
Router(config)# hostname R1
R1(config)# no ip domain-lookup
R1(config)# enable algorithm-type scrypt secret Cisco123!     (Typ 9; alternativ sha256 = Typ 8)
R1(config)# service password-encryption                        (Typ 7, nur Schutz vor Schulterblick)
R1(config)# banner motd #Zugriff nur fuer Berechtigte#
R1(config)# username admin privilege 15 algorithm-type scrypt secret Admin123!
! Konsole
R1(config)# line console 0
R1(config-line)# login local            (oder: password <pw> + login)
R1(config-line)# exec-timeout 10        (Minuten)
R1(config-line)# logging synchronous
R1(config-line)# history size 15
! SSH
R1(config)# ip domain-name beispiel.ch
R1(config)# crypto key generate rsa modulus 2048     (Voraussetzung: Hostname ≠ Default, Domain gesetzt)
R1(config)# ip ssh version 2
R1(config)# line vty 0 15               (Router oft nur 0 4)
R1(config-line)# login local
R1(config-line)# transport input ssh    🔎 Telnet deaktivieren
R1(config-line)# exec-timeout 10
R1# write
```

Prüfen: `show ip ssh`, `show ssh`, `show users`, vom PC aus `ssh -l admin 192.168.1.1`.
🔎 VTY-Zugriff einschränken: `access-list 2 permit 192.168.99.0 0.0.0.255` und unter `line vty 0 15` → `access-class 2 in`.

**Passwort-Typen**

| Typ | Verfahren | Befehl | Bewertung |
|---|---|---|---|
| 0 | Klartext | `enable password`, `password` (Line), `username … password` | unsicher |
| 7 | Vigenère | `service password-encryption` | leicht knackbar, nur «Verschleierung» |
| 5 | MD5-Hash | `enable secret`, `username … secret` | veraltet, aber Minimum laut Aufgabe |
| 8 | PBKDF2-SHA256 | `enable algorithm-type sha256 secret …` | gut |
| 9 | scrypt | `enable algorithm-type scrypt secret …` | **empfohlen** |

Cisco empfiehlt zentral **AAA** mit **RADIUS oder TACACS+**. Benutzer löschen: `no username user`. Abmelden: `logout`.

### 5.2 Grundkonfiguration Switch und Router 🧪

**Switch (L2): Management-IP über ein SVI**

```
S1(config)# interface vlan 1                  (besser: eigenes Management-VLAN, z. B. 99)
S1(config-if)# ip address 192.168.1.2 255.255.255.0
S1(config-if)# no shutdown
S1(config)# ip default-gateway 192.168.1.1    (L2-Switch braucht das für Zugriff aus anderen Netzen)
S1# write
! Entfernen: interface vlan 1 → no ip address → shutdown
```

**Router: Interfaces**

```
R1(config)# interface g0/0                    (auch fa0/0, s0/0/0 …)
R1(config-if)# ip address 192.168.3.1 255.255.255.0
R1(config-if)# description LAN Verwaltung
R1(config-if)# no shutdown                    (Router-Interfaces sind standardmässig shutdown!)
R1# show ip interface brief
R1# show interfaces g0/0                      ("GigabitEthernet0/0 is up, line protocol is up")
R1# show controllers s0/0/0                   (DCE/DTE-Kabel und Clock Rate)
```

**DHCP-Server auf dem Router**

```
R1(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10   (von – bis, vorher ausschliessen)
R1(config)# ip dhcp pool LAN10
R1(dhcp-config)# network 192.168.1.0 255.255.255.0
R1(dhcp-config)# default-router 192.168.1.1
R1(dhcp-config)# dns-server 192.168.1.5
R1(dhcp-config)# lease 1                     (in Tagen)
R1# show ip dhcp binding | show ip dhcp pool | show ip dhcp conflict
```

🔎 **DHCP über Router hinweg:** Liegt der DHCP-Server in einem anderen Netz, braucht das Client-Interface bzw. Subinterface einen **Relay-Agent**: `ip helper-address <DHCP-Server-IP>`. Fehlt dieser, bekommen Clients eine **APIPA-Adresse 169.254.x.x**.

**DHCP-Ablauf (DORA):** Discover → Offer → Request → Acknowledge (UDP 67/68).

### 5.3 VLANs (IEEE 802.1Q) 🧪

- VLANs sind **logische Netze** innerhalb eines physischen Netzes, eine **Layer-2**-Technologie.
- **Jedes VLAN = eigene Broadcast-Domain = eigenes IP-Subnetz.**
- Kommunikation zwischen VLANs nur über **Routing** (Router, L3-Switch, Firewall).
- **Access-Port:** gehört genau zu **einem** VLAN, untagged (Endgeräte).
- **Trunk:** transportiert mehrere VLANs mit **802.1Q-Tag** (4 Byte, 12-Bit-VLAN-ID) zwischen Switches, zu Routern (RoaS) und APs mit mehreren SSIDs. Das **Native VLAN** (Default 1) läuft untagged.
- VLAN-IDs: 0 und 4095 reserviert; **1–1005** Normal Range (1002–1005 reserviert für alte FDDI/Token-Ring-VLANs); **1006–4094** Extended Range.
- **Einsatzbeispiele:** Abteilungs- oder Stockwerk-VLANs (Sicherheit, weniger Broadcasts), **VoIP-VLAN** (priorisiert mit QoS), getrennte SSIDs auf einem AP (Intern auf VLAN 10, Gast auf VLAN 20 nur ins Internet), Server-VLANs.

```
S1(config)# vlan 20
S1(config-vlan)# name Buchhaltung
S1(config)# interface range fa0/2 - 4
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 20      (erstellt VLAN 20, falls es fehlt)
S1(config-if-range)# switchport voice vlan 30       🔎 IP-Telefon mit PC dahinter
! Trunk
S1(config)# interface g0/1
S1(config-if)# description Trunk zu S2
S1(config-if)# switchport trunk encapsulation dot1q  (nur bei Switches, die auch ISL können, z. B. 3560)
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk native vlan 99      (auf BEIDEN Seiten gleich!)
S1(config-if)# switchport trunk allowed vlan 10,20,99
S1(config-if)# switchport trunk allowed vlan add 30  |  remove 30  |  except 5  |  all
```

**Achtung:** `switchport trunk allowed vlan 10,20` **ersetzt** die bisherige Liste. Wer nur ergänzen will, braucht `add`, sonst fallen VLANs vom Trunk.

**Switchport-Modi (DTP)**

| Modus | Verhalten | Ergebnis mit Gegenseite |
|---|---|---|
| `access` | immer Access | – |
| `trunk` | immer Trunk (sendet DTP) | Trunk mit trunk/desirable/auto |
| `dynamic desirable` | versucht aktiv Trunk | Trunk mit trunk/desirable/auto |
| `dynamic auto` | wartet passiv | **auto + auto = Access!** |
| 🔎 `switchport nonegotiate` | DTP aus | Sicherheit: DTP auf allen Ports abschalten |

**Überprüfen**

| Befehl | Worauf achten |
|---|---|
| `show vlan brief` | Existiert das VLAN? Sind die Access-Ports im richtigen VLAN? **Trunk-Ports erscheinen hier nicht.** |
| `show vlan` | zusätzlich Status (active / act/lshut) |
| `show interfaces trunk` | Siehe [Ausgaben interpretieren](#ausgaben): Mode, Native VLAN, allowed, **«forwarding and not pruned»** |
| `show interfaces fa0/1 switchport` | Administrative/Operational Mode, Access VLAN, Native VLAN, Voice VLAN |
| `show interfaces status` | connected/notconnect/err-disabled, VLAN, Duplex, Speed |
| `show mac address-table` | Welche MAC wurde an welchem Port und in welchem VLAN gelernt? |

### 5.4 Inter-VLAN-Routing 🧪

**Router on a Stick (RoaS):** ein physisches Router-Interface, pro VLAN ein Subinterface (Nummer = VLAN-ID). Switch-Port zum Router = **Trunk**.

```
R1(config)# interface g0/0
R1(config-if)# no shutdown                        (physisches Interface aktivieren!)
R1(config)# interface g0/0.10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip address 10.1.1.254 255.255.255.0
R1(config)# interface g0/0.20
R1(config-subif)# encapsulation dot1Q 20
R1(config-subif)# ip address 10.2.1.254 255.255.255.0
R1(config)# interface g0/0.99
R1(config-subif)# encapsulation dot1Q 99 native   🔎 falls Native VLAN 99
```

Achtung: Danach werden **alle VLANs untereinander geroutet**. Einschränken mit ACLs.

**L3-Switch mit SVIs** (Switched Virtual Interfaces), typisch im Distribution Layer:

```
S1(config)# ip routing                            (!! sonst routet der L3-Switch nicht)
S1(config)# vlan 10
S1(config)# interface vlan 10
S1(config-if)# ip address 10.0.10.1 255.255.255.0
S1(config-if)# no shutdown
! Routed Port Richtung WAN-Router
S1(config)# interface g0/1
S1(config-if)# no switchport                      (macht den Port zu einem L3-Port)
S1(config-if)# ip address 10.0.200.2 255.255.255.252
! Default-Route bzw. OSPF/EIGRP Richtung Router
S1(config)# ip route 0.0.0.0 0.0.0.0 10.0.200.1
```

🔎 Ein SVI ist nur **up/up**, wenn das VLAN existiert **und** mindestens ein aktiver Port (Access oder Trunk mit diesem VLAN in Forwarding) vorhanden ist.

### 5.5 VTP (VLAN Trunking Protocol) 🧪

VLANs werden auf dem **VTP-Server** definiert und über **Trunks** in der **VTP-Domain** verteilt. Nützlich in grösseren Netzen.

| Modus | VLANs erstellen/ändern | Übernimmt Updates | Leitet Updates weiter |
|---|---|---|---|
| **Server** (Default) | ja | ja | ja |
| **Client** | nein | ja | ja |
| **Transparent** | ja, nur lokal | nein | ja (VTPv2) |
| 🔎 Off (v3) | ja, nur lokal | nein | nein |

```
S1(config)# vtp domain praxis
S1(config)# vtp mode server
S1(config)# vtp password cisco          (optional; muss überall gleich sein)
S1(config)# vtp version 2               (1, 2 oder 3)
S1(config)# vlan 10
S1(config-vlan)# name labor

S3(config)# vtp mode client             (Domain lernt der Client automatisch, falls noch leer)
S3(config)# vtp domain praxis
S3(config)# vtp password cisco
```

- Auf einem **Transparent**-Switch müssen VLANs, die dort als Access-VLAN verwendet werden, **lokal** angelegt werden.
- Ports werden trotz VTP auf **jedem** Switch lokal den VLANs zugewiesen (`switchport access vlan`).
- Analyse: `show vtp status` (Domain, Mode, Version, **Configuration Revision**, Anzahl VLANs), `show vtp password`, `show vtp counters`, `show vlan brief`.
- VTP-Probleme: Domain-Name (case-sensitive), Passwort oder Version stimmen nicht; **keine Trunks**; Client erhält nichts.
- 🔎 **Achtung Revisionsnummer:** Ein neuer Switch mit **höherer Configuration Revision** in derselben Domain kann die VLAN-Datenbank im ganzen Netz überschreiben. Vor dem Einbau Revision zurücksetzen (Mode transparent und zurück, oder Domain ändern). VTPv3 mit `vtp primary` schützt davor.

### 5.6 Switch-Security (Layer 2) 🧪

| Risiko / Angriff | Gegenmassnahme |
|---|---|
| Rogue-DHCP-Server | **DHCP Snooping** |
| MAC-Flooding (CAM-Table voll), Missbrauch freier Ports | **Port Security**, ungenutzte Ports `shutdown` (und in ein Parkplatz-VLAN) |
| ARP-Poisoning / Man-in-the-Middle | **Dynamic ARP Inspection (DAI)** |
| Unberechtigte Geräte | **802.1X** (Identity Based Networking: Supplicant – Authenticator (Switch) – RADIUS) |
| STP-Angriffe (fremde Root-Bridge) | **PortFast + BPDU Guard**, **Root Guard** |
| Loops (unidirektionale Links) | **Loop Guard** |
| 🔎 VLAN-Hopping | DTP abschalten (`switchport mode access` / `nonegotiate`), Native VLAN ≠ 1 und ungenutzt |

```
! DHCP Snooping
S1(config)# ip dhcp snooping
S1(config)# ip dhcp snooping vlan 10
S1(config)# interface g0/1                        (Uplink Richtung legitimer DHCP-Server)
S1(config-if)# ip dhcp snooping trust
S1# show ip dhcp snooping  |  show ip dhcp snooping binding

! Dynamic ARP Inspection (braucht die DHCP-Snooping-Bindings)
S1(config)# ip arp inspection vlan 20
S1(config)# interface g0/1
S1(config-if)# ip arp inspection trust            (Uplinks)

! Port Security
S1(config)# interface fa0/5
S1(config-if)# switchport mode access             (nicht "dynamic"!)
S1(config-if)# switchport port-security           ⚠️ aktiviert Port Security (fehlt auf der Folie!)
S1(config-if)# switchport port-security maximum 2
S1(config-if)# switchport port-security mac-address sticky    (gelernte MACs in die running-config)
S1(config-if)# switchport port-security violation restrict

! Automatisch aus err-disabled zurückholen (Default 300 s, 30–86400 s)
S1(config)# errdisable recovery cause psecure-violation
S1(config)# errdisable recovery interval 600
```

| Violation-Modus | Unerlaubter Verkehr | Log/SNMP | Violation-Zähler | Port |
|---|---|---|---|---|
| `protect` | verworfen | nein | nein | bleibt up |
| `restrict` | verworfen | ja | ja | bleibt up |
| `shutdown` (**Default**) | verworfen | ja | ja | **err-disabled** |

Analyse: `show port-security`, `show port-security interface fa0/5` (Port Status «Secure-shutdown»?), `show port-security address`, `show interfaces status err-disabled`, `clear mac address-table dynamic`.
**err-disabled manuell beheben:** Ursache entfernen, dann `shutdown` → `no shutdown` auf dem Interface.

### 5.7 Spanning Tree Protocol (STP, RSTP) 🧪

**Wozu?** Redundante Links zwischen Switches erzeugen **Layer-2-Loops** (Broadcast-Stürme, instabile MAC-Tabellen, doppelte Frames). STP (IEEE 802.1D) macht das Netz **loopfrei**, indem es redundante Ports blockiert, und aktiviert sie bei einem Ausfall wieder.

**Bridge-ID (BID)** = 8 Byte: **2 Byte Priorität** (Default 32768, Vielfache von 4096; bei PVST+ wird die VLAN-ID addiert, z. B. 32769 für VLAN 1) + **6 Byte MAC-Adresse**. **Die tiefste BID gewinnt**, bei gleicher Priorität die tiefste MAC.

**Spanning-Tree-Algorithmus**

1. **Root-Bridge wählen:** Jeder Switch sendet Hello-BPDUs und behauptet, Root zu sein. Wer eine BPDU mit tieferer BID empfängt, hört damit auf. Danach sendet nur noch die Root-Bridge Hellos (alle 2 s).
2. **Root Ports (RP) wählen:** Jeder Nicht-Root-Switch wählt **einen** Port mit den **tiefsten Pfadkosten zur Root-Bridge** (Tiebreaker: tiefste BID des Nachbarn, dann tiefste Port-ID).
3. **Designated Ports (DP) wählen:** Pro Segment ein DP (der Switch mit den tieferen Kosten zur Root; bei Gleichstand die tiefere BID). **Alle Ports der Root-Bridge sind DP.**
4. **Alle übrigen Ports werden blockiert** (Blocking/Alternate). Treffen zwei «DP-Kandidaten» aufeinander, blockiert der Switch mit der **höheren BID** seinen Port.

**Pfadkosten (IEEE, Short Mode)**

| Geschwindigkeit | Kosten |
|---|---|
| 10 Mbit/s | 100 |
| 100 Mbit/s | 19 |
| 1 Gbit/s | 4 |
| 10 Gbit/s | 2 |

**Portzustände 802.1D** (Blocking → Listening → Learning → Forwarding, ca. **50 s**: Max Age 20 s + 2 × Forward Delay 15 s)

| Zustand | Daten | BPDUs | MAC lernen |
|---|---|---|---|
| Blocking | verworfen | empfangen | nein |
| Listening | verworfen | empfangen und senden | nein |
| Learning | verworfen | empfangen und senden | **ja** |
| Forwarding | **weitergeleitet** | empfangen und senden | ja |
| Disabled | verworfen | nein | nein |

🔎 **RSTP (802.1w):** Zustände **Discarding / Learning / Forwarding**; Rollen Root, Designated, **Alternate** (Ersatz-Root-Port) und **Backup**; Konvergenz in **wenigen Sekunden** durch Proposal/Agreement statt Timer. PortFast-Ports sind **Edge Ports**.

**STP-Modi bei Cisco**

| Modus | Standard | Beschreibung |
|---|---|---|
| **PVST+** | 802.1D + pro VLAN | Default auf vielen Cisco-Switches, eine STP-Instanz **pro VLAN** |
| **Rapid PVST+** | **802.1w** + pro VLAN | schnelle Konvergenz, kompatibel zu altem STP → **empfohlen** |
| **MST** | 802.1s | mehrere VLANs auf wenige Instanzen abgebildet (gross/Multivendor) |

```
S1(config)# spanning-tree mode rapid-pvst
S1(config)# spanning-tree vlan 10 root primary        (setzt Priorität auf 24576 bzw. tiefer als die aktuelle Root)
S2(config)# spanning-tree vlan 10 root secondary      (28672)
S1(config)# spanning-tree vlan 10 priority 4096       (Alternative: Vielfaches von 4096, 0–61440)
S1(config-if)# spanning-tree vlan 10 cost 40          (Pfad beeinflussen)
S1(config-if)# spanning-tree vlan 10 port-priority 64
```

🔎 **Design-Tipp:** Root-Bridge bewusst auf den **Distribution/Core-Switch** legen (bei HSRP auf denselben Switch wie das aktive Gateway), nie zufällig über die tiefste MAC wählen lassen.

**Schutzfunktionen**

```
S1(config-if)# spanning-tree portfast                 (nur Endgeräte-Ports: sofort Forwarding)
S1(config-if)# spanning-tree bpduguard enable         (BPDU an PortFast-Port → err-disabled)
S1(config)# spanning-tree portfast default            (alle Access-Ports)
S1(config)# spanning-tree portfast bpduguard default
S1(config-if)# spanning-tree guard root               (auf DP Richtung Access: keine "bessere" Root zulassen)
S1(config)# spanning-tree loopguard default           ⚠️ Folie: "spanning loopguard"
S1(config-if)# spanning-tree guard loop               (Folie abgekürzt: "spanning guard loop", funktioniert auch)
```

**Analyse**

```
S1# show spanning-tree                        (alle VLANs)
S1# show spanning-tree vlan 10                (Root ID, Bridge ID, Portrollen und -zustände)
S1# show spanning-tree vlan 10 root | bridge
S1# show spanning-tree summary                (Modus, PortFast/BPDU-Guard default)
S1# show spanning-tree inconsistentports      (Root-/Loop-Guard hat blockiert)
S1# show spanning-tree interface g0/1 detail
S1# debug spanning-tree events
```

### 5.8 EtherChannel / Link Aggregation 🧪

Mehrere physische Links werden zu **einem logischen Link** (Port-Channel) gebündelt: **mehr Bandbreite + Redundanz**, und STP sieht nur **einen** Link (kein Blocking). Je nach Modell bis zu **8 aktive Ports**. Die Last wird **per Hash** (MAC/IP/Port) auf die Links verteilt, nicht per Round-Robin. Andere Namen: LAG, Port-Channel, Bonding bzw. NIC-Teaming (Server).

**Voraussetzungen (beide Seiten gleich!):** gleiche Geschwindigkeit und Duplex, gleicher Switchport-Modus (alle Access im gleichen VLAN **oder** alle Trunk mit gleichem Native VLAN und gleichen Allowed VLANs).

| Protokoll | Modi | Kommt zustande bei |
|---|---|---|
| **statisch** | `on` | on + on (kein Protokoll → Fehlkonfiguration kann Loops erzeugen) |
| **PAgP** (Cisco) | `desirable` (aktiv), `auto` (passiv) | desirable+desirable, desirable+auto (**nicht** auto+auto) |
| **LACP** (IEEE 802.3ad/802.1AX) | `active`, `passive` | active+active, active+passive (**nicht** passive+passive) |

```
S1(config)# interface range g0/1 - 2
S1(config-if-range)# channel-group 1 mode active          (LACP; PAgP: desirable; statisch: on)
S1(config)# interface port-channel 1
S1(config-if)# switchport trunk encapsulation dot1q        (falls nötig)
S1(config-if)# switchport mode trunk
S2: gleich mit "channel-group 1 mode passive" (oder active)
```

Analyse: `show etherchannel summary` (siehe [Ausgaben interpretieren](#ausgaben)), `show etherchannel port-channel`, `show interfaces port-channel 1`.
**Stack/Multi-Chassis:** EtherChannel über mehrere physische Switches mit Stacking-Kabel (Switch-Stack), **VSS** (Virtual Switching System) oder **vPC** (Nexus) → keine Single Points of Failure.

### 5.9 FHRP – First Hop Redundancy (HSRP) 🧪

Problem: Endgeräte kennen nur **ein** Default-Gateway. FHRP stellt eine **virtuelle Gateway-IP (und -MAC)** bereit, die von mehreren Routern bzw. L3-Switches getragen wird.

| Protokoll | Typ | Bemerkung |
|---|---|---|
| **HSRP** (Hot Standby Router Protocol) | Cisco | Active/Standby |
| 🔎 **VRRP** (Virtual Router Redundancy Protocol, RFC 5798) | offen | Master/Backup |
| 🔎 **GLBP** | Cisco | zusätzlich Lastverteilung |
| **CARP** | OpenBSD/pfSense | |

```
R1(config)# interface g0/1
R1(config-if)# ip address 10.0.0.2 255.255.255.0
R1(config-if)# standby version 2               🔎 optional
R1(config-if)# standby 1 ip 10.0.0.1           (virtuelle IP = Gateway der Clients)
R1(config-if)# standby 1 priority 110          (Default 100, höchste gewinnt)
R1(config-if)# standby 1 preempt               (übernimmt nach Wiederkehr wieder die Active-Rolle)
R1(config-if)# standby 1 track g0/0 20         🔎 Priorität −20, wenn der WAN-Link ausfällt

R2(config)# interface g0/1
R2(config-if)# ip address 10.0.0.3 255.255.255.0
R2(config-if)# standby 1 ip 10.0.0.1
R2(config-if)# standby 1 priority 99
R1# show standby   |   show standby brief
```

🔎 **HSRP-Defaults:** Priority 100, Hello 3 s, Hold 10 s, Preempt aus. **v1:** Gruppen 0–255, Multicast 224.0.0.2, virtuelle MAC `0000.0c07.acXX` (XX = Gruppe in Hex). **v2:** Gruppen 0–4095, 224.0.0.102, MAC `0000.0c9f.fXXX`, unterstützt IPv6.
Bei Gleichstand der Priorität gewinnt die **höhere IP-Adresse**. Gruppe, virtuelle IP und Version müssen auf beiden Routern übereinstimmen, sonst werden beide «Active».

---

<a id="b5"></a>
## 6. Block 5 – Routing in IPv4 und IPv6

### 6.1 Routing-Grundlagen

- Ein **Router** verbindet Netze (Layer 3), **blockiert Broadcasts** und leitet Pakete anhand seiner **Routingtabelle** an den nächsten Hop weiter.
- **Routenarten:** **Connected** (direkt am Interface, Interface muss up/up sein), **Static** (`ip route`), **Dynamic** (Routingprotokoll).
- **Entscheid auf dem Client:** Ziel im **eigenen Subnetz** → ARP für die Ziel-MAC, Frame direkt ans Ziel. Ziel in **anderem Subnetz** → ARP für die MAC des **Default-Gateways**, Frame ans Gateway. Auch ein Client hat eine Routingtabelle (`route print`, `ip route`).
- **Auf dem Router:** FCS prüfen → Ziel-MAC = eigene? → entkapseln → **Ziel-IP mit Routingtabelle vergleichen (Longest Prefix Match)** → neu kapseln für den Next Hop (wieder ARP) → weiterleiten. Die **MAC-Adressen ändern sich pro Hop**, die IP-Adressen bleiben (ohne NAT) gleich; bei jedem Router sinkt die TTL um 1.
- Die vier IPv4-Einstellungen eines Hosts: **IP-Adresse, Subnetzmaske, Default-Gateway, DNS-Server**.

**Routingprotokolle einordnen**

| | Distance Vector | Link State | Path Vector |
|---|---|---|---|
| Prinzip | Router tauschen Routingtabellen mit direkten Nachbarn aus («Routing by Rumor») | Jeder Router kennt die ganze Topologie (LSDB) und rechnet selbst (SPF/Dijkstra) | AS-Pfad pro Route |
| Beispiele | RIP, IGRP, EIGRP (🔎 «Advanced Distance Vector») | **OSPF**, IS-IS | **BGP** |

⚠️ Die Folie ordnet BGP unter «Distance Vector» ein. Genauer ist **Path Vector** (so auch das BGP-Skript).

| Protokoll | Metrik |
|---|---|
| RIPv2 | Hop-Anzahl (max. 15) → heute nicht mehr verwenden |
| OSPF | **Cost** = Referenzbandbreite / Interface-Bandbreite (Default-Referenz 100 Mbit/s) |
| EIGRP | zusammengesetzt aus **Bandbreite** (langsamster Link) und **Delay** (Summe) |
| BGP | Pfadattribute (u. a. AS_PATH-Länge) |

**Administrative Distanz (AD)**: Vertrauenswürdigkeit der Quelle. Hat ein Router **mehrere Routen zum selben Präfix aus verschiedenen Quellen**, gewinnt die **tiefste AD**. Die Metrik vergleicht nur Routen **desselben** Protokolls. Vorrang hat immer zuerst das **längste Präfix** (/28 schlägt /24, egal welche AD).

| Quelle | AD | | Quelle | AD |
|---|---|---|---|---|
| Connected | 0 | | IS-IS | 115 |
| Static | 1 | | RIP | 120 |
| EIGRP Summary | 5 | | EGP | 140 |
| **eBGP** | **20** | | ODR | 160 |
| **EIGRP intern** | **90** | | EIGRP extern | 170 |
| IGRP | 100 | | **iBGP** | **200** |
| **OSPF** | **110** | | Floating Static (z. B. Default-Route per DHCP) | 254 |
| | | | Unknown (wird nie verwendet) | 255 |

#### Nachschlagetabelle: Subnetze und Wildcards (IPv4)

Hosts pro Subnetz = 2^Hostbits − 2 (Netz- und Broadcast-Adresse abziehen). Wildcard = 255.255.255.255 − Maske.

| Präfix | Subnetzmaske | Wildcard | Adressen | nutzbare Hosts | Schrittweite |
|---|---|---|---|---|---|
| /16 | 255.255.0.0 | 0.0.255.255 | 65 536 | 65 534 | 1 im 2. Oktett |
| /17 | 255.255.128.0 | 0.0.127.255 | 32 768 | 32 766 | 128 im 3. Oktett |
| /18 | 255.255.192.0 | 0.0.63.255 | 16 384 | 16 382 | 64 im 3. Oktett |
| /19 | 255.255.224.0 | 0.0.31.255 | 8 192 | 8 190 | 32 im 3. Oktett |
| /20 | 255.255.240.0 | 0.0.15.255 | 4 096 | 4 094 | 16 im 3. Oktett |
| /21 | 255.255.248.0 | 0.0.7.255 | 2 048 | 2 046 | 8 im 3. Oktett |
| /22 | 255.255.252.0 | 0.0.3.255 | 1 024 | 1 022 | 4 im 3. Oktett |
| /23 | 255.255.254.0 | 0.0.1.255 | 512 | 510 | 2 im 3. Oktett |
| /24 | 255.255.255.0 | 0.0.0.255 | 256 | 254 | 1 im 3. Oktett |
| /25 | 255.255.255.128 | 0.0.0.127 | 128 | 126 | 128 im 4. Oktett |
| /26 | 255.255.255.192 | 0.0.0.63 | 64 | 62 | 64 |
| /27 | 255.255.255.224 | 0.0.0.31 | 32 | 30 | 32 |
| /28 | 255.255.255.240 | 0.0.0.15 | 16 | 14 | 16 |
| /29 | 255.255.255.248 | 0.0.0.7 | 8 | 6 | 8 |
| /30 | 255.255.255.252 | 0.0.0.3 | 4 | 2 | 4 (Transfernetz zwischen Routern) |
| /32 | 255.255.255.255 | 0.0.0.0 | 1 | 1 | Host-Route, Loopback |

**VLSM (Variable Length Subnet Masking):** Subnetze **nach Grösse absteigend** vergeben, jedes an einer durch seine Blockgrösse teilbaren Adresse beginnen lassen.
Beispiel (NPDO-Lab: Extern ≥ 400, Intern ≥ 100, Verwaltung ≤ 20 IPs, Basis 10.0.0.0):
Extern **/23** → 10.0.0.0–10.0.1.255 (510 Hosts) · Intern **/25** → 10.0.2.0–10.0.2.127 (126) · Verwaltung **/27** → 10.0.2.128–10.0.2.159 (30) · Transfernetze /30 ab 10.0.2.160.

### 6.2 Statisches Routing (IPv4) 🧪

```
R1(config)# ip route 192.168.10.0 255.255.255.0 192.168.9.2      (Zielnetz Maske Next-Hop)
R1(config)# ip route 192.168.10.0 255.255.255.0 g0/1             (Exit-Interface, nur bei P2P sinnvoll)
R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.1                  (Default-Route, "Gateway of last resort")
R1(config)# no ip route 192.168.10.0 255.255.255.0 192.168.9.2   (löschen)
R1# show ip route static  |  show ip route connected
```

**Floating Static Route (Backup-Route):**

```
R1(config)# ip route 10.10.10.0 255.255.255.0 10.10.2.2          (AD 1 → aktiv)
R1(config)# ip route 10.10.10.0 255.255.255.0 10.10.3.2 20       (AD 20 → nur, wenn die erste wegfällt)
```

⚠️ Die Zahl am Ende ist die **administrative Distanz**, keine Metrik (NPDO-Folie «Statisches Routing mit Metrik»). Die Backup-Route wird erst aktiv, wenn die Hauptroute aus der Tabelle verschwindet (z. B. weil das Exit-Interface down geht). Soll sie eine OSPF-Route (AD 110) absichern, muss die AD **> 110** sein.

**Statisches Routing «hin und zurück»:** Jeder Router auf dem Weg braucht eine Route zum Ziel **und** eine zurück zum Quellnetz. Fehlt die Rückroute, schlägt ein Ping fehl, obwohl die Hinroute stimmt.

### 6.3 Routenzusammenfassung (Summarization)

Vorteil: kleinere Routingtabellen, weniger Speicher, weniger Konfiguration, Stabilität.
Vorgehen: alle Subnetz-IDs auflisten → tiefste und höchste Adresse bestimmen → gemeinsame Bits von links zählen.

Beispiel 10.10.1.0/24 bis 10.10.4.0/24: Die gemeinsamen Bits im 3. Oktett (1 = 00000**001**, 4 = 00000**100**) reichen bis Bit 5 → **10.10.0.0/21** (10.10.0.0 – ⚠️ **10.10.7.255**; auf der Folie steht fälschlich 10.0.7.255). Das ebenfalls gezeigte /16 funktioniert, fasst aber viel mehr zusammen als nötig.

Umsetzung: OSPF am ABR `area X range …`, EIGRP am Interface `ip summary-address eigrp …`, BGP mit Null-Route + `network` (siehe oben).

### 6.4 OSPF (Open Shortest Path First, OSPFv2 für IPv4) 🧪

**Grundlagen:** Link-State-IGP für IPv4 (v2) und IPv6 (v3), das meistgenutzte IGP, loopfrei, unterstützt **VLSM/CIDR**. Nachbarn finden sich über **Hello-Pakete** (Multicast **224.0.0.5**, DR/BDR 224.0.0.6, Default Hello 10 s / Dead 40 s). Router tauschen **LSAs** (Link-State Advertisements) aus und speichern sie in der **LSDB**; aus ihr berechnet jeder Router per SPF die besten Wege.
**Areas:** **Area 0 = Backbone**, alle anderen Areas müssen an Area 0 grenzen (sonst Virtual Link). **ABR** (Area Border Router) verbindet Areas und kennt die LSDB beider Areas. Stub Areas reduzieren die LSAs.

```
R1(config)# router ospf 1                                  (Prozess-ID nur lokal, darf je Router verschieden sein)
R1(config-router)# router-id 1.1.1.1
R1(config-router)# network 192.168.2.0 0.0.0.3 area 0      (Wildcard-Maske!)
R1(config-router)# network 10.0.0.0 0.0.255.255 area 0     (alle Interfaces in 10.0.x.x)
R1(config-router)# passive-interface g0/2                  (keine Hellos ins LAN/WAN, Netz wird trotzdem angekündigt)
! 🔎 Alternative pro Interface:
R1(config-if)# ip ospf 1 area 0
```

**Wildcard-Maske** = invertierte Subnetzmaske (255.255.255.255 − Maske): /24 → `0.0.0.255`, /30 → `0.0.0.3`, Host → `0.0.0.0`.

**Router-ID (RID) – Auswahlreihenfolge**
1. manuell mit `router-id`,
2. höchste IP eines aktiven **Loopback**-Interfaces,
3. höchste IP eines aktiven physischen Interfaces.

Die RID muss **eindeutig** sein. Eine Änderung wird erst aktiv nach `clear ip ospf process` (mit *yes* bestätigen) oder nach einem Neustart des Prozesses: `show run | section ospf` kopieren → `R1(config)# no router ospf 1` → Konfiguration wieder einfügen. ⚠️ Die Folie schreibt `R1# no run ospf`, das gibt es nicht.

```
R1(config)# interface loopback 0
R1(config-if)# ip address 1.1.1.1 255.255.255.255          (kein no shutdown nötig)
R1# show ip protocols                                       (Router-ID, Netze, passive Interfaces, Nachbarn)
```

**Default-Route per OSPF verteilen (Internet über den Hauptstandort):**

```
R1(config)# ip route 0.0.0.0 0.0.0.0 200.0.0.2
R1(config)# router ospf 1
R1(config-router)# default-information originate          (nur wirksam, wenn eine Default-Route existiert)
```

Die anderen Router sehen danach `O*E2 0.0.0.0/0`.

**Multi-Area mit manueller Summarization am ABR:**

```
R3(config)# router ospf 1
R3(config-router)# network 10.0.0.0 0.0.255.255 area 0
R3(config-router)# network 10.1.0.0 0.0.255.255 area 1
R3(config-router)# area 1 range 10.1.0.0 255.255.0.0        (Area 1 als ein /16 in Area 0 ankündigen)
```

**Analyse**

| Befehl | Zweck |
|---|---|
| `show ip ospf neighbor` | Nachbarn und Zustand (**FULL** = ok, siehe [Ausgaben](#ausgaben)) |
| `show ip route ospf` | gelernte Routen (O, O IA, O E2) |
| `show ip ospf interface brief` | Interfaces im OSPF, Area, Cost, Zustand (DR/BDR/P2P) |
| `show ip ospf interface g0/0` | Hello/Dead-Timer, Netzwerktyp, passive? |
| `show ip ospf database` | LSDB |
| `show ip protocols` | RID, `network`-Statements, passive Interfaces |
| `debug ip ospf hello` / `debug ip ospf adj` | Mismatch-Meldungen (Timer, Area, Maske) |

🔎 **Voraussetzungen für eine Nachbarschaft:** gleiches **Subnetz und gleiche Maske**, gleiche **Area**, gleiche **Hello-/Dead-Timer**, gleiche **Authentifizierung**, gleiches **Stub-Flag**, **eindeutige Router-ID**, Interface **nicht passiv**, gleiche **MTU** (sonst hängt es in EXSTART/EXCHANGE), kein ACL-Block für OSPF (IP-Protokoll 89).

### 6.5 EIGRP (Enhanced Interior Gateway Routing Protocol) 🧪

Cisco-Protokoll (heute als RFC 7868 offen), «Advanced Distance Vector», schnelle Konvergenz durch Feasible Successors (Backup-Routen), Metrik aus Bandbreite und Delay, Multicast **224.0.0.10**, AD **90** intern / **170** extern. Die **AS-Nummer muss auf allen Routern gleich sein** (anders als die OSPF-Prozess-ID).

```
R1(config)# router eigrp 20
R1(config-router)# eigrp router-id 1.1.1.1              (sonst höchste Loopback-IP, dann höchste IP)
R1(config-router)# network 10.0.0.0 0.255.255.255
R1(config-router)# network 192.168.1.244 0.0.0.3
R1(config-router)# no auto-summary                      (ab IOS 15 Default, sicherheitshalber setzen)
R1(config-router)# passive-interface g2/0               (ins WAN keine Hellos)
R1(config-router)# passive-interface loopback 0
! Manuelle Summarisation auf einem Interface
R1(config)# interface g1/0
R1(config-if)# ip summary-address eigrp 20 10.0.0.0 255.0.0.0
! Default-Route per EIGRP verteilen (Variante aus den Folien)
R1(config)# ip route 0.0.0.0 0.0.0.0 200.0.0.2
R1(config)# interface g0/0                              (Interface nach innen)
R1(config-if)# ip summary-address eigrp 20 0.0.0.0 0.0.0.0
! 🔎 Alternative: router eigrp 20 → redistribute static
```

Analyse: `show ip eigrp neighbors`, `show ip route eigrp` (Code **D**, extern **D EX**), `show ip eigrp interfaces`, `show ip eigrp topology`, `show ip protocols`, `show run | section eigrp`.
🔎 Typische Fehler: verschiedene AS-Nummern, falsche `network`-/Wildcard-Angaben, passive Interfaces, verschiedene K-Werte, Authentifizierung.

**RIP** (nur noch zur Einordnung, muss nicht mehr konfiguriert werden): `router rip` → `version 2` → `network 192.168.1.0` → `no auto-summary`.

### 6.6 IPv6-Grundlagen (Repetition NPDO)

- 128 Bit, hexadezimal in 8 Blöcken zu 16 Bit, **kein Broadcast** (Multicast), **NDP statt ARP**, IPsec integriert, Header fix **40 Byte** (Version, Traffic Class, Flow Label, Payload Length, Next Header, **Hop Limit** = TTL, Source, Destination, Extension Header).
- **Dual Stack:** IPv4 und IPv6 parallel (lange Koexistenz).

**Kürzen:** 1. führende Nullen pro Block weglassen, 2. **einmal** eine Folge von Null-Blöcken durch `::` ersetzen (die längste; bei Gleichstand die erste).
Beispiel: `2001:0000:0000:04f3:0001:0000:0000:0010` → `2001::4f3:1:0:0:10`.

**Präfix bestimmen:** Adresse nach /n Bits abschneiden, z. B. `4004:eeee:ffff:0f0f:…/36` → `4004:eeee:f000::/36`.

| Adresstyp | Bereich | Bemerkung |
|---|---|---|
| Global Unicast (GUA) | `2000::/3` | weltweit eindeutig, geroutet |
| Link-Local | `fe80::/10` | auf jedem IPv6-Interface automatisch, **nicht geroutet**, NDP und Routing-Nachbarn nutzen sie, oft Gateway-Adresse der Clients |
| Unique Local (ULA) | `fc00::/7` (praktisch `fd00::/8`) | privat, entspricht RFC 1918 |
| Multicast | `ff00::/8` | `ff02::1` alle Knoten, `ff02::2` alle Router, `ff02::5`/`::6` OSPF, `ff02::a` EIGRP, `ff02::1:2` DHCPv6 |
| Solicited-Node | `ff02::1:ffXX:XXXX` | letzte 24 Bit der Zieladresse, ersetzt den ARP-Broadcast (L2: `33:33:ff:XX:XX:XX`) |
| Loopback / Unspecified | `::1` / `::` | |
| Dokumentation | `2001:db8::/32` | |

**EUI-64** (Interface-ID aus MAC): MAC teilen → `FFFE` in die Mitte → **7. Bit (U/L-Bit) invertieren**.
Beispiel: `B4:61:75:A8:43:11` → `B461:75FF:FEA8:4311` → B4 = 1011 0100 → 1011 0110 = **B6** → `2001::B661:75FF:FEA8:4311/64`.

**NDP (ICMPv6)**

| Nachricht | Zweck |
|---|---|
| **RS** (Router Solicitation, an `ff02::2`) / **RA** (Router Advertisement, an `ff02::1`) | Router finden, Präfix und Präfixlänge lernen (SLAAC), Default-Gateway |
| **NS** / **NA** (Neighbor Solicitation/Advertisement) | MAC-Adresse auflösen (statt ARP), **DAD** (Duplicate Address Detection) |

**Adressvergabe**

| Methode | RA-Flags | Adresse von | DNS usw. von |
|---|---|---|---|
| **SLAAC** | M=0, O=0 | selbst (Präfix aus RA + EUI-64/Zufall) | (RDNSS in RA) |
| **Stateless DHCPv6** | O=1 (`other-config-flag`) | SLAAC | DHCPv6 |
| **Stateful DHCPv6** | M=1 (`managed-config-flag`) | DHCPv6 | DHCPv6 |

Das **Default-Gateway kommt immer aus dem RA** (Link-Local-Adresse des Routers), nie aus DHCPv6. DHCPv6-Nachrichten: Solicit → Advertise → Request → Reply.

### 6.7 IPv6 auf Cisco konfigurieren 🧪

```
R1(config)# ipv6 unicast-routing                         (!! sonst routet der Router kein IPv6 und sendet keine RAs)
R1(config)# interface g0/0
R1(config-if)# ipv6 enable                                (nur Link-Local)
R1(config-if)# ipv6 address 2001:db8:33:1::1/64          (GUA statisch)
R1(config-if)# ipv6 address 2001:db8:33:1::/64 eui-64    (GUA mit EUI-64)
R1(config-if)# ipv6 address fe80::1 link-local           (Link-Local manuell, gut lesbar als Gateway)
R1(config-if)# no shutdown
! Statisch
R1(config)# ipv6 route 2001:db8:33:2::/64 2001:db8:33:1::2
R1(config)# ipv6 route ::/0 2001:db8:33:1::2             ⚠️ ohne /64 beim Next Hop (Fehler auf NIUS-Folie 186 / NPDO 454)
R1(config)# ipv6 route ::/0 s0/0/1                        (Exit-Interface, bei P2P)
R1(config)# ipv6 route ::/0 g0/1 fe80::2                 🔎 bei Ethernet mit Link-Local-Next-Hop Interface angeben
```

**Switch:** `interface vlan 1` → `ipv6 address 2001:db8:33:1::2/64`.
🔎 In PT fehlt der Befehl auf dem 2960 zunächst: vorher `sdm prefer dual-ipv4-and-ipv6 default` + `reload`. ⚠️ Die Folie zeigt beim IPv6-Switch `ip default-gateway 192.168.1.1`, das gilt nur für IPv4.

**SLAAC:** `ipv6 unicast-routing` + GUA /64 auf dem Interface genügt (RA mit M=0, O=0).

**Stateless DHCPv6** (in PT möglich):

```
R1(config)# ipv6 dhcp pool STATELESSPOOL
R1(config-dhcpv6)# dns-server 2001:db8:33::10
R1(config-dhcpv6)# domain-name firma.local
R1(config)# interface g0/0
R1(config-if)# ipv6 dhcp server STATELESSPOOL
R1(config-if)# ipv6 nd other-config-flag
```

**Stateful DHCPv6** (laut NPDO in PT nicht möglich):

```
R1(config)# ipv6 dhcp pool STATEFULPOOL
R1(config-dhcpv6)# address prefix 2001:db8:33:1::/64
R1(config-dhcpv6)# dns-server 2001:db8:33:3::10
R1(config-dhcpv6)# domain-name firma.local
R1(config)# interface g0/0
R1(config-if)# ipv6 dhcp server STATEFULPOOL
R1(config-if)# ipv6 nd managed-config-flag
R1(config-if)# ipv6 nd prefix 2001:db8:33::/64 14400 14400 no-autoconfig    (SLAAC unterdrücken)
R1# show ipv6 dhcp  |  show ipv6 dhcp binding  |  show ipv6 dhcp pool
```

**Analyse:** `show ipv6 interface brief`, `show ipv6 interface g0/0` (Link-Local, GUA, joined Multicast-Gruppen, ND-Flags), `show ipv6 route` (connected/static/`show ipv6 route 2001:db8:33:2::11`), `show ipv6 neighbors`, Client: `ipconfig` / `ip -6 addr`, `ping6`, `traceroute6`, `ip -6 neighbor`.

### 6.8 OSPFv3 und EIGRP für IPv6 🧪

**OSPFv3** wird **pro Interface** aktiviert (kein `network`). Die Router-ID bleibt eine 32-Bit-Zahl und muss manuell gesetzt werden, wenn keine IPv4-Adresse vorhanden ist.

```
R1(config)# ipv6 unicast-routing
R1(config)# ipv6 router ospf 1
R1(config-rtr)# router-id 1.1.1.1
R1(config-rtr)# passive-interface g0/2               (z. B. Richtung WAN/LAN ohne Nachbarn)
R1(config-rtr)# default-information originate        (Default-Route verteilen, braucht ipv6 route ::/0 …)
R1(config)# interface g0/0
R1(config-if)# ipv6 ospf 1 area 0
R1(config)# interface g0/1
R1(config-if)# ipv6 ospf 1 area 0
```

Analyse: `show ipv6 protocols`, `show ipv6 ospf`, `show ipv6 ospf neighbor`, `show ipv6 ospf interface [brief]`, `show ipv6 route ospf`, `show ipv6 ospf database`.

**EIGRP für IPv6**

```
R1(config)# ipv6 unicast-routing
R1(config)# ipv6 router eigrp 200
R1(config-rtr)# eigrp router-id 1.1.1.1              (Folie: "router-id"; 🔎 klassisches IOS nutzt meist "eigrp router-id")
R1(config-rtr)# no shutdown                          🔎 bei älteren IOS-Versionen ist der Prozess sonst "shutdown"
R1(config-rtr)# passive-interface g0/2
R1(config)# interface g0/0
R1(config-if)# ipv6 eigrp 200
R1(config)# interface g0/1
R1(config-if)# ipv6 eigrp 200
```

Analyse: `show ipv6 protocols`, `show ipv6 eigrp neighbors`, `show ipv6 eigrp interfaces`, `show ipv6 eigrp topology`, `show ipv6 route eigrp`.

---

<a id="b6"></a>
## 7. Block 6 – ACLs, NAT und Kombination der Technologien

In Block 6 werden alle Technologien in einem **gemeinsamen PT-Lab** kombiniert (IPv4, IPv6, VLAN, VTP, **RSTP**, **ACL**, **NAT/PAT**, FHRP). Praxistransfer: eigenes Netz fertig konfigurieren (RSTP, NAT beim Internetzugang, sichere ACLs vor allem Richtung Internet).

### 7.1 Firewalls und Zonen

| Typ | Funktion |
|---|---|
| Statischer Paketfilter | sequenzielle Regeln (Quell-/Ziel-IP, Port); z. B. Router-ACL |
| Dynamischer Paketfilter (**Stateful Inspection**) | merkt sich Verbindungen: Antworten sind nur erlaubt, wenn vorher eine Anfrage ging |
| Application Level Gateway | prüft auf Anwendungsebene (Proxies für HTTP, SMTP …) |
| UTM (Unified Threat Management) | SPI-Firewall + IDS/IPS + Antivirus + Content-Filter + VPN |
| Personal Firewall | auf dem Client, immer aktiv lassen |

**Zonenkonzept (DMZ):** Internet → Firewall → **DMZ** (Webserver, Mailrelay, FTP, externes WLAN) → Firewall → **interne Zone** (Server, Clients). Grundsatz: **implizit alles verbieten (Deny)**, nur Nötiges erlauben. Eine «Any-Any-Allow»-Regel am Schluss höchstens vorübergehend zum Beobachten verwenden.
Firewall von aussen prüfen (nur eigene IPs, mit Erlaubnis): heise Netzwerk-Check, GRC ShieldsUP!, SSL Labs.

### 7.2 Access Control Lists (ACLs) 🧪

**Regeln**

- ACLs werden **von oben nach unten** abgearbeitet. **Die erste passende Regel gilt**, danach wird nichts mehr geprüft → Reihenfolge ist entscheidend (spezifisch vor allgemein).
- Am Ende steht immer ein **implizites `deny any`** (nicht sichtbar). Eine ACL nur mit `deny`-Einträgen blockiert also **alles**.
- Pro Interface, pro Richtung (**in**/**out**) und pro Protokoll (IPv4/IPv6) ist **eine** ACL erlaubt.
- **in** = Pakete, die ins Interface hinein kommen (vor dem Routing); **out** = Pakete, die das Interface verlassen.
- Eine ACL wirkt erst, wenn sie einem Interface zugewiesen ist (`ip access-group`) bzw. einer VTY-Line (`access-class`). Eine zugewiesene, aber **nicht existierende** ACL lässt alles durch.
- 🔎 Vom Router **selbst erzeugte** Pakete (z. B. Ping vom Router) werden von einer **ausgehenden** ACL nicht gefiltert.

**Wildcard-Masken:** 0 = Bit muss passen, 1 = egal.
`0.0.0.0` = genau ein Host (Kurzform `host 10.0.0.10`); `255.255.255.255` = alle (Kurzform `any`); `0.0.0.255` = /24.

| Typ | Nummern | Prüft | 🔎 Platzierung |
|---|---|---|---|
| **Standard** | 1–99, 1300–1999 | **nur Quell-IP** | möglichst **nahe beim Ziel** |
| **Extended** | 100–199, 2000–2699 | Protokoll, Quell-/Ziel-IP, Quell-/Ziel-Port | möglichst **nahe bei der Quelle** |
| **Named** (standard/extended) | Name | wie oben | wie oben, mit Sequenznummern **bearbeitbar** |

```
! Nummerierte Standard-ACL
R1(config)# access-list 1 deny 10.0.0.0 0.0.0.255
R1(config)# access-list 1 permit any                  (sonst blockiert das implizite deny alles!)
R1(config)# interface g0/0
R1(config-if)# ip access-group 1 out                  ⚠️ Folie: "ip access-groups"

! Nummerierte Extended-ACL
R1(config)# access-list 100 deny tcp any any eq 80
R1(config)# access-list 100 permit ip any any
R1(config)# interface g0/1
R1(config-if)# ip access-group 100 in

! Named Extended-ACL (Beispiel aus den Folien)
R1(config)# ip access-list extended LISTE1
R1(config-ext-nacl)# permit tcp host 10.0.0.10 host 10.0.0.1 eq telnet
R1(config-ext-nacl)# deny tcp host 10.0.0.11 host 10.0.0.1 eq telnet
R1(config-ext-nacl)# permit icmp host 10.0.0.10 host 10.0.0.1 echo
R1(config-ext-nacl)# permit ip any any
R1(config)# interface g0/0
R1(config-if)# ip access-group LISTE1 out
```

Syntax Extended: `permit|deny <protokoll> <quelle> <wildcard> [eq <port>] <ziel> <wildcard> [eq <port>]`
Protokolle: `ip`, `tcp`, `udp`, `icmp`, `ospf`, `eigrp`. Ports: `eq 22` / `eq www` / `eq domain` (53), `gt`, `lt`, `range 1000 2000`, bei ICMP `echo`, `echo-reply`. TCP-Antworten: `established`.

**Sequenznummern und Bearbeiten**

```
R1# show access-lists                           (alle ACLs mit Sequenznummern und Treffern "(x matches)")
R1(config)# ip access-list extended 100          (auch nummerierte ACLs so bearbeiten)
R1(config-ext-nacl)# no 10                       (einzelnen Eintrag löschen)
R1(config-ext-nacl)# 5 permit tcp 10.0.0.0 0.0.0.255 host 10.1.1.10 eq 80   (vor Eintrag 10 einfügen)
R1(config)# ip access-list resequence 100 10 10  🔎 neu nummerieren
R1(config-if)# no ip access-group 100 in         (ACL vom Interface entfernen)
R1(config)# no access-list 100                   (ganze ACL löschen)
```

⚠️ `no access-list 101 deny tcp any any eq 80` (Folie) löscht nicht nur diese Zeile, sondern die **ganze nummerierte ACL**. Einzelne Einträge nur über `ip access-list … → no <Seq>` löschen. (Auf der Folie steht zudem 101 statt 100.)
⚠️ Die NPDO-Folie «Access Lists einrichten» zeigt `access-list 1 permit ip 10.0.0.0 0.0.0.255 10.1.1.10 0.0.0.255`. Eine **Standard**-ACL kennt aber **nur die Quelle** und kein Protokoll, der Befehl ist ungültig. Für Quelle + Ziel braucht es eine Extended-ACL (100–199). Ausserdem passt `10.1.1.10 0.0.0.255` auf das ganze Netz 10.1.1.0/24; für einen Host `host 10.1.1.10` schreiben.

**Anzeigen:** `show access-lists [100]`, `show ip access-lists`, `show ip interface g0/0` (welche ACL ist in/out gesetzt), `show running-config | include access`.
Zeitbasierte ACLs: `time-range`, prüfen mit `show time-range` (Uhrzeit mit `clock set` bzw. NTP korrekt?).

🔎 **Typisches Muster «sichere ACL ins Internet» (Extended, in auf dem LAN-Subinterface)**

```
ip access-list extended VLAN10-IN
 permit udp any any eq bootps                                    (DHCP-Discover/Request von 0.0.0.0 zum Router!)
 permit udp 192.168.10.0 0.0.0.255 host 192.168.99.10 eq 53     (interner DNS)
 permit tcp 192.168.10.0 0.0.0.255 any eq 80
 permit tcp 192.168.10.0 0.0.0.255 any eq 443
 permit icmp 192.168.10.0 0.0.0.255 any echo
 deny   ip any any                                               (explizit, damit Treffer sichtbar werden)
```

Nicht vergessen: Eine **inbound**-ACL filtert auch Verkehr **an den Router selbst**. Deshalb DHCP erlauben (UDP 67/68), falls der Router für dieses Netz **DHCP-Server oder Relay** ist, dazu DNS (UDP 53, oft auch TCP 53) und Routingprotokolle (OSPF/EIGRP), wenn die ACL auf einem Transfer-Interface liegt. Genau so ein vergessener DNS-Eintrag war der Fehler in **Lab 03**.

### 7.3 NAT (Network Address Translation) 🧪

**Warum?** Private Adressen (RFC 1918) werden im Internet nicht geroutet. NAT ersetzt die private **Quelladresse** durch eine öffentliche und merkt sich die Zuordnung in der **NAT-Tabelle**, damit Antworten zurückfinden. Heute fast immer **PAT** (Port Address Translation, «Overload»): viele interne Hosts teilen sich **eine** öffentliche IP, unterschieden durch Ports.

| Begriff | Bedeutung |
|---|---|
| **SNAT** (Source NAT, outbound) | interne Quelladresse → öffentliche Adresse (z. B. PAT) |
| **DNAT** (Destination NAT, inbound) | öffentliche Zieladresse/Port → interner Server (**Port Forwarding**) |
| Static NAT | feste 1:1-Zuordnung (Server) |
| Dynamic NAT | Zuordnung aus einem Pool öffentlicher Adressen (1:1, solange Adressen frei sind) |
| PAT / Overload | n:1 über Ports |
| 🔎 Inside Local / Inside Global | private Adresse des internen Hosts / seine öffentliche Adresse nach NAT |

```
! 1. Interfaces markieren (IMMER nötig)
R1(config)# interface g0/0                 (LAN, auch jedes Subinterface g0/0.10 …)
R1(config-if)# ip nat inside
R1(config)# interface g0/1                 (WAN)
R1(config-if)# ip nat outside

! 2a. Static NAT
R1(config)# ip nat inside source static 10.0.0.10 203.0.113.10

! 2b. Dynamic NAT mit Pool
R1(config)# ip nat pool POOL01 203.0.113.1 203.0.113.254 netmask 255.255.255.0
!                                                     (oder: prefix-length 24)
R1(config)# access-list 1 permit 10.0.0.0 0.0.0.255
R1(config)# ip nat inside source list 1 pool POOL01

! 2c. PAT auf die WAN-Interface-Adresse (häufigster Fall)
R1(config)# access-list 1 permit 10.0.0.0 0.0.0.255
R1(config)# access-list 1 permit 10.0.1.0 0.0.0.255
R1(config)# ip nat inside source list 1 interface g0/1 overload

! 2d. Port Forwarding (DNAT) auf internen Webserver
R1(config)# ip nat inside source static tcp 10.0.0.10 443 192.0.2.1 443
```

- Die ACL für NAT legt nur fest, **wer** übersetzt wird (Standard-ACL mit den internen Netzen).
- **ACL + PAT:** In einer **ausgehenden** ACL auf dem WAN-Interface steht bereits die **übersetzte** (öffentliche) Adresse, z. B. `permit tcp host 203.0.113.1 any eq 80`.

**Analyse:** `show ip nat translations` (leer? → siehe Troubleshooting), `show ip nat statistics` (inside/outside Interfaces, Hits/Misses, zugeordnete ACL), `debug ip nat`, `clear ip nat translation *`.

---

<a id="b7"></a>
## 8. Block 7 und 8 – Strukturierte Störungsbehebung

Ziel von Block 7/8: durch **VLANs, STP, Routing und ACLs** verursachte Störungen strukturiert ermitteln, lösen und beurteilen. In der Prüfung sind Fehler in PT-Dateien zu finden und auf dem Lösungsblatt zu dokumentieren.

### 8.1 Leitfaden: Vorgehen bei einer Störung

1. **Problem aufnehmen und verifizieren:** Wer ist betroffen? Was genau geht nicht (Ping? Name? Webseite? nur langsam? nur beim Start)? Seit wann? **Was wurde geändert?** Dann selbst nachstellen (z. B. Ping vom betroffenen Host).
2. **Umfang eingrenzen:** Nur ein Host, ein VLAN, ein Standort oder alle? **Funktioniert ein vergleichbares Gerät?** (Lab Phase 1.3: «Können A und B miteinander kommunizieren?» → Ja → Problem liegt bei C, dessen Port oder der Verbindung SW1–SW2.)
3. **Informationen sammeln:** Topologie und IP-Konzept (Doku, `show cdp neighbors`), `show`-Befehle, Logs.
4. **Hypothese bilden: «Was muss wahr sein, damit es funktioniert?»** Jede Voraussetzung wird zu einem Prüfpunkt (siehe 8.3).
5. **Hypothese gezielt testen** (passende Methode wählen, siehe 8.2).
6. **Beheben:** eine Änderung nach der anderen, vorher die Konfiguration sichern.
7. **Verifizieren:** ursprünglichen Test wiederholen und prüfen, ob nichts anderes kaputt ging. **Konvergenz abwarten** (STP bis ca. 50 s, Routingprotokolle einige Sekunden).
8. **Dokumentieren:** betroffenes Gerät, Fehlerbeschreibung, Befehle zur Fehlersuche, Befehle zur Behebung. Genau dieses Format verlangen die Lösungsdateien der Labs.
9. Falls nötig **eskalieren** (Provider, Hersteller, 2nd Level).

### 8.2 Troubleshooting-Methoden 🔎

| Methode | Vorgehen | Geeignet, wenn … |
|---|---|---|
| **Bottom-up** | ab Layer 1 (Kabel, Link) nach oben | physisches Problem vermutet, neue Installation |
| **Top-down** | ab Layer 7 (Applikation) nach unten | ein einzelner Dienst geht nicht (z. B. nur Web) |
| **Divide and Conquer** | in der Mitte starten (meist **Layer 3: Ping**), dann je nach Ergebnis hoch oder runter | Standardfall; ein erfolgreicher Ping bestätigt L1–L3 (so im Lab Phase 1.8) |
| **Follow the Path** | dem Weg des Pakets folgen (Host → Switch → Gateway → Router …), z. B. mit `traceroute` | Routing-/Mehrhop-Probleme |
| **Compare Configurations / Spot the Differences** | funktionierendes mit nicht funktionierendem Gerät vergleichen | «alle anderen funktionieren» (Lab 03) |
| **Swap Components / Move the Problem** | Komponente tauschen (Kabel, Port, PC) | Client- oder Hardwareproblem abgrenzen |

### 8.3 Was muss wahr sein? Prüfpunkte pro Schicht

**Layer 1 – physisch**
- Geräte eingeschaltet, richtiges Kabel (in PT: Straight-Through vs. Crossover, serielles DCE/DTE) und am **richtigen Port**.
- Interfaces `up`: `show ip interface brief`, `show interfaces status`; Router-Interfaces **`no shutdown`**!
- Keine Fehlerzähler (CRC, Collisions) und kein Duplex-/Speed-Mismatch: `show interfaces`.

**Layer 2 – Sicherung**
- Access-Port im **richtigen VLAN**, VLAN **existiert** auf **jedem** Switch auf dem Weg (`show vlan brief`).
- Verbindung zwischen Switches **auf beiden Seiten Trunk** (oder beide Access im gleichen VLAN), VLAN **allowed** und **nicht gepruned**, **Native VLAN gleich** (`show interfaces trunk`).
- **STP:** Port in Forwarding? Root-Bridge sinnvoll? PortFast auf Endgeräte-Ports (`show spanning-tree`).
- Port nicht **err-disabled** (Port Security, BPDU Guard), EtherChannel gebündelt (`show etherchannel summary`).
- VTP-Domain, -Passwort und -Modus korrekt (`show vtp status`).

**Layer 3 – Vermittlung**
- Host: korrekte **IP, Maske, Gateway** (und DNS). Gateway gleiches Subnetz wie der Host.
- Gateway (Router-Subinterface/SVI) mit richtiger IP, **`encapsulation dot1Q <VLAN>`** korrekt, auf L3-Switch **`ip routing`**.
- **Route zum Ziel und zurück** auf jedem Router (`show ip route`), Default-Route vorhanden und verteilt, korrekter **Next Hop** (erreichbar? `ping <next-hop>`).
- Routingprotokoll: Nachbarn vorhanden (`show ip ospf neighbor`), richtige `network`-Statements und Areas, keine falschen `passive-interface` (`show ip protocols`).
- **HSRP:** virtuelle IP = Gateway der Clients (`show standby brief`).

**Layer 4–7**
- **ACLs:** richtige ACL, richtiges Interface, richtige Richtung, richtige Reihenfolge, implizites deny beachten (`show access-lists` Trefferzähler, `show ip interface`).
- **NAT:** inside/outside korrekt, ACL umfasst die internen Netze (`show ip nat translations`/`statistics`).
- **DHCP/DNS:** Pool, `ip helper-address`, DNS-Server erreichbar und in ACLs erlaubt (UDP 53).
- Dienst läuft (Server), Port offen.

### 8.4 Ausgaben interpretieren
<a id="ausgaben"></a>

**`ping` (Cisco) und `traceroute`**

| Zeichen | Bedeutung |
|---|---|
| `!` | Echo Reply erhalten → ok |
| `.` | Timeout (keine Antwort: Route fehlt beim Ziel oder Rückweg, Host down, ACL verwirft ohne Meldung) |
| `U` | Destination Unreachable von einem Router (keine Route, oder ACL mit Unreachable-Meldung) |
| `.!!!!` | erstes Paket verloren wegen **ARP-Auflösung** → normal |
| traceroute `* * *` | Hop antwortet nicht (Paket verloren, Router ohne Route, ICMP gefiltert) |
| traceroute `!H` / `!N` / `!A` | Host / Netz unerreichbar / **administratively prohibited (ACL)** |

Vorgehen beim Ping vom Host: `127.0.0.1` (TCP/IP-Stack) → eigene IP → **Gateway** → Gateway des Ziels → Ziel → Name (DNS). Der erste Schritt, der scheitert, zeigt die Schicht bzw. den Abschnitt.
Traceroute: Der **letzte Hop, der antwortet**, ist der letzte funktionierende Router. Das Problem liegt dort (fehlende oder falsche Route) oder beim nächsten Hop.

**`show ip interface brief`** (Status / Protocol)

| Status / Protocol | Bedeutung | Typische Ursache |
|---|---|---|
| up / up | ok | – |
| **administratively down** / down | Interface mit `shutdown` deaktiviert | `no shutdown` fehlt (Router-Default!) |
| down / down | Layer 1 | Kabel fehlt oder falsch, Gegenseite down, falscher Port |
| up / **down** | Layer 2 | serielle Leitung: **Encapsulation-Mismatch** (HDLC vs. PPP), **Clock Rate** fehlt, PPP-Authentifizierung fehlgeschlagen |
| (Switch) `err-disabled` in `show interfaces status` | Port wegen Sicherheitsverletzung abgeschaltet | Port Security, BPDU Guard |

Bei SVIs (`Vlan10 … up/down`): VLAN existiert nicht oder kein aktiver Port in diesem VLAN.

**`show interfaces trunk`** (vier Blöcke)

1. Port, **Mode** (on/desirable/auto), Encapsulation (802.1q), **Status** (trunking), **Native VLAN**.
2. **VLANs allowed on trunk** → fehlt ein VLAN hier: `switchport trunk allowed vlan` prüfen.
3. **VLANs allowed and active in management domain** → fehlt es hier: das VLAN **existiert auf diesem Switch nicht** (`vlan X` anlegen, VTP prüfen).
4. **VLANs in spanning tree forwarding state and not pruned** → fehlt es nur hier: STP blockiert oder **konvergiert noch** (bis ca. 50 s warten) oder VTP-Pruning.

Erscheint ein Port **gar nicht** in der Ausgabe, ist er kein Trunk (Gegenseite prüfen: Trunk ↔ Access-Mismatch, auto+auto).

**`show vlan brief`:** Ports, die hier **fehlen**, sind Trunks (oder Routed Ports). Ein Access-Port in einem **nicht existierenden VLAN** ist inaktiv und leitet nichts weiter.

**`show spanning-tree vlan X`**
- **Root ID** mit «This bridge is the root» → dieser Switch ist Root. Sonst zeigt Root ID Priorität und MAC der Root plus den eigenen Root Port.
- **Bridge ID** = eigene Priorität (+ VLAN-ID) und MAC.
- Pro Port: **Role** (Root, Desg, Altn, Back), **Sts** (FWD, BLK, LRN, LIS, DSC), Cost, Type (**P2p Edge** = PortFast aktiv).
- Prüffragen: Ist die gewünschte Root-Bridge Root? Blockiert ein Port, der eigentlich forwarden sollte? Endgeräte-Ports ohne PortFast (`Edge` fehlt)?

**`show etherchannel summary`**

| Flag | Bedeutung |
|---|---|
| `P` | Port ist im Port-Channel **gebündelt** (gut) |
| `S` / `R` | Layer-2- / Layer-3-Port-Channel |
| `U` | Port-Channel in Betrieb (gut: `Po1(SU)`) |
| `D` | down |
| `I` | stand-alone: kein Partner (Modus passt nicht, z. B. passive+passive, auto+auto) |
| `s` | suspended: Parameter ungleich (Speed, Duplex, VLAN, Trunk-Einstellungen) |

**`show ip route`**
- Codes: **C** connected, **L** local (eigene IP /32), **S** static, **S\*** statische Default-Route, **O** OSPF, **O IA** OSPF inter-area, **O\*E2** per OSPF verteilte Default-Route, **D** EIGRP, **D EX** EIGRP extern, **B** BGP, **R** RIP.
- `[110/2]` = **[AD/Metrik]**. `via 10.1.1.2` = Next Hop.
- **«Gateway of last resort is not set»** → keine Default-Route (Lab 01!).
- Fehlt ein Netz: Ist das Interface des Zielnetzes up? Route/`network`-Statement vorhanden? Nachbarschaft da?

**`show ip ospf neighbor`**

| Zustand | Bedeutung |
|---|---|
| **FULL** (/DR, /BDR, /-) | ok |
| 2WAY/DROTHER | normal zwischen zwei DROTHERs im Multi-Access-Netz |
| INIT | Hellos kommen nur in eine Richtung (ACL, Multicast-Problem, Authentifizierung) |
| EXSTART / EXCHANGE (hängt) | **MTU-Mismatch** oder doppelte Router-ID |
| kein Eintrag | Area, Subnetz/Maske, Hello/Dead-Timer, Authentifizierung stimmen nicht; Interface passiv; `network` fehlt; Interface down; doppelte RID |

**`show access-lists`:** `(15 matches)` pro Zeile. Zählt die erwartete permit-Zeile **nicht** hoch → ACL am falschen Interface oder in falscher Richtung, oder eine frühere Zeile greift zuerst. Steigt der Zähler eines `deny` → hier wird blockiert.
**`show ip interface g0/0`:** zeigt «Outgoing access list is …» / «Inbound access list is …».

**`show ip nat translations`** leer oder ohne erwartete Einträge → `ip nat inside`/`outside` fehlt oder vertauscht, NAT-ACL erfasst das interne Netz nicht (falsche Wildcard), falsches Interface im `overload`-Befehl, keine Route/Default-Route ins Internet. `show ip nat statistics`: Inside/Outside-Interfaces und **Misses** prüfen.

**`show standby brief`:** Spalten Grp, Pri, **P** (preempt), **State** (Active/Standby), Active, Standby, Virtual IP. **Beide Router «Active»** → sie hören sich nicht (Gruppennummer, Version, VLAN/Subnetz verschieden, L2-Verbindung fehlt). «Standby: unknown» → kein Partner.

**`show port-security interface fa0/5`:** Port Status (**Secure-up** / **Secure-shutdown**), Violation Mode, Maximum MAC, **Security Violation Count**, Last Source Address (welche MAC hat verletzt).

**`show cdp neighbors [detail]`:** Nachbargerät, lokaler Port, Port beim Nachbarn, Plattform, mit `detail` auch dessen IP. Ideal, um die Verkabelung zu überprüfen und die Topologie zu dokumentieren. CDP meldet auch **Native VLAN mismatch** und **Duplex mismatch** als Log-Meldung. Offener Standard: LLDP (`lldp run`, `show lldp neighbors`). 🔎 Aus Sicherheitsgründen an Ports Richtung Internet/Kunden deaktivieren (`no cdp enable`).

**`show interfaces`:** «line protocol», Duplex/Speed, **input errors, CRC** (Kabel, Störungen, Duplex), **late collisions** (Duplex-Mismatch), Last input/output, Load.

### 8.5 Symptom → Ursache → Befehle → Lösung

| Symptom | Mögliche Ursache | Finden mit | Beheben |
|---|---|---|---|
| Host erhält **169.254.x.x** (APIPA) | DHCP-Pool fehlt/falsch, `ip helper-address` fehlt, Port im falschen VLAN, DHCP-Snooping ohne `trust`, ACL blockiert UDP 67/68 | `show ip dhcp pool`, `show ip dhcp binding`, `show run \| section dhcp`, `show vlan brief`, `show ip dhcp snooping` | Pool korrigieren, `ip helper-address <server>`, `switchport access vlan X`, `ip dhcp snooping trust` |
| Host erreicht **Gateway nicht** | falsche IP/Maske/Gateway am Host, Port im falschen VLAN, Trunk zum Router fehlt, falsche `encapsulation dot1Q`-ID, physisches Router-Interface `shutdown`, SVI down | `ipconfig`, `show vlan brief`, `show interfaces trunk`, `show ip interface brief`, `show run interface g0/0.10` | korrigieren, `no shutdown`, `switchport mode trunk` |
| Hosts im **gleichen VLAN** auf verschiedenen Switches erreichen sich nicht | Trunk ↔ Access-Mismatch, VLAN auf einem Switch nicht angelegt, VLAN nicht allowed, Native-VLAN-Mismatch, STP blockiert | `show interfaces status`, `show interfaces trunk`, `show vlan brief`, `show spanning-tree` | `switchport mode trunk`, `vlan X`, `switchport trunk allowed vlan add X` |
| Verbindung **nach dem Start 30–50 s eingeschränkt**, DHCP-Timeout beim Booten | Kein **PortFast** auf Access-Ports, klassisches STP statt RSTP | `show run`, `show spanning-tree summary` | `spanning-tree mode rapid-pvst`, `spanning-tree portfast` + `bpduguard enable` |
| Port plötzlich tot (**err-disabled**) | Port-Security-Verletzung, BPDU Guard hat ausgelöst | `show interfaces status err-disabled`, `show port-security interface …`, `show log` | Ursache beseitigen, `shutdown` → `no shutdown`, ggf. `errdisable recovery` |
| Netz extrem langsam, LEDs blinken dauernd | **Layer-2-Loop** (STP deaktiviert, statisches EtherChannel nur einseitig) | `show spanning-tree`, `show interfaces` (Broadcast-Zähler), `show etherchannel summary` | STP aktivieren, redundanten Link trennen, EtherChannel korrigieren |
| **Anderes Subnetz** nicht erreichbar, Traceroute bricht ab | Route fehlt, **falscher Next Hop**, Rückroute fehlt, OSPF-Nachbarschaft fehlt, `network` fehlt, falsches `passive-interface` | `show ip route`, `ping <next-hop>`, `show run \| include ip route`, `show ip ospf neighbor`, `show ip protocols` | Route korrigieren (`no ip route …` / `ip route …`), OSPF-Parameter angleichen |
| **Internet** nicht erreichbar, intern alles ok | Default-Route fehlt am Grenzrouter oder wird **nicht verteilt**, NAT fehlt/falsch, ACL | `show ip route` («Gateway of last resort is not set»), `show ip nat translations`, `show access-lists` | `ip route 0.0.0.0 0.0.0.0 <ISP>`, `default-information originate`, NAT inside/outside |
| Ping auf IP ok, aber **Webseite per Name** nicht | **DNS**: falscher DNS-Server beim Client/DHCP, **ACL blockiert UDP 53**, DNS-Server down | `nslookup`, `ipconfig /all`, `show access-lists` | DNS-Eintrag im DHCP-Pool, ACL-Eintrag `permit udp … eq 53` |
| Ping ok, **Dienst** (HTTP, SSH) nicht | ACL blockiert Port, Dienst läuft nicht | `show access-lists`, Browser/`telnet <IP> 80` | ACL anpassen, Dienst starten |
| Nur **ein Host** betroffen, andere im gleichen Netz ok | Host-Konfiguration, falscher Port/VLAN, Port Security, Kabel | Vergleich mit funktionierendem Host, `show mac address-table`, `show port-security` | korrigieren |
| **OSPF-Nachbar** fehlt | Area, Subnetz, Timer, passive, doppelte RID, MTU, ACL | `show ip ospf neighbor`, `show ip ospf interface`, `show ip protocols`, `debug ip ospf hello` | angleichen, `no passive-interface`, `clear ip ospf process` |
| **HSRP**: beide Router Active | Gruppe, Version oder Subnetz verschieden, keine L2-Verbindung | `show standby brief` | Parameter angleichen |
| Serielle Verbindung **up/down** | Encapsulation-Mismatch, Clock Rate fehlt am DCE, PPP-Authentifizierung | `show interfaces s0/0/0`, `show controllers s0/0/0`, `debug ppp authentication` | `encapsulation` angleichen, `clock rate`, Benutzer/Passwort |
| **SSH** geht nicht | keine RSA-Keys, kein `ip domain-name`, kein lokaler Benutzer bzw. `login local`, `transport input` falsch, VTY-ACL | `show ip ssh`, `show run \| section line vty` | Keys erzeugen, Benutzer, `transport input ssh` |
| **VTP**: Switch erhält keine VLANs | Domain/Passwort/Version verschieden, kein Trunk, Switch im Transparent-Modus | `show vtp status`, `show interfaces trunk` | angleichen |
| **EtherChannel** bündelt nicht | Modus-Kombination (auto+auto, passive+passive), ungleiche Parameter | `show etherchannel summary` (Flags I/s) | Modus bzw. Parameter angleichen |
| **IPv6**: Host ohne globale Adresse / kein Routing | `ipv6 unicast-routing` fehlt, falsches Präfix, falsche `ipv6 route` | `show ipv6 interface brief`, `show ipv6 route`, `ipconfig` | `ipv6 unicast-routing`, Route korrigieren |

### 8.6 Gelöste Labs aus dem Unterricht

**Lab 01 – LAB_Fehlersuche (Mathias Gut)**
- **Symptom:** Die Laptops «GL1» und «Verwaltung» können die Webseite *ifa.ch* nicht aufrufen.
- **Fehler auf R4:** Die **Default-Route fehlt** und sie wird **nicht per OSPF verteilt**.
- **Gefunden mit:** `ping` und `traceroute` (ICMP), `show run` (bzw. `show ip route`: «Gateway of last resort is not set» auf den internen Routern).
- **Behebung:**
  ```
  R4(config)# ip route 0.0.0.0 0.0.0.0 192.0.2.10
  R4(config)# router ospf 1
  R4(config-router)# default-information originate
  ```

**Lab 02 – LAB_Fehlersuche (Mathias Gut)**
- **Symptom:** Beim Laptop GL1 ist die Verbindung **nach dem Starten einige Zeit eingeschränkt**, zudem ist *www.ifa.ch* nicht erreichbar.
- **Fehler auf S11:** 1. **PortFast und BPDU Guard** nicht aktiviert, 2. Switch nicht auf **RSTP** konfiguriert, 3. **VLAN 20 fehlt** auf dem Switch.
- **Erklärung:** Mit klassischem STP braucht ein Port nach dem Link-up bis ca. 30–50 s bis Forwarding → DHCP und Anmeldung beim Start scheitern. Ein Access-Port in einem nicht existierenden VLAN ist inaktiv, und ein Trunk transportiert ein nicht angelegtes VLAN nicht.
- **Gefunden mit:** `show run`, `show vlan` (zusätzlich hilfreich: `show spanning-tree summary`, `show interfaces trunk`).
- **Behebung:**
  ```
  S11(config)# spanning-tree mode rapid-pvst
  S11(config)# interface range f0/1-20
  S11(config-if-range)# spanning-tree portfast
  S11(config-if-range)# spanning-tree bpduguard enable
  S11(config)# vlan 20
  ```

**Lab 03 – LAB_Fehlersuche (Mathias Gut)**
- **Symptom:** Der Laptop «Verwaltung» kann *ifa.ch* nicht erreichen, **alle anderen Geräte funktionieren**.
- **Fehler auf R2:** In der ACL `acl` fehlt der Eintrag für den **DNS-Zugriff** aus dem Netz 192.168.21.0/24.
- **Gefunden mit:** `ping` und `traceroute` funktionieren **bis zum Webserver** (L3 ist also ok, das Problem liegt höher → DNS/ACL), `show access-lists` (Vergleich mit den Einträgen der funktionierenden Netze).
- **Behebung:**
  ```
  R2(config)# ip access-list extended acl
  R2(config-ext-nacl)# permit udp 192.168.21.0 0.0.0.255 host 172.20.20.100 eq 53
  ```
  🔎 Falls die ACL am Ende ein explizites `deny` hat, den Eintrag mit einer tieferen Sequenznummer davor einfügen.

**Troubleshooting Fundamentals – Phase 1.3 (Witty Networks)**
- **Symptom:** Host C (an SW2) erreicht Host A und B (an SW1) nicht.
- **Vorgehen:** Problem bestätigen (Ping von C scheitert) → **Vergleichstest:** A ↔ B funktioniert → deren Ports sind ok, Problem liegt bei C, dessen Port oder dem Link SW1–SW2 → Anforderungen L1 (Geräte an, Kabel, Ports «connected») und L2 (gleiches VLAN, Inter-Switch-Link auf beiden Seiten Trunk oder beide Access im gleichen VLAN, VLAN auf dem Trunk erlaubt) prüfen.
- **Befund mit `show interfaces status`:** Alle Host-Ports sind in VLAN 10. **SW1 hat den Uplink als Trunk, SW2 als Access-Port in VLAN 1** → VLAN 10 kann den Link nicht passieren.
- **Behebung auf SW2:**
  ```
  SW2(config)# interface fa0/1
  SW2(config-if)# switchport mode trunk
  SW2# show interfaces trunk
  ```
  (Beide Seiten als Access in VLAN 10 wäre auch eine Lösung.)
- **Wichtig:** Direkt nach der Änderung kann der Ping noch scheitern, weil **STP den Port erst durch die Zustände führt** (ca. 50 s). Erst wenn VLAN 10 in der letzten Zeile «**VLANs in spanning tree forwarding state and not pruned**» erscheint, funktioniert es.

**Troubleshooting Fundamentals – Phase 1.8 (Witty Networks)**
- **Symptom:** Host A erreicht Host D (anderes Netz) nicht. (Ein Ping kann auch an ACLs scheitern!)
- **Vorgehen (Divide and Conquer ab Layer 3):** Ein erfolgreicher L3-Test bestätigt auch L1 und L2. Anforderungen: korrekte IPs, Gateways, Routen der Gateways zum Zielnetz.
  1. Host A → eigenes Gateway pingen: ok (bestätigt IP und Gateway von A).
  2. Auf RTR1 → Gateway von D pingen: scheitert → ganzes Zielnetz nicht erreichbar, nicht nur Host D.
  3. `traceroute` von RTR1: scheitert **schon am ersten Hop** (RTR2 hätte sonst «TTL exceeded» gemeldet) → RTR1 kennt das Ziel nicht oder hat eine falsche Route.
  4. `show ip route`: Route nach 192.168.2.0/24 **ist vorhanden**.
  5. Next Hop 10.1.1.4 pingen: scheitert. `show run | include ip route` → **falscher Next Hop** (richtig ist 10.1.1.2 = RTR2 im Transfernetz).
- **Behebung:**
  ```
  RTR1(config)# no ip route 192.168.2.0 255.255.255.0 10.1.1.4
  RTR1(config)# ip route 192.168.2.0 255.255.255.0 10.1.1.2
  ```
  Validieren: `traceroute` zeigt nun RTR2 als Hop, der Ping von A nach D klappt.

**Packet Tracer 1.1.3.5 – IPv4- und IPv6-Schnittstellen** (Anleitung vorhanden, Lösung hier als Vorschlag; Passwörter: User `cisco`, Enable `class`)

```
R1(config)# interface g0/0
R1(config-if)# ip address 172.16.20.1 255.255.255.128
R1(config-if)# no shutdown
R1(config)# interface g0/1
R1(config-if)# ip address 172.16.20.129 255.255.255.128
R1(config-if)# no shutdown
! PC1: 172.16.20.10/25 GW 172.16.20.1 · PC2: 172.16.20.138/25 GW 172.16.20.129

R2(config)# ipv6 unicast-routing
R2(config)# interface g0/0
R2(config-if)# ipv6 address 2001:db8:c0de:12::1/64
R2(config-if)# ipv6 address fe80::2 link-local
R2(config-if)# no shutdown
R2(config)# interface g0/1
R2(config-if)# ipv6 address 2001:db8:c0de:13::1/64
R2(config-if)# ipv6 address fe80::2 link-local      (gleiche Link-Local auf mehreren Interfaces ist erlaubt)
R2(config-if)# no shutdown
! PC3: 2001:db8:c0de:12::a/64 GW fe80::2 · PC4: 2001:db8:c0de:13::a/64 GW fe80::2
```

Weitere PT-Dateien ohne schriftliche Anleitung: `Troubleshooting_Challenge.pka` (Fehlersuch-Challenge), `02/enable_secret.pkt` (Block 2, Passwort/Recovery), die Labs 01–03 (`0X_LAB_Fehlersuche.pkt`) sowie `Phase 1.3.pka` und `Troubleshooting Fundamentals Lab - Phase 1.8.pka`. Diese nur in PT öffnen und mit dem Leitfaden oben lösen.

🔎 **PT-Hilfsmittel beim Troubleshooting:** **Simulationsmodus** (Paket Schritt für Schritt verfolgen, bei verworfenen Paketen zeigt PT den Grund an), Maus-Hover über Geräte (Interface-Status, IPs), die Link-Farben (rot = down, orange = STP blockiert/Listening), bei `.pka`-Aktivitäten **«Check Results»**.

### 8.7 Eigene Fehler-Labs erstellen (Aufgabe B7, Praxistransfer Block 7)

Lieferobjekte:
- **Ausgangslage.pkt** bzw. PT-Datei **mit Fehlern** (nur auf Cisco-Geräten; lieber mehrere einzelne Aufgaben als zu viele Fehler in einer Datei),
- **Fehlerbeschreibung.txt** (Symptom aus Benutzersicht, wie bei den Labs 01–03),
- **Lösung.txt** mit **pro Fehler:** betroffenes Gerät (z. B. R1), konkrete Fehlerbeschreibung, **Commands zur Fehlersuche**, **Commands zur Behebung**,
- PT-Datei **ohne Fehler**,
- ein kurzer **allgemeiner Leitfaden** (Vorgehensweisen zur Eingrenzung, verwendete Tools), siehe 8.1–8.3.

### 8.8 Cheat-Sheet: Prüf-Commands

**Switch (Cisco CLI)**

```
show running-config | section interface      show interfaces status
show vlan brief                              show interfaces trunk
show interfaces fa0/1 switchport             show mac address-table [interface fa0/1]
show spanning-tree [vlan X] [summary]        show spanning-tree inconsistentports
show etherchannel summary                    show vtp status
show port-security [interface fa0/1]         show interfaces status err-disabled
show ip dhcp snooping [binding]              show cdp neighbors [detail]
show ip interface brief   (SVIs, L3-Switch)  show ip route   (L3-Switch: ip routing?)
show logging                                 show version
```

**Router (Cisco CLI)**

```
show ip interface brief                      show interfaces g0/0 | s0/0/0
show controllers s0/0/0                      show running-config interface g0/0.10
show ip route [static|ospf|eigrp|bgp|0.0.0.0] show ip protocols
show ip ospf neighbor | interface brief      show ip eigrp neighbors
show ip bgp summary                          show standby brief
show access-lists                            show ip interface g0/0   (ACL in/out)
show ip nat translations | statistics        show ip dhcp binding | pool | conflict
show ipv6 interface brief                    show ipv6 route
show ipv6 ospf neighbor                      show cdp neighbors detail
ping <ip> [source <interface>]               traceroute <ip>
debug ip packet | ospf hello | nat  →  undebug all
```

🔎 **Erweiterter Ping** `ping 192.168.2.10 source g0/1` testet den **Rückweg** aus Sicht eines LAN-Netzes (ein normaler Ping vom Router nutzt die IP des Ausgangsinterfaces).

**Allgemein (Endgeräte)**

| Zweck | Windows | Linux |
|---|---|---|
| IP-Konfiguration | `ipconfig /all` | `ip addr`, `ip -6 addr` |
| DHCP erneuern | `ipconfig /release` + `/renew` | `dhclient -r` + `dhclient` |
| Routingtabelle | `route print` | `ip route` |
| ARP/Nachbarn | `arp -a` | `ip neigh` |
| Erreichbarkeit | `ping`, `tracert`, `pathping` | `ping`, `traceroute -n`, `mtr` |
| DNS | `nslookup`, `ipconfig /flushdns` | `dig`, `host`, `nslookup` |
| offene Verbindungen | `netstat -an` | `ss -tulpen`, `netstat -tulpen` |
| Port testen | `Test-NetConnection <IP> -Port 443` | `nc -vz <IP> 443`, `nmap -p 443 <IP>` |
| Paketanalyse | Wireshark | Wireshark, `tcpdump`, `tshark` |

---

<a id="praxistransfer"></a>
## 9. Praxistransfer-Aufgaben (Selbststudium)

Durchgehendes Beispiel: ein **mittelständisches Unternehmen mit mindestens 2 Standorten**, das Block für Block in PT ausgebaut wird (ca. 3 Lernstunden pro Block, 28 Lektionen Selbststudium total).

| Block | Praxistransfer |
|---|---|
| 1 | Unternehmen beschreiben (Branche, Standorte, Geräte). **Redundante 2- oder 3-Schichten-Architektur** in PT mit ≥ 2 Standorten, **Internet über den Hauptstandort**, IP-Konzept direkt im PT dokumentieren. |
| 2 | **Konzept SNMP und Konfigurationssicherung** (mit Versionskontrolle und Inhaltsverzeichnis). PT-Grundkonfiguration: Hostnamen, `no ip domain-lookup`, sicherer Zugang über Konsole und **SSH**, `enable secret` (mind. MD5), Konfiguration sichern. |
| 3 | **WLAN-Konzept** für alle Standorte: Anzahl APs (Montageort, Ausrichtung, Clients pro AP, Einsatzzweck QoS/Roaming), VLANs und SSIDs, Verschlüsselung pro SSID, Gäste-WLAN, Messverfahren, Störquellen. |
| 4 | Alle **IP-Adressen** konfigurieren, **VLANs mit VTP**. |
| 5 | **OSPF** (Area 0 genügt) mit **Default-Route über den Hauptstandort**. Zusätzlich ein IPv6-Beispiel mit **OSPFv3** inkl. Default-Route. |
| 6 | Fertig konfigurieren: **RSTP**, **NAT** beim Internetzugang, **sichere ACLs** (vor allem ins Internet). Eigene Liste der Vorgehensweise bei Störungen mit Prüf-Commands (Switch, Router, allgemein) → [Kapitel 8](#b7). |
| 7 | Eigenes **Fehler-Lab** (PT mit Fehlern, TXT mit Fehlersuche und Lösung, PT ohne Fehler) → [8.7](#b7). |
| 8 | Prüfungsvorbereitung: PT-Übungen mit Fehlern lösen, CLI-Command-Sammlung und Zusammenfassung finalisieren, Unterlagen offline bereitlegen (kein Internet!), Kugelschreiber. |

### Vorlage: Grundkonfiguration (Zusammenzug aus den Folien)

```
! ===== Router (z. B. Hauptstandort mit Internet) =====
enable
configure terminal
hostname R1
no ip domain-lookup
enable algorithm-type scrypt secret <PW>      ! falls auf älterem PT-Image nicht vorhanden: enable secret <PW>
service password-encryption
username admin privilege 15 algorithm-type scrypt secret <PW>
ip domain-name firma.local
crypto key generate rsa modulus 2048
ip ssh version 2
line console 0
 login local
 logging synchronous
 exec-timeout 10
line vty 0 4
 login local
 transport input ssh
!
interface g0/0
 no shutdown
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 ip nat inside
interface g0/0.99
 description Management
 encapsulation dot1Q 99
 ip address 192.168.99.1 255.255.255.0
interface g0/1
 description WAN
 ip address 203.0.113.2 255.255.255.252
 ip nat outside
 no shutdown
!
ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 192.168.99.10
!
ip route 0.0.0.0 0.0.0.0 203.0.113.1
router ospf 1
 router-id 1.1.1.1
 network 192.168.0.0 0.0.255.255 area 0
 passive-interface g0/1
 default-information originate
!
access-list 1 permit 192.168.0.0 0.0.255.255
ip nat inside source list 1 interface g0/1 overload
end
write

! ===== Access-Switch =====
enable
configure terminal
hostname S1
no ip domain-lookup
enable algorithm-type scrypt secret <PW>      ! Fallback: enable secret <PW>
vtp domain firma
vtp mode client
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
interface range fa0/1 - 20
 switchport mode access
 switchport access vlan 10
interface g0/1
 switchport mode trunk
interface vlan 99
 ip address 192.168.99.11 255.255.255.0
 no shutdown
ip default-gateway 192.168.99.1
interface range fa0/21 - 24
 shutdown
end
write
```

(Bei `spanning-tree portfast default` wirkt PortFast nur auf Access-Ports. SSH-Zeilen wie beim Router ergänzen.)

---

<a id="korrekturen"></a>
## 10. Korrekturen zu den Kursunterlagen

Beim Durcharbeiten gefundene Fehler und Unschärfen in den Unterlagen. In der Prüfung zählt, was in PT funktioniert.

**Cisco-Befehle**

| # | Stelle | In der Unterlage | Korrekt |
|---|---|---|---|
| 1 | NPDO ACL-Folien | `ip access-groups 1 out` | `ip access-group 1 out` |
| 2 | NPDO «Access Lists einrichten» | Standard-ACL `access-list 1 permit ip 10.0.0.0 0.0.0.255 10.1.1.10 0.0.0.255` | Standard-ACLs prüfen **nur die Quelle** und kennen kein Protokoll → Extended-ACL (100–199) verwenden. Für einen Host `host 10.1.1.10` statt `10.1.1.10 0.0.0.255`. |
| 3 | NPDO ACL-Folien | `no access-list 101 deny tcp any any eq 80` löscht «die ACL-Zeile» | Löscht die **ganze** nummerierte ACL (und müsste 100 heissen). Einzelne Zeilen: `ip access-list extended 100` → `no <Seq>`. |
| 4 | NPDO «Statisches Routing mit Metrik» | Zahl am Ende = Metrik | Das ist die **administrative Distanz** (Floating Static Route). |
| 5 | NIUS 186, NPDO 454 | `ipv6 route ::/0 2001:db8:33:1::2/64` | Next Hop ohne Präfixlänge: `ipv6 route ::/0 2001:db8:33:1::2` (NIUS 195 ist korrekt). |
| 6 | NIUS 158, NPDO 219 | `enable algorithm-type script secret` | `enable algorithm-type scrypt secret` |
| 7 | CCNA Command Guide Kap. 22 | `algorithm-type shaw256` | `algorithm-type sha256` |
| 8 | NIUS 208 | `router ospf1` | `router ospf 1` |
| 9 | NIUS 207, NPDO 397 | `R1# no run ospf` | `R1(config)# no router ospf 1` (oder `clear ip ospf process`) |
| 10 | NIUS 33 (iBGP) | R2-Block mit Prompt `R1(config-router)# neighbor 10.0.2.1 update-source loopback 0` und «R1 Lo0 = 10.0.2.2»; Loopback-Beispiel mit 1.1.1.1 | Prompt/Beschriftung R2; die Loopback-IPs müssen den `neighbor`-IPs entsprechen (10.0.2.1 / 10.0.2.2). |
| 11 | NIUS 30 (BGP-Summarisation) | nur `ip route 192.0.2.0 255.255.255.0 null0` | zusätzlich `network 192.0.2.0 mask 255.255.255.0` unter `router bgp 20` nötig. |
| 12 | NPDO 335 (PAgP) | `interface GigabitEthernet 0/1-2`; S2 `channel-group 2`, aber `interface port-channel 1` | `interface range g0/1 - 2`; Port-Channel-Nummer = Channel-Group-Nummer (`interface port-channel 2`). |
| 13 | NPDO 327 | `spanning loopguard` (global) | `spanning-tree loopguard default` (das Schlüsselwort `default` fehlt; Abkürzungen wie `spanning` akzeptiert IOS) |
| 14 | NPDO 299 (Port Security) | Befehlsliste ohne Aktivierung | Zuerst `switchport port-security` (ohne diesen Befehl ist Port Security nicht aktiv). |
| 15 | NIUS 184, NPDO 452 (IPv6 auf Switch) | `ip default-gateway 192.168.1.1` | gilt nur für IPv4; in PT auf dem 2960 zuerst `sdm prefer dual-ipv4-and-ipv6 default` + `reload`. |
| 16 | NIUS 77 | `0x2120: Boot in rommon` | Standardwert ist **0x2100**; 0x2120 ändert zusätzlich die Konsolen-Baudrate. |
| 17 | NIUS 93 (SNMP) | `snmp-server host 10.0.0.10 snmpsrv01` | Letztes Argument = Community-String; ohne `version 2c` werden v1-Traps gesendet. |
| 18 | NIUS 42/43 (PPP CHAP) | beidseitig `username USER password CISCO` | CHAP nutzt den **Hostnamen des Peers** als Benutzernamen (`username R2 …` auf R1 und umgekehrt) oder `ppp chap hostname USER`. |
| 19 | NPDO 237 (NTP) | `feature ntp`, `ntp server ch.pool.ntp.org` | `feature ntp` ist NX-OS. Hostnamen brauchen DNS, nach `no ip domain-lookup` die Server-IP verwenden. |
| 20 | NPDO 296 | `ip dhcp snooping vlan10` | `ip dhcp snooping vlan 10` |
| 21 | NPDO 428 | `show time range` | `show time-range` |

**Theorie**

| # | Stelle | In der Unterlage | Korrekt |
|---|---|---|---|
| 22 | Zusatzfolien WLAN (2016) | 802.11ad im 5-GHz-Band | **60 GHz** |
| 23 | NPDO 374 (Summarization) | 10.10.0.0/21 = 10.10.0.0 – 10.0.7.255 | **10.10.0.0 – 10.10.7.255** |
| 24 | NIUS 23, NPDO 379 | BGP als Distance-Vector-Protokoll | **Path-Vector-Protokoll** (so auch im BGP-Skript) |
| 25 | NIUS 17 (MPLS) | «Technologie wird/wurde IP over ATM genannt» | MPLS ist nicht «IP over ATM». Es hat u. a. die früheren IP-über-ATM-Overlay-Netze abgelöst. |
| 26 | NPDO 351 | VRRP = «Virtual Routing Redundancy Protocol» | **Virtual Router** Redundancy Protocol |
| 27 | NPDO 488 | Umkehrung der Kapselung heisst «Fragmentierung» | **Entkapselung** (Decapsulation); Fragmentierung ist das Aufteilen zu grosser Pakete (MTU). |
| 28 | Zusatzfolien WLAN | «5 GHz darf nur in geschlossenen Räumen verwendet werden» | gilt in CH für die Kanäle 36–64; 100–140 sind auch im Freien erlaubt (DFS Pflicht). |

**Wireshark**

| # | Stelle | In der Unterlage | Korrekt |
|---|---|---|---|
| 29 | NIUS 109 «Capture Filter» | enthält `ip.addr == …` und `not(tcp.port==80) …` | Das ist **Display-Filter**-Syntax. Capture-Filter: `host …`, `not tcp port 80`. |
| 30 | NIUS 111 | `ether.addr == 00-02-a3-bb-00-01` | `eth.addr == 00:02:a3:bb:00:01` |
| 31 | NIUS 111 | `ip.src ! = 192.168.1.1` | `ip.src != 192.168.1.1` (für «alles ausser Host»: `!(ip.addr == 192.168.1.1)`) |
| 32 | Wireshark-Skript, Kap. 8.1 | `ip.port == 80 \|\| tcp.port == 8080`; Tabelle «Inhaltssuche» mit kopierten Beschreibungen | `tcp.port == 80 \|\| tcp.port == 8080`; `http.host matches "\.ch$"` zeigt HTTP-Hosts, die auf .ch enden. |
| 33 | NIUS 102 | Filter `bootp` | seit Wireshark 3.0 `dhcp` |

---

<a id="hinweise"></a>
## 11. Hinweise zum Material und Lücken

- **MOCO:** Die NIUS-Folien von 2022 erwähnen eine gemeinsame Prüfung mit dem Fach MOCO. Im aktuellen Unterrichtsplan kommt MOCO nicht vor, es ist daher nicht Teil dieser Zusammenfassung.
- **NPDO nur teilweise übernommen:** Aus dem Vorgängermodul sind die Cisco-Themen (CLI, VLAN, VTP, STP, EtherChannel, HSRP, Routing, ACL, NAT, IPv6) sowie Netzwerkmanagement, Wireshark und die Konnektivitäts-Tools enthalten. **Nicht enthalten** ist NPDO-Block 4 (Debian-Server: Installation, feste IP, OpenSSH, BIND-DNS, isc-dhcp-server, ebenfalls LAB-markiert). Subnetting-, DHCP- und DNS-Theorie sind nur knapp als Nachschlagehilfe aufgenommen.
- **Leere Ordner:** `03`, `04`, `05`, `07`, `08` sind leer.
- **Nicht vorhanden**, obwohl in den Folien erwähnt: `LAB4.3_Packet-Retransmission.pdf`, `LAB_6.1_Wireless-Traffic.pcapng`, `07_LAB_NIUS_ENDKONFIGURATION_ACL.pkt`.
- **Packet-Tracer-Dateien** (`.pkt`/`.pka`) lassen sich nur in PT öffnen. Ausgewertet sind sie hier über die zugehörigen Anleitungen und Lösungsdateien (Labs 01–03, Phase 1.3/1.8, 1.1.3.5). Für `Troubleshooting_Challenge.pka` und `enable_secret.pkt` gibt es keine schriftliche Lösung.
- **`Loop-Absatz.loop`** ist eine Microsoft-Loop-Datei mit nur einem **leeren Absatz** (kein Inhalt).
- **`02/The Ultimate PCAP v20250325.pcapng`** (16 MB) ist ein Übungs-Mitschnitt mit sehr vielen Protokollen zum Üben der Wireshark-Filter. Er wurde hier nicht einzeln analysiert.
- **Versionsstände:** NIUS-Folien V1.2 (2022, Mathias Gut), NPDO-Folien V1.0 (2023), WLAN-Zusatzfolien von **2016** (Standards und Kanäle teils veraltet, deshalb ergänzt), BGP- und Wireshark-Skript 2026 (Andreas Cahen).
- **LAB-Symbol:** Die Markierung 🧪 wurde über das eingebettete «LAB>_»-Bild in den PDFs ermittelt. Markiert sind in NIUS u. a. BGP (eBGP), HDLC/PPP/PPPoE, curl/httping/iperf3, DNS-Abfragen (host, dig), Konfigurationsdateien, Debugging, Recovery, Passwort-Recovery, Backup, SNMPv2, CLI-Zugriff und Passwörter, Switch/Router-Grundkonfiguration, DHCP, IPv6 (Adressen, statisch, SLAAC, DHCPv6), OSPFv3, EIGRPv6, OSPF (Router-ID, passive, Default-Route, ABR), EIGRP. In NPDO zusätzlich VLAN/Trunk, RoaS, L3-Switch, VTP, DHCP Snooping, Port Security, STP, EtherChannel, HSRP, ACL, NAT und die Linux-Netzwerkbefehle.
- **Open Book:** Den **CCNA 200-301 Portable Command Guide** (Empson, im Ordner) offline mitnehmen. Er enthält zu jedem Thema die Befehle mit Erklärung (u. a. Kap. 9 VLANs, 11 STP, 12 EtherChannel, 16 OSPF, 18 NAT, 20 L2-Security, 21 ACLs, 22 Monitoring/Hardening).

---

<a id="quellen"></a>
## 12. Quellen

**Kursunterlagen (Ordner `Kursmaterialien/`)**
- Gut, Mathias: *NIUS – Networking Part 3*, Foliensatz V1.2 (18.05.2022) – `NIUS_LD2020_V1_2_SV1.pdf`
- Gut, Mathias: *NPDO – Netzwerk-Planung, -Design und -Optimierung*, Foliensatz V1.0 (29.10.2023) – `06/NPDO_LD2023_V1_0_SV1.pdf`
- Fachplan NIUS.TA1A V_I-1.0 – `NIUS.TA1A_V_I-1.0 STU.pdf`
- Gut, Mathias: *Aufgaben zum Selbststudium NIUS* V1.1 (07.01.2024)
- Aufgabenblätter B1 (WAN-Anbindung), B3 (WLAN-Planung), B7 (Fehlersuche)
- Cahen, Andreas: *Einführung in BGP* (18.04.2026) – `01/bgp.pdf`
- Cahen, Andreas: *Wireshark, eine Einführung* (19.02.2026) – `02/Wireshark_Einfuehrung.pdf`
- Zusatzfolien NIUS Block 3 WLAN (2016)
- Tutorial *Managed WiFi mit Cisco Wireless Controller*
- York, Tiffany (Witty Networks): *Troubleshooting Fundamentals Lab – Phase 1.3 / 1.8*
- Lab 01–03 `Fehlerbeschreibung.txt` / `Lösung.txt` (Mathias Gut)
- Cisco Networking Academy: *Packet Tracer 1.1.3.5 – Konfigurieren von IPv4- und IPv6-Schnittstellen*
- Empson, Scott: *CCNA 200-301 Portable Command Guide*, Cisco Press

**Online-Recherche (abgerufen am 28.09.2026)**
- BAKOM: [WLAN / RLAN](https://www.bakom.admin.ch/de/wlan-rlan), [Neue Frequenzen für Breitband-Wi-Fi](https://www.bakom.admin.ch/de/bakom/de/home/das-bakom/medieninformationen/bakom-infomailing/infomailing-58/neue-frequenzen-fur-breitbandwifi.html)
- inside-it.ch: [EU gibt Teile des 6-GHz-Spektrums für Wi-Fi frei](https://www.inside-it.ch/post/eu-gibt-teile-des-6-ghz-spektrums-fuer-wi-fi-frei-20210630)
- Elektronik-Kompendium: [WLAN-Frequenzen und WLAN-Kanäle](https://www.elektronik-kompendium.de/sites/net/1712061.htm); iWay: [Welcher WLAN-Kanal ist der beste](https://www.iway.ch/ueber-iway/blog/wlan-kanal-waehlen/)
- Cisco: [What Is Wi-Fi 7?](https://www.cisco.com/site/us/en/learn/topics/networking/what-is-wi-fi-7.html); Cisco Meraki: [Wi-Fi 7 (802.11be) Technical Guide](https://documentation.meraki.com/Wireless/Design_and_Configure/Architecture_and_Best_Practices/Wi-Fi_7_(802.11be)_Technical_Guide)
- Wi-Fi Alliance: [Security (WPA3)](https://www.wi-fi.org/discover-wi-fi/security)
- Cisco: [Understand Site Survey Guidelines for WLAN Deployment](https://www.cisco.com/c/en/us/support/docs/wireless/5500-series-wireless-controllers/116057-site-survey-guidelines-wlan-00.html)
- Cisco: [Configure DHCP Option 43 for Lightweight Access Points](https://www.cisco.com/c/en/us/support/docs/wireless-mobility/wireless-lan-wlan/97066-dhcp-option-43-00.html)
- Cisco Press: [Structured Troubleshooting Approaches](https://www.ciscopress.com/articles/article.asp?p=2273070&seqNum=2)
- Cisco: [Configuring HSRP (Nexus 3000 Guide)](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus3000/sw/unicast/503_u1_2/nexus3000_unicast_config_gd_503_u1_2/l3_hsrp.html); NetworkLessons: [HSRP](https://networklessons.com/cisco/ccie-routing-switching/hsrp-hot-standby-routing-protocol)
- NetworkLessons: [How to configure SNMPv3 on Cisco IOS Router](https://networklessons.com/system-management/how-to-configure-snmpv3-on-cisco-ios-router)
- Cisco: [BGP Best Path Selection Algorithm](https://www.cisco.com/c/en/us/support/docs/ip/border-gateway-protocol-bgp/13753-25.html); Cisco Press: [BGP Neighbor States](https://www.ciscopress.com/articles/article.asp?p=2756480&seqNum=4)
- RFC Editor: [RFC 6996 – AS Reservation for Private Use](https://www.rfc-editor.org/rfc/rfc6996.html)
- RtBrick: [MPLS Basic Concepts](https://documents.rtbrick.com/trainings/current/mpls/mpls_intro.html)
- Cisco: [Understand OSPF Neighbor States](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13685-13.html), [Troubleshoot OSPF Neighbor Problems](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13699-29.html)
- Cisco: [Understand Configuration Register Usage](https://www.cisco.com/c/en/us/support/docs/routers/10000-series-routers/50421-config-register-use.html)
- BSI: [NET.1.1 Netzarchitektur und -design (Edition 2023)](https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Grundschutz/IT-GS-Kompendium_Einzel_PDFs_2023/09_NET_Netze_und_Kommunikation/NET_1_1_Netzarchitektur_und_design_Edition_2023.pdf?__blob=publicationFile&v=3), [NET.1.2 Netzmanagement](https://www.allianz-fuer-cybersicherheit.de/SharedDocs/Downloads/DE/BSI/Grundschutz/IT-GS-Kompendium_Einzel_PDFs_2021/09_NET_Netze_und_Kommunikation/NET_1_2_Netzmanagement_Edition_2021.pdf?__blob=publicationFile&v=2)
- Wireshark Wiki: [Display Filters](https://wiki.wireshark.org/DisplayFilters)
