# n8n Automation Workflows

> A progressive collection of n8n automation workflows — from basic triggers to autonomous AI agents capable of classification, decision-making, and structured output.

![Status](https://img.shields.io/badge/status-stable-success?style=flat-square)
![Tool](https://img.shields.io/badge/n8n-EA4B71?style=flat-square&logo=n8n&logoColor=white)
![AI](https://img.shields.io/badge/AI-OpenAI-1a1a1a?style=flat-square&logo=openai&logoColor=white)

---

## Overview

A structured set of n8n workflows organized by difficulty. They cover the practical patterns you actually use in production automation: triggers, branching logic, API integrations, AI-driven classification, and autonomous decision-making.

Each `.json` file is a workflow you can import directly into your own n8n instance.

## Contents

```
n8n-automation-workflows/
├── Nivel Facil/        — Basic triggers and simple data flow
├── Nivel Medio/        — Conditional logic, API integrations, transformations
└── Nivel Difícil/      — AI-powered workflows
    ├── Clasificación por IA           AI-based content classification
    ├── Desiciones basadas en IA       Branching logic driven by LLM output
    ├── IA + API Data                  LLM enrichment of external API data
    ├── Salida estructurada            Structured JSON output from natural language
    └── Sistema autónomo final         End-to-end autonomous AI agent
```

## How to use

1. Spin up an n8n instance (self-hosted or cloud).
2. From the n8n editor, choose **Import from File** and select any `.json` from this repo.
3. Configure your credentials (API keys for any external service used).
4. Activate the workflow.

## Highlights

- **Sistema autónomo final** — an end-to-end agent that ingests data, classifies it with an LLM, makes routing decisions, and produces structured output. The largest and most complete workflow in the repo.
- **Salida estructurada** — demonstrates how to force an LLM into reliable, schema-following JSON output for downstream systems.
- **IA + API Data** — pattern for hybrid pipelines that combine deterministic APIs with LLM reasoning.

## Stack

- [n8n](https://n8n.io/) — low-code workflow automation
- OpenAI API (for AI nodes)
- REST APIs and Webhooks
- JSON

## What I learned building these

- Designing workflows that fail gracefully (retries, fallbacks, error branches)
- Forcing reliable structured output from LLMs in production-style pipelines
- The boundary between deterministic code and AI-driven logic
- How to decompose a complex automation into composable, debuggable nodes

---

Built by **Joel Fayad** — Frontend Developer & Automation Engineer based in Colombia.
