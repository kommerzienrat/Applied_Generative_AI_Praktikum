# AGENTS.md - Praktikum notebooks

## Notebook modifications

### 1. uv/pip fallback
All notebooks install missing Python packages with this fallback order:
1. `python -m uv pip install --system`
2. `uv pip install --system`
3. `python -m pip install --break-system-packages`

### 2. Colab Ollama bootstrap
`P01`, `P04`, and `P05` bootstrap local Ollama in Colab when no remote endpoint is configured:
- install the Ollama binary when needed via `curl -fsSL https://ollama.com/install.sh | sh`
- start `ollama serve` in the background if the local server is not reachable
- pull the default model automatically

### 3. No skip logic
LLM and API calls should fail clearly instead of being skipped.
Do not use “Übersprungen” or similar skip messages.

### 4. Default model
The default model is `qwen3.5:0.8b` in `P01`, `P04`, and `P05`.
