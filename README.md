# 🔍 repo-audit-agent

> **> `repo-audit-agent` helps developers perform fast first-pass repository reviews using [Hermes Agent](https://hermes-agent.org)**

[![Hermes Agent](https://img.shields.io/badge/Powered%20by-Hermes%20Agent-blue)](https://hermes-agent.org)
[![Python](https://img.shields.io/badge/Python-3.11%2B-green)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)
[![Hermes Agent Challenge](https://img.shields.io/badge/Hermes%20Agent-Challenge%202026-orange)](https://dev.to)

`repo-audit-agent` uses **Hermes Agent** to autonomously analyze any GitHub repository and generate a comprehensive technical audit report — including tech stack detection, code quality scoring, risk register, and improvement roadmap.

---

## ✨ What It Does

Hermes Agent browses the target repository, analyzes its codebase, and produces a structured Markdown report with:

| Section | Description |
|---------|-------------|
| **Executive Summary** | Project purpose, maturity, and overall health |
| **Tech Stack** | Detected languages, frameworks, and tools |
| **Code Quality Score** | 1–10 rating with justification |
| **Risk Register** | Top 5 risks with severity and impact |
| **Improvement Roadmap** | Top 5 actionable priorities |
| **Conclusion** | Final assessment and next steps |

---

## 🚀 Quick Start

### 1. Install Hermes Agent

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

### 2. Configure your LLM API key

```bash
# Option A: Gemini (Google AI Studio — free tier available)
echo "GOOGLE_API_KEY=your-key-here" >> ~/.hermes/.env
hermes setup  # Select Google AI Studio

# Option B: Any other provider supported by Hermes Agent
hermes setup
```

### 3. Clone and run repo-audit-agent

```bash
git clone https://github.com/PropLUG/repo-audit-agent
cd repo-audit-agent

python3 audit.py https://github.com/NousResearch/hermes-agent
```

That's it — Hermes Agent does the rest. ☕

---

## 📖 Usage

```
usage: repo-audit-agent [-h] [--output DIR] [--max-turns N] [--timeout SECONDS] repo_url

positional arguments:
  repo_url              GitHub repository URL to analyze

options:
  --output DIR          Directory to save reports (default: ./reports)
  --max-turns N         Maximum Hermes Agent iterations (default: 15)
  --timeout SECONDS     Maximum seconds to wait (default: 300)
  --version             Show version and exit
```

### Examples

```bash
# Analyze any public GitHub repository
python3 audit.py https://github.com/NousResearch/hermes-agent

# Save report to custom directory
python3 audit.py https://github.com/owner/repo --output ./my-audits

# Give Hermes Agent more time for large repos
python3 audit.py https://github.com/owner/large-repo --max-turns 25 --timeout 600
```

---

## 📄 Sample Report

```markdown
# Technical Audit Report: NousResearch/hermes-agent

Generated: 2026-05-29 21:07 UTC
Tool: repo-audit-agent v1.0.0 powered by Hermes Agent

## Executive Summary

The hermes-agent repository is a substantial, well-structured project...

## Tech Stack

- **Primary:** Python 46.7%, TypeScript 7.9%
- **Config:** YAML, TOML, JSON
- **Infrastructure:** Docker, Bash, Systemd

## Code Quality Score

**Score: 7/10**

Strong documentation coverage (23.7% comment ratio)...

## Risk Register (Top 5)

| # | Risk | Severity |
|---|------|----------|
| 1 | Dependency sprawl across 5+ languages | Medium |
| 2 | Documentation drift risk | Medium |
...

## Improvement Roadmap (Top 5)

1. **Automated dependency scanning** — Implement Dependabot...
2. **Performance profiling** — Profile critical Python paths...
```

---

## 🏗️ Architecture

```
repo-audit-agent
│
├── audit.py              ← Main script (CLI entry point)
│   │
│   ├── parse_args()      ← CLI argument parsing
│   ├── validate_repo_url() ← Input validation
│   ├── build_audit_prompt() ← Constructs Hermes Agent prompt
│   ├── run_hermes_audit() ← Invokes Hermes Agent
│   └── save_report()     ← Persists Markdown report
│
└── reports/              ← Generated audit reports
    └── audit_<repo>_<timestamp>.md
```

### How Hermes Agent Powers the Audit

`repo-audit-agent` uses Hermes Agent's **agentic capabilities**:

1. **Planning** — Hermes breaks the audit into sub-tasks
2. **Tool Use** — Hermes browses GitHub, reads files, analyzes code
3. **Multi-step Reasoning** — Hermes synthesizes findings into structured output
4. **Report Generation** — Hermes produces the final Markdown report

---

## 🛠️ Requirements

- Python 3.11+
- [Hermes Agent](https://hermes-agent.org) installed and configured
- A valid API key for any Hermes-supported LLM provider

---

## 🌍 Real-World Use Cases

This tool was built to audit real Italian public-sector repositories:

- `fatturapa-mcp-server` — FatturaPA electronic invoicing
- `sdi-ops-monitor` — SDI operations monitoring  
- `conto-termico-gse` — GSE thermal account management
- `GaraAI` — AI-powered public procurement

---

## 🤝 Contributing

Contributions welcome! Open an issue or submit a PR.

---

## 📜 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 🏆 Built for the Hermes Agent Challenge 2026

This project was built as a submission for the [Hermes Agent Challenge](https://dev.to/challenges/hermes-agent) on Dev.to.

**Hermes Agent** is an open-source agentic system by [Nous Research](https://nousresearch.com) capable of planning, tool use, and multi-step reasoning.


## 🗺️ Roadmap

Features planned for future releases:

- [ ] **GitHub API integration** — Read actual source code, commit history, open issues, and pull requests for deeper analysis
- [ ] **Telegram notifications** — Send audit reports directly to Telegram when complete
- [ ] **Batch mode** — Audit multiple repositories in one command
- [ ] **Custom report templates** — Define your own audit sections and scoring criteria
- [ ] **CI/CD integration** — Run audits automatically on pull requests
- [ ] **Historical tracking** — Compare audit scores over time to track improvements