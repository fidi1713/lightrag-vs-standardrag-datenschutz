# LightRAG vs. Standard-RAG: Ein empirischer Vergleich der Antwortqualität bei Multi-Hop-Datenschutzfragen


Dieses Repository enthält die vollständigen Experimentdaten zur Nachvollziehbarkeit der Untersuchung: alle 24 Einzelbewertungen (8 Multi-Hop-Datenschutzfragen × 3 Konfigurationen), die Bewertungsmethodik sowie den verwendeten Dokumentenkorpus.

## Inhalt

| Pfad | Inhalt |
|------|--------|
| `bewertungsmethodik.md` | Vorgehen der Antwortbewertung (LLM-as-Judge mit Claude Opus 4.6, manuelle Nachprüfung, Definition von TP/FP/FN, Berechnung von Precision/Recall/F1/Citation Accuracy) |
| `ergebnisse_gesamt.md` | Übersichtstabellen aller Einzel- und Durchschnittswerte (entspricht Tab. 4 und Tab. 5 in der Projektarbeit) |
| `einzelbewertungen/` | Detailbewertungen pro Frage und Konfiguration, gegliedert nach Hop-Stufe |
| `korpus/` | Verwendeter Dokumentenkorpus (Text-Dateien zu fiktiven Unternehmen, Tools, Datenschutzregelungen) |

## Konfigurationen

| Kürzel | System | Temperatur (KG-Aufbau / Antwort) |
|--------|--------|----------------------------------|
| Standard-RAG | Chunk-basiertes RAG | – / 0,0 |
| LightRAG (T=0) | Graph-basiertes RAG | 0,0 / 0,0 |
| LightRAG (T=1) | Graph-basiertes RAG | 1,0 / 0,0 |

## Bezug zur Projektarbeit

Im Text der Projektarbeit wird auf dieses Repository als Quelle für die vollständigen Einzelbewertungen verwiesen. Der Kapitel-4-Text fasst die Ergebnisse zusammen; die Detailprüfung (Claims pro Frage, TP/FP/FN-Klassifikation, LiteLLM-Protokoll-Auszüge) erfolgt hier.

## Rechte

Alle Rechte vorbehalten. Eine Nutzung, Vervielfältigung oder Weiterverbreitung der Inhalte — ganz oder in Teilen — bedarf der vorherigen schriftlichen Zustimmung des Autors.
