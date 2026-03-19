# Praktikum Notebooks: Lokal und Google Colab Quickstart

Dieses Repository enthaelt 5 Jupyter-Notebooks fuer das Praktikum:

- P01_Entwicklungsumgebung.ipynb
- P02_Tokenizer_Embeddings_MLP.ipynb
- P03_Transformer_Attention.ipynb
- P04_Halluzinationen_Perplexity.ipynb
- P05_Prompting_InContextLearning.ipynb

## 1) Lokaler Start (empfohlen)

### Voraussetzungen

- Python 3.11+
- Jupyter Notebook oder Jupyter Lab
- Optional fuer LLM-Notebooks: Ollama

### Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install jupyter ipykernel
```

Optionaler Kernel-Name:

```bash
python -m ipykernel install --user --name praktikum-llm --display-name "Python (praktikum-llm)"
```

Dann Jupyter starten:

```bash
jupyter lab
```

Hinweis: Die Setup-Zellen in den Notebooks installieren fehlende Pakete versionsfixiert nach.

## 2) Google Colab Start

### Fuer P02 und P03

Diese Notebooks benoetigen keinen Remote-LLM-Endpoint.
Einfach Notebook oeffnen und die Setup-Zelle ausfuehren.

### Fuer P04 und P05

Es gibt zwei zulaessige Modi in Colab:

1. Remote OpenAI-kompatibler Endpoint

Setze in der ersten Colab-Startzelle vor der Setup-Ausfuehrung:

```python
import os
os.environ["LLM_BASE_URL"] = "https://<dein-endpoint>/v1"
os.environ["LLM_API_KEY"] = "<optional>"
os.environ["LLM_MODEL"] = "qwen2.5:7b"
```

1. Lokales Ollama in Colab

- Kein `LLM_BASE_URL` setzen.
- `ollama serve` muss in der Colab-Session laufen und ein Modell verfuegbar sein.
- Falls lokales Ollama nicht erreichbar ist, erscheint ein klarer Hinweis im Notebook.

## 3) P01 Besonderheit in Colab

P01 nutzt die Ollama-REST-API direkt.
In Colab ist localhost normalerweise nicht erreichbar.
Setze deshalb:

```python
import os
os.environ["OLLAMA_BASE_URL"] = "https://<dein-ollama-host>"
os.environ["LLM_MODEL"] = "qwen2.5:7b"
```

Wenn kein externer Ollama-Host vorhanden ist, werden API-Teile im Notebook sauber uebersprungen.

## 4) Erwartetes Verhalten bei Fehlern

- Fehlende Pakete: werden in den Setup-Zellen automatisch installiert (wenn aktiviert).
- Fehlender Endpoint in Colab (P04/P05): es wird lokales Ollama versucht; bei Fehlschlag kommt ein klarer Runtime-Hinweis.
- Lokales Ollama nicht erreichbar (P01/P04/P05): klare Hinweise und ueberspringbare Demonstrationszellen.

## 5) Empfohlene Ausfuehrungsreihenfolge

1. P01_Entwicklungsumgebung.ipynb
2. P02_Tokenizer_Embeddings_MLP.ipynb
3. P03_Transformer_Attention.ipynb
4. P04_Halluzinationen_Perplexity.ipynb
5. P05_Prompting_InContextLearning.ipynb
