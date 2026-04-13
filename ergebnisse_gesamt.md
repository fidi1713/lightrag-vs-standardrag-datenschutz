# Ergebnisse Final Gesamt

> Alle Testergebnisse auf einen Blick – finale Version (Neuberechnung 11.04.2026).
> **Metriken:** RAGAS Factual Correctness (Precision, Recall, F1) + Citation Accuracy
> **Bewertungsmethode:** Claude Opus 4.6 als LLM-as-Judge + manuelle Nachprüfung durch den Autor
> **Systeme:** B1 = Standard-RAG (Open WebUI), B2 = LightRAG Mix (KG Temp 0.0), B3 = LightRAG Mix (KG Temp 1.0)
> **Bewertungsmethodik:** siehe `Testfragen_final/bewertungsmethodik.md`

---

## 1. Einzelergebnisse pro Frage

| Frage | Hops | Fakten | B1 P | B1 R | B1 F1 | B2 P | B2 R | B2 F1 | B3 P | B3 R | B3 F1 |
|-------|------|--------|------|------|-------|------|------|-------|------|------|-------|
| 1 Löschrecht | 2 | 6 | 1,00 | 0,58 | **0,74** | 0,71 | 0,42 | 0,53 | 1,00 | 0,50 | 0,67 |
| 2 AVV Personio | 2 | 3 | 1,00 | 0,67 | 0,80 | 0,71 | 0,83 | 0,77 | 1,00 | 0,83 | **0,91** |
| 3 DSFA Lagerraum | 3 | 4 | 0,50 | 0,25 | 0,33 | 0,71 | 0,63 | 0,67 | 1,00 | 0,63 | **0,77** |
| 4 Speicherfristen | 3 | 5 | 0,00 | 0,00 | 0,00 | 1,00 | 0,10 | 0,18 | 1,00 | 0,60 | **0,75** |
| 5 Microsoft 365 | 4 | 8 | 0,43 | 0,19 | 0,26 | 1,00 | 0,81 | **0,90** | 1,00 | 0,69 | 0,81 |
| 6 Lieferanten | 4 | 4 | 1,00 | 0,25 | 0,40 | 1,00 | 0,25 | 0,40 | 1,00 | 0,38 | **0,55** |
| 7 Personal Drittland | 5 | 5 | 0,00 | 0,00 | 0,00 | 0,67 | 0,40 | **0,50** | 0,00 | 0,00 | 0,00 |
| 8 Rezeption Drittland | 5 | 5 | 1,00 | 0,30 | 0,46 | 1,00 | 0,60 | **0,75** | 0,50 | 0,40 | 0,44 |

---

## 2. Ergebnisse pro Hop-Stufe

### 2-Hop

| Metrik | B1: Standard-RAG | B2: LightRAG (T=0) | B3: LightRAG (T=1) |
|--------|:-:|:-:|:-:|
| Ø Precision | 1,00 | 0,71 | 1,00 |
| Ø Recall | 0,63 | 0,63 | 0,67 |
| **Ø F1** | **0,77** | **0,65** | **0,79** |
| Ø Citation Acc. | 0,75 | 0,75 | 0,50 |

### 3-Hop

| Metrik | B1: Standard-RAG | B2: LightRAG (T=0) | B3: LightRAG (T=1) |
|--------|:-:|:-:|:-:|
| Ø Precision | 0,25 | 0,86 | 1,00 |
| Ø Recall | 0,13 | 0,36 | 0,61 |
| **Ø F1** | **0,17** | **0,42** | **0,76** |
| Ø Citation Acc. | 0,17 | 0,67 | 0,50 |

### 4-Hop

| Metrik | B1: Standard-RAG | B2: LightRAG (T=0) | B3: LightRAG (T=1) |
|--------|:-:|:-:|:-:|
| Ø Precision | 0,71 | 1,00 | 1,00 |
| Ø Recall | 0,22 | 0,53 | 0,53 |
| **Ø F1** | **0,33** | **0,65** | **0,68** |
| Ø Citation Acc. | 0,33 | 0,67 | 0,67 |

### 5-Hop

| Metrik | B1: Standard-RAG | B2: LightRAG (T=0) | B3: LightRAG (T=1) |
|--------|:-:|:-:|:-:|
| Ø Precision | 0,50 | 0,83 | 0,25 |
| Ø Recall | 0,15 | 0,50 | 0,20 |
| **Ø F1** | **0,23** | **0,63** | **0,22** |
| Ø Citation Acc. | 0,30 | 0,20 | 0,50 |

---

## 3. Gesamtdurchschnitt (alle 8 Fragen)

| Metrik | B1: Standard-RAG | B2: LightRAG (T=0) | B3: LightRAG (T=1) |
|--------|:-:|:-:|:-:|
| Ø Precision | 0,62 | 0,85 | 0,81 |
| Ø Recall | 0,28 | 0,51 | 0,50 |
| **Ø F1** | **0,37** | **0,59** | **0,61** |
| Ø Citation Acc. | 0,39 | 0,57 | 0,54 |

**Hinweis:** B3 erreicht den höchsten Ø F1 (0,61), obwohl sowohl Ø Precision (0,81 < 0,85) als auch Ø Recall (0,50 < 0,51) niedriger sind als bei B2. Dies ergibt sich daraus, dass Ø F1 als arithmetisches Mittel der acht einzelnen F1-Werte berechnet wird, nicht aus Ø Precision und Ø Recall. B3 erzielt bei 6 von 8 Fragen einen höheren F1-Wert als B2 (ausgeglichenere P/R-Verhältnisse pro Frage), fällt jedoch bei den beiden 5-Hop-Fragen deutlich ab (Frage 7: F1 = 0,00).

Berechnung Ø F1:
- B1: (0,74+0,80+0,33+0,00+0,26+0,40+0,00+0,46)/8 = 2,99/8 = 0,37
- B2: (0,53+0,77+0,67+0,18+0,90+0,40+0,50+0,75)/8 = 4,70/8 = 0,59
- B3: (0,67+0,91+0,77+0,75+0,81+0,55+0,00+0,44)/8 = 4,90/8 = 0,61

---

## 4. Scorecard F1

| Frage | Hops | Gewinner |
|-------|------|----------|
| 1 Löschrecht | 2 | Standard-RAG |
| 2 AVV Personio | 2 | LightRAG B3 |
| 3 DSFA | 3 | LightRAG B3 |
| 4 Speicherfristen | 3 | LightRAG B3 |
| 5 Microsoft 365 | 4 | LightRAG B2 |
| 6 Lieferanten | 4 | LightRAG B3 |
| 7 Personal Drittland | 5 | LightRAG B2 |
| 8 Rezeption Drittland | 5 | LightRAG B2 |
| **Gesamt** | | **LightRAG 7 – Standard-RAG 1** |

---

## 5. T=0 vs T=3 Vergleich F1 (Temperatur-Effekt)

| Frage | Hops | B2 (T=0) | B3 (T=1) | Unterschied |
|-------|------|----------|----------|-------------|
| 1 | 2 | 0,53 | **0,67** | B3 +0,14 |
| 2 | 2 | 0,77 | **0,91** | B3 +0,14 |
| 3 | 3 | 0,67 | **0,77** | B3 +0,10 |
| 4 | 3 | 0,18 | **0,75** | B3 +0,57 |
| 5 | 4 | **0,90** | 0,81 | B2 +0,09 |
| 6 | 4 | 0,40 | **0,55** | B3 +0,15 |
| 7 | 5 | **0,50** | 0,00 | B2 +0,50 |
| 8 | 5 | **0,75** | 0,44 | B2 +0,31 |

**Befund:** B3 (T=1) ist bei 2–4 Hops überlegen (6 von 6 Fragen). B2 (T=0) ist bei 5-Hop überlegen (2 von 2). Bei 5-Hop bricht B3 ein durch falsche Dienstleister-Zuordnungen (Microsoft 365, Google LLC als FP). Bei n=1 pro Frage kein belastbarer systematischer Temperature-Effekt.

---

## 6. Citation Accuracy

| Frage | Hops | B1 CA | B2 CA | B3 CA |
|-------|------|-------|-------|-------|
| 1 Löschrecht | 2 | 1,00 | 0,50 | 0,50 |
| 2 AVV Personio | 2 | 0,50 | 1,00 | 0,50 |
| 3 DSFA | 3 | 0,33 | 1,00 | 0,67 |
| 4 Speicherfristen | 3 | 0,00 | 0,33 | 0,33 |
| 5 Microsoft 365 | 4 | 0,67 | 1,00 | 1,00 |
| 6 Lieferanten | 4 | 0,00 | 0,33 | 0,33 |
| 7 Personal Drittland | 5 | 0,20 | 0,20 | 0,40 |
| 8 Rezeption Drittland | 5 | 0,40 | 0,20 | 0,60 |
| **Ø Gesamt** | | **0,39** | **0,57** | **0,54** |
