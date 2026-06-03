# Webwright

<p align="center">
  <img src="assets/webwright_logo.svg" alt="Webwright logo" width="320">
</p>

<p align="center"><b>Turn Your Coding Models to Be State-of-the-art Browser Agents</b></p>

<p align="center">
  <img src="https://test-ind-api.fyinformation.cc/" alt="Python">
</p>

- 📝 **Blog:** [Webwright: A Terminal Is All You Need For Web Agents](https://www.microsoft.com/en-us/research/articles/webwright-a-terminal-is-all-you-need-for-web-agents/)
- 🌐 **Project Page:** [microsoft.github.io/Webwright](https://microsoft.github.io/Webwright/)

Webwright gives LLM a terminal where it can launch multiple browser sessions to inspect the page and complete a web task. It captures and inspects page screenshots/states only when needed. It enforces each web task to be completed end-to-end within a re-runnable Python script, i.e. your web agent browsing history is a single code file. No multi-agent system, no graph engine, no plugin layer, no hidden orchestration — just a terminal, a browser, and a model.

Already got your favorite agents, and wonder how to make Claude Code, Codex, Hermes, OpenClaw more capable in browser tasks? Consider adding [Webwright plugin/skills](#-use-as-a-claude-code-skill)!

## 🗺️ Project Map

```
webwright/
├── pyproject.toml           # package: webwright
├── src/webwright/
│   ├── run/cli.py           # CLI entrypoint (`webwright`)
│   ├── agents/default.py    # core agent loop
│   ├── environments/        # Playwright browser workspace
│   ├── tools/               # image_qa, self_reflection
│   ├── models/              # openai_model, anthropic_model, base
│   ├── config/              # base.yaml, model_openai.yaml, model_claude.yaml
│   └── utils/
├── assets/
│   └── task_showcase/       # tiny Flask dashboard for repeatable runs
│       ├── app.py
│       ├── templates/       # dashboard.html, task.html
│       └── tasks/<short_id>/ # task.json + report.json per task
├── tests/
└── outputs/                 # run artifacts (trajectories, screenshots)
```

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Chromium installed through Playwright
- An API key for your chosen backend (OpenAI, Anthropic, or OpenRouter)

### Install

```bash
pip install -e .
playwright install chromium
```

### Run

Export credentials for the configured backend (for example, `OPENAI_API_KEY`
with `model_openai.yaml` or `ANTHROPIC_API_KEY` with `model_claude.yaml`). The
`image_qa` and `self_reflection` tools use the same configured model by default,
so an Anthropic run does not require an OpenAI key. Then:

```bash
python -m webwright.run.cli \
    -c base.yaml -c model_openai.yaml \
    -t "Search for flights from SEA to JFK on 2026-08-15 to 2026-08-20" \
    --start-url https://www.google.com/flights \
    --task-id demo_openai \
    -o outputs/default
```
