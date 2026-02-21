# Lösungsvorschlag: Digitale Probeklausur 2 (WS25/26)
**Modul:** BCSM302 - ISM Systeme und KRITIS
**Dozent:** Dr.-Ing. Erfan Koza

---

## Aufgabe 1: Asset-Register (12 Punkte)

**Frage:** Tragen Sie die fehlenden Informationen ein. Was beinhaltet das Asset-Register?

*Hinweis zur Lösung: Das Diagramm stellt den Informationsfluss im ISMS dar.*

*   **Oberer Kasten (Input für Register):** **Geschäftsprozesse / Inventarisierung**
    *   *Erklärung:* Assets leiten sich aus den Geschäftsprozessen ab.
*   **Mittlerer Kasten (Zentrales Element):** **Asset-Register (Asset-Inventar)**
    *   *Inhalt:* Liste aller Werte (Hard-, Software, Daten, Personen, Standorte), Asset-Owner, Klassifizierung.
*   **Rechter Kasten (Output oben - "Referenziert auf"):** **Risiken (Risikoanalyse)**
    *   *Erklärung:* Auf Basis der Assets werden Bedrohungen und Schwachstellen analysiert.
*   **Rechter Kasten (Output unten):** **Sicherheitsmaßnahmen (Controls)**
    *   *Erklärung:* Zum Schutz der Assets werden Maßnahmen definiert.

---

## Aufgabe 2: NIS2-Betroffenheit (10 Punkte)

**Frage 1:** Nach welchen Kriterien erfolgt die NIS2-Betroffenheit? Nennen Sie mindestens zwei Kriterien.

1.  **Unternehmensgröße:** Mittlere und Großunternehmen (ab 50 Mitarbeiter oder > 10 Mio. € Jahresumsatz/Bilanzsumme).
2.  **Sektor-Zugehörigkeit:** Das Unternehmen ist in einem definierten Sektor tätig (z. B. "Wesentliche Sektoren" wie Energie, Gesundheit, Verkehr oder "Wichtige Sektoren" wie Post, Abfallwirtschaft).

---

## Aufgabe 3: Dokumentenlenkung / Klassifizierung (10 Punkte)

**Frage 1:** Nennen Sie die vier in der Lehre vermittelten Klassifizierungsstufen für Informationen und Dokumente.

*(Die Nummerierung im PDF begann bei 3, hier die vollständige Liste)*

3.  **Öffentlich (Public)**
4.  **Intern (Internal)**
5.  **Vertraulich (Confidential)**
6.  **Streng Vertraulich (Strictly Confidential / Secret)**

---

## Aufgabe 4: Beziehungen im ISMS (10 Punkte)

**Frage 1:** Ordnen Sie die Begrifflichkeiten (Assets, Controls, Vulnerabilitäten, Risiken, Bedrohungen) dem Diagramm zu.

*   **Box oben links:** **Controls (Maßnahmen)**
    *   *Pfeil nach rechts:* reduzieren **Risiken**.
*   **Box unten links:** **Assets (Werte)**
    *   *Pfeil nach oben:* besitzen **Vulnerabilitäten**.
*   **Box Mitte:** **Vulnerabilitäten (Schwachstellen)**
    *   *Pfeil nach rechts:* erhöhen **Risiken**.
*   **Box unten rechts:** **Bedrohungen**
    *   *Pfeil nach links:* nutzen **Vulnerabilitäten**.
    *   *Pfeil nach oben:* erhöhen **Risiken**.
*   **Box rechts:** **Risiken**
    *   *Pfeil nach links:* verursachen Schaden an **Assets**.

---

## Aufgabe 5: Risikomanagement (22 Punkte)

### Teil a) Risikomatrix Entwurf (2 Punkte)
*Vorgabe: $R = F \times C$. Toleranzgrenze ist 4.*

**Lösung:**
Alle Felder mit einem Ergebnis **< 4** sind **Grün** (akzeptabel).
Alle Felder mit einem Ergebnis **≥ 4** sind **Gelb/Rot** (nicht akzeptabel).

| Wahrscheinlichkeit \ Auswirkung | 1 (Gering) | 2 (Mittel) | 3 (Hoch) | 4 (Kritisch) |
| :--- | :--- | :--- | :--- | :--- |
| **1** | 1 (Grün) | 2 (Grün) | 3 (Grün) | 4 (Gelb) |
| **2** | 2 (Grün) | 4 (Gelb) | 6 (Gelb) | 8 (Rot) |
| **3** | 3 (Grün) | 6 (Gelb) | 9 (Rot) | 12 (Rot) |
| **4** | 4 (Gelb) | 8 (Rot) | 12 (Rot) | 16 (Rot) |

---

### Teil b) Risikoklassen und Strategien (4 Punkte)

*Beispielhafte Einteilung basierend auf der Matrix oben:*

| Risikoklasse | Zugeordnete Werte | Zugeordnete Behandlungsstrategie |
| :--- | :--- | :--- |
| **Risikoklasse 1** (Niedrig) | Werte 1 – 3 | **Risikoakzeptanz** (Accept) |
| **Risikoklasse 2** (Mittel) | Werte 4 – 6 | **Risikoreduzierung** (Mitigate) / Risikotransfer |
| **Risikoklasse 3** (Hoch) | Werte 8 – 12 | **Risikoreduzierung** (Mitigate) / Risikovermeidung |
| **Risikoklasse 4** (Kritisch) | Wert 16 | **Risikovermeidung** (Avoid) |

---

### Teil c) Verfahrensfehler identifizieren (8 Punkte)

*Analyse der Tabelle auf Seite 7 des PDFs:*
*   *Klasse 1 (Grün): Akzeptanz*
*   *Klasse 2 (Gelb): Akzeptanz, Reduzierung, Transfer, Vermeidung*
*   *Klasse 3 (Rot): Reduzierung, Transfer*

**Fehler 1 mit Begründung:**
*   **Fehlende Option "Vermeidung" in Risikoklasse 3 (Rot).**
    *   *Begründung:* Bei der höchsten Risikoklasse (Rot) muss die Option der Risikovermeidung (Unterlassung der Aktivität) zwingend gegeben sein, falls eine Reduzierung nicht möglich ist. Es ist unlogisch, diese Option bei Klasse 2 ("Gelb") anzubieten, aber bei der kritischeren Klasse 3 wegzulassen.

**Fehler 2 mit Begründung:**
*   **Option "Risikoakzeptanz" in Risikoklasse 2 (Gelb).**
    *   *Begründung:* Risiken, die die Toleranzgrenze (hier Grün/Klasse 1) überschreiten, dürfen im Normalfall nicht ohne Weiteres akzeptiert werden ("Accept"). Für gelbe/rote Bereiche ist eine Behandlung (Reduktion/Transfer) vorzusehen. Akzeptanz ist typischerweise nur für Risiken unterhalb der Akzeptanzgrenze (Klasse 1) vorgesehen.

---

## Aufgabe 6: ISO 27001 Audit / Cloud-Sicherheit (20 Punkte)

**Szenario:**
Das Unternehmen schließt Control A.8.14 (Redundanz) aus dem SoA aus ("Nicht anwendbar"), weil die Kernsysteme in der Azure Cloud laufen und Microsoft die Verfügbarkeit via SLA regelt.

**Antwort / Bewertung:**

**Die getroffene Auswahl und Begründung im SoA ist fachlich und normativ fehlerhaft.**

**Begründung:**

1.  **Unterscheidung Anwendbarkeit vs. Implementierung:**
    Ein Control (Maßnahme) ist im *Statement of Applicability (SoA)* als **anwendbar (applicable)** zu kennzeichnen, wenn das zugehörige Risiko existiert. Das Risiko eines Systemausfalls besteht für die Stadtwerke weiterhin. Dass die Redundanz technisch durch einen Dienstleister (Microsoft Azure) erbracht wird, ist die Art der **Umsetzung**, kein Grund für den **Ausschluss**.

2.  **Verantwortung bleibt beim Unternehmen:**
    Auch bei Outsourcing in die Cloud bleibt die Organisation (der Cloud-Kunde) dafür verantwortlich, sicherzustellen, dass die Anforderungen an Verfügbarkeit erfüllt werden (siehe Kapitel 5.23 Informationssicherheit für die Nutzung von Cloud-Diensten).

3.  **Korrektes Vorgehen:**
    Das Control A.8.14 muss im SoA als **"Anwendbar: JA"** markiert werden.
    In der Spalte "Umsetzung/Begründung" muss stehen: *"Die Anforderung wird durch die Nutzung der Geo-Redundanz-Mechanismen des Cloud-Providers Microsoft Azure gemäß SLA XYZ umgesetzt."*

**Fazit:** Als Auditor ist hier eine **Abweichung (Non-Conformity)** festzustellen, da ein relevantes Sicherheitsrisiko (Verfügbarkeit) fälschlicherweise als "nicht anwendbar" deklariert wurde.