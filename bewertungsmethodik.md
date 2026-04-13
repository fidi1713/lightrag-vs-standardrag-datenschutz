# Bewertungsmethodik – RAGAS Factual Correctness

> Diese Datei definiert das vollständige Bewertungsverfahren für alle 24 Antworten (8 Fragen × 3 Bedingungen).
> Jede Berechnung muss gegen diese Definitionen geprüft werden.

---

## 1. Bewertungsverfahren (zweistufig)

### Stufe 1: Automatisierte Bewertung (LLM-as-Judge)

Claude Opus 4.6 bewertet jede generierte Antwort anhand eines strukturierten Verfahrens gegen die Referenzantwort (Anhang 10.3).

### Stufe 2: Manuelle Nachprüfung (Autor)

Der Autor prüft jede automatisierte Bewertung manuell nach, um domänenspezifische Nuancen korrekt zu erfassen.

---

## 2. Bewertungsschritte pro Antwort

### Schritt 1 – Referenz-Claims prüfen (→ TP und FN)

Jede erwartete Aussage (F1–Fn) aus dem Anhang wird gegen die Systemantwort geprüft:

| Bewertung | TP-Beitrag | FN-Beitrag | Kriterium |
|-----------|:--:|:--:|-----------|
| Vollständig adressiert | 1,0 | 0,0 | Aussage der Referenzantwort ist in der Systemantwort vollständig und konkret enthalten |
| Partiell adressiert | 0,5 | 0,5 | Aussage ist konzeptionell erkennbar, aber unvollständig oder vage formuliert (z.B. "gesetzliche Gründe" statt "Art. 17 Abs. 3 lit. b") |
| Nicht adressiert | 0,0 | 1,0 | Aussage ist nicht erwähnt oder zu weit vom Referenz-Claim entfernt |

**Berechnung:**
- **TP** = Summe aller TP-Beiträge
- **FN** = Summe aller FN-Beiträge = Anzahl Referenz-Claims − TP

**Kontrolle:** TP + FN = Anzahl Referenz-Claims (muss immer stimmen!)

### Schritt 2 – Response-Claims prüfen (→ FP)

Die Systemantwort wird auf zusätzliche Aussagen geprüft, die nicht in der Referenz enthalten sind.

**FP-Definition (Relevanzfilter):**

| Aussage ist... | Bewertung | Beispiel |
|----------------|:---------:|---------|
| Inhaltlich falsch | **FP** | "Art. 35 Abs. 3 lit. b = hohes Risiko" (falsche Zuordnung) |
| Fachlich korrekt aber irrelevant für die Frage | **FP** | Art. 18 (Einschränkung) bei einer Löschfrage |
| Fachlich korrekt UND thematisch relevant | **kein FP** | Art. 5 Abs. 1 lit. e (Speicherbegrenzung) bei Löschfrage |

**Berechnung:**
- **FP** = Anzahl der als FP klassifizierten zusätzlichen Aussagen

---

## 3. Metriken pro Frage

### Precision (Korrektheit)

```
Precision = TP / (TP + FP)
```

Misst: Wie viele der gemachten Aussagen sind korrekt und relevant?

**Sonderfall:** Wenn TP = 0 und FP = 0 → Precision ist nicht definiert (–)

### Recall (Vollständigkeit)

```
Recall = TP / (TP + FN)
```

Entspricht: TP / Anzahl Referenz-Claims

Misst: Wie viel der erwarteten Referenzinformation wurde abgedeckt?

### F1-Score

```
F1 = 2 × Precision × Recall / (Precision + Recall)
```

**Harmonisches Mittel** von Precision und Recall. Bestraft Ungleichgewichte stärker als das arithmetische Mittel.

Beispiel: P = 1,00 und R = 0,10 → arithmetisch wäre 0,55, **F1 = 0,18**

**Sonderfall:** Wenn TP = 0 → F1 = 0,0

### Citation Accuracy

```
Citation Accuracy = korrekt zitierte Quellen / erwartete Quellen
```

Eine Quelle zählt als "korrekt zitiert", wenn sie in der Quellenliste der Systemantwort erscheint.

---

## 4. Durchschnitte pro Hop-Stufe

Alle Durchschnitte sind **arithmetische Mittel** der Einzelwerte:

```
Ø P = (P_Frage_a + P_Frage_b) / 2
Ø R = (R_Frage_a + R_Frage_b) / 2
Ø F1 = (F1_Frage_a + F1_Frage_b) / 2
Ø Citation Acc. = (CA_Frage_a + CA_Frage_b) / 2
```

**WICHTIG:** Ø F1 wird aus den einzelnen F1-Werten berechnet, **NICHT** aus Ø P und Ø R!

---

## 5. Kontrollprüfungen

Vor Abgabe jeder Bewertung folgende Kontrollen durchführen:

| Prüfung | Formel | Muss gelten |
|---------|--------|-------------|
| TP + FN = Referenz-Claims | z.B. TP=2,5 + FN=3,5 = 6 | Immer = Anzahl F1–Fn |
| Precision ≤ 1,0 | TP / (TP + FP) | Immer |
| Recall ≤ 1,0 | TP / (TP + FN) | Immer |
| F1 ≤ min(P, R) × 2 | Harmonisches Mittel ≤ arithmetisches Mittel | Immer |
| F1 = 0 wenn TP = 0 | Unabhängig von FP | Immer |

---

## 6. Dokumentationsformat pro Antwort

```markdown
**Schritt 1 – Referenz-Claims:**

| Aussage | Typ | Score | Begründung |
|---------|-----|-------|------------|
| F1: ... | TP/FN | 1,0/0,5/0,0 | ... |

**Schritt 2 – Zusätzliche Response-Claims:**

| Aussage | Typ | Begründung |
|---------|-----|------------|
| ... | FP/– | ... |

**Zusammenfassung: TP = x | FP = y | FN = z**
Kontrolle: TP + FN = [Anzahl Referenz-Claims] ✓

| Metrik | Score | Berechnung |
|--------|-------|------------|
| Precision | ... | TP/(TP+FP) |
| Recall | ... | TP/(TP+FN) |
| F1 | ... | 2×P×R/(P+R) |
| Citation Acc. | ... | x/y |
```
