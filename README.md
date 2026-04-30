[README.md](https://github.com/user-attachments/files/27264338/README.md)
# Abstra GPU Unified Project

Unified project package for:

- Abstra Memory Intro: presentation / entry layer only.
- Abstra Engine: Kernel + Agent 1 + Agent 2 + Agent 3 real-time telemetry panel.
- BasarLab Pro: DUO / GIANT Suppression / GIANT Blur-Map viewer with `SimulationConfig`.
- Agent 3 ROCm worker scaffold: GPU simulation backend endpoint.

## Role contract

| Layer | Role |
|---|---|
| DNA Kernel | gate/routing for LLM pipeline |
| Agent 1 | analysis only |
| Agent 2 | prompt engineering + local ComfyUI path |
| Agent 3 | real-time simulation/telemetry only; optional LLM telemetry analyzer; no chat production |

## Install frontend

```bash
npm install
npm run dev
```

## Run Agent 3 backend

```bash
cd gpu
python -m venv .venv
source .venv/bin/activate
pip install -r requirements-rocm.txt
python agent3_rocm_worker.py
```

Then:

```bash
curl http://localhost:8790/health
```

## Run LLM proxy

```bash
cp .env.example .env
npm run llm-proxy
```

The proxy is centralized intentionally. Add provider-specific SDK/API calls server-side.

## SimulationConfig

Official schema:

```txt
src/config/basar.simulation-config.v1.schema.json
```

Example:

```txt
src/config/basar.simulation-config.v1.example.json
```

The same config is valid for:

- React viewer injection
- Abstra Engine bridge
- Agent 3 ROCm worker
