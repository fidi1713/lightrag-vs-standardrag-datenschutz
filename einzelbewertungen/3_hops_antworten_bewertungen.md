# Testfragen 3 Hops: Antworten und Bewertungen

> **Bewertungsmethode:** Claude Opus 4.6 als LLM-as-Judge + manuelle Nachprüfung durch den Autor
> **Metriken:** Precision, Recall, F1 (RAGAS Factual Correctness) + Citation Accuracy
> **Bewertungsverfahren (zweistufig):**
> - Schritt 1: Referenz-Claims (F1–Fn aus Anhang) gegen Antwort prüfen → TP (1,0/0,5) oder FN
> - Schritt 2: Antwort auf zusätzliche Claims scannen → FP wenn irrelevant oder inhaltlich falsch, kein FP wenn korrekt + relevant
> **FP-Definition (Relevanzfilter):** Inhaltlich falsch → FP. Fachlich korrekt aber irrelevant → FP. Fachlich korrekt UND thematisch relevant → kein FP.
> **Konfigurationen:** B1 = Standard-RAG | B2 = LightRAG (T=0) | B3 = LightRAG (T=1)

---

## Frage 3: DSFA Lagerraum

### Frage
> Alfreds Futterkiste hat zwei Bosch FLEXIDOME 8100i Kameras im Lagerraum installiert. Muss eine Datenschutz-Folgenabschätzung durchgeführt werden?

### Hop-Kette

| Hop | Quelle | Erwartetes Ergebnis | Folgefrage |
|-----|--------|---------------------|------------|
| 1 | DSGVO Art. 35 Abs. 1 | DSFA erforderlich, wenn Verarbeitung voraussichtlich hohes Risiko für Rechte und Freiheiten zur Folge hat | Was bedeutet „hohes Risiko" konkret bei Kameras? |
| 2 | DSK-Orientierungshilfe | Hohes Risiko bei Schwenk/Zoom, Personenerkennung, hoher Auflösung, Fernzugriff | Verfügt die installierte Kamera über diese Funktionen? |
| 3 | Gebäudetechnik | FLEXIDOME 8100i: PTRZ (Schwenk/Zoom), IVA Pro (Personenerkennung), Audio | Schlussfolgerung |

### Erwartete Aussagen (Anhang)

| Aussage | Inhalt | Quelle |
|---------|--------|--------|
| F1 | DSFA erforderlich bei hohem Risiko für Rechte und Freiheiten (Art. 35 Abs. 1 DSGVO) | DSGVO Art. 35 |
| F2 | Hohes Risiko bei Schwenk/Zoom, Personenerkennung, hoher Auflösung | DSK-Orientierungshilfe Kap. 3.4.3 |
| F3 | Kamera hat risikorelevante Funktionen: Schwenk/Zoom (PTRZ), Personenerkennung (IVA Pro) | Gebäudetechnik.txt |
| F4 | DSFA nach Art. 35 DSGVO ist erforderlich | Schlussfolgerung |

### Erwartete Quellen
DSGVO (Art. 35), DSK-Orientierungshilfe Videoüberwachung, Gebäudetechnik.txt

### Referenzantwort

> 1. Relevante Rechtsgrundlagen: Art. 35 Abs. 1 DSGVO verpflichtet zur Durchführung einer Datenschutz-Folgenabschätzung (DSFA), wenn eine Verarbeitung aufgrund der Art, des Umfangs, der Umstände und der Zwecke voraussichtlich ein hohes Risiko für die Rechte und Freiheiten natürlicher Personen zur Folge hat. Die DSK-Orientierungshilfe (Kap. 3.4.3) konkretisiert, dass sich ein hohes Risiko aus der Art der Datenverarbeitung ergeben kann, insbesondere bei hoher Auflösung, Fernzugriff, Zoom- und Schwenkbarkeit sowie automatisierten Erkennungsfunktionen.
> 2. Analyse: Die Bosch FLEXIDOME 8100i verfügt über PTRZ-Funktionalität (Schwenken, Neigen, Rollen, Zoomen), Intelligent Video Analytics (IVA Pro) mit Deep-Learning-basierter Personen- und Fahrzeugerkennung sowie Audio-Ein- und -Ausgang. Der Lagerraum ist ein nicht öffentlich zugänglicher Bereich. Nach der DSK-Orientierungshilfe begründen die Schwenk-/Zoomfähigkeit und die automatisierte Personenerkennung ein hohes Risiko. Nicht benötigte Funktionen wie PTRZ und Audio sind zu deaktivieren.
> 3. Handlungsempfehlung: Ja, Alfreds Futterkiste muss vor Inbetriebnahme der Kameras eine DSFA nach Art. 35 DSGVO durchführen.

---

### Antwort B1: Standard-RAG (Open WebUI, GPT-4o-mini, Temp 0.0)

**Zeitstempel:** 2026-04-04T13:31:14Z – 2026-04-04T13:31:26Z (12s gesamt)

**Antwort:**
> 1. **Relevante Rechtsgrundlagen:**
>    - Gemäß Art. 35 Abs. 3 Buchst. b der Datenschutz-Grundverordnung (DS-GVO) ist eine Datenschutz-Folgenabschätzung (DSFA) erforderlich, wenn durch die Verarbeitung, insbesondere durch neue Technologien, ein hohes Risiko für die Rechte und Freiheiten natürlicher Personen besteht. Dies gilt insbesondere, wenn besondere Kategorien personenbezogener Daten gemäß Art. 9 Abs. 1 DS-GVO verarbeitet werden.
>    - Der Verantwortliche einer Videoüberwachungsanlage muss eine DSFA durchführen, wenn die Art, der Umfang, die Umstände und die Zwecke der Verarbeitung voraussichtlich ein hohes Risiko zur Folge haben [1].
>
> 2. **Analyse:**
>    - In Ihrem Fall hat Alfreds Futterkiste zwei Bosch FLEXIDOME 8100i Kameras im Lagerraum installiert. Es ist zu prüfen, ob durch diese Kameras besondere Kategorien personenbezogener Daten verarbeitet werden oder ob die Videoüberwachung ein hohes Risiko für die Rechte und Freiheiten der betroffenen Personen darstellt.
>    - Wenn die Kameras beispielsweise in Bereichen installiert sind, in denen sensible Daten erfasst werden (z.B. in Umkleidekabinen oder Toiletten), oder wenn sie eine umfassende Überwachung des Publikums ermöglichen, könnte dies ein hohes Risiko darstellen, was eine DSFA erforderlich macht.
>
> 3. **Handlungsempfehlung:**
>    - Alfreds Futterkiste sollte eine Datenschutz-Folgenabschätzung durchführen, um die Risiken der Videoüberwachung zu bewerten. Zusammenfassend ist eine DSFA in diesem Fall wahrscheinlich erforderlich.

**Quellen:**
- [1] Orientierungshilfe Videoüberwachung durch nicht-öffentliche Stellen.pdf

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Query-Generierung via Tool-Calling | 373 (256+117) | 3s |
| 2 | Antwort-Generierung mit Chunks | 4.256 (3.720+536) | 9s |
| **Gesamt** | | **4.629** | **12s** |

**Log 1 – Query-Generierung:**
2 Suchqueries generiert:
- Query 1: "Datenschutz-Folgenabschätzung Kameras"
- Query 2: "DSFA Anforderungen"

**Log 2 – Retrieval-Ergebnisse (Chunks mit Distance-Scores):**

Query 1:

| Chunk | Quelle | Distance |
|-------|--------|----------|
| DSFA bei besonderen Kategorien (Art. 9, Art. 35 Abs. 3 lit. b) | DSK-Orientierungshilfe | 0,925 |
| Checkliste Punkt 13: DSFA durchgeführt? | DSK-Orientierungshilfe | 0,899 |
| Überschrift "Datenschutz-Folgenabschätzung" | DSGVO | 0,888 |
| DSFA bei hohem Risiko (Art. 35 Abs. 1) | DSK-Orientierungshilfe | 0,886 |
| Risikobewertung bei Videoüberwachung | DSK-Orientierungshilfe | 0,873 |

Query 2:

| Chunk | Quelle | Distance |
|-------|--------|----------|
| Allgemeine Anforderungen Aufsichtsbehörde | DSGVO | 0,751 |
| Errichtung Aufsichtsbehörde | DSGVO | 0,736 |
| DPF-Zertifizierung US-Unternehmen | Länderspez. Regelungen | 0,733 |
| Zertifizierungsverfahren Aufsichtsbehörde | DSGVO | 0,730 |
| Rechtsverbindliche Maßnahmen Aufsichtsbehörde | DSGVO | 0,727 |

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: DSFA bei hohem Risiko, Art. 35 Abs. 1 | TP | 0,5 | "hohes Risiko für die Rechte und Freiheiten natürlicher Personen" vorhanden, aber falscher Absatz: zitiert Art. 35 Abs. 3 lit. b statt Abs. 1. Konzept stimmt, rechtliche Zuordnung nicht. |
| F2: Schwenk/Zoom, Personenerkennung, hohe Auflösung | FN | 0,0 | Keine konkreten Risikokriterien der Orientierungshilfe benannt |
| F3: PTRZ, IVA Pro | FN | 0,0 | Keine Kamerafunktionen identifiziert – Gebäudetechnik.txt nicht retrievt |
| F4: DSFA erforderlich | TP | 0,5 | "wahrscheinlich erforderlich" / "sollte eine DSFA durchführen" – Hedging, keine klare Aussage |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "Art. 35 Abs. 3 Buchst. b" beschrieben als "hohes Risiko durch neue Technologien" | **FP** | Inhaltlich falsch: Art. 35(3)(b) betrifft "umfangreiche Verarbeitung besonderer Kategorien (Art. 9)", nicht hohes Risiko allgemein. Falsche Zuordnung. |
| "besondere Kategorien personenbezogener Daten gemäß Art. 9 Abs. 1" als Prüfpunkt | – | Fachlich korrekt (Art. 35(3)(b) Inhalt) + thematisch relevant → kein FP |
| "Umkleidekabinen oder Toiletten" als hypothetisches Szenario | – | Fachlich korrekt + thematisch relevant (Beispiel für sensible Bereiche) → kein FP |
| "Verantwortliche muss DSFA durchführen wenn hohes Risiko" [1] | – | Korrekt (Art. 35 Abs. 1) + relevant → kein FP |

**Zusammenfassung: TP = 1,0 | FP = 1 | FN = 3,0**
Kontrolle: TP + FN = 1,0 + 3,0 = 4,0 = 4 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,50 | 1,0/(1,0+1) |
| Recall | 0,25 | 1,0/(1,0+3,0) = 1,0/4,0 |
| **F1** | **0,33** | 2×0,50×0,25/(0,50+0,25) = 0,25/0,75 = 0,3333 |
| Citation Acc. | 0,33 | 1/3 (DSK-Orientierungshilfe ✓, Gebäudetechnik ✗, DSGVO ✗) |

**Befunde:**
1. Gebäudetechnik.txt nicht retrievt. Keine der 10 Chunks stammt aus Gebäudetechnik.txt.
2. Suchqueries enthalten kein kameraspezifisches Keyword ("Bosch FLEXIDOME 8100i" fehlt).
3. DSK-Orientierungshilfe gefunden (4 von 5 Chunks in Query 1), aber nur allgemeine DSFA-Abschnitte.
4. Query 2 liefert überwiegend irrelevante Chunks (Aufsichtsbehörde, Zertifizierung, DPF).

---

### Antwort B2: LightRAG (T=0) (GPT-4o-mini, KG Temp 0.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-04T13:04:33Z – 2026-04-04T13:04:44Z (11s gesamt)

**Antwort:**
> ### Relevante Rechtsgrundlagen
>
> Gemäß **Artikel 35** der Datenschutz-Grundverordnung (DS-GVO) ist eine Datenschutz-Folgenabschätzung (DSFA) erforderlich, wenn eine Form der Verarbeitung, insbesondere bei der Verwendung neuer Technologien, voraussichtlich ein hohes Risiko für die Rechte und Freiheiten natürlicher Personen zur Folge hat. Dies gilt insbesondere für:
> - Systematische und umfangreiche Bewertung persönlicher Aspekte natürlicher Personen.
> - Umfassende Verarbeitung besonderer Kategorien personenbezogener Daten.
> - Systematische großflächige Überwachung öffentlicher Bereiche.
>
> ### Analyse
>
> Da Alfreds Futterkiste zwei Bosch FLEXIDOME 8100i Kameras im Lagerraum installiert hat, liegt eine Form der Videoüberwachung vor. Die Kameras erfassen voraussichtlich personenbezogene Daten der Kunden, die den Lagerraum betreten. Die Videoüberwachung könnte als systematisch und umfangreich angesehen werden, insbesondere wenn sie kontinuierlich und zur Überwachung aller Kunden erfolgt.
>
> **Folgende Punkte sind entscheidend:**
> - **Hohes Risiko:** Der Lagerraum ist ein öffentlich zugänglicher Bereich, in dem eine Vielzahl von Personen identifiziert werden können.
> - **Technologie:** Die verwendeten Kameras verfügen über fortschrittliche technische Funktionen, die dazu geeignet sind, eine umfassende Datenverarbeitung vorzunehmen.
>
> ### Handlungsempfehlung
>
> Alfreds Futterkiste muss eine Datenschutz-Folgenabschätzung durchführen, bevor die videoüberwachenden Maßnahmen in Betrieb genommen werden. Zusätzlich sollten alle gesetzlich geforderten Transparenzpflichten beachtet und implementiert werden.

**Quellen:**
- [1] Orientierungshilfe Videoüberwachung durch nicht-öffentliche Stellen.pdf
- [2] Amtsblatt_EU_DSGVO.pdf
- [3] Gebaeudetechnik.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 705 (639+66) | 2s |
| 2 | Antwort-Generierung | 35.012 (34.296+716) | 5s |
| **Gesamt** | | **35.717** | **11s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Datenschutz", "Datenschutz-Folgenabschätzung", "Überwachungskameras"
- low_level_keywords: "Alfreds Futterkiste", "Bosch FLEXIDOME 8100i", "Lagerraum", "Installation", "Kameras"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: Orientierungshilfe Videoüberwachung, Amtsblatt_EU_DSGVO.pdf, Gebaeudetechnik.txt (alle 3 erwarteten Quellen)
- KG Entities (Auswahl): Bosch FLEXIDOME 8100i 4 MP – X Series (NDE-8703-RXT), Datenschutz-Folgenabschätzung, Alfreds Futterkiste, Videoüberwachung, Artikel 35, Bosch Security Systems, Optischer Zoom, Starlight X-Technologie, HDR X, IVA Pro, Zwei-Wege-Audio, Cloud-basierte Dienste
- KG Relationships (Auswahl): FLEXIDOME → Optischer Zoom (3x), FLEXIDOME → Starlight X-Technologie, FLEXIDOME → HDR X, FLEXIDOME → Video Analytics (IVA Pro), FLEXIDOME → Zwei-Wege-Audio, FLEXIDOME → Cloud-basierte Dienste, Datenschutz-Folgenabschätzung → Videoüberwachung, Art. 35 Absatz 3 → Datenschutz-Folgenabschätzung

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: DSFA bei hohem Risiko, Art. 35 Abs. 1 | TP | 1,0 | "Gemäß Artikel 35... hohes Risiko für die Rechte und Freiheiten natürlicher Personen" – korrekt, ohne falschen Absatz |
| F2: Schwenk/Zoom, Personenerkennung, hohe Auflösung | TP | 0,5 | "fortschrittliche technische Funktionen, die dazu geeignet sind, eine umfassende Datenverarbeitung vorzunehmen" → richtige Richtung, aber keine konkreten Kriterien der Orientierungshilfe benannt |
| F3: PTRZ, IVA Pro | FN | 0,0 | Nur "fortschrittliche technische Funktionen" – keine konkreten Features, obwohl Gebäudetechnik.txt retrievt und KG-Relationships vorhanden (FLEXIDOME → IVA Pro, Optischer Zoom) |
| F4: DSFA erforderlich | TP | 1,0 | "muss eine Datenschutz-Folgenabschätzung durchführen" – klar, ohne Hedging |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "Der Lagerraum ist ein öffentlich zugänglicher Bereich" | **FP** | Inhaltlich falsch: Ein Lagerraum ist kein öffentlich zugänglicher Bereich im DSGVO-Sinn. Referenzantwort bestätigt: "nicht öffentlich zugänglicher Bereich." |
| Drei DSFA-Kriterien aus Art. 35 Abs. 3 (systematische Bewertung, besondere Kategorien, Überwachung) | – | Korrekt (Art. 35 Abs. 3 lit. a–c) + relevant → kein FP |
| Transparenzpflichten beachten | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 2,5 | FP = 1 | FN = 1,5**
Kontrolle: TP + FN = 2,5 + 1,5 = 4,0 = 4 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,71 | 2,5/(2,5+1) = 2,5/3,5 = 0,7143 |
| Recall | 0,63 | 2,5/(2,5+1,5) = 2,5/4,0 = 0,6250 |
| **F1** | **0,67** | 2×0,7143×0,6250/(0,7143+0,6250) = 0,8929/1,3393 = 0,6667 |
| Citation Acc. | 1,00 | 3/3 (DSK-Orientierungshilfe ✓, Gebäudetechnik ✓, DSGVO ✓) |

**Befunde:**
1. Alle 3 erwarteten Quellen retrievt (Gebäudetechnik.txt, DSK-Orientierungshilfe, DSGVO).
2. KG-Entity "Bosch FLEXIDOME 8100i" korrekt extrahiert mit Relationships zu allen technischen Features.
3. KG-Relationships FLEXIDOME → IVA Pro und → Optischer Zoom vorhanden, aber in der Antwort nicht konkret benannt.
4. "Öffentlich zugänglicher Bereich" ist eine falsche Einschätzung des Lagerraums.

---

### Antwort B3: LightRAG (T=1) (GPT-4o-mini, KG Temp 1.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-08T09:33:19Z – 2026-04-08T09:33:57Z (38s gesamt)

**Antwort:**
> ### 1. Relevante Rechtsgrundlagen
> Gemäß Art. 35 DS-GVO ist eine DSFA durchzuführen, wenn die Verarbeitung wahrscheinlich ein hohes Risiko für die Rechte und Freiheiten natürlicher Personen zur Folge hat. Relevante Kriterien: Umfang und Art der Überwachung, Verarbeitung besonderer Kategorien personenbezogener Daten. Die Orientierungshilfe besagt, dass eine DSFA vorab durchgeführt werden muss bei neuen Technologien oder umfangreichen Überwachungsmaßnahmen.
>
> ### 2. Analyse
> Alfreds Futterkiste verwendet zwei Bosch FLEXIDOME 8100i Kameras im Lagerraum. Diese können hochauflösende Videoaufnahmen machen und eine erhebliche Menge an Daten erfassen. Eine systematische Überwachung im Lagerraum kann als umfangreiche Überwachung angesehen werden.
>
> ### 3. Handlungsempfehlung
> Alfreds Futterkiste sollte eine DSFA durchführen, bevor die Videoüberwachung aktiviert wird.

**Quellen:**
- [1] Orientierungshilfe Videoüberwachung
- [2] Gebaeudetechnik.txt
- [3] Stellungnahme MV

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 702 (639+63) | 3s |
| 2 | Antwort-Generierung | 35.678 (34.948+730) | 30s |
| **Gesamt** | | **36.380** | **33s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Datenschutz-Folgenabschätzung", "Überwachungssysteme", "Kamerainstallation"
- low_level_keywords: "Alfreds Futterkiste", "Bosch FLEXIDOME 8100i", "Lagerraum", "Datenschutz"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: [1] Orientierungshilfe, [2] Gebäudetechnik, [3] Stellungnahme MV
- KG Entities: Bosch FLEXIDOME 8100i (Fixed-Dome-Kamera), Datenschutz-Folgenabschätzung (Art. 35), Alfreds Futterkiste, Lagerräume
- KG Relationships: DSFA → Videoüberwachung, DSFA → Kameratechnik, FLEXIDOME → Technische Funktionen, FLEXIDOME → IVA Pro, FLEXIDOME → Audio, FLEXIDOME → Cloud-basierte Dienste

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: DSFA bei hohem Risiko, Art. 35 Abs. 1 | TP | 1,0 | "Gemäß Art. 35... hohes Risiko für die Rechte und Freiheiten" – korrekt |
| F2: Schwenk/Zoom, Personenerkennung, hohe Auflösung | TP | 0,5 | "hochauflösende Videoaufnahmen" + "umfangreiche Überwachungsmaßnahmen" → Richtung stimmt, aber keine konkreten Kriterien der Orientierungshilfe |
| F3: PTRZ, IVA Pro | FN | 0,0 | Nur "hochauflösende Videoaufnahmen" – keine konkreten Funktionen, obwohl Gebäudetechnik retrievt |
| F4: DSFA erforderlich | TP | 1,0 | "sollte eine DSFA durchführen" – Schlussfolgerung klar |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "neue Technologien" als DSFA-Kriterium | – | Korrekt (Art. 35 Abs. 1) + relevant → kein FP |
| "systematische Überwachung im Lagerraum" | – | Korrekt + relevant. B3 sagt NICHT "öffentlich zugänglich" (anders als B2). → kein FP |

**Zusammenfassung: TP = 2,5 | FP = 0 | FN = 1,5**
Kontrolle: TP + FN = 2,5 + 1,5 = 4,0 = 4 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 2,5/(2,5+0) |
| Recall | 0,63 | 2,5/(2,5+1,5) = 2,5/4,0 = 0,6250 |
| **F1** | **0,77** | 2×1,00×0,6250/(1,00+0,6250) = 1,25/1,625 = 0,7692 |
| Citation Acc. | 0,67 | 2/3 (Orientierungshilfe ✓, Gebäudetechnik ✓, DSGVO ✗) |

**Befunde:**
1. 2 von 3 erwarteten Quellen retrievt (Gebäudetechnik, Orientierungshilfe). DSGVO nicht direkt als Quelle zitiert.
2. KG-Relationships FLEXIDOME → IVA Pro und → Audio vorhanden, aber nicht konkret in Antwort benannt.
3. Kein FP – im Unterschied zu B2 keine falsche Einschätzung des Lagerraums.

---

### Ergebnisübersicht Frage 3

| System | TP | FP | FN | P | R | F1 | CA |
|--------|----|----|----|----|----|----|-----|
| B1: Standard-RAG | 1,0 | 1 | 3,0 | 0,50 | 0,25 | **0,33** | 0,33 |
| B2: LightRAG (T=0) | 2,5 | 1 | 1,5 | 0,71 | 0,63 | **0,67** | 1,00 |
| B3: LightRAG (T=1) | 2,5 | 0 | 1,5 | 1,00 | 0,63 | **0,77** | 0,67 |

**Gewinner: LightRAG (T=1)** (F1 0,77)

---
---

## Frage 4: Speicherfristen Personalabteilung

### Frage
> Welche personenbezogenen Daten verarbeitet Alfreds Futterkiste in der Personalabteilung und wie lange dürfen diese gespeichert werden?

### Hop-Kette

| Hop | Quelle | Erwartetes Ergebnis | Folgefrage |
|-----|--------|---------------------|------------|
| 1 | Abteilungen | Personalabteilung von Alfreds Futterkiste umfasst die Arbeitsbereiche Recruiting und Lohnabrechnung | Welche Daten werden in diesen Bereichen verarbeitet? |
| 2 | Arbeitsbereiche | Recruiting: Bewerbermanagement, Stellenausschreibungen, Bewerberkommunikation; Lohnabrechnung: Gehaltsabrechnung, Sozialversicherungsmeldungen, Lohnsteueranmeldung | Wie lange dürfen diese Daten gespeichert werden? |
| 3 | Aufbewahrungsfristen | Bewerbungsunterlagen: 6 Monate nach Abschluss des Auswahlverfahrens; Lohnunterlagen: 6 Jahre | Schlussfolgerung |

### Erwartete Aussagen (Anhang)

| Aussage | Inhalt | Quelle |
|---------|--------|--------|
| F1 | Personalabteilung umfasst Recruiting und Lohnabrechnung | Abteilungen.txt |
| F2 | Recruiting verarbeitet Bewerbermanagement und Bewerberkommunikation | Arbeitsbereiche.txt |
| F3 | Lohnabrechnung verarbeitet Gehaltsabrechnungen und Sozialversicherungsmeldungen | Arbeitsbereiche.txt |
| F4 | Bewerbungsunterlagen: 6 Monate nach Abschluss des Auswahlverfahrens | Aufbewahrungsfristen.txt |
| F5 | Lohnunterlagen und Entgeltabrechnungen: 6 Jahre | Aufbewahrungsfristen.txt |

### Erwartete Quellen
Abteilungen.txt, Arbeitsbereiche.txt, Aufbewahrungsfristen.txt

### Referenzantwort

> 1. Relevante Rechtsgrundlagen: Art. 5 Abs. 1 lit. e DSGVO legt den Grundsatz der Speicherbegrenzung fest. Art. 17 Abs. 1 DSGVO verpflichtet zur Löschung, sobald der Zweck entfällt. Die konkreten Aufbewahrungsfristen ergeben sich aus arbeitsrechtlichen Vorschriften (§ 15 Abs. 4 AGG, § 61b ArbGG) und steuerrechtlichen Vorschriften.
> 2. Analyse: Die Personalabteilung von Alfreds Futterkiste umfasst die Arbeitsbereiche Recruiting und Lohnabrechnung. Im Recruiting werden Bewerberdaten verarbeitet (Bewerbermanagement, Stellenausschreibungen, Bewerberkommunikation). In der Lohnabrechnung werden Gehaltsabrechnungen, Sozialversicherungsmeldungen und Lohnsteueranmeldungen verarbeitet. Bewerbungsunterlagen dürfen nach Abschluss des Auswahlverfahrens maximal 6 Monate gespeichert werden. Lohnunterlagen und Entgeltabrechnungen sind 6 Jahre aufzubewahren.
> 3. Handlungsempfehlung: Alfreds Futterkiste muss die Speicherfristen pro Datenart einhalten. Bewerbungsunterlagen sind spätestens 6 Monate nach Abschluss des Auswahlverfahrens zu löschen. Bei Rücknahme einer Bewerbung ist unverzüglich zu löschen. Lohnunterlagen sind 6 Jahre aufzubewahren und danach zu löschen.

---

### Antwort B1: Standard-RAG (Open WebUI, GPT-4o-mini, Temp 0.0)

**Antwort:**
> 1. **Relevante Rechtsgrundlagen:**
>    - Art. 6 DSGVO: Rechtmäßigkeit der Verarbeitung
>    - Art. 13 DSGVO: Informationspflichten
>    - Art. 17 DSGVO: Recht auf Löschung
>    - Art. 5 DSGVO: Zweckbindung und Speicherbegrenzung
>
> 2. **Analyse:**
>    - Personalabteilung verarbeitet: Kontaktdaten, Identifikationsdaten, Beschäftigungsdaten, ggf. Gesundheitsdaten.
>    - Maximale Speicherdauer beträgt 72 Stunden (aus Stellungnahmen zur Videobeobachtung).
>
> 3. **Handlungsempfehlung:**
>    - Speicherdauer auf 72 Stunden begrenzen, es sei denn rechtliche Gründe für längere Speicherung.

**Quellen:**
- [2] Stellungnahmen Videoüberwachung
- [3] Stellungnahmen Videoüberwachung

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Personal → Recruiting + Lohnabrechnung | FN | 0,0 | Nur allgemein "Personalabteilung", keine Arbeitsbereiche |
| F2: Recruiting → Bewerbermanagement | FN | 0,0 | Nicht erwähnt |
| F3: Lohnabrechnung → Gehaltsabrechnungen | FN | 0,0 | Nur allgemein "Beschäftigungsdaten" |
| F4: Bewerbungsunterlagen 6 Monate | FN | 0,0 | Nicht erwähnt |
| F5: Lohnunterlagen 6 Jahre | FN | 0,0 | Nicht erwähnt |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "Maximale Speicherdauer 72 Stunden" | **FP** | Inhaltlich falsch: 72h gilt für Videoaufzeichnungen (Stellungnahmen), nicht für Personaldaten. Schwerwiegender Kontextfehler durch falsches Retrieval. |
| Art. 6, Art. 13, Art. 17, Art. 5 als Rechtsgrundlagen | – | Korrekt + relevant (Datenschutzgrundsätze) → kein FP |
| "Kontaktdaten, Identifikationsdaten, Beschäftigungsdaten, Gesundheitsdaten" | – | Allgemeine Kategorien, fachlich korrekt + relevant → kein FP |

**Zusammenfassung: TP = 0 | FP = 1 | FN = 5**
Kontrolle: TP + FN = 0 + 5 = 5 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,00 | 0/(0+1) |
| Recall | 0,00 | 0/(0+5) |
| **F1** | **0,00** | TP=0 → F1=0,0 |
| Citation Acc. | 0,00 | 0/3 (Abteilungen ✗, Arbeitsbereiche ✗, Aufbewahrungsfristen ✗) |

**Befunde:**
1. Kein einziges relevantes Stammdaten-Dokument retrievt (weder Abteilungen, Arbeitsbereiche noch Aufbewahrungsfristen).
2. Stellungnahmen zur Videoüberwachung als Quellen – 72-Stunden-Frist für Videoaufzeichnungen fälschlich auf Personaldaten angewendet.
3. Schwerwiegender Kontextfehler durch falsches Retrieval.

---

### Antwort B2: LightRAG (T=0) (GPT-4o-mini, KG Temp 0.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-08T10:41:16Z – 2026-04-08T10:41:41Z (25s gesamt)

**Antwort:**
> Art. 5 Abs. 1 lit. e DSGVO: Speicherbegrenzung. Datenminimierung. Personalabteilung verarbeitet: Identitätsdaten, Arbeitsvertragliche Daten, Gesundheitsdaten. Speicherdauer variabel, abhängig von rechtlichen Anforderungen. Empfehlung: Regelmäßige Überprüfung und Löschung.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [3] Abteilungen.txt

**Nicht retrievt:** Arbeitsbereiche.txt, Aufbewahrungsfristen.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 687 (629+58) | 2s |
| 2 | Antwort-Generierung | 35.754 (35.211+543) | 19s |
| **Gesamt** | | **36.441** | **21s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Personenbezogene Daten", "Personalabteilung", "Speicherdauer"
- low_level_keywords: "Alfreds Futterkiste", "Datenverarbeitung", "Datenschutz", "Aufbewahrungsfrist"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: [1] DSGVO, [2] Unternehmensverzeichnis, [3] Abteilungen, [4] Stellungnahme Thüringen, [5] Stellungnahme NRW, [6] Stellungnahme BW
- Nicht retrievt: Arbeitsbereiche.txt, Aufbewahrungsfristen.txt
- KG Entities: Gesetzliche Aufbewahrungsfristen, Steuerrechtliche Aufbewahrungsfristen, Arbeitsrechtliche Aufbewahrungsfristen, Handelsrechtliche Aufbewahrungsfristen, Speicherbegrenzung, Datenminimierung, 72 Stunden

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Personal → Recruiting + Lohnabrechnung | FN | 0,0 | Nur allgemein "Personalabteilung" |
| F2: Recruiting → Bewerbermanagement | FN | 0,0 | Nicht erwähnt |
| F3: Lohnabrechnung → Gehaltsabrechnungen | TP | 0,5 | "Arbeitsvertragliche Daten" → konzeptionell in Richtung Lohnabrechnung, aber vage und nicht dokumentenbasiert |
| F4: Bewerbungsunterlagen 6 Monate | FN | 0,0 | Nicht erwähnt |
| F5: Lohnunterlagen 6 Jahre | FN | 0,0 | Keine konkrete Frist |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "Speicherdauer variabel, abhängig von rechtlichen Anforderungen" | – | Korrekt + relevant → kein FP |
| "Identitätsdaten, Arbeitsvertragliche Daten, Gesundheitsdaten" | – | Allgemein, fachlich korrekt + relevant → kein FP |
| "Regelmäßige Überprüfung und Löschung" | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 0,5 | FP = 0 | FN = 4,5**
Kontrolle: TP + FN = 0,5 + 4,5 = 5,0 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 0,5/(0,5+0) |
| Recall | 0,10 | 0,5/(0,5+4,5) = 0,5/5,0 |
| **F1** | **0,18** | 2×1,00×0,10/(1,00+0,10) = 0,20/1,10 = 0,1818 |
| Citation Acc. | 0,33 | 1/3 (Abteilungen ✓, Arbeitsbereiche ✗, Aufbewahrungsfristen ✗) |

**Befunde:**
1. Abteilungen.txt retrievt, aber Arbeitsbereiche.txt und Aufbewahrungsfristen.txt fehlen.
2. KG kennt Aufbewahrungsfristen-Entities (steuerrechtlich, arbeitsrechtlich) als allgemeine Konzepte, aber ohne konkrete Fristen.
3. "Arbeitsvertragliche Daten" als einziger partieller Treffer.

---

### Antwort B3: LightRAG (T=1) (GPT-4o-mini, KG Temp 1.0, Antwort Temp 0.0)

**Antwort:**
> ### Relevante Rechtsgrundlagen
> - Art. 5 Abs. 1 lit. e DS-GVO: Speicherbegrenzung
> - Art. 88 DS-GVO: Verarbeitung im Beschäftigungskontext
>
> ### Analyse
> In der Personalabteilung werden verarbeitet:
> - Bewerbungsunterlagen: Lebensläufe, Anschreiben, Zeugniskopien
> - Mitarbeiterdaten: Kontaktdaten, Sozialversicherungsnummern, Bankverbindungen, Arbeitsverträge, Lohnabrechnungen
>
> Speicherfristen:
> - Bewerbungsunterlagen: 6 Monate nach Abschluss des Auswahlverfahrens (AGG)
> - Mitarbeiterdaten: Dauer des Arbeitsverhältnisses + bis zu 10 Jahren (Steuerrecht)
>
> ### Handlungsempfehlung
> Regelmäßige Überprüfung und Löschung nach Fristablauf.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] Orientierungshilfe Videoüberwachung (irrelevant)
- [3] Unternehmensverzeichnis.txt
- [4] Abteilungen.txt

**Nicht retrievt:** Arbeitsbereiche.txt, Aufbewahrungsfristen.txt

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Personal → Recruiting + Lohnabrechnung | TP | 0,5 | "Bewerbungsunterlagen" und "Mitarbeiterdaten/Lohnabrechnungen" → impliziert Arbeitsbereiche, benennt sie aber nicht explizit als "Recruiting" und "Lohnabrechnung" |
| F2: Recruiting → Bewerbermanagement | TP | 0,5 | "Bewerbungsunterlagen: Lebensläufe, Anschreiben, Zeugniskopien" → richtiger Bereich, aber nicht die konkreten Verarbeitungstätigkeiten (Bewerbermanagement, Bewerberkommunikation) |
| F3: Lohnabrechnung → Gehaltsabrechnungen, SV-Meldungen | TP | 0,5 | "Lohnabrechnungen" + "Sozialversicherungsnummern" → teilweise, aber aus LLM-Vorwissen (SV-Nummern ≠ SV-Meldungen) |
| F4: Bewerbungsunterlagen 6 Monate | TP | 1,0 | "6 Monate nach Abschluss des Auswahlverfahrens (AGG)" – korrekt und konkret |
| F5: Lohnunterlagen 6 Jahre | TP | 0,5 | "bis zu 10 Jahren (Steuerrecht)" statt 6 Jahre – fachlich korrekt als Allgemeinwissen (§ 147 AO), aber dokumentenspezifische Angabe ist 6 Jahre |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Art. 5 Abs. 1 lit. e Speicherbegrenzung | – | Korrekt + relevant → kein FP |
| Art. 88 Beschäftigungskontext | – | Korrekt + relevant → kein FP |
| "Lebensläufe, Anschreiben, Zeugniskopien" | – | Korrekt + relevant (Konkretisierung) → kein FP |
| "Kontaktdaten, SV-Nummern, Bankverbindungen, Arbeitsverträge" | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 3,0 | FP = 0 | FN = 2,0**
Kontrolle: TP + FN = 3,0 + 2,0 = 5,0 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 3,0/(3,0+0) |
| Recall | 0,60 | 3,0/(3,0+2,0) = 3,0/5,0 |
| **F1** | **0,75** | 2×1,00×0,60/(1,00+0,60) = 1,20/1,60 = 0,7500 |
| Citation Acc. | 0,33 | 1/3 (Abteilungen ✓, Arbeitsbereiche ✗, Aufbewahrungsfristen ✗) |

**Befunde:**
1. Weder Arbeitsbereiche.txt noch Aufbewahrungsfristen.txt retrievt – die Fristen stammen aus LLM-Vorwissen.
2. "6 Monate Bewerbung (AGG)" korrekt aus Vorwissen.
3. "10 Jahre Steuerrecht" weicht von dokumentenspezifischer Angabe "6 Jahre" ab.
4. Die inhaltlich korrekte Tendenz maskiert das Retrieval-Defizit.

---

### Ergebnisübersicht Frage 4

| System | TP | FP | FN | P | R | F1 | CA |
|--------|----|----|----|----|----|----|-----|
| B1: Standard-RAG | 0 | 1 | 5 | 0,00 | 0,00 | **0,00** | 0,00 |
| B2: LightRAG (T=0) | 0,5 | 0 | 4,5 | 1,00 | 0,10 | **0,18** | 0,33 |
| B3: LightRAG (T=1) | 3,0 | 0 | 2,0 | 1,00 | 0,60 | **0,75** | 0,33 |

**Gewinner: LightRAG (T=1)** (F1 0,75)

---
---

## Gesamtübersicht 3-Hop

| Frage | System | TP | FP | FN | P | R | F1 | CA |
|-------|--------|----|----|----|----|----|----|-----|
| 3 DSFA | B1 | 1,0 | 1 | 3,0 | 0,50 | 0,25 | **0,33** | 0,33 |
| 3 DSFA | B2 | 2,5 | 1 | 1,5 | 0,71 | 0,63 | **0,67** | 1,00 |
| 3 DSFA | B3 | 2,5 | 0 | 1,5 | 1,00 | 0,63 | **0,77** | 0,67 |
| 4 Speicherfristen | B1 | 0 | 1 | 5 | 0,00 | 0,00 | **0,00** | 0,00 |
| 4 Speicherfristen | B2 | 0,5 | 0 | 4,5 | 1,00 | 0,10 | **0,18** | 0,33 |
| 4 Speicherfristen | B3 | 3,0 | 0 | 2,0 | 1,00 | 0,60 | **0,75** | 0,33 |

### Ø 3-Hop

| System | Ø P | Ø R | Ø F1 | Ø CA |
|--------|-----|-----|------|------|
| B1: Standard-RAG | 0,25 | 0,13 | **0,17** | 0,17 |
| B2: LightRAG (T=0) | 0,86 | 0,36 | **0,42** | 0,67 |
| B3: LightRAG (T=1) | 1,00 | 0,61 | **0,76** | 0,50 |
