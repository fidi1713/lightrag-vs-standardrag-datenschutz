# Testfragen 2 Hops: Antworten und Bewertungen

> **Bewertungsmethode:** Claude Opus 4.6 als LLM-as-Judge + manuelle Nachprüfung durch den Autor
> **Metriken:** Precision, Recall, F1 (RAGAS Factual Correctness) + Citation Accuracy
> **Bewertungsverfahren (zweistufig):**
> - Schritt 1: Referenz-Claims (F1–Fn aus Anhang) gegen Antwort prüfen → TP (1,0/0,5) oder FN
> - Schritt 2: Antwort auf zusätzliche Claims scannen → FP wenn irrelevant oder inhaltlich falsch, kein FP wenn korrekt + relevant
> **FP-Definition (Relevanzfilter):** Inhaltlich falsch → FP. Fachlich korrekt aber irrelevant → FP. Fachlich korrekt UND thematisch relevant → kein FP.
> **Konfigurationen:** B1 = Standard-RAG | B2 = LightRAG (T=0) | B3 = LightRAG (T=1)

---

## Frage 1: Löschrecht

### Frage
> Ein Kunde von Alfreds Futterkiste verlangt die Löschung seiner Daten. Muss das Unternehmen der Forderung nachkommen?

### Hop-Kette

| Hop | Quelle | Erwartetes Ergebnis | Folgefrage |
|-----|--------|---------------------|------------|
| 1 | DSGVO Art. 17 | Löschpflicht besteht (Abs. 1), aber Ausnahme bei rechtlicher Verpflichtung (Abs. 3 lit. b) | Welche konkreten Aufbewahrungsfristen gelten? |
| 2 | Aufbewahrungsfristen | Rechnungen/Buchungsbelege: 8 Jahre (§ 147 AO), Handelsbriefe: 6 Jahre (§ 257 HGB) | Schlussfolgerung |

### Erwartete Aussagen (Anhang)

| Aussage | Inhalt | Quelle |
|---------|--------|--------|
| F1 | Recht auf Löschung nach Art. 17 Abs. 1 DSGVO | DSGVO Art. 17 |
| F2 | Ausnahmen nach Art. 17 Abs. 3 DSGVO, insbesondere lit. b (rechtliche Verpflichtung) | DSGVO Art. 17 |
| F3 | Ob gelöscht werden muss, hängt von der Art der gespeicherten Daten ab | DSGVO Art. 17 |
| F4 | Rechnungen und Buchungsbelege: 8 Jahre Aufbewahrungspflicht (§ 147 AO) | Aufbewahrungsfristen |
| F5 | Daten ohne Aufbewahrungspflicht sind unverzüglich zu löschen | DSGVO Art. 17 / Aufbewahrungsfristen |
| F6 | Prüfung erforderlich, welche konkreten Aufbewahrungsfristen für die jeweiligen Datenarten gelten | DSGVO Art. 17 / Aufbewahrungsfristen |

### Erwartete Quellen
DSGVO (Art. 17), Aufbewahrungsfristen.txt

### Referenzantwort

> 1. Relevante Rechtsgrundlagen: Art. 17 Abs. 1 DSGVO gewährt der betroffenen Person das Recht auf Löschung ihrer personenbezogenen Daten. Art. 17 Abs. 3 DSGVO definiert Ausnahmen, bei denen die Löschpflicht entfällt. Im vorliegenden Fall ist insbesondere Art. 17 Abs. 3 lit. b relevant: Die Löschpflicht entfällt, soweit die Verarbeitung zur Erfüllung einer rechtlichen Verpflichtung erforderlich ist. Die konkreten Aufbewahrungspflichten ergeben sich aus § 147 AO und § 257 HGB.
> 2. Analyse: Alfreds Futterkiste verarbeitet als Lebensmittelhändler verschiedene personenbezogene Daten seiner Kunden. Ob und welche Daten gelöscht werden müssen, hängt von der Art der gespeicherten Daten ab. Rechnungen und Buchungsbelege unterliegen einer gesetzlichen Aufbewahrungspflicht von 8 Jahren (§ 147 AO). Diese Daten darf das Unternehmen nicht löschen, solange die Frist läuft. Für alle personenbezogenen Daten, für die keine gesetzliche Aufbewahrungspflicht besteht, greift die Löschpflicht nach Art. 17 Abs. 1 DSGVO.
> 3. Handlungsempfehlung: Alfreds Futterkiste muss die gespeicherten Daten des Kunden differenziert prüfen: Daten mit gesetzlicher Aufbewahrungspflicht (insbesondere Rechnungen und Buchungsbelege, 8 Jahre nach § 147 AO) dürfen nicht gelöscht werden. Alle übrigen personenbezogenen Daten des Kunden sind unverzüglich zu löschen. Es ist zu prüfen, ob weitere Ausnahmen nach Art. 17 Abs. 3 DSGVO einschlägig sind und welche konkreten Aufbewahrungsfristen für die jeweiligen Datenarten gelten.

---

### Antwort B1: Standard-RAG (Open WebUI, GPT-4o-mini, Temp 0.0)

**Zeitstempel:** 2026-04-01T09:37:29Z – 2026-04-01T09:37:44Z (15s gesamt, davon 12s relevant)

**Antwort:**
> 1. **Relevante Rechtsgrundlagen:**
>    - Artikel 17 der Datenschutz-Grundverordnung (DSGVO) regelt das Recht auf Löschung personenbezogener Daten. Demnach hat die betroffene Person das Recht, die Löschung ihrer Daten zu verlangen, wenn die Daten für die Zwecke, für die sie erhoben wurden, nicht mehr benötigt werden oder wenn die betroffene Person ihre Einwilligung widerruft und es keine andere Rechtsgrundlage für die Verarbeitung gibt.
>    - Artikel 5 Abs. 1 lit. e der DSGVO besagt, dass personenbezogene Daten nur so lange gespeichert werden dürfen, wie es für die Zwecke, für die sie verarbeitet werden, erforderlich ist (Speicherbegrenzung).
>
> 2. **Analyse:**
>    Im vorliegenden Fall hat der Kunde von Alfreds Futterkiste das Recht, die Löschung seiner Daten zu verlangen. Das Unternehmen ist verpflichtet, dieser Forderung nachzukommen, sofern die Daten nicht mehr benötigt werden oder keine gesetzlichen Aufbewahrungspflichten bestehen. Wenn die Daten beispielsweise zur Erfüllung eines Vertrages notwendig sind, könnte das Unternehmen die Löschung verweigern, bis der Vertrag erfüllt ist. Andernfalls muss das Unternehmen die Daten unverzüglich löschen, wenn der Zweck der Verarbeitung entfällt (Art. 17 Abs. 1 DSGVO).
>
> 3. **Handlungsempfehlung:**
>    Alfreds Futterkiste sollte die Anfrage des Kunden zur Löschung der Daten prüfen. Wenn die Daten nicht mehr benötigt werden oder keine gesetzlichen Aufbewahrungspflichten bestehen, muss das Unternehmen die Löschung unverzüglich durchführen. Es ist ratsam, die Gründe für die Datenverarbeitung und mögliche gesetzliche Aufbewahrungspflichten zu überprüfen, um sicherzustellen, dass die Löschung rechtmäßig erfolgt.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] stellungnahme_videoueberwachung_tlfdi-thueringen_2024-12-10.md
- [3] Aufbewahrungsfristen.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Query-Generierung via Tool-Calling | 362 (242+120) | 2s |
| 2 | Antwort-Generierung mit Chunks | 4.075 (3.580+495) | 10s |
| **Gesamt (relevant)** | | **4.437** | **12s** |

**Log 1 – Query-Generierung:**
2 Suchqueries generiert:
- Query 1: "Datenlöschung Kundenrechte"
- Query 2: "DSGVO Artikel zur Datenlöschung"

**Log 2 – Retrieval-Ergebnisse (Chunks mit Distance-Scores):**

Query 1:

| Chunk | Quelle | Distance |
|-------|--------|----------|
| Art. 17 Abs. 1 (Recht auf Löschung) | Amtsblatt_EU_DSGVO.pdf | 0,803 |
| Erwägungsgrund (Löschung wenn nicht mehr benötigt) | Amtsblatt_EU_DSGVO.pdf | 0,783 |
| Vertragsdaten nicht löschen solange Vertrag läuft | Amtsblatt_EU_DSGVO.pdf | 0,777 |
| Schadenersatz | Amtsblatt_EU_DSGVO.pdf | 0,775 |
| Frage 6: Löschfrist Speichersystem | stellungnahme_tlfdi-thueringen | 0,763 |

Query 2:

| Chunk | Quelle | Distance |
|-------|--------|----------|
| Header: Löschpflicht + Aufbewahrungspflicht | Aufbewahrungsfristen.txt | 0,839 |
| Art. 17 Abs. 1 lit. e (Löschung bei rechtl. Verpflichtung) | Amtsblatt_EU_DSGVO.pdf | 0,836 |
| Recht auf Löschung + Beschränkungen | Amtsblatt_EU_DSGVO.pdf | 0,836 |
| Grundsatz: unverzüglich löschen + § 147 AO, § 257 HGB | Aufbewahrungsfristen.txt | 0,830 |
| Auftragsverarbeiter löscht nach Auftrag | Amtsblatt_EU_DSGVO.pdf | 0,819 |

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Recht auf Löschung nach Art. 17 Abs. 1 | TP | 1,0 | "Artikel 17 der DSGVO regelt das Recht auf Löschung" – korrekt benannt und erklärt |
| F2: Ausnahmen nach Art. 17 Abs. 3, insb. lit. b | TP | 0,5 | "keine gesetzlichen Aufbewahrungspflichten bestehen" als Ausnahme erwähnt, aber ohne Art. 17 Abs. 3 lit. b |
| F3: Ob gelöscht werden muss, hängt von Datenart ab | TP | 0,5 | "Gründe für die Datenverarbeitung und mögliche gesetzliche Aufbewahrungspflichten überprüfen" → impliziert Differenzierung |
| F4: Rechnungen/Buchungsbelege: 8 Jahre (§ 147 AO) | FN | 0,0 | Nicht erwähnt – obwohl Aufbewahrungsfristen.txt als Quelle zitiert wird |
| F5: Daten ohne Aufbewahrungspflicht unverzüglich löschen | TP | 1,0 | "muss das Unternehmen die Löschung unverzüglich durchführen" wenn keine Aufbewahrungspflichten bestehen |
| F6: Prüfung konkreter Aufbewahrungsfristen pro Datenart | TP | 0,5 | "mögliche gesetzliche Aufbewahrungspflichten zu überprüfen" – richtige Richtung, aber ohne Konkretisierung |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Art. 5 Abs. 1 lit. e Speicherbegrenzung | – | Korrekt + relevant (Speicherbegrenzungsgrundsatz) → kein FP |
| Vertragserfüllung als Ausnahme | – | Korrekt + relevant (Art. 17 Abs. 1 lit. b Kontext) → kein FP |

**Zusammenfassung: TP = 3,5 | FP = 0 | FN = 2,5**

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 3,5/(3,5+0) |
| Recall | 0,58 | 3,5/(3,5+2,5) = 0,5833 |
| **F1** | **0,74** | 2×1,00×0,5833/(1,00+0,5833) = 0,7368 |
| Citation Accuracy | 1,00 | 2/2 (DSGVO ✓, Aufbewahrungsfristen ✓) |

**Befunde:**
1. Aufbewahrungsfristen.txt wurde retrievt (Query 2, Distance 0,839 und 0,830).
2. Die konkreten Fristen (8 Jahre, § 147 AO) fehlen in der Antwort trotz Retrieval.
3. 2 eigenständige Suchqueries generiert – Query 2 war entscheidend.
4. 3.580 Prompt Tokens – ca. 10× weniger als LightRAG.
5. 1 von 3 zitierten Quellen irrelevant (Stellungnahme Thüringen).

---

### Antwort B2: LightRAG (T=0) (GPT-4o-mini, KG Temp 0.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-01T07:43:57Z – 2026-04-01T07:44:29Z (32s)

**Antwort:**
> ### Relevante Rechtsgrundlagen
>
> Im vorliegenden Fall sind folgende Artikel der Datenschutz-Grundverordnung (DSGVO) relevant:
>
> - **Artikel 17**: Dieser Artikel regelt das „Recht auf Löschung" (Recht auf Vergessenwerden). Die betroffene Person ist berechtigt, von dem Verantwortlichen die Löschung ihrer personenbezogenen Daten zu verlangen, wenn einer der im Artikel genannten Gründe zutrifft, wie zum Beispiel, wenn die personenbezogenen Daten für die Zwecke, für die sie erhoben wurden, nicht mehr notwendig sind.
>
> - **Artikel 18**: Bezieht sich auf das Recht, die Verarbeitung zu beschränken. Dies gilt, wenn die betroffene Person die Richtigkeit der Daten bestreitet, die Verarbeitung unrechtmäßig ist oder die Daten für die Geltendmachung, Ausübung oder Verteidigung von Rechtsansprüchen benötigt werden.
>
> ### Analyse
>
> In diesem spezifischen Fall hat der Kunde von Alfreds Futterkiste das Recht, die Löschung seiner personenbezogenen Daten zu verlangen. Das Unternehmen muss auf diesen Antrag eingehen, es sei denn, es besteht ein rechtlicher Grund, der die weitere Verarbeitung rechtfertigt. Die DSGVO legt klar fest, dass die Löschung erfolgen muss, wenn:
> 1. Die personenbezogenen Daten nicht mehr notwendig sind.
> 2. Die betroffene Person ihre Einwilligung zur Verarbeitung widerruft, und es besteht keine anderweitige Rechtsgrundlage.
> 3. Die betroffene Person Widerspruch gegen die Verarbeitung einlegt.
> 4. Die Verarbeitung der Daten unrechtmäßig ist.
>
> Da hier keine spezifischen Umstände genannt wurden, die einer Löschung entgegenstehen, muss Alfreds Futterkiste der Forderung nachkommen und die Daten des Kunden löschen, sofern diese unter die oben genannten Bedingungen fallen.
>
> ### Handlungsempfehlung
>
> Alfreds Futterkiste sollte folgende Schritte unternehmen:
> - Den Antrag des Kunden auf Löschung seiner personenbezogenen Daten prüfen.
> - Die rechtlichen Grundlagen in Bezug auf die Notwendigkeit der Datenverarbeitung bewerten.
> - Im Falle der Erfüllung der Voraussetzungen gemäß Artikel 17 DSGVO die personenbezogenen Daten unverzüglich löschen.
> - Den Kunden über die durchgeführte Löschung informieren und die Löschbestätigung bereitstellen.
>
> Sollte das Unternehmen die Daten aus gesetzlichen Gründen oder zur Erfüllung von Verträgen weiterhin benötigen, muss es den Kunden darüber in Kenntnis setzen und die entsprechende rechtliche Grundlage darlegen.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | – | – |
| 2 | Antwort-Generierung | 35.665 (34.984+681) | 32s |
| **Gesamt** | | **35.665** | **32s** |

**Retrieval-Kontext:**
- Retrievte Dokumente: Amtsblatt_EU_DSGVO.pdf, 3× Stellungnahmen Videoüberwachung, Unternehmensverzeichnis.txt
- Nicht retrievt: Aufbewahrungsfristen.txt
- KG Entities (Auswahl): Alfreds Futterkiste, DSGVO, Betroffene Person, Art. 17, Art. 18, Verantwortliche, Auftragsverarbeiter
- KG Relationships (Auswahl): Art. 17 → betroffene Person (Löschrecht), Betroffene Person → Recht auf Vergessenwerden

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Recht auf Löschung nach Art. 17 Abs. 1 | TP | 1,0 | "Artikel 17 regelt das Recht auf Löschung" – korrekt |
| F2: Ausnahmen nach Art. 17 Abs. 3, insb. lit. b | TP | 0,5 | "gesetzliche Gründe" als Ausnahme in Handlungsempfehlung, aber ohne Art. 17 Abs. 3 lit. b |
| F3: Ob gelöscht werden muss, hängt von Datenart ab | TP | 0,5 | "es sei denn, es besteht ein rechtlicher Grund" + "Sollte... aus gesetzlichen Gründen... benötigen" → Konzept der Differenzierung vorhanden, aber Hauptschlussfolgerung negiert es ("Da hier keine spezifischen Umstände") |
| F4: Rechnungen/Buchungsbelege: 8 Jahre (§ 147 AO) | FN | 0,0 | Nicht erwähnt, Aufbewahrungsfristen.txt nicht retrievt |
| F5: Daten ohne Aufbewahrungspflicht unverzüglich löschen | TP | 0,5 | "die personenbezogenen Daten unverzüglich löschen" wenn "Voraussetzungen gemäß Art. 17 erfüllt" – "unverzüglich" vorhanden, aber Bedingung weniger präzise als Referenz (Art. 17 allgemein statt "keine Aufbewahrungspflicht") |
| F6: Prüfung konkreter Aufbewahrungsfristen pro Datenart | FN | 0,0 | "Notwendigkeit der Datenverarbeitung bewerten" → zu weit weg von "Aufbewahrungsfristen prüfen". Kein Bezug zu Aufbewahrung oder konkreten Fristen. |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Art. 18 (Einschränkung der Verarbeitung) | **FP** | Irrelevant – Kunde will Löschung, nicht Einschränkung. Art. 18 ist nicht einschlägig. |
| 4 Löschbedingungen (a–d) aus Art. 17 Abs. 1 | – | Korrekt + relevant (Art. 17 Kontext) → kein FP |
| Löschbestätigung bereitstellen | – | Korrekt + relevant (Verfahrenshinweis) → kein FP |
| Kunden informieren | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 2,5 | FP = 1 | FN = 3,5**

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,71 | 2,5/(2,5+1) |
| Recall | 0,42 | 2,5/(2,5+3,5) |
| **F1** | **0,53** | 2×0,71×0,42/(0,71+0,42) |
| Citation Accuracy | 0,50 | 1/2 (DSGVO ✓, Aufbewahrungsfristen ✗) |

**Befunde:**
1. Aufbewahrungsfristen.txt nicht retrievt – der zweite Hop fehlt vollständig.
2. Keine KG-Entity für "Aufbewahrungsfristen" oder "§ 147 AO" im Kontext.
3. 3 von 5 retrievten Dokumenten sind irrelevant (Videoüberwachungs-Stellungnahmen).
4. Art. 18 wird genannt, obwohl der Kunde Löschung verlangt.
5. 34.984 Prompt Tokens – relevante Passage konkurriert mit ~35.000 Tokens Gesamtkontext.

---

### Antwort B3: LightRAG (T=1) (GPT-4o-mini, KG Temp 1.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-06T14:50:08Z – 2026-04-06T14:50:42Z (34s)

**Antwort:**
> ### 1. Relevante Rechtsgrundlagen
>
> Im vorliegenden Fall ist vor allem **Artikel 17 der Datenschutz-Grundverordnung (DSGVO)** relevant. Artikel 17 regelt das **Recht auf Löschung** personenbezogener Daten, auch als "Recht auf Vergessenwerden" bekannt. Die betroffene Person hat laut diesem Artikel das Recht, die Löschung ihrer personenbezogenen Daten zu verlangen, wenn bestimmte Voraussetzungen erfüllt sind:
>
> - Die personenbezogenen Daten sind für die Zwecke, für die sie erhoben oder verarbeitet wurden, nicht mehr notwendig.
> - Die betroffene Person widerruft ihre Einwilligung, auf die sich die Verarbeitung stützt, und es fehlt an einer anderen rechtlichen Grundlage für die Verarbeitung.
> - Die betroffene Person legt Widerspruch gegen die Verarbeitung ein und es liegen keine vorrangigen berechtigten Gründe für die Verarbeitung vor.
> - Die personenbezogenen Daten wurden unrechtmäßig verarbeitet.
> - Die Löschung ist zur Erfüllung einer rechtlichen Verpflichtung nach dem Unionsrecht oder dem Recht der Mitgliedstaaten erforderlich, dem der Verantwortliche unterliegt.
>
> ### 2. Analyse
>
> In diesem speziellen Fall, in dem ein Kunde von Alfreds Futterkiste die Löschung seiner Daten fordert, müsste das Unternehmen folgende Schritte unternehmen:
>
> - **Prüfung des Antrags**: Das Unternehmen muss zunächst überprüfen, ob die angeforderten Daten tatsächlich verarbeitet werden und ob die Anfrage rechtmäßig ist.
>
> - **Berechtigte Gründe für die Verarbeitung**: Alfreds Futterkiste sollte evaluieren, ob es noch rechtliche Gründe gibt, die die weitere Verarbeitung der Daten rechtfertigen. Beispielsweise könnte eine gesetzliche Aufbewahrungspflicht bestehen oder der Kunde könnte noch Neukundeninformationen eingab. Wenn keine solchen Gründe vorliegen, muss die Löschung in der Regel erfolgen.
>
> - **Fristen für die Datenverarbeitung**: Wenn die Daten für die ursprünglichen Zwecke nicht mehr notwendig sind, ist das Unternehmen verpflichtet, diese unverzüglich zu löschen.
>
> ### 3. Handlungsempfehlung
>
> Falls die Überprüfung ergibt, dass die Daten nicht mehr erforderlich sind oder keine anderen rechtlichen Grundlagen für die Aufbewahrung bestehen, sollte **Alfreds Futterkiste** der Löschungsforderung des Kunden nachkommen. Damit wird das Unternehmen nicht nur den gesetzlichen Anforderungen gerecht, sondern respektiert auch die Rechte der betroffenen Person gemäß der DSGVO.
>
> Sollte es jedoch Gründe geben, die eine Löschung ausschließen (z. B. weiterhin relevante rechtliche Ansprüche), muss das Unternehmen dies dem Kunden transparent kommunizieren.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] Orientierungshilfe Videoüberwachung durch nicht-öffentliche Stellen.pdf

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 677 (630+47) | 1s |
| 2 | Antwort-Generierung | 36.487 (35.739+748) | 34s |
| **Gesamt** | | **37.164** | **35s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Datenschutz", "Kundenrechte", "Datenlöschung"
- low_level_keywords: "Alfreds Futterkiste", "Kunde", "Forderung"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: [1] DSGVO, [2] Orientierungshilfe, [3] Stellungnahme MV, [4] Stellungnahme NRW, [5] Stellungnahme Thüringen, [6] Unternehmensverzeichnis
- Nicht retrievt: Aufbewahrungsfristen.txt
- KG Entities (Auswahl): Alfreds Futterkiste, Recht auf Löschung, Artikel 17, Betroffene Person, Löschung, DSGVO, Verantwortlicher, Auftragsverarbeiter, Personenbezogene Daten
- KG Relationships (Auswahl): Recht auf Löschung → betroffene Person, Artikel 17 → Betroffene Person (Löschrecht), Betroffene Person → Löschung, Artikel 17 → DSGVO

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: Recht auf Löschung nach Art. 17 Abs. 1 | TP | 1,0 | "Artikel 17 regelt das Recht auf Löschung" – korrekt und ausführlich |
| F2: Ausnahmen nach Art. 17 Abs. 3, insb. lit. b | TP | 0,5 | "gesetzliche Aufbewahrungspflicht bestehen" als Ausnahme, aber ohne Art. 17 Abs. 3 lit. b |
| F3: Ob gelöscht werden muss, hängt von Datenart ab | TP | 0,5 | "evaluieren, ob es noch rechtliche Gründe gibt" → erkennt Differenzierungsbedarf |
| F4: Rechnungen/Buchungsbelege: 8 Jahre (§ 147 AO) | FN | 0,0 | Nicht erwähnt, Aufbewahrungsfristen.txt nicht retrievt |
| F5: Daten ohne Aufbewahrungspflicht unverzüglich löschen | TP | 0,5 | "unverzüglich zu löschen" wenn "nicht mehr notwendig", aber ohne explizite Aufbewahrungspflicht-Differenzierung |
| F6: Prüfung konkreter Aufbewahrungsfristen pro Datenart | TP | 0,5 | "ob keine anderen rechtlichen Grundlagen für die Aufbewahrung bestehen" → Konzept vorhanden, aber keine konkreten Fristen |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| 5 Löschbedingungen aus Art. 17 Abs. 1 | – | Korrekt + relevant → kein FP |
| Prüfung des Antrags | – | Korrekt + relevant (Verfahrenshinweis) → kein FP |
| Transparent kommunizieren bei Ablehnung | – | Korrekt + relevant → kein FP |

**Zusammenfassung: TP = 3,0 | FP = 0 | FN = 3,0**

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 3,0/(3,0+0) |
| Recall | 0,50 | 3,0/(3,0+3,0) |
| **F1** | **0,67** | 2×1,00×0,50/(1,00+0,50) |
| Citation Accuracy | 0,50 | 1/2 (DSGVO ✓, Aufbewahrungsfristen ✗) |

**Befunde:**
1. Aufbewahrungsfristen.txt nicht retrievt – identisches Problem wie bei B2.
2. B3 erkennt den Differenzierungsbedarf ("evaluieren, ob rechtliche Gründe"), B2 nicht ("keine Umstände genannt").
3. Keine FP – die Antwort bleibt thematisch fokussiert (kein Art. 18 wie bei B2).
4. 35.739 Prompt Tokens – umfangreicher Kontext ohne Aufbewahrungsfristen.

---

### Ergebnisübersicht Frage 1

| System | TP | FP | FN | Precision | Recall | F1 |
|--------|----|----|----|----|----|----|
| B1: Standard-RAG | 3,5 | 0 | 2,5 | 1,00 | 0,58 | **0,74** |
| B2: LightRAG (T=0) | 2,5 | 1 | 3,5 | 0,71 | 0,42 | **0,53** |
| B3: LightRAG (T=1) | 3,0 | 0 | 3,0 | 1,00 | 0,50 | **0,67** |

**Gewinner: Standard-RAG** (F1 0,74)

---
---

## Frage 2: Auftragsverarbeitungsvertrag Personio

### Frage
> Muss Alfreds Futterkiste mit Personio einen Auftragsverarbeitungsvertrag abschließen?

### Hop-Kette

| Hop | Quelle | Erwartetes Ergebnis | Folgefrage |
|-----|--------|---------------------|------------|
| 1 | DSGVO Art. 28 | AVV erforderlich wenn Dienstleister personenbezogene Daten im Auftrag verarbeitet | Verarbeitet Personio Daten im Auftrag von Alfreds Futterkiste? |
| 2 | Arbeitsbereiche | Personio wird im Recruiting eingesetzt (Bewerberdaten) → Auftragsverarbeitung liegt vor | Schlussfolgerung |

### Erwartete Aussagen (Anhang)

| Aussage | Inhalt | Quelle |
|---------|--------|--------|
| F1 | AVV nach Art. 28 DSGVO erforderlich wenn Dienstleister personenbezogene Daten im Auftrag verarbeitet | DSGVO Art. 28 |
| F2 | Personio wird im Recruiting eingesetzt und verarbeitet Bewerberdaten | Arbeitsbereiche |
| F3 | Auftragsverarbeitung liegt vor, AVV muss abgeschlossen werden | DSGVO Art. 28 / Arbeitsbereiche |

### Erwartete Quellen
DSGVO (Art. 28), Arbeitsbereiche

### Referenzantwort

> 1. Relevante Rechtsgrundlagen: Art. 28 Abs. 1 DSGVO verpflichtet den Verantwortlichen, die Verarbeitung personenbezogener Daten durch einen Auftragsverarbeiter auf Grundlage eines Vertrags oder eines anderen Rechtsinstruments vorzunehmen.
> 2. Analyse: Personio wird bei Alfreds Futterkiste im Recruiting eingesetzt und verarbeitet dabei personenbezogene Daten von Bewerbern im Auftrag des Unternehmens. Damit liegt eine Auftragsverarbeitung im Sinne von Art. 28 DSGVO vor.
> 3. Handlungsempfehlung: Ja, Alfreds Futterkiste muss mit Personio einen Auftragsverarbeitungsvertrag nach Art. 28 DSGVO abschließen.

---

### Antwort B1: Standard-RAG (Open WebUI, GPT-4o-mini, Temp 0.0)

**Zeitstempel:** 2026-04-07T15:07:35Z – 2026-04-07T15:07:44Z (9s gesamt)

**Antwort:**
> 1. **Relevante Rechtsgrundlagen:**
>    - Gemäß der DSGVO ist ein AVV erforderlich, wenn ein Verantwortlicher personenbezogene Daten durch einen Auftragsverarbeiter verarbeiten lässt. Die relevanten Artikel sind insbesondere Artikel 28 der DSGVO.
>
> 2. **Analyse:**
>    - Wenn Alfreds Futterkiste Personio mit der Verarbeitung personenbezogener Daten beauftragt, ist ein AVV notwendig. Dieser Vertrag muss die Art und den Zweck der Verarbeitung, die Dauer, die Art der personenbezogenen Daten sowie die Rechte und Pflichten beider Parteien festlegen.
>
> 3. **Handlungsempfehlung:**
>    - Alfreds Futterkiste sollte mit Personio einen AVV abschließen, um die rechtlichen Anforderungen der DSGVO zu erfüllen.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Query-Generierung via Tool-Calling | 299 (243+56) | 2s |
| 2 | Antwort-Generierung mit Chunks | 1.979 (1.623+356) | 6s |
| **Gesamt (relevant)** | | **2.278** | **8s** |

**Log 1 – Query-Generierung:**
- Query: "Auftragsverarbeitungsvertrag Personio"

**Log 2 – Retrieval-Ergebnisse:**

| Chunk | Quelle | Distance |
|-------|--------|----------|
| Auftragsverarbeiter Pflichten | DSGVO | 0,811 |
| Überschrift „Auftragsverarbeiter" | DSGVO | 0,801 |
| Überschrift „Verantwortlicher und Auftragsverarbeiter" | DSGVO | 0,784 |
| Vertragsinhalte (Dauer, Zweck, Datenarten) | DSGVO | 0,777 |
| Standardvertragsklauseln für Auftragsverarbeiter | DSGVO | 0,777 |

Kein Stammdaten-Dokument retrievt.

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: AVV nach Art. 28 erforderlich | TP | 1,0 | Art. 28 korrekt benannt und erklärt |
| F2: Personio im Recruiting, Bewerberdaten | FN | 0,0 | Nicht erwähnt – sagt nur allgemein "wenn beauftragt" |
| F3: AVV muss abgeschlossen werden | TP | 1,0 | "sollte einen AVV abschließen" |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Vertragsinhalte (Art, Zweck, Dauer, Datenarten, Rechte) | – | Korrekt (Art. 28 Abs. 3) + relevant → kein FP |

**Zusammenfassung: TP = 2,0 | FP = 0 | FN = 1,0**

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 2,0/(2,0+0) |
| Recall | 0,67 | 2,0/(2,0+1,0) |
| **F1** | **0,80** | 2×1,00×0,67/(1,00+0,67) |
| Citation Accuracy | 0,50 | 1/2 (DSGVO ✓, Arbeitsbereiche ✗) |

**Befunde:**
1. Ausschließlich DSGVO-Chunks retrievt (Art. 28).
2. Kein Stammdaten-Dokument gefunden – Arbeitsbereiche.txt fehlt.
3. Korrekte Schlussfolgerung (AVV nötig) basiert auf LLM-Vorwissen (Personio = HR-Tool), nicht auf dokumentengestützter Herleitung.

---

### Antwort B2: LightRAG (T=0) (GPT-4o-mini, KG Temp 0.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-08T10:38:19Z – 2026-04-08T10:38:40Z (21s gesamt)

**Antwort:**
> Art. 28 DSGVO: Verantwortlicher muss mit Auftragsverarbeitern zusammenarbeiten, die ausreichende Garantien bieten. Art. 6: Angemessene Verträge erforderlich. Da Personio GmbH als Dienstleister personenbezogene Daten verarbeitet, ist AVV notwendig. Empfehlung: Umgehend AVV abschließen.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [2] Dienstleister.txt
- [3] Unternehmensverzeichnis.txt
- [5] Arbeitsbereiche.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 675 (625+50) | 1s |
| 2 | Antwort-Generierung | 35.015 (34.611+404) | 14s |
| **Gesamt** | | **35.690** | **15s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Auftragsverarbeitungsvertrag", "Personio", "Alfreds Futterkiste"
- low_level_keywords: "Datenschutz", "Vertragsabschluss", "Verarbeitung von Daten"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: [1] DSGVO, [2] Dienstleister, [3] Unternehmensverzeichnis, [4] Abteilungen, [5] Arbeitsbereiche
- KG Entities: Personio GmbH ("Dienstleister für Alfreds Futterkiste"), Personio ("Tool im Recruiting"), Recruiting ("Bewerbermanagement"), Auftragsverarbeiter, Artikel 28
- KG Relationships: Alfreds Futterkiste → Personio GmbH, Personio → Recruiting, Auftragsverarbeiter → Verantwortlicher

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: AVV nach Art. 28 erforderlich | TP | 1,0 | Art. 28 korrekt |
| F2: Personio im Recruiting, Bewerberdaten | TP | 0,5 | "Personio GmbH als Dienstleister, verarbeitet personenbezogene Daten" – ohne konkreten Recruiting-Bezug |
| F3: AVV muss abgeschlossen werden | TP | 1,0 | "umgehend AVV abschließen" |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| "Art. 6: Angemessene Verträge erforderlich" | **FP** | Inhaltlich falsch: Art. 6 DSGVO regelt Rechtsgrundlagen der Verarbeitung (Einwilligung, Vertrag, etc.), nicht Vertragsanforderungen für Auftragsverarbeitung. Falsche Zuordnung. |

**Zusammenfassung: TP = 2,5 | FP = 1 | FN = 0,5**

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 0,71 | 2,5/(2,5+1) |
| Recall | 0,83 | 2,5/(2,5+0,5) |
| **F1** | **0,77** | 2×0,71×0,83/(0,71+0,83) |
| Citation Accuracy | 1,00 | 2/2 (DSGVO ✓, Arbeitsbereiche ✓ – [5] Arbeitsbereiche.txt in Quellenliste) |

**Befunde:**
1. KG enthält die Kette Alfreds Futterkiste → Personio GmbH → Personio → Recruiting.
2. Arbeitsbereiche.txt als Quelle zitiert, aber Recruiting-Bezug nicht in der Antwort genutzt.
3. "Art. 6: Angemessene Verträge erforderlich" ist eine falsche Zuordnung (Art. 6 ≠ Vertragsanforderungen).

---

### Antwort B3: LightRAG (T=1) (GPT-4o-mini, KG Temp 1.0, Antwort Temp 0.0)

**Zeitstempel:** 2026-04-07T15:08:12Z – 2026-04-07T15:08:43Z (31s gesamt)

**Antwort:**
> ### Relevante Rechtsgrundlagen
> Artikel 28 der DS-GVO ist entscheidend. Ein Verantwortlicher, der personenbezogene Daten im Auftrag eines Auftragsverarbeiters verarbeiten lässt, muss einen Vertrag abschließen. Der Auftragsverarbeiter muss hinreichende Garantien für geeignete technische und organisatorische Maßnahmen bieten.
>
> ### Analyse
> Da die Personio GmbH als Dienstleister für Alfreds Futterkiste fungiert und personenbezogene Daten verarbeitet, ist Alfreds Futterkiste als Verantwortlicher verpflichtet, mit Personio einen AVV abzuschließen. Die Vereinbarung muss Gegenstand, Dauer, Art und Zweck der Verarbeitung, Kategorien betroffener Personen sowie Pflichten und Rechte festlegen.
>
> ### Handlungsempfehlung
> Alfreds Futterkiste sollte umgehend einen AVV mit Personio abschließen.

**Quellen:**
- [1] Amtsblatt_EU_DSGVO.pdf
- [4] Dienstleister.txt
- [5] Abteilungen.txt

**Retrieval-Daten (LiteLLM):**

| Log | Zweck | Tokens (Prompt+Completion) | Dauer |
|-----|-------|---------------------------|-------|
| 1 | Keyword-Extraktion | 674 (625+49) | 2s |
| 2 | Antwort-Generierung | 35.583 (35.095+488) | 23s |
| **Gesamt** | | **36.257** | **25s** |

**Log 1 – Keyword-Extraktion:**
- high_level_keywords: "Auftragsverarbeitungsvertrag", "Alfreds Futterkiste", "Personio"
- low_level_keywords: "Vertrag", "Datenschutz", "Compliance", "Services"

**Log 2 – Retrieval-Kontext:**
- Retrievte Dokumente: [1] DSGVO, [2] Orientierungshilfe, [3] Unternehmensverzeichnis, [4] Dienstleister, [5] Abteilungen, [6] Tools, [7] Arbeitsbereiche – alle 7 Stammdaten-Dokumente
- KG Entities (Auswahl): Alfreds Futterkiste, Personio GmbH ("Dienstleister für Alfreds Futterkiste"), Personio ("Tool im Recruiting für Bewerbermanagement"), Recruiting ("Bewerbermanagement, Stellenausschreibungen"), Auftragsverarbeiter
- KG Relationships (Auswahl): Alfreds Futterkiste → Personio GmbH ("ist ein Dienstleister"), Personio → Recruiting ("wird im Bereich Recruiting eingesetzt"), Alfreds Futterkiste → Personal ("hat Personalabteilung mit Recruiting und Lohnabrechnung"), Auftragsverarbeiter → Verantwortlicher (Vertragspflicht)

**Bewertung:**

**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: AVV nach Art. 28 erforderlich | TP | 1,0 | Art. 28 korrekt benannt und erklärt |
| F2: Personio im Recruiting, Bewerberdaten | TP | 0,5 | "Personio GmbH als Dienstleister, verarbeitet personenbezogene Daten" – richtige Richtung, aber ohne konkreten Bezug zu Recruiting/Bewerberdaten |
| F3: AVV muss abgeschlossen werden | TP | 1,0 | "verpflichtet, mit Personio einen AVV abzuschließen" |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| Auftragsverarbeiter muss Garantien bieten (TOM) | – | Korrekt (Art. 28 Abs. 1) + relevant → kein FP |
| Vertragsinhalte (Gegenstand, Dauer, Art, Zweck, Kategorien, Rechte) | – | Korrekt (Art. 28 Abs. 3) + relevant → kein FP |

**Zusammenfassung: TP = 2,5 | FP = 0 | FN = 0,5**

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | 1,00 | 2,5/(2,5+0) |
| Recall | 0,83 | 2,5/(2,5+0,5) |
| **F1** | **0,91** | 2×1,00×0,83/(1,00+0,83) |
| Citation Accuracy | 0,50 | 1/2 (DSGVO ✓, Arbeitsbereiche ✗ – retrievt aber nicht als Quelle der Schlussfolgerung genutzt) |

**Befunde:**
1. LightRAG (T=1) retrievt alle 7 Stammdaten-Dokumente.
2. KG enthält die komplette Kette: Alfreds Futterkiste → Personio GmbH → Personio → Recruiting.
3. Dennoch nutzt die Antwort den Recruiting-Bezug nicht explizit.
4. Retrieval erfolgreich, aber LLM-Nutzung des ~35k-Token-Kontexts suboptimal.

---

### Ergebnisübersicht Frage 2

| System | TP | FP | FN | Precision | Recall | F1 |
|--------|----|----|----|----|----|----|
| B1: Standard-RAG | 2,0 | 0 | 1,0 | 1,00 | 0,67 | **0,80** |
| B2: LightRAG (T=0) | 2,5 | 1 | 0,5 | 0,71 | 0,83 | **0,77** |
| B3: LightRAG (T=1) | 2,5 | 0 | 0,5 | 1,00 | 0,83 | **0,91** |

**Gewinner: LightRAG (T=1)** (F1 0,91)

---
---

## Gesamtübersicht 2-Hop

| Frage | System | TP | FP | FN | P | R | F1 | CA |
|-------|--------|----|----|----|----|----|----|-----|
| 1 Löschrecht | B1 | 3,5 | 0 | 2,5 | 1,00 | 0,58 | **0,74** | 1,00 |
| 1 Löschrecht | B2 | 2,5 | 1 | 3,5 | 0,71 | 0,42 | **0,53** | 0,50 |
| 1 Löschrecht | B3 | 3,0 | 0 | 3,0 | 1,00 | 0,50 | **0,67** | 0,50 |
| 2 AVV | B1 | 2,0 | 0 | 1,0 | 1,00 | 0,67 | **0,80** | 0,50 |
| 2 AVV | B2 | 2,5 | 1 | 0,5 | 0,71 | 0,83 | **0,77** | 1,00 |
| 2 AVV | B3 | 2,5 | 0 | 0,5 | 1,00 | 0,83 | **0,91** | 0,50 |

### Ø 2-Hop

| System | Ø P | Ø R | Ø F1 | Ø CA |
|--------|-----|-----|------|------|
| B1: Standard-RAG | 1,00 | 0,63 | **0,77** | 0,75 |
| B2: LightRAG (T=0) | 0,71 | 0,63 | **0,65** | 0,75 |
| B3: LightRAG (T=1) | 1,00 | 0,67 | **0,79** | 0,50 |
