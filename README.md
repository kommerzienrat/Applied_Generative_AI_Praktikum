# Praktikum: Applied Generative AI – NLP

Dieses Repository enthält die Jupyter-Notebooks für das Praktikum im Sommersemester 2026. Die Materialien decken den Bogen von Entwicklungsumgebung, Transformer-Grundlagen und Prompting bis hin zu RAG, Agenten, Security, Evaluation und Deployment ab.

## Inhalte

| Notebook | Termin | Thema |
|----------|--------|-------|
| `P01_Entwicklungsumgebung.ipynb` | 01 | Setup & Ollama-Grundlagen |
| `P02_Tokenizer_Embeddings_MLP.ipynb` | 02 | Tokenisierung, Embeddings & MLP |
| `P03_Transformer_Attention.ipynb` | 03 | Transformer-Architektur & Attention |
| `P04_Halluzinationen_Perplexity.ipynb` | 04 | Halluzinationen & Perplexity |
| `P05_Prompting_InContextLearning.ipynb` | 05 | Prompt-Engineering & In-Context Learning |
| `P06_RAG_Systeme.ipynb` | 06 | RAG-Pipeline, ChromaDB, Chunking & Generation |
| `P07_Finetuning_PEFT.ipynb` | 07 | LoRA, QLoRA & Parameter-Efficient Fine-Tuning |
| `P08_Hardware_Inferenz.ipynb` | 08 | GPU-Speicher, KV-Cache, Quantisierung |
| `P09_Agenten_MCP.ipynb` | 09 | ReAct-Pattern & Model Context Protocol |
| `P10_Evaluation_Benchmarks.ipynb` | 10 | RAG-Evaluation, RAGAS & LLM-as-Judge |
| `P11_Ethik_Sicherheit_Recht.ipynb` | 11 | EU AI Act, OWASP Top 10, Bias & Datenschutz |
| `P12_Zusammenfassung_Wiederholung.ipynb` | 12 | Capstone-Session & Semester-Review |

## Ausführungswege

Die Notebooks sind für zwei Nutzungsszenarien gedacht:

- lokal mit `uv`, virtuellem Environment und Jupyter
- in Google Colab für die frühen, nicht lokal gebundenen Übungen

In beiden Fällen gilt:

- Die Notebooks sollen mit `Run All` von oben nach unten durchlaufen können, wenn alle Voraussetzungen erfüllt sind.
- Wesentliche Fehler dürfen nicht verschleiert oder stillschweigend übersprungen werden.
- Installationen innerhalb der Notebooks sollen über `uv` erfolgen.
- Die Materialien sollen auf Standard-Laptops ohne GPU lauffähig bleiben.
- Zielplattform ist auch Python 3.13.

## Lokaler Start mit uv

### Voraussetzungen

- Python 3.11 bis 3.13
- `uv`
- JupyterLab oder Jupyter Notebook
- Ollama für alle LLM-bezogenen Notebooks

### Installation von uv, pip und Jupyter

#### Option 1: Mit uv (empfohlen)

`uv` ist ein extrem schneller Python-Paketmanager, der Abhängigkeiten effizienter verwaltet als pip.

**Installation von uv:**
```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (mit winget)
winget install AstralEq.uv
```

**Einrichtung eines Projekts mit Jupyter:**
```bash
# Neues Projekt initialisieren
uv init mein-projekt
cd mein-projekt

# Virtuelle Umgebung erstellen und aktivieren
uv venv
source .venv/bin/activate  # Linux/macOS
# oder: .venv\Scripts\activate  # Windows

# Jupyter und Abhängigkeiten installieren
uv add jupyterlab ipykernel nbconvert
uv pip install -r requirements.txt

# Jupyter-Kernel registrieren (optional)
python -m ipykernel install --user --name praktikum --display-name "Python (praktikum)"

# Jupyter starten
jupyter lab
```

#### Option 2: Mit pip (traditionell)

Falls Sie pip bevorzugen:

```bash
# Virtuelle Umgebung erstellen
python3 -m venv .venv
source .venv/bin/activate  # Linux/macOS
# oder: .venv\Scripts\activate  # Windows

# pip und Jupyter installieren
python -m pip install --upgrade pip
pip install jupyterlab ipykernel nbconvert -r requirements.txt

# Jupyter-Kernel registrieren (optional)
python -m ipykernel install --user --name praktikum --display-name "Python (praktikum)"

# Jupyter starten
jupyter lab
```

#### Wichtige Hinweise

- **Verwenden Sie virtuelle Umgebungen**, um Abhängigkeitskonflikte zu vermeiden.
- **`uv` vs. pip**: `uv` ist deutlich schneller und moderner, `pip` ist universell verfügbar.
- **Colab-spezifisch**: In Google Colab ist `uv` bereits vorinstalliert, kann aber spezielle Umgebungsvariablen benötigen (siehe Colab-Abschnitt).

### Paketinstallation in lokalen Notebooks

Wenn ein Notebook weitere Abhängigkeiten nachinstallieren muss, ist `uv` das primäre Werkzeug:

- innerhalb einer aktiven virtuellen Umgebung: `uv pip install ...`
- außerhalb einer virtuellen Umgebung: `uv pip install --system ...`

Fehlende Voraussetzungen sollen einen harten Fehler erzeugen, statt nur als Warnung ausgegeben zu werden.

## Google Colab

P01 bis P05 lassen sich auch in Colab als eigenständige Arbeitsblätter bearbeiten. Für P06 bis P12 ist die Referenzausführung derzeit lokal vorgesehen, weil diese Notebooks einen lokalen Ollama-Dienst über `OLLAMA_BASE_URL` voraussetzen und bei entfernten Hosts absichtlich mit einem harten Fehler abbrechen.

### Voraussetzungen in Colab

- Python-Runtime in Colab
- Installation der benötigten Pakete über `uv`
- für geeignete LLM-Notebooks: ein erreichbarer Modellzugang für die konkrete Übung

### Minimaler Colab-Start

```bash
!pip install -q uv
!uv pip install --system -r requirements.txt jupyterlab ipykernel nbconvert
```

**Achtung**: Google Colab setzt spezielle Umgebungsvariablen für `uv`, die zu Problemen führen können. Verwenden Sie folgende Methode für zuverlässige Installation:

```python
import os
os.environ["UV_CONSTRAINT"] = ""
os.environ["UV_BUILD_CONSTRAINT"] = ""
os.environ["UV_PRERELEASE"] = "if-necessary-or-explicit"
os.environ["UV_SYSTEM_PYTHON"] = "false"

!uv pip install --system -r requirements.txt jupyterlab ipykernel nbconvert
```

Für Notebooks mit LLM- oder Embedding-Zugriff müssen zusätzlich die benötigten Modelle verfügbar sein. Je nach Notebook ist das typischerweise:

```bash
!curl https://ollama.ai/install.sh | sh
!ollama pull qwen3.5:0.8b
!ollama pull nomic-embed-text
```

**Ollama in Colab**: Die Installation von Ollama in Colab ist möglich, erfordert aber zusätzliche Schritte. Verwenden Sie für den Remote-Zugriff einen Tunnel-Dienst wie ngrok oder cloudflared.

Wichtig: Die späteren Ollama-Notebooks P06 bis P12 verwenden aktuell keinen generischen Remote-Endpoint über `LLM_BASE_URL`, sondern prüfen explizit auf einen lokalen Ollama-Dienst unter `OLLAMA_BASE_URL`.

Auch in Colab gilt: Wenn Modelle, Bibliotheken oder Dienste fehlen, soll das Notebook mit einem klaren Fehler abbrechen.

## Ollama-Setup

Mehrere Notebooks erwarten einen laufenden Ollama-Dienst sowie kleine Modelle, damit die Übungen auf Standard-Laptops flüssig bleiben. Für P06 bis P12 ist aktuell eine lokale Ollama-Instanz Teil der Voraussetzungen.

### Lokale Installation (macOS/Linux)

```bash
# Ollama installieren (curl erforderlich)
curl -fsSL https://ollama.com/install.sh | sh

# Modell herunterladen
ollama pull qwen3.5:0.8b
ollama pull nomic-embed-text

# Ollama-Server starten
ollama serve
```

### Lokale Installation (Windows)

Ollama für Windows kann direkt von [ollama.com](https://ollama.com) heruntergeladen werden.

### Colab-Installation

In Google Colab muss Ollama manuell installiert werden. Zusätzlich wird `zstandard` für erweiterte Funktionalität empfohlen:

```python
# curl und Ollama installieren
!pip install -q uv zstandard
!curl -fsSL https://ollama.com/install.sh | sh

# Modell herunterladen
!ollama pull qwen3.5:0.8b

# Server im Hintergrund starten
!nohup ollama serve &
```

**Alternative mit colab-xterm (funktioniert auch im Free-Tier):**
```python
!pip install colab-xterm zstandard
%load_ext colabxterm
%xterm
# Dann im Terminal: curl -fsSL https://ollama.com/install.sh | sh
# Und: ollama pull qwen3.5:0.8b
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

## Hinweise für Maintainer

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

Die Notebooks sind didaktisch so angelegt, dass sie auch außerhalb einer GPU-Umgebung nutzbar bleiben. Die Referenzausführung ist für P01 bis P05 lokal oder in Colab möglich; ab P06 ist aktuell ein lokaler Ollama-Dienst Teil der vorgesehenen Ausführung.
