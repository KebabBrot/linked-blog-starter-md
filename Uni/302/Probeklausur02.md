# Probeklausur 02‑BCSM302_PK_-V0.1-2026 – Aufgaben mit Lösungsskizzen


## Aufgabe 1 (20 Punkte)

**Aufgabenstellung (gekürzt):**  
Sie als Informationssicherheitsbeauftragter der Stadtwerke Energy GmbH als Verteilnetzbetreiber im Gas‑ und Strombereich müssen zunächst präzisieren, in welchen Bereichen Ihr Unternehmen im Sinne der Gesetzgebung als KRITIS zu definieren ist. In einem ersten Schritt stellen Sie fest, dass Ihr Unternehmen die gesetzlichen Anforderungen nach § 11 Abs. 1a EnWG erfüllen muss.[file:1]  
Die Stadtwerke Energy GmbH besitzt zwei dedizierte Netzwerke (Büro‑Netz, Prozess‑Netz). Beide werden im eigenen Rechenzentrum betrieben, sind logisch teilweise getrennt, besitzen aber eine V‑LAN‑Schnittstelle für die Übertragung der Zählerdaten vom Prozess‑ in das Büro‑Netz.[file:1] Das Prozess‑Netz ist für Messsysteme nach § 21d EnWG zuständig und kann über Sicherheitsgateways/Proxy ins Internet gehen, damit ein externer Dienstleister per VPN/2FA administriert.[file:1] Im Büro‑Netz haben 230, im Prozess‑Netz 70 Mitarbeiter logische Zugänge.[file:1]  

**Aufgabenteil:**  
Frage 1: Lässt sich der Scope der Stadtwerke Energy GmbH in Form eines dedizierten Anwendungsbereichs, also eines gezielt abgegrenzten Geltungs‑ und Anwendungsbereichs, definieren? Argumentieren Sie Ihre Ausführungen unter Nutzung der oben vorgegebenen Textbeschreibungen. (8 Punkte)[file:1]

### Musterlösung Frage 1

Ja, der Scope kann als dedizierter Anwendungsbereich definiert werden, muss aber alle KRITIS‑relevanten Prozesse, Systeme und Schnittstellen umfassen.[file:1]

Begründung (in Sätzen formulierbar):

- Das Prozess‑Netzwerk bildet mit den Messsystemen nach § 21d EnWG den KRITIS‑relevanten Kern, da hier die für die Energieversorgung kritischen Prozesse laufen.[file:1]  
- Über die V‑LAN‑Management‑Schnittstelle werden Verbrauchsdaten in das Büro‑Netz zur Abrechnung übertragen; diese Schnittstelle ist sicherheitsrelevant und Teil des Anwendungsbereichs.[file:1]  
- Externer Zugriff über Sicherheitsgateways, Proxy und VPN mit 2FA ist für Betrieb und Sicherheit des Prozess‑Netzes wesentlich und daher im ISMS‑Scope zu berücksichtigen.[file:1]  
- Ein sachdienlicher dedizierter Scope beschreibt das ISMS für alle KRITIS‑bezogenen Prozesse im Prozess‑Net inklusive Remote‑Zugängen und der Schnittstelle zum Büro‑Netz.[file:1]  

---

**Aufgabenteil:**  
Frage 2: Welche normativen Gesichtspunkte sind bei der Implementierung eines Informationssicherheits‑Managementsystems (ISMS) für die Stadtwerke Energy GmbH zu berücksichtigen und vollständig zu erfüllen? Beziehen Sie sich in Ihrer Antwort ausdrücklich auf die Vorgaben des IT‑Sicherheitskatalogs der Bundesnetzagentur gemäß § 11 Abs. 1a EnWG. (4 Punkte)[file:1]

### Musterlösung Frage 2

- Der IT‑Sicherheitskatalog verlangt die Einführung, den Betrieb und die kontinuierliche Verbesserung eines ISMS **nach ISO/IEC 27001** als normative Grundlage.[file:1]  
- Das ISMS muss alle für den Netzbetrieb relevanten KRITIS‑Prozesse, Anlagen und Systeme der Stadtwerke Energy GmbH umfassen.[file:1]  
- Es sind ein systematisches Informationssicherheits‑Risikomanagement, die Auswahl geeigneter Controls, deren Umsetzung sowie Überwachung und Verbesserung entsprechend ISO/IEC 27001 umzusetzen.[file:1]  
- Prüf‑ und Zertifizierungsgrundlage ist ein Audit des ISMS auf Basis der ISO/IEC 27001 in der im IT‑Sicherheitskatalog angegebenen Fassung.[file:1]  

---

**Aufgabenteil:**  
Frage 4 (Scope‑Mitarbeiter‑Bestimmung): Kann die Anzahl der Mitarbeiter innerhalb des Anwendungsbereiches auf 70 reduziert werden? (8 Punkte)  
Wenn Ja: Begründen Sie Ihre Antwort gemäß Textbeschreibung.  
Wenn Nein: Begründen Sie Ihre Antwort gemäß Textbeschreibung.[file:1]

### Musterlösung Frage 4

Antwort: **Nein**, die Anzahl der Mitarbeiter im Anwendungsbereich kann nicht auf 70 reduziert werden.[file:1]

Begründung:

- Im Büro‑Netz verarbeiten 230 Mitarbeiter die aus dem Prozess‑Netz übermittelten Verbrauchsdaten für die Abrechnung; dies ist Teil der kritischen Dienstleistung.[file:1]  
- Die V‑LAN‑Schnittstelle zwischen Prozess‑ und Büro‑Netz erzeugt sicherheitsrelevante Abhängigkeiten, die im ISMS‑Scope berücksichtigt werden müssen.[file:1]  
- Der Scope muss alle Prozesse, Systeme und Personen einbeziehen, die zur KRITIS‑Dienstleistung beitragen; eine Beschränkung auf die 70 Prozess‑Netz‑Mitarbeiter blendet wesentliche Risiken aus.[file:1]  

---

## Aufgabe 2 (4 Punkte)

**Aufgabenstellung (gekürzt):**  
Abbildung 1: IT‑Sicherheitskatalog gemäß § 11 Abs. 1a Energiewirtschaftsgesetz, S. 10.[file:1]  

Frage: Nach welcher normativen Grundlage erfolgt die Prüfung des ISMS der Stadtwerke Energy GmbH? (4 Punkte)[file:1]

### Musterlösung

Die Prüfung des ISMS erfolgt auf Grundlage der **ISO/IEC 27001** in der im IT‑Sicherheitskatalog gemäß § 11 Abs. 1a EnWG referenzierten Fassung (aktuell ISO/IEC 27001:2022).[file:1]

---

## Aufgabe 3 (6 Punkte)

**Aufgabenstellung (gekürzt):**  
Die IT‑Polis GmbH ist IT‑Dienstleister für OT‑Netzwerke; ihre dedizierten Softwarelösungen werden nur in den Netzwerken der Auftraggeber betrieben.[file:1] E‑Mail‑Verkehr über öffentliche Netzwerke wird vor betrügerischen Tätigkeiten und unbefugter Offenlegung geschützt.[file:1]  
Es ist zu entscheiden, ob das Control A.14.1.2 „Sicherung von Anwendungsdiensten in öffentlichen Netzwerken“ in die Statement of Applicability aufgenommen werden muss.[file:1]

Controls – A.14.1.2  
Bezeichnung: Sicherung von Anwendungsdiensten in öffentlichen Netzwerken.[file:1]  
Maßnahme: Information, die durch Anwendungsdienste über öffentliche Netzwerke übertragen wird, ist vor betrügerischer Tätigkeit, Vertragsstreitigkeiten und unbefugter Offenlegung sowie Veränderung geschützt.[file:1]

### Musterlösung

**Einbeziehung:** Ja.[file:1]

**Begründung (SoA‑Text):**

Die IT‑Polis GmbH nutzt Anwendungsdienste wie E‑Mail‑Kommunikation über öffentliche Netzwerke zur Übertragung sensibler Informationen zu Kunden und Partnern.[file:1] Diese Informationen unterliegen einem erhöhten Schutzbedarf hinsichtlich Vertraulichkeit, Integrität und Authentizität und sind Bedrohungen wie Betrug, unbefugter Offenlegung und Veränderung ausgesetzt.[file:1] Das Control A.14.1.2 adressiert genau diese Risiken und ist aus risikobasierter Sicht zwingend relevant; daher wird es in die Statement of Applicability aufgenommen und durch geeignete technische und organisatorische Maßnahmen umgesetzt.[file:1]

---

## Aufgabe 4 (10 Punkte)

**Aufgabenstellung (gekürzt):**  
Ein Krankenhaus betreibt ein ISMS nach ISO/IEC 27001:2022.[file:1] Die interne Revision überprüft jährlich mit den Verfahren aus Kapitel 9 (interne Audits, Managementbewertung, Wirksamkeitsprüfung) die fortlaufende Angemessenheit und Wirksamkeit des ISMS.[file:1] In der internen Revision ist auch der Informationssicherheitsbeauftragte als Prüfer integriert.[file:1]  

Frage: Analysieren Sie, ob die beschriebene Vorgehensweise mit den Anforderungen der ISO/IEC 27001 (Kapitel 9.2) vereinbar ist. Begründen Sie Ihre Antwort. Gehen Sie hierbei darauf ein, welche der Grundprinzipien der IS betroffen sind. (10 Punkte)[file:1]

### Musterlösung

Die beschriebenen Verfahren (interne Audits, Managementbewertungen, Wirksamkeitsprüfungen) entsprechen grundsätzlich Kapitel 9 der ISO/IEC 27001.[file:1] Problematisch ist jedoch, dass der Informationssicherheitsbeauftragte als Prüfer in der internen Revision eingesetzt ist und damit potenziell seine eigenen Aufgaben und Maßnahmen auditieren könnte.[file:1]  

Kapitel 9.2 fordert, dass interne Audits objektiv, unparteiisch und frei von Interessenkonflikten sind; Auditoren dürfen ihr eigenes Werk nicht auditieren.[file:1] Wird der ISB als Prüfer für seine eigenen Verantwortungsbereiche eingesetzt, ist die geforderte Unabhängigkeit verletzt und damit die Integrität des Auditprozesses betroffen.[file:1]  

Die Vorgehensweise ist nur dann konform, wenn organisatorisch sichergestellt wird, dass der ISB nicht die von ihm verantworteten Prozesse und Maßnahmen prüft und die interne Revision die Trennung von Verantwortung und Kontrolle wahrt.[file:1]

---

## Aufgabe 5 (14 Punkte)

**Aufgabenstellung (gekürzt):**  
Skizzieren Sie das Phasenmodell nach ISO/IEC 27001, das zur Einführung eines ISMS operationalisiert werden kann. Füllen Sie die entsprechenden Felder aus.[file:1]

### Musterlösung (Phasenmodell)

Ein mögliches Phasenmodell (orientiert am PDCA‑Zyklus):

1. **Initiierung / Kontext & Scope**  
   - Kontext der Organisation bestimmen (interne/externe Themen, interessierte Parteien).[file:1]  
   - Anforderungen ermitteln und den Geltungsbereich des ISMS festlegen.[file:1]  

2. **Planung / Politik & Risikomanagement**  
   - Informationssicherheitspolitik und -ziele definieren.[file:1]  
   - Rollen, Verantwortlichkeiten und Ressourcen festlegen.[file:1]  
   - Verfahren und Kriterien für das Risikomanagement bestimmen.[file:1]  

3. **Risikobeurteilung**  
   - Informationswerte, Bedrohungen und Schwachstellen identifizieren.[file:1]  
   - Risiken analysieren und bewerten (Eintrittswahrscheinlichkeit, Auswirkung) und Risikokriterien anwenden.[file:1]  

4. **Risikobehandlung**  
   - Behandlungsoptionen (Akzeptanz, Minderung, Vermeidung, Transfer) festlegen.[file:1]  
   - Maßnahmen/Controls auswählen (Annex) und im Risikobehandlungsplan dokumentieren.[file:1]  
   - Statement of Applicability (SoA) erstellen/aktualisieren.[file:1]  

5. **Implementierung & Betrieb**  
   - Ausgewählte Controls und Prozesse implementieren.[file:1]  
   - Mitarbeiter schulen, Bewusstsein schaffen, operative Steuerung sicherstellen.[file:1]  
   - Notwendige dokumentierte Informationen erstellen und pflegen.[file:1]  

6. **Überwachung & Bewertung**  
   - Monitoring und Messung durchführen, interne Audits planen und durchführen.[file:1]  
   - Managementbewertung zur Beurteilung von Angemessenheit und Wirksamkeit des ISMS.[file:1]  

7. **Verbesserung**  
   - Nichtkonformitäten und Vorfälle analysieren, Korrektur‑ und Verbesserungsmaßnahmen ableiten.[file:1]  
   - Kontinuierliche Verbesserung des ISMS gemäß PDCA‑Ansatz.[file:1]  

---

## Aufgabe 6 (6 Punkte)

**Aufgabenstellung:**  
Nennen Sie drei obligatorische Informationen und Schritte, welche in einen Risikobehandlungsplan integriert werden müssen, damit der Behandlungsplan sachdienlich umgesetzt werden kann. (3 Positionen)[file:1]

### Musterlösung

Beispiel‑Nennungen:

1. Beschreibung der ausgewählten Risikobehandlungsmaßnahmen (Controls) inklusive Zuordnung zu den jeweiligen Risiken.[file:1]  
2. Festlegung von Verantwortlichkeiten (Verantwortlicher/Owner je Maßnahme) und erforderlichen Ressourcen.[file:1]  
3. Zeitplan mit Fristen und Meilensteinen sowie Kriterien/Terminen für die Wirksamkeitsüberprüfung
