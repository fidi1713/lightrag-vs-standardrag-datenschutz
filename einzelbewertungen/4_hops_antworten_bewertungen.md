# Testfragen 4 Hops: Antworten und Bewertungen

> **Bewertungsmethode:** Claude Opus 4.6 als LLM-as-Judge + manuelle Nachprüfung durch den Autor
> **Metriken:** Precision, Recall, F1 (RAGAS Factual Correctness) + Citation Accuracy
> **Bewertungsverfahren (zweistufig):**
> - Schritt 1: Referenz-Claims (F1–Fn aus Anhang) gegen Antwort prüfen → TP (1,0/0,5) oder FN
> - Schritt 2: Antwort auf zusätzliche Claims scannen → FP wenn irrelevant oder inhaltlich falsch, kein FP wenn korrekt + relevant
> **FP-Definition (Relevanzfilter):** Inhaltlich falsch → FP. Fachlich korrekt aber irrelevant → FP. Fachlich korrekt UND thematisch relevant → kein FP.
> **Konfigurationen:** B1 = Standard-RAG | B2 = LightRAG (T=0) | B3 = LightRAG (T=1)

---

## Frage 5: Microsoft 365 und Standardvertragsklauseln

### Frage
> Alfreds Futterkiste möchte Microsoft 365 für die Buchhaltung einsetzen. Sind Standardvertragsklauseln für den Datentransfer zwingend erforderlich?

### Hop-Kette

| Hop | Quelle | Erwartetes Ergebnis | Folgefrage |
|-----|--------|---------------------|------------|
| 1 | DSGVO Art. 44–49 | Drittlandtransfer nur bei Angemessenheitsbeschluss (Art. 45) oder SCCs (Art. 46) zulässig | Wer ist der Hersteller von Microsoft 365? |
| 2 | Tools | Hersteller: Microsoft Corporation | Wo sitzt Microsoft Corporation? |
| 3 | Dienstleister | Redmond, USA, EU-Hosting, DPF-zertifiziert | Welche Regelungen gelten für US-Unternehmen? |
| 4 | Länderspezifische Regelungen | DPF-Angemessenheitsbeschluss gilt für zertifizierte Unternehmen → SCCs nicht erforderlich | Schlussfolgerung |

### Erwartete Aussagen (Anhang)

| Aussage | Inhalt | Quelle |
|---------|--------|--------|
| F1 | Drittlandtransfer nur bei Angemessenheitsbeschluss (Art. 45) oder SCCs (Art. 46) zulässig | DSGVO |
| F2 | Microsoft 365 wird von Microsoft Corporation hergestellt | Tools.txt |
| F3 | Microsoft Corporation sitzt in Redmond, USA | Dienstleister.txt |
| F4 | Hosting in EU-Rechenzentrum (Niederlande/Irland) | Dienstleister.txt |
| F5 | Microsoft ist DPF-zertifiziert | Dienstleister.txt |
| F6 | Bei DPF-zertifizierten US-Unternehmen gilt der Angemessenheitsbeschluss als Rechtsgrundlage (Art. 45 DSGVO) | Länderspez. Regelungen |
| F7 | SCCs für den Datentransfer sind daher nicht zwingend erforderlich | Schlussfolgerung |
| F8 | Empfehlung: SCCs als vertragliche Absicherung beibehalten, falls Angemessenheitsbeschluss aufgehoben wird | Länderspez. Regelungen |

### Erwartete Quellen
DSGVO (Art. 44–49), Tools.txt, Länderspezifische_Datenschutzregelungen.txt

### Referenzantwort

> 1. Relevante Rechtsgrundlagen: Art. 44–49 DSGVO regeln die Übermittlung personenbezogener Daten in Drittländer. Für Datentransfers an US-Unternehmen bestehen zwei mögliche Rechtsgrundlagen: Der Angemessenheitsbeschluss für das EU-U.S. Data Privacy Framework (Art. 45 DSGVO) bei DPF-zertifizierten Unternehmen oder Standardvertragsklauseln nach Art. 46 DSGVO bei nicht zertifizierten Unternehmen. US-Unternehmen unterliegen US-Gesetzen (CLOUD Act, FISA 702), die den Zugriff auf Daten unabhängig vom Speicherort ermöglichen.
> 2. Analyse: Microsoft 365 wird von Microsoft Corporation (USA) hergestellt und in einem EU-Rechenzentrum (Niederlande/Irland) gehostet. Microsoft ist DPF-zertifiziert. Damit gilt der Angemessenheitsbeschluss der EU-Kommission als Rechtsgrundlage für den Datentransfer (Art. 45 DSGVO). Art. 46 DSGVO (SCCs) kommt nur zur Anwendung, wenn kein Angemessenheitsbeschluss vorliegt.
> 3. Handlungsempfehlung: Standardvertragsklauseln sind für den Datentransfer bei Microsoft 365 nicht zwingend erforderlich, da Microsoft DPF-zertifiziert ist und der Angemessenheitsbeschluss greift. Es wird jedoch empfohlen, SCCs als vertragliche Absicherung beizubehalten, falls der Angemessenheitsbeschluss aufgehoben wird. Die DPF-Zertifizierung ist im DPF-Register des US-Handelsministeriums zu prüfen.

---

### Antwort B1: Standard-RAG (Open WebUI, GPT-4o-mini, Temp 0.0)

**Zeitstempel:** 2026-04-04T10:08:11Z – 2026-04-04T10:08:24Z (13s gesamt)

**Antwort:**
> 1. **Relevante Rechtsgrundlagen:**
>    - Artikel 45 der Datenschutz-Grundverordnung (DSGVO) regelt die Übermittlung personenbezogener Daten in Drittländer, wobei ein Angemessenheitsbeschluss der Europäischen Kommission erforderlich ist, um sicherzustellen, dass das Datenschutzniveau im Drittland angemessen ist.
>    - Artikel 46 der DSGVO sieht vor, dass bei nicht zertifizierten Unternehmen in Drittländern geeignete Garantien, wie Standardvertragsklauseln (SCCs), erforderlich sind.
>
> 2. **Analyse:**
>    - Da Microsoft 365 in den USA gehostet wird und die USA nicht über einen Angemessenheitsbeschluss der EU verfügen, sind Standardvertragsklauseln für den Datentransfer zwingend erforderlich, um die rechtlichen Anforderungen der DSGVO zu erfüllen. Dies bedeutet, dass Alfreds Futterkiste SCCs als vertragliche Absicherung verwenden sollte, um sicherzustellen, dass die Datenübertragung rechtmäßig erfolgt [2].
>
> 3. **Handlungsempfehlung:**
>    - Alfreds Futterkiste sollte sicherstellen, dass bei der Nutzung von Microsoft 365 Standardvertragsklauseln implementiert werden. Zudem ist es ratsam, ein Transfer Impact Assessment (TIA) durchzuführen, um die Auswirkungen des Datentransfers auf den Datenschutz zu bewerten.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] Laenderspezifische_Datenschutzregelungen.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Query-Generierung via Tool-Calling | 370 (252+118) | 4s |
| 2 | Antwort-Generierung mit Chunks | 3.818 (3.464+354) | 9s |
| **Gesamt** | | **4.188** | **13s** |

**Log 1 – Query-Generierung:**
2 Suchqueries: "Standardvertragsklauseln Datentransfer Microsoft 365", "Datenschutz Microsoft 365 Standardvertragsklauseln"

**Log 2 – Retrieval-Ergebnisse:**

Query 1:

| Chunk | Quelle | Distance |
|-------|--------|----------|
| Auftragsverarbeiter können individuellen Vertrag oder SCCs verwenden | DSGVO | 0,766 |
| Vertragsklauseln zwischen Verantwortlichem und Drittland | DSGVO | 0,759 |
| SCCs als Bestandteil der Zertifizierung (Art. 42/43) | DSGVO | 0,756 |
| Erwägungsgrund 168: Durchführungsrechtsakte SCCs | DSGVO | 0,750 |
| "(Art. 45 DSGVO). Bei nicht zertifizierten US-Unternehmen sind geeignete Garantien nach Art. 46..." | Länderspez. Regelungen | 0,749 |

Kein Stammdaten-Dokument (Tools.txt) retrievt.

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Art. 45/46 Drittlandtransfer | TP | 1,0 | Art. 45 und 46 korrekt benannt und erklärt |
| F2: Microsoft Corporation | TP | 0,5 | Microsoft als US-Unternehmen identifiziert, aber nicht explizit "Microsoft Corporation hergestellt" |
| F3: Redmond, USA | FN | 0,0 | Nicht erwähnt |
| F4: EU-Hosting | FN | 0,0 | Sagt fälschlich "in den USA gehostet" → Gegenteil |
| F5: DPF-zertifiziert | FN | 0,0 | DPF nicht erwähnt |
| F6: Art. 45 bei DPF | FN | 0,0 | Sagt "USA nicht über Angemessenheitsbeschluss" → Gegenteil |
| F7: SCCs nicht zwingend | FN | 0,0 | Sagt "SCCs zwingend erforderlich" → Gegenteil |
| F8: SCCs als Empfehlung | FN | 0,0 | SCCs als Pflicht behandelt, nicht als Empfehlung |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "Microsoft 365 in den USA gehostet" | **FP** | Inhaltlich falsch: EU-Rechenzentrum (Niederlande/Irland) laut Dienstleister.txt |
| "USA nicht über einen Angemessenheitsbeschluss" | **FP** | Inhaltlich falsch: DPF-Angemessenheitsbeschluss existiert seit Juli 2023 |
| TIA empfohlen | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 1,5 | FP = 2 | FN = 6,5**
Kontrolle: TP + FN = 1,5 + 6,5 = 8,0 = 8 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,43 | 1,5/(1,5+2) = 1,5/3,5 = 0,4286 |
| Recall | 0,19 | 1,5/8,0 = 0,1875 |
| **F1** | **0,26** | 2×0,4286×0,1875/(0,4286+0,1875) = 0,1607/0,6161 = 0,2609 |
| Citation Acc. | 0,67 | 2/3 (DSGVO ✓, Länderspez. ✓, Tools ✗) |

**Befunde:**
1. Tools.txt nicht retrievt – keine Information über EU-Hosting oder DPF-Zertifizierung.
2. Zwei faktische Fehler: "in den USA gehostet" und "USA nicht über Angemessenheitsbeschluss."
3. Der retrievte Chunk aus Länderspez. Regelungen beginnt mitten im Satz – der Satz über DPF-zertifizierte Unternehmen wurde beim Chunking abgeschnitten.

---

### Antwort B2: LightRAG (T=0) (GPT-4o-mini, KG Temp 0.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-04T10:14:53Z – 2026-04-04T10:15:19Z (26s gesamt)

**Antwort:**
> ### 1. Relevante Rechtsgrundlagen
> Für den Datentransfer von personenbezogenen Daten im Rahmen der Nutzung von Microsoft 365 müssen die folgenden Artikel der DSGVO beachtet werden:
> - **Artikel 44**: Allgemeine Bedingungen für die Übermittlung an Drittländer.
> - **Artikel 45**: Übermittlung auf Grundlage eines Angemessenheitsbeschlusses.
> - **Artikel 46**: Voraussetzungen für Übermittlungen bei Abwesenheit eines Angemessenheitsbeschlusses.
> - **Artikel 28**: Bedingungen für Auftragsverarbeiter.
>
> ### 2. Analyse
> Microsoft 365 wird in einem **EU-Rechenzentrum** gehostet und hat seit dem 10. Juli 2023 eine **DPF-Zertifizierung** (EU-U.S. Data Privacy Framework). Dies bedeutet, dass für die Übermittlung personenbezogener Daten an Microsoft SCCs nur dann zwingend erforderlich sind, wenn diese Daten an ein nicht zertifiziertes US-Unternehmen übertragen werden.
>
> Da Microsoft 365 als DPF-zertifiziert gilt, ist für den Datentransfer an Microsoft keine zusätzliche Garantie, wie etwa SCCs, notwendig, solange die Daten gemäß den Bedingungen des Angemessenheitsbeschlusses verarbeitet werden.
>
> ### 3. Handlungsempfehlung
> - Der Einsatz von Microsoft 365 für die Buchhaltung ist zulässig, und es sind keine Standardvertragsklauseln erforderlich, solange das DPF-Framework als Rechtsgrundlage genutzt wird.
> - Überprüfen Sie regelmäßig die DPF-Zertifizierung von Microsoft.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] Laenderspezifische_Datenschutzregelungen.txt
- [5] Tools.txt
- [6] Dienstleister.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 703 (638+65) | 2s |
| 2 | Antwort-Generierung | 34.627 (34.029+598) | 21s |
| **Gesamt** | | **35.330** | **26s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Microsoft 365", "Buchhaltung", "Datentransfer", "Standardvertragsklauseln"
- low_level_keywords: "Alfreds Futterkiste", "Cloud-Dienste", "Datenübertragung", "Rechtliche Anforderungen"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: DSGVO, Länderspez. Regelungen, Unternehmensverzeichnis, Abteilungen, Tools, Dienstleister, Stellungnahme Thüringen, Arbeitsbereiche (alle 8 Dokumente)
- KG Entities: Alfreds Futterkiste, Microsoft, Microsoft Corporation, EU-Rechenzentrum, USA, CLOUD Act, FISA 702, SCCs, Angemessenheitsbeschluss, Artikel 45, Artikel 46, Transfer Impact Assessment
- KG Relationships: EU-Rechenzentrum → Microsoft Corporation, Angemessenheitsbeschluss → USA, SCCs → USA ("bei nicht zertifizierten US-Unternehmen"), Alfreds Futterkiste → Microsoft

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Art. 45/46 Drittlandtransfer | TP | 1,0 | Art. 44, 45, 46 korrekt benannt und differenziert |
| F2: Microsoft Corporation | TP | 1,0 | Microsoft als Auftragsverarbeiter identifiziert, Tools.txt zitiert |
| F3: Redmond, USA | TP | 0,5 | Als US-Unternehmen identifiziert, Redmond nicht explizit |
| F4: EU-Hosting | TP | 1,0 | "wird in einem EU-Rechenzentrum gehostet" |
| F5: DPF-zertifiziert | TP | 1,0 | "hat seit dem 10. Juli 2023 eine DPF-Zertifizierung" – konkret und korrekt |
| F6: Art. 45 bei DPF | TP | 1,0 | Art. 45 als Angemessenheitsbeschluss erklärt, DPF als Rechtsgrundlage |
| F7: SCCs nicht zwingend | TP | 1,0 | "keine zusätzliche Garantie, wie etwa SCCs, notwendig" |
| F8: SCCs als Empfehlung | FN | 0,0 | Nicht erwähnt – empfiehlt stattdessen "regelmäßige DPF-Prüfung" |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Art. 28 (Auftragsverarbeiter) | – | Korrekt + relevant (Microsoft verarbeitet Daten im Auftrag) → kein FP |
| Art. 44 allgemein | – | Korrekt + relevant → kein FP |
| "regelmäßig DPF-Zertifizierung überprüfen" | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 6,5 | FP = 0 | FN = 1,5**
Kontrolle: TP + FN = 6,5 + 1,5 = 8,0 = 8 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 6,5/(6,5+0) |
| Recall | 0,81 | 6,5/8,0 = 0,8125 |
| **F1** | **0,90** | 2×1,00×0,8125/(1,00+0,8125) = 1,625/1,8125 = 0,8966 |
| Citation Acc. | 1,00 | 3/3 (DSGVO ✓, Länderspez. ✓, Tools ✓) |

**Befunde:**
1. Alle erwarteten Dokumente retrievt. Insgesamt alle 8 Korpus-Dokumente im Kontext.
2. KG-Entities CLOUD Act und FISA 702 vorhanden – der Graph bildet die US-Rechtslage ab.
3. KG-Entity "SCCs" mit Relationship "bei nicht zertifizierten US-Unternehmen" – differenziert korrekt.
4. DPF-Zertifizierung klar erkannt, kein Hedging.
5. F8 (SCCs als Empfehlung) fehlt – alternative Empfehlung "regelmäßige DPF-Prüfung" stattdessen.

---

### Antwort B3: LightRAG (T=1) (GPT-4o-mini, KG Temp 1.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-08T09:44:59Z – 2026-04-08T09:45:38Z (39s gesamt)

**Antwort:**
> Art. 44-49 DSGVO regeln Datenübermittlung in Drittländer. Microsoft 365 wird in EU-Rechenzentrum gehostet und hat DPF-Zertifizierung. SCCs werden als vertragliche Absicherung benötigt wenn kein DPF vorliegt. Da Microsoft DPF-zertifiziert ist, sind SCCs nicht zwingend erforderlich. Empfehlung: Regelmäßige Überwachung der DPF-Bestimmungen.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [3] Länderspezifische_Datenschutzregelungen.txt
- [6] Tools.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 701 (638+63) | 2s |
| 2 | Antwort-Generierung | 34.594 (33.990+604) | 33s |
| **Gesamt** | | **35.295** | **35s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Microsoft 365", "Buchhaltung", "Datentransfer", "Standardvertragsklauseln"
- low_level_keywords: "Alfreds Futterkiste", "Cloud-Dienste", "Datenübertragung", "Datenschutz"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: [1] DSGVO, [2] Orientierungshilfe, [3] Länderspez. Regelungen, [4] Unternehmensverzeichnis, [5] Abteilungen, [6] Tools, [7] Dienstleister, [8] Stellungnahme Thüringen
- KG Entities: Microsoft 365 ("gehostet in EU-Rechenzentrum"), EU-U.S. DPF ("erlaubt Transfer an zertifizierte US-Unternehmen"), Standardvertragsklauseln, SCCs → TIA Relationship, USA
- KG Relationships: Buchhaltung → Microsoft 365, EU-Rechenzentrum → Microsoft 365 ("DPF-Zertifizierung"), DPF → USA ("ohne zusätzliche Garantien")

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Art. 45/46 Drittlandtransfer | TP | 1,0 | "Art. 44-49 DSGVO regeln Datenübermittlung in Drittländer" |
| F2: Microsoft Corporation | TP | 0,5 | "Microsoft" erwähnt, aber nicht "Microsoft Corporation hergestellt" |
| F3: Redmond, USA | FN | 0,0 | USA nicht explizit erwähnt |
| F4: EU-Hosting | TP | 1,0 | "EU-Rechenzentrum" |
| F5: DPF-zertifiziert | TP | 1,0 | "DPF-Zertifizierung" |
| F6: Art. 45 bei DPF | TP | 0,5 | DPF als Grundlage erklärt, aber Art. 45 nicht explizit als Angemessenheitsbeschluss benannt |
| F7: SCCs nicht zwingend | TP | 1,0 | "SCCs nicht zwingend erforderlich" |
| F8: SCCs als Empfehlung | TP | 0,5 | "SCCs werden als vertragliche Absicherung benötigt wenn kein DPF" → Konzept vorhanden, aber als allgemeine Regel formuliert statt als fallspezifische Empfehlung |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "Regelmäßige Überwachung der DPF-Bestimmungen" | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 5,5 | FP = 0 | FN = 2,5**
Kontrolle: TP + FN = 5,5 + 2,5 = 8,0 = 8 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 5,5/(5,5+0) |
| Recall | 0,69 | 5,5/8,0 = 0,6875 |
| **F1** | **0,81** | 2×1,00×0,6875/(1,00+0,6875) = 1,375/1,6875 = 0,8148 |
| Citation Acc. | 1,00 | 3/3 (DSGVO ✓, Länderspez. ✓, Tools ✓) |

**Befunde:**
1. Alle 3 erwarteten Quellen retrievt.
2. KG-Relationship Buchhaltung → Microsoft 365 vorhanden – der Graph verknüpft den Einsatzzweck.
3. Art. 45 nicht explizit als Angemessenheitsbeschluss benannt (F6=TP0,5 vs. B2 TP1,0).
4. SCCs als Absicherungskonzept vorhanden, aber als allgemeine Regel statt fallspezifische Empfehlung.

---

### Ergebnisübersicht Frage 5

| System | TP | FP | FN | P | R | F1 | CA |
|--------|----|----|----|----|----|----|-----|
| B1: Standard-RAG | 1,5 | 2 | 6,5 | 0,43 | 0,19 | **0,26** | 0,67 |
| B2: LightRAG (T=0) | 6,5 | 0 | 1,5 | 1,00 | 0,81 | **0,90** | 1,00 |
| B3: LightRAG (T=1) | 5,5 | 0 | 2,5 | 1,00 | 0,69 | **0,81** | 1,00 |

**Gewinner: LightRAG (T=0)** (F1 0,90)

---
---

## Frage 6: Datentransfer an Lebensmittellieferanten

### Frage
> Alfreds Futterkiste übermittelt Kontaktdaten an seine Lebensmittellieferanten. Sind zusätzliche Garantien für den Datentransfer erforderlich?

### Hop-Kette

| Hop | Quelle | Erwartetes Ergebnis | Folgefrage |
|-----|--------|---------------------|------------|
| 1 | DSGVO Art. 44–49 | Zusätzliche Garantien nur bei Drittlandtransfer ohne Angemessenheitsbeschluss | Wer sind die Lebensmittellieferanten? |
| 2 | Unternehmensverzeichnis | Dienstleister identifizieren | Welche davon sind Lebensmittellieferanten und wo sitzen sie? |
| 3 | Dienstleister | Exotic Liquids (London, UK), Tokyo Traders (Tokyo, Japan) | Gelten Angemessenheitsbeschlüsse? |
| 4 | Länderspezifische Regelungen | UK: Angemessenheitsbeschluss; Japan: Angemessenheitsbeschluss → keine Garantien nötig | Schlussfolgerung |

### Erwartete Aussagen (Anhang)

| Aussage | Inhalt | Quelle |
|---------|--------|--------|
| F1 | Zusätzliche Garantien (SCCs) nur bei Drittlandtransfer ohne Angemessenheitsbeschluss erforderlich (Art. 44–46 DSGVO) | DSGVO |
| F2 | Lebensmittellieferanten: Exotic Liquids (London, UK) und Tokyo Traders (Tokyo, Japan) | Unternehmensverzeichnis + Dienstleister |
| F3 | Für UK und Japan bestehen Angemessenheitsbeschlüsse der EU-Kommission | Länderspez. Regelungen |
| F4 | Zusätzliche Garantien für den Datentransfer sind nicht erforderlich | Schlussfolgerung |

### Erwartete Quellen
Unternehmensverzeichnis.txt, Dienstleister.txt, Länderspezifische_Datenschutzregelungen.txt

### Referenzantwort

> 1. Relevante Rechtsgrundlagen: Art. 44-49 DSGVO regeln die Übermittlung personenbezogener Daten in Drittländer. Datenübermittlungen in Länder mit Angemessenheitsbeschluss der EU-Kommission sind ohne zusätzliche Garantien zulässig (Art. 45 DSGVO).
> 2. Analyse: Die Lebensmittellieferanten von Alfreds Futterkiste sind Exotic Liquids mit Sitz in London, Vereinigtes Königreich, sowie Tokyo Traders mit Sitz in Tokyo, Japan. Für Datentransfers in das Vereinigte Königreich und nach Japan bestehen jeweils Angemessenheitsbeschlüsse der EU-Kommission.
> 3. Handlungsempfehlung: Zusätzliche Garantien wie Standardvertragsklauseln sind für den Datentransfer an beide Lebensmittellieferanten nicht erforderlich, da Angemessenheitsbeschlüsse bestehen.

---

### Antwort B1: Standard-RAG (Open WebUI, GPT-4o-mini, Temp 0.0)

**Zeitstempel:** 2026-04-05T10:45:41Z – 2026-04-05T10:45:50Z (8s gesamt)

**Antwort:**
> 1. **Relevante Rechtsgrundlagen:**
>    - Artikel 45 Absatz 1 der DSGVO besagt, dass personenbezogene Daten nur an ein Drittland übermittelt werden dürfen, wenn geeignete Garantien vorhanden sind, es sei denn, es liegt ein Beschluss nach Absatz 3 vor.
>    - Artikel 46 der DSGVO behandelt die geeigneten Garantien für die Übermittlung.
>
> 2. **Analyse:**
>    - In Ihrem Fall übermittelt Alfreds Futterkiste Kontaktdaten an Lebensmittellieferanten. Wenn diese Lieferanten in einem Drittland ansässig sind, das nicht über einen Angemessenheitsbeschluss der EU verfügt, sind zusätzliche Garantien erforderlich. Diese können beispielsweise Standard-Datenschutzklauseln umfassen.
>
> 3. **Handlungsempfehlung:**
>    - Alfreds Futterkiste sollte überprüfen, ob die Lebensmittellieferanten in einem Drittland ansässig sind und ob für dieses Land ein Angemessenheitsbeschluss vorliegt. Falls nicht, müssen geeignete Garantien implementiert werden.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Query-Generierung (Tool-Calling) | 3.452 (3.028+424) | 8s |
| **Gesamt** | | **3.452** | **8s** |

**Queries:** "Datentransfer Kontaktdaten Lebensmittellieferanten Datenschutz", "Zusätzliche Garantien Datentransfer Datenschutz"
Alle 20 retrievten Chunks stammen ausschließlich aus der DSGVO. Kein Stammdaten-Dokument gefunden.

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Art. 44-46 Drittlandtransfer | TP | 1,0 | Art. 45 und 46 korrekt benannt |
| F2: Exotic Liquids, Tokyo Traders | FN | 0,0 | Keine konkreten Lieferanten identifiziert |
| F3: Angemessenheitsbeschlüsse UK+Japan | FN | 0,0 | Nur allgemein "ob Angemessenheitsbeschluss vorliegt" |
| F4: Keine Garantien erforderlich | FN | 0,0 | Delegiert Prüfung an Unternehmen, keine Schlussfolgerung |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "sollte überprüfen ob Lieferanten in Drittland" | – | Korrekt + relevant → kein FP |
| Standard-Datenschutzklauseln als Beispiel | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 1,0 | FP = 0 | FN = 3,0**
Kontrolle: TP + FN = 1,0 + 3,0 = 4,0 = 4 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 1,0/(1,0+0) |
| Recall | 0,25 | 1,0/4,0 |
| **F1** | **0,40** | 2×1,00×0,25/(1,00+0,25) = 0,50/1,25 |
| Citation Acc. | 0,00 | 0/3 (Unternehmensverz. ✗, Dienstleister ✗, Länderspez. ✗) |

**Befunde:**
1. Alle 20 Chunks stammen ausschließlich aus der DSGVO – kein einziges Stammdaten-Dokument.
2. Die Suchqueries enthalten keinen unternehmensspezifischen Suchbegriff.
3. Die Antwort delegiert die Prüfung an das Unternehmen statt sie selbst durchzuführen.

---

### Antwort B2: LightRAG (T=0) (GPT-4o-mini, KG Temp 0.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-05T08:55:14Z – 2026-04-05T08:55:44Z (30s gesamt)

**Antwort:**
> ### 1. Relevante Rechtsgrundlagen
> Die Übermittlung von personenbezogenen Daten an Drittländer ist durch die DSGVO geregelt, insbesondere Artikel 44 bis 49.
> - **Artikel 44**: Datenübermittlungen in Drittländer nur zulässig wenn DSGVO-konform.
> - **Artikel 45**: Übermittlung bei Angemessenheitsbeschluss.
> - **Artikel 46**: Geeignete Garantien wenn kein Angemessenheitsbeschluss.
>
> ### 2. Analyse
> Alfreds Futterkiste übermittelt Kontaktdaten an Lebensmittellieferanten.
> - Wenn Lieferanten in Drittland ohne Angemessenheitsbeschluss → Garantien nach Art. 46 erforderlich.
> - Dazu können SCCs gehören.
>
> ### 3. Handlungsempfehlung
> Es wird empfohlen, einen Transfer Impact Assessment (TIA) durchzuführen und geeignete Garantien in Form von Standarddatenschutzklauseln zu implementieren, wenn die Lieferanten ihren Sitz in einem Drittland ohne Angemessenheitsbeschluss haben.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] Laenderspezifische_Datenschutzregelungen.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | (nicht erhoben) | – |
| 2 | Antwort-Generierung | 35.089 (34.437+652) | 30s |
| **Gesamt** | | **~35.089** | **30s** |

**Retrieval-Kontext:**
- Retrievte Dokumente: DSGVO, Länderspez. Regelungen, Orientierungshilfe, Unternehmensverzeichnis
- Nicht retrievt: Dienstleister.txt
- KG Entities: Alfreds Futterkiste, Exotic Liquids ("Lebensmittelhandel, London, UK"), Tokyo Traders ("Lebensmittelhandel, Tokyo, Japan"), Datenübermittlung, Drittland, SCCs
- KG Relationships: Alfreds Futterkiste → Exotic Liquids, Alfreds Futterkiste → Tokyo Traders, Exotic Liquids → London, Tokyo Traders → Tokyo
- Fehlende KG-Relationships: Tokyo → Japan, London → UK

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Art. 44-46 Drittlandtransfer | TP | 1,0 | Art. 44, 45, 46 korrekt benannt und differenziert |
| F2: Exotic Liquids, Tokyo Traders | FN | 0,0 | Nicht benannt – obwohl KG-Entities mit korrekten Descriptions vorhanden |
| F3: Angemessenheitsbeschlüsse UK+Japan | FN | 0,0 | Nur allgemein "wenn Angemessenheitsbeschluss vorliegt" |
| F4: Keine Garantien erforderlich | FN | 0,0 | Empfiehlt SCCs+TIA → falsche Richtung für diesen Fall |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "SCCs+TIA wenn Drittland ohne Angemessenheitsbeschluss" | – | Korrekt als Konditionalsatz + relevant → kein FP |

**Zusammenfassung: TP = 1,0 | FP = 0 | FN = 3,0**
Kontrolle: TP + FN = 1,0 + 3,0 = 4,0 = 4 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 1,0/(1,0+0) |
| Recall | 0,25 | 1,0/4,0 |
| **F1** | **0,40** | 2×1,00×0,25/(1,00+0,25) = 0,50/1,25 |
| Citation Acc. | 0,33 | 1/3 (Länderspez. ✓, Unternehmensverz. ✗, Dienstleister ✗) |

**Befunde:**
1. KG-Entities "Exotic Liquids" und "Tokyo Traders" im Kontext vorhanden mit korrekten Descriptions, aber vom LLM nicht in der Antwort verwendet.
2. KG-Relationships Exotic Liquids → London und Tokyo Traders → Tokyo vorhanden, aber London → UK und Tokyo → Japan fehlen.
3. Dienstleister.txt nicht als Chunk retrievt.
4. Die Hop-Kette bricht bei Stadt → Land ab (fehlende Graph-Beziehung).

---

### Antwort B3: LightRAG (T=1) (GPT-4o-mini, KG Temp 1.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-08T09:52:12Z – 2026-04-08T09:52:42Z (30s gesamt)

**Antwort:**
> Art. 44-49 DSGVO regeln Datenübermittlung in Drittländer. Angemessenheitsbeschluss oder geeignete Garantien erforderlich. Alfreds Futterkiste sollte prüfen, ob Lieferanten in Drittland ansässig sind. Falls Angemessenheitsbeschluss vorliegt → keine Garantien nötig. Falls nicht → SCCs erforderlich.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] Länderspezifische_Datenschutzregelungen.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 698 (637+61) | 4s |
| 2 | Antwort-Generierung | 34.573 (33.980+593) | 21s |
| **Gesamt** | | **35.271** | **25s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Datenschutz", "Datentransfer", "Lebensmittellieferanten", "Garantieanforderungen"
- low_level_keywords: "Alfreds Futterkiste", "Kontaktdaten", "Zusätzliche Garantien"

**Retrieval-Kontext:**
- Retrievte Dokumente: [1] DSGVO, [2] Länderspez. Regelungen, [3] Orientierungshilfe, [4] Unternehmensverzeichnis
- Nicht retrievt: Dienstleister.txt
- KG Entities: Exotic Liquids ("Lebensmittelhandel, London, UK"), Tokyo Traders ("Lebensmittelhandel, Tokyo, Japan"), Drittland, EU-U.S. DPF, Angemessenheitsbeschluss
- KG Relationships: Alfreds Futterkiste → Exotic Liquids, Alfreds Futterkiste → Tokyo Traders, Angemessenheitsbeschluss → USA

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Art. 44-46 Drittlandtransfer | TP | 1,0 | "Art. 44-49 DSGVO" korrekt |
| F2: Exotic Liquids, Tokyo Traders | FN | 0,0 | Nicht identifiziert, obwohl KG-Entities vorhanden |
| F3: Angemessenheitsbeschlüsse UK+Japan | FN | 0,0 | Nur allgemein "falls Angemessenheitsbeschluss" |
| F4: Keine Garantien erforderlich | TP | 0,5 | "Falls Angemessenheitsbeschluss vorliegt → keine Garantien nötig" → Konzept korrekt, aber nur als Konditionalsatz, nicht als fallspezifische Schlussfolgerung |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "sollte prüfen ob Lieferanten in Drittland" | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 1,5 | FP = 0 | FN = 2,5**
Kontrolle: TP + FN = 1,5 + 2,5 = 4,0 = 4 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 1,5/(1,5+0) |
| Recall | 0,38 | 1,5/4,0 = 0,3750 |
| **F1** | **0,55** | 2×1,00×0,375/(1,00+0,375) = 0,75/1,375 = 0,5455 |
| Citation Acc. | 0,33 | 1/3 (Länderspez. ✓, Unternehmensverz. ✗, Dienstleister ✗) |

**Befunde:**
1. KG-Entities Exotic Liquids und Tokyo Traders im Kontext vorhanden, aber nicht in der Antwort verwendet.
2. B3 formuliert die Regel korrekt als Konditional ("falls Angemessenheitsbeschluss → keine Garantien") – im Unterschied zu B2, das SCCs+TIA empfiehlt.
3. Dienstleister.txt nicht retrievt – Stadt→Land-Verknüpfung fehlt im Graph.

---

### Ergebnisübersicht Frage 6

| System | TP | FP | FN | P | R | F1 | CA |
|--------|----|----|----|----|----|----|-----|
| B1: Standard-RAG | 1,0 | 0 | 3,0 | 1,00 | 0,25 | **0,40** | 0,00 |
| B2: LightRAG (T=0) | 1,0 | 0 | 3,0 | 1,00 | 0,25 | **0,40** | 0,33 |
| B3: LightRAG (T=1) | 1,5 | 0 | 2,5 | 1,00 | 0,38 | **0,55** | 0,33 |

**Gewinner: LightRAG (T=1)** (F1 0,55)

---
---

## Gesamtübersicht 4-Hop

| Frage | System | TP | FP | FN | P | R | F1 | CA |
|-------|--------|----|----|----|----|----|----|-----|
| 5 Microsoft 365 | B1 | 1,5 | 2 | 6,5 | 0,43 | 0,19 | **0,26** | 0,67 |
| 5 Microsoft 365 | B2 | 6,5 | 0 | 1,5 | 1,00 | 0,81 | **0,90** | 1,00 |
| 5 Microsoft 365 | B3 | 5,5 | 0 | 2,5 | 1,00 | 0,69 | **0,81** | 1,00 |
| 6 Lieferanten | B1 | 1,0 | 0 | 3,0 | 1,00 | 0,25 | **0,40** | 0,00 |
| 6 Lieferanten | B2 | 1,0 | 0 | 3,0 | 1,00 | 0,25 | **0,40** | 0,33 |
| 6 Lieferanten | B3 | 1,5 | 0 | 2,5 | 1,00 | 0,38 | **0,55** | 0,33 |

### Ø 4-Hop

| System | Ø P | Ø R | Ø F1 | Ø CA |
|--------|-----|-----|------|------|
| B1: Standard-RAG | 0,71 | 0,22 | **0,33** | 0,33 |
| B2: LightRAG (T=0) | 1,00 | 0,53 | **0,65** | 0,67 |
| B3: LightRAG (T=1) | 1,00 | 0,53 | **0,68** | 0,67 |
