# Praktikum Notebooks: local and Google Colab quickstart

This repository contains 5 practical Jupyter notebooks:

- `P01_Entwicklungsumgebung.ipynb`
- `P02_Tokenizer_Embeddings_MLP.ipynb`
- `P03_Transformer_Attention.ipynb`
- `P04_Halluzinationen_Perplexity.ipynb`
- `P05_Prompting_InContextLearning.ipynb`

## 1) Local start

### Requirements

- Python 3.11+
- Jupyter Notebook or JupyterLab
- Ollama for `P01`, `P04`, and `P05`

### Minimal setup

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install jupyterlab ipykernel
```

Optional kernel registration:

```bash
python -m ipykernel install --user --name praktikum-llm --display-name "Python (praktikum-llm)"
```

Start Jupyter:

```bash
jupyter lab
```

### Notebook package installation behavior

All notebooks install missing Python packages from their setup cells with this fallback order:

1. `python -m uv pip install --system ...`
2. `uv pip install --system ...`
3. `python -m pip install --break-system-packages ...`

## 2) Google Colab start

### `P02` and `P03`

These notebooks do not require an LLM endpoint.
Open the notebook and run the setup cell.

### `P01`, `P04`, and `P05`

The default mode is local Ollama inside the notebook session.

- If no `LLM_BASE_URL` is set, the notebook uses local Ollama.
- In Colab, the setup cell installs Ollama when needed, starts `ollama serve`, and pulls the default model automatically.
- The default model is `qwen3.5:0.8b`.

Optional remote override for `P04` and `P05`:

```python
import os
os.environ["LLM_BASE_URL"] = "https://<your-endpoint>/v1"
os.environ["LLM_API_KEY"] = "<optional>"
os.environ["LLM_MODEL"] = "qwen3.5:0.8b"
```

## 3) `P01` bootstrap behavior

`P01` does bootstrap Ollama in the notebook, but only for the Colab/local-host path.

- In Colab, the setup cell installs Ollama if needed, starts the server, and pulls `qwen3.5:0.8b`.
- On a local machine, `P01` expects the Ollama binary to already be installed.
- After setup, the notebook runs directly against the local Ollama API and Python client without skip logic.

Optional local pre-install command:

```bash
ollama pull qwen3.5:0.8b
ollama serve
```

## 4) Runtime behavior

- Missing Python packages are installed from the setup cells.
- `P01`, `P04`, and `P05` no longer use “skip” cells for missing Ollama/API access.
- LLM/API cells are expected to run directly after the setup cell succeeded.
- The optional reasoning section in `P04` still requires a separate reasoning model if that section is executed.

## 5) Recommended order

1. `P01_Entwicklungsumgebung.ipynb`
2. `P02_Tokenizer_Embeddings_MLP.ipynb`
3. `P03_Transformer_Attention.ipynb`
4. `P04_Halluzinationen_Perplexity.ipynb`
5. `P05_Prompting_InContextLearning.ipynb`
