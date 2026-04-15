# Praktikum: Applied Generative AI – NLP

Dieses Repository enthält die Jupyter-Notebooks für das Praktikum im Sommersemester 2026. Die Materialien decken den Bogen von Entwicklungsumgebung, Transformer-Grundlagen und Prompting bis hin zu RAG, Agenten, Security, Evaluation und Deployment ab.

## Inhalte

- `P01_Entwicklungsumgebung.ipynb`: Setup, Ollama-Grundlagen und erste lokale Modellaufrufe.
- `P02_Tokenizer_Embeddings_MLP.ipynb`: Tokenisierung, Embeddings und ein kompaktes MLP-Beispiel.
- `P03_Transformer_Attention.ipynb`: Attention-Mechanismen, Transformer-Bausteine und Visualisierung.
- `P04_Halluzinationen_Perplexity.ipynb`: Halluzinationen, Perplexity und reasoning-nahe Modellvergleiche.
- `P05_Prompting_InContextLearning.ipynb`: Prompt-Engineering, In-Context Learning und Chain-of-Thought.
- `P06_WebScraping_Embeddings.ipynb`: Web-Scraping, Chunking und Embedding-Engineering.
- `P07_Vektordatenbanken_RAG.ipynb`: ChromaDB, Retrieval-Pipelines und faktentreues RAG.
- `P08_Reasoning_Agenten.ipynb`: ReAct, Reflection und einfache Agenten-Architekturen.
- `P09_AdvancedAgents_Security.ipynb`: Red Teaming, Prompt Injection und Moderations-Layer.
- `P10_Evaluation_Benchmarks.ipynb`: Golden Datasets, Faithfulness und Benchmarking von RAG-Systemen.
- `P11_Deployment_Quantization.ipynb`: Modelfiles, API-Wrapper und Deployment-Konzepte.
- `P12_Zusammenfassung_Wiederholung.ipynb`: Capstone-Session, Architekturreflexion und Semester-Review.

## Ausfuehrungswege

Die Notebooks sind fuer zwei Nutzungsszenarien gedacht:

- lokal mit `uv`, virtuellem Environment und Jupyter
- in Google Colab fuer die fruehen, nicht lokal gebundenen Uebungen

In beiden Faellen gilt:

- Die Notebooks sollen mit `Run All` von oben nach unten durchlaufen koennen, wenn alle Voraussetzungen erfuellt sind.
- Wesentliche Fehler duerfen nicht verschleiert oder stillschweigend uebersprungen werden.
- Installationen innerhalb der Notebooks sollen ueber `uv` erfolgen.
- Die Materialien sollen auf Standard-Laptops ohne GPU lauffaehig bleiben.
- Zielplattform ist auch Python 3.13.

## Lokaler Start mit uv

### Voraussetzungen

- Python 3.11 bis 3.13
- `uv`
- JupyterLab oder Jupyter Notebook
- Ollama fuer alle LLM-bezogenen Notebooks

### Empfohlenes Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip uv
uv pip install -r requirements.txt jupyterlab ipykernel nbconvert
```

Optionales Kernel-Setup:

```bash
python -m ipykernel install --user --name praktikum --display-name "Python (praktikum)"
```

Jupyter starten:

```bash
jupyter lab
```

### Paketinstallation in lokalen Notebooks

Wenn ein Notebook weitere Abhaengigkeiten nachinstallieren muss, ist `uv` das primaere Werkzeug:

- innerhalb einer aktiven virtuellen Umgebung: `uv pip install ...`
- ausserhalb einer virtuellen Umgebung: `uv pip install --system ...`

Fehlende Voraussetzungen sollen einen harten Fehler erzeugen, statt nur als Warnung ausgegeben zu werden.

## Google Colab

P01 bis P05 lassen sich auch in Colab als eigenstaendige Arbeitsblaetter bearbeiten. Fuer P06 bis P12 ist die Referenzausfuehrung derzeit lokal vorgesehen, weil diese Notebooks einen lokalen Ollama-Dienst ueber `OLLAMA_BASE_URL` voraussetzen und bei entfernten Hosts absichtlich mit einem harten Fehler abbrechen.

### Voraussetzungen in Colab

- Python-Runtime in Colab
- Installation der benoetigten Pakete ueber `uv`
- fuer geeignete LLM-Notebooks: ein erreichbarer Modellzugang fuer die konkrete Uebung

### Minimaler Colab-Start

```bash
!pip install -q uv
!uv pip install --system -r requirements.txt jupyterlab ipykernel nbconvert
```

Fuer Notebooks mit LLM- oder Embedding-Zugriff muessen zusaetzlich die benoetigten Modelle verfuegbar sein. Je nach Notebook ist das typischerweise:

```bash
!ollama pull qwen3.5:0.8b
!ollama pull nomic-embed-text
```

Wichtig: Die spaeteren Ollama-Notebooks P06 bis P12 verwenden aktuell keinen generischen Remote-Endpoint ueber `LLM_BASE_URL`, sondern pruefen explizit auf einen lokalen Ollama-Dienst unter `OLLAMA_BASE_URL`.

Auch in Colab gilt: Wenn Modelle, Bibliotheken oder Dienste fehlen, soll das Notebook mit einem klaren Fehler abbrechen.

## Ollama-Setup

Mehrere Notebooks erwarten einen laufenden Ollama-Dienst sowie kleine Modelle, damit die Uebungen auf Standard-Laptops fluesig bleiben. Fuer P06 bis P12 ist aktuell eine lokale Ollama-Instanz Teil der Voraussetzungen.

```bash
ollama pull qwen3.5:0.8b
ollama pull nomic-embed-text
ollama serve
```

Hinweise:

- `qwen3.5:0.8b` wird in mehreren Chat-, Prompting-, Agenten- und Evaluationsnotebooks verwendet.
- `nomic-embed-text` wird für Embeddings, Retrieval und RAG benötigt.
- Die Ollama-CLI-Version und die Python-Bibliothek sollen konsistent gehalten werden.
- Einzelne Notebooks erzeugen zusätzlich lokale Artefakte wie persistente ChromaDB-Verzeichnisse oder Modelfiles im Arbeitsverzeichnis.

## Arbeitsweise der Notebooks

- Notebooks sollen von oben nach unten mit `Run All` ausführbar sein, sofern die Voraussetzungen erfüllt sind.
- Wesentliche Fehler sollen nicht verschleiert werden. Fehlende Pakete, Modelle oder Dienste sind zu beheben, statt Zellen stillschweigend zu überspringen.
- Installationen innerhalb der Notebooks sollen über `uv` erfolgen: in virtuellen Umgebungen mit `uv pip install`, außerhalb davon mit `uv pip install --system`.
- Original-Notebooks sollen ohne Outputs und ohne Execution Counts im Repository liegen. Getestete Varianten gehören in separate Dateien wie `*_tested.ipynb`.

## Hinweise fuer Maintainer

- Dokumentation und Notebook-Inhalt sollen die Vorgaben aus `AGENTS.md` einhalten.
- Neue Notebooks sollen inhaltlich am Semesterplan ausgerichtet und auf Linux, macOS, Windows und Colab nutzbar sein.
- Vor Freigabe sollte jedes Notebook einmal komplett in sauberer Umgebung getestet werden.

## Empfohlene Reihenfolge

1. `P01_Entwicklungsumgebung.ipynb`
2. `P02_Tokenizer_Embeddings_MLP.ipynb`
3. `P03_Transformer_Attention.ipynb`
4. `P04_Halluzinationen_Perplexity.ipynb`
5. `P05_Prompting_InContextLearning.ipynb`
6. `P06_WebScraping_Embeddings.ipynb`
7. `P07_Vektordatenbanken_RAG.ipynb`
8. `P08_Reasoning_Agenten.ipynb`
9. `P09_AdvancedAgents_Security.ipynb`
10. `P10_Evaluation_Benchmarks.ipynb`
11. `P11_Deployment_Quantization.ipynb`
12. `P12_Zusammenfassung_Wiederholung.ipynb`

## Projektstruktur

- `data/`: optionale Datenablage und lokale Arbeitsartefakte.
- `exportToHTML/`: optionale HTML-Exporte der Notebooks, wird bei Bedarf erzeugt.
- `requirements.txt`: zentrale Python-Abhängigkeiten für das Praktikum.
- `pyproject.toml`: Projektmetadaten und zusätzliche Python-Abhängigkeiten.

## Hinweis zu Colab

Die Notebooks sind didaktisch so angelegt, dass sie auch außerhalb einer GPU-Umgebung nutzbar bleiben. Die Referenzausfuehrung ist fuer P01 bis P05 lokal oder in Colab moeglich; ab P06 ist aktuell ein lokaler Ollama-Dienst Teil der vorgesehenen Ausfuehrung.
