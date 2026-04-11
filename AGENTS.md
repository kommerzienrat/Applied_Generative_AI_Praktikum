# Praktikum: Applied Generative AI – NLP (Sommersemester 2026)

Dieses Projekt umfasst die Jupyter-Notebooks für das Praktikum.

## Notebook-Design-Mandate (BINDEND)

### 1. Keine Fehlerverschleierung ("Safety Nets")
- Notebooks dürfen **keine** `try-except`-Blöcke oder `if`-Bedingungen enthalten, die wesentliche Fehler (z. B. fehlende Bibliotheken, fehlende Ollama-Modelle) nur als Warnung ausgeben oder Teile lautlos überspringen.
- Wenn eine Voraussetzung fehlt, **MUSS** das Notebook mit einem harten Fehler (`RuntimeError`, `ImportError`, etc.) abbrechen.
- Studenten sollen gezwungen sein, das Problem (z. B. Modell mit `ollama pull` laden) zu beheben, bevor sie fortfahren können.

### 2. Durchlauffähigkeit & Stabilität
- Ein Notebook muss von oben nach unten ("Run All") fehlerfrei durchlaufen können, sofern alle Voraussetzungen erfüllt sind.
- **Python 3.13 Kompatibilität**: Alle Notebooks müssen unter Python 3.13 stabil laufen. Künstliche Python-Versionssperren sind untersagt.
- **Durchlaufzeiten**: Benchmarks und Trainingsepochen (z. B. in P02) sind so zu wählen, dass der Durchlauf insgesamt zügig (wenige Minuten) erfolgt.

### 3. Paketmanagement & Umgebung
- Primäres Tool für alle Installationen innerhalb der Notebooks ist `uv`.
- Der Befehl `uv pip install --system` (außerhalb von Venvs) bzw. `uv pip install` (innerhalb von Venvs) ist konsequent zu nutzen.
- **Ollama Versionen**: CLI-Version (aktuell v0.20.x) und Python-Library (aktuell v0.6.1) sind konsistent zu halten.

### 4. Zustand der Auslieferung
- Original-Notebooks müssen in einem **sauberen Zustand** (keine Outputs, keine Execution Counts) vorliegen.
- Getestete Versionen werden separat (z. B. als `*_tested.ipynb`) gespeichert, um die Originale nicht zu verändern.

## Projektstruktur
- `P01_Entwicklungsumgebung.ipynb`: Setup & erste Ollama-Schritte.
- `P02_Tokenizer_Embeddings_MLP.ipynb`: Tokenisierung & MLP-Training (MNIST).
- `P03_Transformer_Attention.ipynb`: Transformer-Details & Visualisierung.
- `P04_Halluzinationen_Perplexity.ipynb`: Halluzinationen & Reasoning-Modelle.
- `P05_Prompting_InContextLearning.ipynb`: Prompt-Engineering Strategien.
