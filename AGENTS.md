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
- Stoff muss für insg. 90  min reichen.

### 3. Paketmanagement & Umgebung
- Primäres Tool für alle Installationen innerhalb der Notebooks ist `uv`.
- Der Befehl `uv pip install --system` (außerhalb von Venvs) bzw. `uv pip install` (innerhalb von Venvs) ist konsequent zu nutzen.
- **Ollama Versionen**: CLI-Version (aktuell v0.20.x) und Python-Library (aktuell v0.6.1) sind konsistent zu halten.

### 4. Zustand der Auslieferung
- Original-Notebooks müssen in einem **sauberen Zustand** (keine Outputs, keine Execution Counts) vorliegen.
- Getestete Versionen werden separat (z. B. als `*_tested.ipynb`) gespeichert, um die Originale nicht zu verändern.

## Erstellungs- & Verifizierungsworkflow

### 1. Inhaltsbasierte Erstellung
- Neue Notebooks (z. B. P06–P08) werden strikt auf Basis des Semesterplans (`Semesterplan_lang.docx`) erstellt.
- Die Inhalte müssen für Studierende verständlich und auf Standard-Laptops (auch ohne GPU) ausführbar sein.

### 2. Plattformunabhängigkeit
- Alle Notebooks müssen **Standalone** funktionieren (Linux, Windows, macOS und Google Colab).
- Hardware-Schonung: Verwendung kleiner Modelle (z. B. 0.8B Parameter), um flüssige Ausführung auf MacBook Air / Office-Laptops zu gewährleisten.
- **Ollama-Installation**: Muss auf allen Plattformen funktionieren:
  - `curl` ist erforderlich für die Ollama-Installation (macOS/Linux vorinstalliert, Windows über ollama.com)
  - `zstandard` Python-Paket wird für erweiterte Funktionalität empfohlen
  - Colab: Ollama muss manuell installiert werden mit `curl -fsSL https://ollama.com/install.sh | sh`
- **Cross-Platform Code**: Keine plattformspezifischen Pfade oder Befehle fest einprogrammieren
- Environment-Variablen nutzen: `OLLAMA_BASE_URL`, `LLM_MODEL` etc.

### 3. Verifizierungspflicht
- Jedes Notebook MUSS vor der Freigabe einmal komplett ("Run All") in einer sauberen Umgebung ausgeführt werden.
- **Modell-Validierung**: Die Outputs der LLM-Modelle (z. B. Reasoning-Pfade, Extraktionsergebnisse) müssen explizit auf ihre inhaltliche Sinnhaftigkeit ("Sinnhaftigkeit") geprüft werden.

### 4. Misc
- Nutze Umlaute, also ä statt ae, um die Lesbarkeit zu verbessern.
- Alle Notebooks müssen in einem einheitlichen Stil (z. B. Markdown-Formatierung, Code-Kommentare) erstellt werden, um die Konsistenz zu gewährleisten.

## Projektstruktur
- `P01_Entwicklungsumgebung.ipynb`: Setup & erste Ollama-Schritte (Termin 01).
- `P02_Tokenizer_Embeddings_MLP.ipynb`: Tokenisierung, Embeddings & MLP-Training (Termin 02).
- `P03_Transformer_Attention.ipynb`: Transformer-Architektur & Attention-Mechanismen (Termin 03).
- `P04_Halluzinationen_Perplexity.ipynb`: Halluzinationen, Perplexity & LLMs (Termin 04).
- `P05_Prompting_InContextLearning.ipynb`: Prompt-Engineering & Zero/Few-Shot Learning (Termin 05).
- `P06_RAG_Systeme.ipynb`: RAG-Pipeline, ChromaDB, Chunking & Generation (Termin 06).
- `P07_Finetuning_PEFT.ipynb`: LoRA, QLoRA & Parameter-Efficient Fine-Tuning (Termin 07).
- `P08_Hardware_Inferenz.ipynb`: GPU-Speicher, KV-Cache, Quantisierung & Serving (Termin 08).
- `P09_Agenten_MCP.ipynb`: ReAct-Pattern, Tool Use & Model Context Protocol (Termin 09).
- `P10_Evaluation_Benchmarks.ipynb`: RAG-Evaluation, RAGAS & LLM-as-Judge (Termin 10).
- `P11_Ethik_Sicherheit_Recht.ipynb`: EU AI Act, OWASP Top 10, Bias & Datenschutz (Termin 11).
- `P12_Zusammenfassung_Wiederholung.ipynb`: Capstone-Session & Semester-Review (Termin 12).
