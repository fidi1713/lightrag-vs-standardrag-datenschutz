# Testfragen 5 Hops: Antworten und Bewertungen

> **Bewertungsmethode:** Claude Opus 4.6 als LLM-as-Judge + manuelle Nachprüfung durch den Autor
> **Metriken:** Precision, Recall, F1 (RAGAS Factual Correctness) + Citation Accuracy
> **Bewertungsverfahren (zweistufig):**
> - Schritt 1: Referenz-Claims (F1–Fn aus Anhang) gegen Antwort prüfen → TP (1,0/0,5) oder FN
> - Schritt 2: Antwort auf zusätzliche Claims scannen → FP wenn irrelevant oder inhaltlich falsch, kein FP wenn korrekt + relevant
> **FP-Definition (Relevanzfilter):** Inhaltlich falsch → FP. Fachlich korrekt aber irrelevant → FP. Fachlich korrekt UND thematisch relevant → kein FP.
> **Konfigurationen:** B1 = Standard-RAG | B2 = LightRAG (T=0) | B3 = LightRAG (T=1)

---

## Frage 7: Drittlandtransfer Personalabteilung Hotel Sonnenberg

### Frage
> Liegt bei den IT-Systemen der Personalabteilung von Hotel Sonnenberg ein Drittlandtransfer vor?

### Hop-Kette

| Hop | Quelle | Erwartetes Ergebnis | Folgefrage |
|-----|--------|---------------------|------------|
| 1 | Abteilungen | Personalabteilung umfasst Recruiting und Lohnabrechnung | Welche Tools? |
| 2 | Arbeitsbereiche | Recruiting nutzt Personio, Lohnabrechnung nutzt DATEV | Wer stellt her? |
| 3 | Tools | Personio: Personio GmbH; DATEV: DATEV eG | Wo sitzen sie? |
| 4 | Dienstleister | Personio GmbH: München, DE; DATEV eG: Nürnberg, DE | Drittland? |
| 5 | Länderspezifische Regelungen | Deutschland = EU → kein Drittlandtransfer | Schlussfolgerung |

### Erwartete Aussagen (Anhang)

| Aussage | Inhalt | Quelle |
|---------|--------|--------|
| F1 | Personalabteilung hat Arbeitsbereiche Recruiting und Lohnabrechnung | Abteilungen.txt |
| F2 | Recruiting nutzt Personio, Lohnabrechnung nutzt DATEV | Arbeitsbereiche.txt |
| F3 | Personio GmbH sitzt in München, Deutschland | Dienstleister.txt |
| F4 | DATEV eG sitzt in Nürnberg, Deutschland | Dienstleister.txt |
| F5 | Deutschland = EU/EWR → kein Drittlandtransfer | Länderspez. Regelungen |

### Erwartete Quellen
Abteilungen, Arbeitsbereiche, Tools, Dienstleister, Länderspezifische_Datenschutzregelungen

### Referenzantwort

> 1. Relevante Rechtsgrundlagen: Datenübermittlungen innerhalb der EU gelten nicht als Drittlandtransfer und sind ohne zusätzliche Garantien zulässig. Bei Übermittlungen in Drittländer außerhalb der EU sind zusätzliche Maßnahmen erforderlich.
> 2. Analyse: Die Personalabteilung von Hotel Sonnenberg umfasst die Arbeitsbereiche Recruiting und Lohnabrechnung. Im Recruiting wird Personio eingesetzt (Personio GmbH, München). Für die Lohnabrechnung wird DATEV genutzt (DATEV eG, Nürnberg). Beide Dienstleister sitzen in Deutschland.
> 3. Handlungsempfehlung: Nein, bei den IT-Systemen der Personalabteilung von Hotel Sonnenberg liegt kein Drittlandtransfer vor. Zusätzliche Garantien nach Art. 46 DSGVO sind nicht erforderlich.

---

### Antwort B1: Standard-RAG (Open WebUI, GPT-4o-mini, Temp 0.0)

**Zeitstempel:** 2026-04-06T10:32:08Z – 2026-04-06T10:32:16Z (8s gesamt)

**Antwort:**
> 1. **Relevante Rechtsgrundlagen:**
>    - Der Angemessenheitsbeschluss der EU-Kommission für das EU-U.S. Data Privacy Framework (DPF) seit dem 10. Juli 2023 erlaubt den Transfer personenbezogener Daten aus der EU an zertifizierte US-Unternehmen ohne weitere Garantien [1].
>    - US-Unternehmen unterliegen jedoch US-Gesetzen (wie dem CLOUD Act und FISA 702), die den Zugriff auf Daten unabhängig vom Speicherort ermöglichen [1].
>
> 2. **Analyse:**
>    - Wenn die IT-Systeme der Personalabteilung von Hotel Sonnenberg personenbezogene Daten an ein US-Unternehmen übermitteln oder von einem solchen Unternehmen gehostet werden, könnte ein Drittlandtransfer vorliegen.
>    - Sollte Hotel Sonnenberg Daten an ein US-Unternehmen übermitteln, das nicht zertifiziert ist oder nicht unter das DPF fällt, wäre dies ein klarer Verstoß gegen die Datenschutzbestimmungen der EU.
>
> 3. **Handlungsempfehlung:**
>    - Hotel Sonnenberg sollte sicherstellen, dass alle IT-Systeme entweder in der EU gehostet werden oder dass sie mit einem zertifizierten US-Unternehmen arbeiten, das unter das DPF fällt.

**Quellen:**
- [1] Länderspezifische_Datenschutzregelungen.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Query-Generierung via Tool-Calling | 294 (243+51) | 1s |
| 2 | Antwort-Generierung mit Chunks | 2.090 (1.636+454) | 7s |
| **Gesamt** | | **2.384** | **8s** |

**Log 1 – Query-Generierung:**
1 Suchquery: "Drittlandtransfer"

**Log 2 – Retrieval-Ergebnisse:**

| Chunk | Quelle | Distance |
|-------|--------|----------|
| DPF-Angemessenheitsbeschluss | Länderspez. Regelungen | 0,749 |
| "Drittinteresse" (falscher Match) | Orientierungshilfe | 0,741 |
| Übermittlung an Drittländer | DSGVO | 0,710 |
| USA: CLOUD Act, FISA 702 | Länderspez. Regelungen | 0,709 |
| "Abschnitt 3" | DSGVO | 0,695 |

Kein Organisationsdokument retrievt (weder Abteilungen, Arbeitsbereiche, Tools noch Dienstleister).

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Personal → Recruiting + Lohnabrechnung | FN | 0,0 | Nicht erwähnt |
| F2: Recruiting→Personio, Lohn→DATEV | FN | 0,0 | Nicht erwähnt |
| F3: Personio GmbH München, DE | FN | 0,0 | Nicht erwähnt |
| F4: DATEV eG Nürnberg, DE | FN | 0,0 | Nicht erwähnt |
| F5: DE = EU → kein Drittlandtransfer | FN | 0,0 | Keine Schlussfolgerung – nur "sollte sicherstellen" |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| DPF-Angemessenheitsbeschluss erklärt | – | Korrekt + relevant → kein FP |
| CLOUD Act, FISA 702 | – | Korrekt + relevant → kein FP |
| "klarer Verstoß gegen die Datenschutzbestimmungen der EU" bei nicht-zertifiziertem US-Unternehmen | **FP** | Inhaltlich falsch: Art. 46 DSGVO bietet legale Alternativen (SCCs). Ein Transfer an nicht-DPF-zertifizierte Unternehmen ist kein "klarer Verstoß", sondern erfordert zusätzliche Garantien. |

**Zusammenfassung: TP = 0 | FP = 1 | FN = 5**
Kontrolle: TP + FN = 0 + 5 = 5 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,00 | 0/(0+1) |
| Recall | 0,00 | 0/(0+5) |
| **F1** | **0,00** | TP=0 → F1=0,0 |
| Citation Acc. | 0,20 | 1/5 (Länderspez. ✓, Abteilungen ✗, Arbeitsbereiche ✗, Tools ✗, Dienstleister ✗) |

**Befunde:**
1. Kein einziges Organisationsdokument retrievt. Nur Länderspez. Regelungen und DSGVO.
2. Nur 1 Suchquery ("Drittlandtransfer") – kein unternehmensspezifischer Suchbegriff.
3. Die Antwort ist reine DSGVO-Theorie ohne Fallbezug.

---

### Antwort B2: LightRAG (T=0) (GPT-4o-mini, KG Temp 0.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-06T09:17:07Z – 2026-04-06T09:17:37Z (30s gesamt)

**Antwort:**
> ### 1. Relevante Rechtsgrundlagen
> Laut Artikel 44 DSGVO dürfen personenbezogene Daten nur dann an Drittländer übermittelt werden, wenn geeignete Garantien bestehen.
>
> ### 2. Analyse des konkreten Falls
> Hotel Sonnenberg nutzt verschiedene Dienstleister für seine IT-Systeme:
> - **Cloudbeds Inc.** ist ein Dienstleister mit Sitz in den USA. Es gibt keinen Hinweis auf DPF-Zertifizierung → Drittlandtransfer, angemessene Garantien erforderlich.
> - **Andere Dienstleister** wie Personio GmbH, SAP SE, DATEV eG und Resmio GmbH befinden sich alle in Deutschland (EU) und unterliegen der DSGVO → keinen Drittlandtransfer.
>
> ### 3. Handlungsempfehlung
> Hotel Sonnenberg sollte sicherstellen, dass für jegliche Datenübermittlung an Cloudbeds Inc. geeignete Garantien existieren (SCCs, TIA).

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [4] Tools.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 675 (626+49) | 2s |
| 2 | Antwort-Generierung | 34.454 (33.872+582) | 23s |
| **Gesamt** | | **35.129** | **30s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "IT-Systeme", "Personalabteilung", "Drittlandtransfer"
- low_level_keywords: "Hotel Sonnenberg", "Gesetzgebung", "Datenschutz", "IT-Infrastruktur"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: DSGVO, Länderspez. Regelungen, Unternehmensverzeichnis, Tools, Dienstleister, Abteilungen, Orientierungshilfe
- Nicht retrievt: Arbeitsbereiche.txt
- KG Entities: Hotel Sonnenberg, Personal ("Recruiting und Lohnabrechnung"), Cloudbeds Inc., Personio GmbH, DATEV eG, SAP SE, Resmio GmbH
- KG Relationships: Hotel Sonnenberg → Personal ("Recruiting und Lohnabrechnung")
- Fehlende KG-Relationships: ❌ Recruiting → Personio, ❌ Lohnabrechnung → DATEV

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Personal → Recruiting + Lohnabrechnung | FN | 0,0 | Nicht als Arbeitsbereiche der Personalabteilung identifiziert |
| F2: Recruiting→Personio, Lohn→DATEV | TP | 0,5 | Personio und DATEV als EU-Dienstleister erwähnt, aber nicht der Personalabteilung zugeordnet – als Teil aller Hotel-Sonnenberg-Dienstleister gelistet |
| F3: Personio GmbH München, DE | TP | 0,5 | "in Deutschland (EU)" → Land korrekt, München nicht erwähnt |
| F4: DATEV eG Nürnberg, DE | TP | 0,5 | "in Deutschland (EU)" → Land korrekt, Nürnberg nicht erwähnt |
| F5: DE = EU → kein Drittlandtransfer | TP | 0,5 | "keinen Drittlandtransfer" für DE-basierte Dienstleister → korrekte Schlussfolgerung, aber nicht Personalabteilung-spezifisch |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Cloudbeds als Drittlandtransfer-Risiko | **FP** | Cloudbeds wird im Reservierungsmanagement (Rezeption) eingesetzt, nicht in der Personalabteilung. Falsche Abteilungszuordnung. |

**Zusammenfassung: TP = 2,0 | FP = 1 | FN = 3,0**
Kontrolle: TP + FN = 2,0 + 3,0 = 5,0 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,67 | 2,0/(2,0+1) = 2,0/3,0 = 0,6667 |
| Recall | 0,40 | 2,0/5,0 |
| **F1** | **0,50** | 2×0,6667×0,40/(0,6667+0,40) = 0,5333/1,0667 = 0,5000 |
| Citation Acc. | 0,20 | 1/5 (Tools ✓, Abteilungen ✗, Arbeitsbereiche ✗, Dienstleister ✗, Länderspez. ✗) |

**Befunde:**
1. KG-Relationship "Hotel Sonnenberg → Personal: Recruiting und Lohnabrechnung" vorhanden, aber nicht in der Antwort genutzt.
2. Fehlende KG-Relationships Recruiting → Personio und Lohnabrechnung → DATEV verhindern korrekte Abteilungszuordnung.
3. Das System listet ALLE Dienstleister statt nur die der Personalabteilung.
4. Cloudbeds wird fälschlich als relevant für die Personalabteilung dargestellt.

---

### Antwort B3: LightRAG (T=1) (GPT-4o-mini, KG Temp 1.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-08T09:56:49Z – 2026-04-08T09:57:20Z (31s gesamt)

**Antwort:**
> Art. 44 ff. DSGVO regeln Datenübermittlung in Drittstaaten. Hotel Sonnenberg arbeitet mit Microsoft 365 (DPF-zertifiziert, EU-Hosting) und Cloudbeds Inc. (USA, kein DPF). Da Cloudbeds keine DPF-Zertifizierung besitzt → Drittlandtransfer liegt vor. Empfehlung: SCCs + TIA mit Cloudbeds.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] Länderspezifische_Datenschutzregelungen.txt
- [5] Dienstleister.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 676 (626+50) | 3s |
| 2 | Antwort-Generierung | 35.970 (35.203+767) | 24s |
| **Gesamt** | | **36.646** | **27s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "IT-Systeme", "Personalabteilung", "Drittlandtransfer"
- low_level_keywords: "Hotel Sonnenberg", "Datenschutz", "Datenübertragung", "Gesetzgebung"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: [1] DSGVO, [2] Länderspez. Regelungen, [3] Unternehmensverzeichnis, [4] Tools, [5] Dienstleister, [6] Abteilungen, [7] Orientierungshilfe
- Nicht retrievt: Arbeitsbereiche.txt
- KG Entities: Hotel Sonnenberg, Personal ("Recruiting und Lohnabrechnung"), Cloudbeds Inc., DATEV eG, Resmio GmbH
- Fehlende KG-Relationships: ❌ Recruiting → Personio, ❌ Lohnabrechnung → DATEV, ❌ Rezeption → Cloudbeds

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Personal → Recruiting + Lohnabrechnung | FN | 0,0 | Nicht identifiziert |
| F2: Recruiting→Personio, Lohn→DATEV | FN | 0,0 | Personio und DATEV nicht als Tools der Personalabteilung erkannt |
| F3: Personio GmbH München, DE | FN | 0,0 | Nicht erwähnt |
| F4: DATEV eG Nürnberg, DE | FN | 0,0 | Nicht erwähnt |
| F5: DE = EU → kein Drittlandtransfer | FN | 0,0 | Keine Schlussfolgerung für Personal-Tools |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Cloudbeds als relevant für Personalabteilung | **FP** | Cloudbeds gehört zur Rezeption, nicht zur Personalabteilung |
| Microsoft 365 als relevant für Personalabteilung | **FP** | Microsoft 365 wird in der Buchhaltung eingesetzt, nicht im Personal |

**Zusammenfassung: TP = 0 | FP = 2 | FN = 5**
Kontrolle: TP + FN = 0 + 5 = 5 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,00 | 0/(0+2) |
| Recall | 0,00 | 0/(0+5) |
| **F1** | **0,00** | TP=0 → F1=0,0 |
| Citation Acc. | 0,40 | 2/5 (Länderspez. ✓, Dienstleister ✓, Abteilungen ✗, Arbeitsbereiche ✗, Tools ✗) |

**Befunde:**
1. KG-Entities und -Relationships nahezu identisch mit B2, aber B3 benennt Personio/DATEV nicht.
2. Cloudbeds und Microsoft 365 werden fälschlich der Personalabteilung zugeordnet.
3. Fehlende KG-Relationships Recruiting → Personio und Lohnabrechnung → DATEV verhindern korrekte Zuordnung (wie bei B2).

---

### Ergebnisübersicht Frage 7

| System | TP | FP | FN | P | R | F1 | CA |
|--------|----|----|----|----|----|----|-----|
| B1: Standard-RAG | 0 | 1 | 5 | 0,00 | 0,00 | **0,00** | 0,20 |
| B2: LightRAG (T=0) | 2,0 | 1 | 3,0 | 0,67 | 0,40 | **0,50** | 0,20 |
| B3: LightRAG (T=1) | 0 | 2 | 5 | 0,00 | 0,00 | **0,00** | 0,40 |

**Gewinner: LightRAG (T=0)** (F1 0,50)

---
---

## Frage 8: Drittlandtransfer Rezeption Hotel Sonnenberg

### Frage
> Liegt bei den IT-Systemen der Rezeption von Hotel Sonnenberg ein Drittlandtransfer vor?

### Hop-Kette

| Hop | Quelle | Erwartetes Ergebnis | Folgefrage |
|-----|--------|---------------------|------------|
| 1 | Abteilungen | Rezeption umfasst Gästeempfang und Reservierungsmanagement | Welche Tools? |
| 2 | Arbeitsbereiche | Gästeempfang nutzt SAP Business One, Reservierungsmanagement nutzt Cloudbeds | Wer stellt her? |
| 3 | Tools | SAP Business One: SAP SE; Cloudbeds: Cloudbeds Inc. | Wo sitzen sie? |
| 4 | Dienstleister | SAP SE: Walldorf, DE; Cloudbeds Inc.: San Diego, USA, keine DPF-Zertifizierung | Welche Regelungen? |
| 5 | Länderspezifische Regelungen | DE = EU, kein Drittland; USA ohne DPF: SCCs + TIA erforderlich | Schlussfolgerung |

### Erwartete Aussagen (Anhang)

| Aussage | Inhalt | Quelle |
|---------|--------|--------|
| F1 | Rezeption umfasst Gästeempfang und Reservierungsmanagement | Abteilungen.txt |
| F2 | Gästeempfang nutzt SAP Business One, Reservierungsmanagement nutzt Cloudbeds | Arbeitsbereiche.txt |
| F3 | SAP SE sitzt in Walldorf, Deutschland → kein Drittlandtransfer | Dienstleister.txt + Länderspez. |
| F4 | Cloudbeds Inc. sitzt in San Diego, USA, keine DPF-Zertifizierung → Drittlandtransfer | Dienstleister.txt |
| F5 | Bei nicht DPF-zertifizierten US-Unternehmen: SCCs nach Art. 46 DSGVO + TIA erforderlich | Länderspez. Regelungen |

### Erwartete Quellen
Abteilungen, Arbeitsbereiche, Tools, Dienstleister, Länderspezifische_Datenschutzregelungen

### Referenzantwort

> 1. Relevante Rechtsgrundlagen: Datenübermittlungen innerhalb der EU gelten nicht als Drittlandtransfer. Ohne DPF-Zertifizierung des empfangenden US-Unternehmens sind SCCs nach Art. 46 DSGVO erforderlich, ergänzt um ein TIA.
> 2. Analyse: Die Rezeption umfasst Gästeempfang und Reservierungsmanagement. Im Reservierungsmanagement wird Cloudbeds eingesetzt (Cloudbeds Inc., San Diego, USA, Hosting USA). Cloudbeds ist nicht DPF-zertifiziert – Drittlandtransfer liegt vor. Im Gästeempfang wird SAP Business One eingesetzt (SAP SE, Walldorf, DE) – kein Drittlandtransfer.
> 3. Handlungsempfehlung: Ja, bei Cloudbeds liegt ein Drittlandtransfer vor. SCCs + TIA erforderlich. Für SAP Business One kein Handlungsbedarf.

---

### Antwort B1: Standard-RAG (Open WebUI, GPT-4o-mini, Temp 0.0)

**Zeitstempel:** 2026-04-06T10:29:38Z – 2026-04-06T10:29:48Z (10s gesamt)

**Antwort:**
> 1. **Relevante Rechtsgrundlagen:**
>    - Art. 44 DSGVO regelt die Übermittlung personenbezogener Daten in Drittländer.
>    - US-Unternehmen wie Cloudbeds Inc. unterliegen US-Gesetzen (CLOUD Act, FISA 702), die den Zugriff auf Daten unabhängig vom Speicherort ermöglichen [4].
>
> 2. **Analyse:**
>    - Hotel Sonnenberg nutzt IT-Systeme von Cloudbeds Inc. mit Sitz in den USA [5]. Da die USA kein mit der DSGVO vergleichbares Datenschutzniveau haben, liegt bei Cloudbeds ein Drittlandtransfer vor. Dies gilt auch bei EU-Hosting [4].
>
> 3. **Handlungsempfehlung:**
>    - Hotel Sonnenberg sollte sicherstellen, dass bei der Nutzung von Cloudbeds Inc. geeignete Maßnahmen (z.B. Standardvertragsklauseln) implementiert sind.

**Quellen:**
- [4] Länderspezifische_Datenschutzregelungen.txt
- [5] Dienstleister.txt (Cloudbeds Inc.)

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Query-Generierung via Tool-Calling | 299 (242+57) | 2s |
| 2 | Antwort-Generierung mit Chunks | 2.069 (1.592+477) | 8s |
| **Gesamt** | | **2.368** | **10s** |

**Log 1 – Query-Generierung:**
1 Suchquery: "Drittlandtransfer IT-Systeme Hotel Sonnenberg"

**Log 2 – Retrieval-Ergebnisse:**

| Chunk | Quelle | Distance |
|-------|--------|----------|
| Hotel Sonnenberg (alle Dienstleister) | Unternehmensverzeichnis | 0,789 |
| Hotel Sonnenberg Personal (falsche Abteilung!) | Abteilungen | 0,773 |
| DATEV (DE-Hosting) | Tools | 0,712 |
| USA: CLOUD Act, FISA 702 | Länderspez. Regelungen | 0,705 |
| Cloudbeds Inc., San Diego, USA | Dienstleister | 0,701 |

Standard-RAG findet Cloudbeds über semantische Nähe "Hotel Sonnenberg ↔ Hotellerie", nicht über die 5-Hop-Kette.

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Rezeption → Gästeempfang + Reservierungsmanagement | FN | 0,0 | Nicht identifiziert; Abteilungen.txt liefert Personal statt Rezeption |
| F2: Gästeempfang→SAP, Reservierung→Cloudbeds | TP | 0,5 | Cloudbeds identifiziert, aber nicht über Reservierungsmanagement; SAP nicht erwähnt |
| F3: SAP DE → kein Drittlandtransfer | FN | 0,0 | SAP nicht erwähnt |
| F4: Cloudbeds USA, kein DPF → Drittlandtransfer | TP | 0,5 | Cloudbeds USA ✓, Drittlandtransfer ✓, aber DPF-Status nicht explizit geprüft |
| F5: SCCs + TIA erforderlich | TP | 0,5 | "Standardvertragsklauseln" erwähnt, TIA fehlt |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| CLOUD Act, FISA 702 | – | Korrekt + relevant → kein FP |
| "Dies gilt auch bei EU-Hosting" | – | Korrekt (US-Gesetze gelten unabhängig vom Hosting) + relevant → kein FP |

**Zusammenfassung: TP = 1,5 | FP = 0 | FN = 3,5**
Kontrolle: TP + FN = 1,5 + 3,5 = 5,0 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 1,5/(1,5+0) |
| Recall | 0,30 | 1,5/5,0 |
| **F1** | **0,46** | 2×1,00×0,30/(1,00+0,30) = 0,60/1,30 = 0,4615 |
| Citation Acc. | 0,40 | 2/5 (Länderspez. ✓, Dienstleister ✓, Abteilungen ✗, Arbeitsbereiche ✗, Tools ✗) |

**Befunde:**
1. Cloudbeds über semantische Nähe "Hotel Sonnenberg ↔ Hotellerie" gefunden – nicht über Hop-Kette.
2. Abteilungen.txt liefert den falschen Abschnitt (Personal statt Rezeption).
3. DPF-Prüfung fehlt, obwohl Tools.txt teilweise retrievt wurde (nur DATEV-Chunk, nicht Cloudbeds-Chunk).

---

### Antwort B2: LightRAG (T=0) (GPT-4o-mini, KG Temp 0.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-06T10:12:41Z – 2026-04-06T10:13:23Z (42s gesamt)

**Antwort:**
> ### 1. Relevante Rechtsgrundlagen
> - **Artikel 44** DSGVO: Übermittlung an Drittländer.
> - **Artikel 45** DSGVO: Angemessenheitsbeschluss.
> - **Artikel 46** DSGVO: Geeignete Garantien.
>
> ### 2. Analyse
> Hotel Sonnenberg nutzt Cloudbeds Inc. als Softwareanbieter für das Reservierungsmanagement, mit Sitz in den USA. Cloudbeds hat keine DPF-Zertifizierung, was bedeutet, dass ein Drittlandtransfer ohne zusätzliche Garantien nicht zulässig ist. Um einen rechtmäßigen Datenfluss in die USA zu gewährleisten, wären SCCs erforderlich. Hotel Sonnenberg müsste geeignete Garantien implementieren und ein Transfer Impact Assessment (TIA) durchführen.
>
> ### 3. Handlungsempfehlung
> - Vertragliche Absicherung mit Cloudbeds durch EU-Standardvertragsklauseln (SCCs).
> - Transfer Impact Assessment (TIA) durchführen.
> - Regelmäßige Überprüfungen der Datenschutzstandards der IT-Dienstleister.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [3] Länderspezifische_Datenschutzregelungen.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 676 (625+51) | 2s |
| 2 | Antwort-Generierung | 34.444 (33.618+826) | 36s |
| **Gesamt** | | **35.120** | **42s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "IT-Systeme", "Rezeption", "Drittlandtransfer", "Hotel Sonnenberg"
- low_level_keywords: "Hotel", "IT-Systeme der Rezeption", "Drittlandtransfer"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: DSGVO, Orientierungshilfe, Länderspez. Regelungen, Unternehmensverzeichnis, Tools, Dienstleister, Abteilungen
- Nicht retrievt: Arbeitsbereiche.txt
- KG Entities: Rezeption ("Gästeempfang und Reservierungsmanagement"), Cloudbeds ("Tool im Reservierungsmanagement"), SAP Business One ("Tool im Gästeempfang"), Cloudbeds Inc. ("USA, Software/Hotellerie")
- KG Relationships: Hotel Sonnenberg → Rezeption ✓, Cloudbeds → Reservierungsmanagement ✓, Gästeempfang → SAP Business One ✓, Cloudbeds → DPF: "Cloudbeds hat keine DPF-Zertifizierung" ✓

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Rezeption → Gästeempfang + Reservierungsmanagement | TP | 0,5 | "Reservierungsmanagement" erwähnt, "Gästeempfang" nicht explizit als Arbeitsbereich benannt |
| F2: Gästeempfang→SAP, Reservierung→Cloudbeds | TP | 0,5 | "Cloudbeds Inc. als Softwareanbieter für das Reservierungsmanagement" ✓, SAP für Gästeempfang nicht erwähnt |
| F3: SAP DE → kein Drittlandtransfer | FN | 0,0 | SAP nicht erwähnt – Antwort fokussiert nur auf Cloudbeds |
| F4: Cloudbeds USA, kein DPF → Drittlandtransfer | TP | 1,0 | "Cloudbeds Inc., USA, keine DPF-Zertifizierung, Drittlandtransfer" – korrekt und vollständig |
| F5: SCCs + TIA erforderlich | TP | 1,0 | "SCCs erforderlich" + "Transfer Impact Assessment (TIA) durchführen" – beides explizit |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Art. 44, 45, 46 als Rechtsgrundlagen | – | Korrekt + relevant → kein FP |
| "Regelmäßige Überprüfungen der Datenschutzstandards" | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 3,0 | FP = 0 | FN = 2,0**
Kontrolle: TP + FN = 3,0 + 2,0 = 5,0 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 3,0/(3,0+0) |
| Recall | 0,60 | 3,0/5,0 |
| **F1** | **0,75** | 2×1,00×0,60/(1,00+0,60) = 1,20/1,60 = 0,7500 |
| Citation Acc. | 0,20 | 1/5 (Länderspez. ✓, Abteilungen ✗, Arbeitsbereiche ✗, Tools ✗, Dienstleister ✗) |

**Befunde:**
1. KG-Relationships für Rezeption vollständig vorhanden: Cloudbeds → Reservierungsmanagement, Gästeempfang → SAP Business One, Cloudbeds → DPF: Nein.
2. Cloudbeds korrekt der Rezeption zugeordnet (anders als bei Frage 7, wo Cloudbeds fälschlich der Personalabteilung zugeordnet wurde).
3. SAP Business One nicht erwähnt, obwohl KG-Relationship "Gästeempfang → SAP Business One" vorhanden.
4. Das LLM priorisiert das Drittlandtransfer-relevante Tool (Cloudbeds) und ignoriert das unproblematische (SAP).

---

### Antwort B3: LightRAG (T=1) (GPT-4o-mini, KG Temp 1.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-08T10:04:15Z – 2026-04-08T10:05:02Z (47s gesamt)

**Antwort:**
> Art. 44-49 DSGVO regeln Datenübermittlung in Drittländer. Hotel Sonnenberg (Österreich) nutzt Microsoft 365 (EU-Hosting, DPF-zertifiziert → kein Drittland), Google LLC (USA, DPF-zertifiziert), Cloudbeds Inc. (USA, kein DPF → Drittlandtransfer). Empfehlung: SCCs mit Cloudbeds, Dokumentation nach Art. 30.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [3] Länderspezifische_Datenschutzregelungen.txt
- [4] Unternehmensverzeichnis.txt
- [5] Tools.txt
- [6] Dienstleister.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 659 (625+34) | 2s |
| 2 | Antwort-Generierung | 34.286 (33.420+866) | 41s |
| **Gesamt** | | **34.945** | **47s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "IT-Systeme", "Rezeption", "Drittlandtransfer"
- low_level_keywords: "Hotel Sonnenberg"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: DSGVO, Orientierungshilfe, Länderspez. Regelungen, Unternehmensverzeichnis, Tools, Dienstleister, Abteilungen
- KG Entities: Rezeption ("Gästeempfang und Reservierungsmanagement"), Cloudbeds ("Tool im Reservierungsmanagement"), SAP Business One ("Tool im Gästeempfang")
- KG Relationships: Hotel Sonnenberg → Rezeption ✓, Cloudbeds → Reservierungsmanagement ✓, Gästeempfang → SAP Business One ✓

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Rezeption → Gästeempfang + Reservierungsmanagement | FN | 0,0 | Rezeption als Abteilung nicht explizit identifiziert – listet stattdessen allgemein Dienstleister |
| F2: Gästeempfang→SAP, Reservierung→Cloudbeds | TP | 0,5 | Cloudbeds erwähnt, SAP nicht erwähnt |
| F3: SAP DE → kein Drittlandtransfer | FN | 0,0 | SAP nicht erwähnt |
| F4: Cloudbeds USA, kein DPF → Drittlandtransfer | TP | 1,0 | "Cloudbeds Inc. (USA, kein DPF → Drittlandtransfer)" – korrekt |
| F5: SCCs + TIA erforderlich | TP | 0,5 | "SCCs mit Cloudbeds" ✓, TIA nicht erwähnt |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Microsoft 365 als Rezeption-System | **FP** | Microsoft 365 wird in der Buchhaltung eingesetzt, nicht in der Rezeption |
| Google LLC als Rezeption-System | **FP** | Google LLC ist nicht der Rezeption zugeordnet in den Dokumenten |

**Zusammenfassung: TP = 2,0 | FP = 2 | FN = 3,0**
Kontrolle: TP + FN = 2,0 + 3,0 = 5,0 = 5 Referenz-Claims ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,50 | 2,0/(2,0+2) = 2,0/4,0 |
| Recall | 0,40 | 2,0/5,0 |
| **F1** | **0,44** | 2×0,50×0,40/(0,50+0,40) = 0,40/0,90 = 0,4444 |
| Citation Acc. | 0,60 | 3/5 (Länderspez. ✓, Tools ✓, Dienstleister ✓, Abteilungen ✗, Arbeitsbereiche ✗) |

**Befunde:**
1. KG enthält korrekte Tool-Zuordnungen (Cloudbeds → Reservierungsmanagement, SAP → Gästeempfang), aber das LLM nutzt sie nicht vollständig.
2. Microsoft 365 und Google LLC werden fälschlich als Rezeption-Systeme dargestellt – gleicher Fehler wie bei Frage 7.
3. Bei ~34k Tokens Kontext mit vielen Dienstleistern werden irrelevante Dienstleister hervorgehoben.

---

### Ergebnisübersicht Frage 8

| System | TP | FP | FN | P | R | F1 | CA |
|--------|----|----|----|----|----|----|-----|
| B1: Standard-RAG | 1,5 | 0 | 3,5 | 1,00 | 0,30 | **0,46** | 0,40 |
| B2: LightRAG (T=0) | 3,0 | 0 | 2,0 | 1,00 | 0,60 | **0,75** | 0,20 |
| B3: LightRAG (T=1) | 2,0 | 2 | 3,0 | 0,50 | 0,40 | **0,44** | 0,60 |

**Gewinner: LightRAG (T=0)** (F1 0,75)

---
---

## Gesamtübersicht 5-Hop

| Frage | System | TP | FP | FN | P | R | F1 | CA |
|-------|--------|----|----|----|----|----|----|-----|
| 7 Personal Drittland | B1 | 0 | 1 | 5 | 0,00 | 0,00 | **0,00** | 0,20 |
| 7 Personal Drittland | B2 | 2,0 | 1 | 3,0 | 0,67 | 0,40 | **0,50** | 0,20 |
| 7 Personal Drittland | B3 | 0 | 2 | 5 | 0,00 | 0,00 | **0,00** | 0,40 |
| 8 Rezeption Drittland | B1 | 1,5 | 0 | 3,5 | 1,00 | 0,30 | **0,46** | 0,40 |
| 8 Rezeption Drittland | B2 | 3,0 | 0 | 2,0 | 1,00 | 0,60 | **0,75** | 0,20 |
| 8 Rezeption Drittland | B3 | 2,0 | 2 | 3,0 | 0,50 | 0,40 | **0,44** | 0,60 |

### Ø 5-Hop

| System | Ø P | Ø R | Ø F1 | Ø CA |
|--------|-----|-----|------|------|
| B1: Standard-RAG | 0,50 | 0,15 | **0,23** | 0,30 |
| B2: LightRAG (T=0) | 0,83 | 0,50 | **0,63** | 0,20 |
| B3: LightRAG (T=1) | 0,25 | 0,20 | **0,22** | 0,50 |
