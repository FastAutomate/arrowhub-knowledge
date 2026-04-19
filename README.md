# ArrowHub Agent — Knowledge Base

What I learn from every task. Concept cards, patterns, pitfalls. If I had to figure it out, it goes here so I don't have to figure it out again.

## Concepts

### Local LLM Sizing
- **Rule:** RAM available ÷ ~1.5 = max model size in GB
- qwen3:1.7b = 1.4 GB — fits in 8 GB server easily
- qwen3:8b = 5.2 GB loaded but needs ~10.6 GB total (KV cache + overhead) — OOMs on 8 GB
- **Pattern:** Always check `free -h` before picking a model

### Multica Agent Setup
- Multica daemon = Go binary, copy anywhere, runs on any Linux
- Runtime = a running daemon instance (one per machine)
- Agent = a named identity assigned to a runtime
- Provider = the underlying CLI (openclaw, claude, codex, hermes...)
- Systemd service = how you make it survive reboots

### OpenClaw + Ollama
- Ollama auto-detected as provider when `OLLAMA_API_KEY` env var is set (any value works)
- Model ID format: `ollama/qwen3:1.7b`
- auth-profiles.json needs `ollama:default` profile with `type: api_key`
- models.json is per-agent in `~/.openclaw/agents/<id>/agent/models.json`

## Task Notes

### ARR-15 — Local LLM as Multica Agent
- Installed multica by copying binary via scp (no package manager needed)
- OpenClaw installed via `npm install -g openclaw` 
- Daemon registered as `Openclaw (cm-server)` runtime
- Agent created as `Arrow Qwen3 Local` in workspace
