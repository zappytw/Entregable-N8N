# n8n Automation Workflows

> A progressive collection of 15 n8n workflows — from basic triggers and transformations, to multi-API composition, to autonomous AI pipelines that classify content and persist to Google Sheets.

![Status](https://img.shields.io/badge/status-stable-success?style=flat-square)
![Tool](https://img.shields.io/badge/n8n-EA4B71?style=flat-square&logo=n8n&logoColor=white)
![AI](https://img.shields.io/badge/OpenAI-GPT--4o--mini-1a1a1a?style=flat-square&logo=openai&logoColor=white)

---

## Overview

Fifteen n8n workflows organized into three difficulty tiers. They cover the patterns you actually use building real automations: triggers, API consumption, transformations, filters, conditional logic, error handling, AI integration, and persistence to external systems.

Each `.json` file is a complete workflow you can import directly into your own n8n instance.

## Contents

### Nivel Fácil (5 workflows)
Foundations — triggers, static data, basic API consumption, transformations, persistence.
- `Consumo de API pública`
- `Ejecución Programada`
- `Flujo con datos estáticos`
- `Persistencia de Datos`
- `Transformación de datos`

### Nivel Medio (5 workflows)
Composition — combining APIs, conditional logic, filtering, error handling, dynamic parameters.
- `Combinación de APIs`
- `Decisiones automatizadas`
- `Filtrado de datos`
- `Manejo de errores`
- `Parámetros dinámicos`

### Nivel Difícil (5 workflows)
AI-integrated pipelines using **OpenAI GPT-4o-mini**.
- `Clasificación por IA` — pulls a random post from a public API, sends it to GPT-4o-mini, and classifies sentiment + category.
- `Decisiones basadas en IA` — branching logic driven by LLM output.
- `IA + API Data` — combines external API data with LLM-based enrichment.
- `Salida estructurada` — forces the LLM to return strict JSON for downstream parsing.
- `Sistema autónomo final` — end-to-end scheduled pipeline. Full details below.

## Highlight: Sistema autónomo final

The most complete workflow in the repo — a scheduled, AI-classified, persisted pipeline. Here's what it does end-to-end:

1. **Schedule Trigger** fires every 1 minute
2. **HTTP Request** fetches a random post from `dummyjson.com/posts/{random_id}`
3. **Filter** lets the post through only if `likes > dislikes` (engagement gate)
4. The filtered post is sent in parallel:
   - to **GPT-4o-mini** (configured with `textFormat.textOptions.type: "json_object"` to force valid JSON output)
   - to a **Merge** node, which keeps a copy of the original data
5. **Edit Fields** extracts the AI response from the LLM output structure
6. **Merge** combines the original post + AI classification side-by-side
7. **IF** evaluates: `decision == "reportar"` OR `sentimiento == "negativo"`
   - **True** → appended to the **"Noticias Negativas"** sheet in a Google Sheets document
   - **False** → appended to the **"Noticias Positivas"** sheet

The LLM system prompt enforces this output schema:

```json
{
  "decision": "reportar" | "ignorar",
  "sentimiento": "positivo" | "negativo" | "neutral",
  "nivel_urgencia": "alto" | "medio" | "bajo",
  "razon": "..."
}
```

That's a production-style pattern: scheduled ingestion → deterministic filter → AI classification with forced structured output → conditional persistence to two destinations.

## How to use

1. Spin up an n8n instance (self-hosted or cloud).
2. From the n8n editor, choose **Import from File** and select any `.json` from this repo.
3. Configure your credentials:
   - **OpenAI API** for any workflow in `Nivel Difícil`
   - **Google Sheets OAuth2** for `Sistema autónomo final`
4. Activate the workflow.

## Stack

- [n8n](https://n8n.io/) — workflow automation
- OpenAI **GPT-4o-mini** (for AI-tier workflows)
- Google Sheets API (for persistence in `Sistema autónomo final`)
- Public REST APIs (`dummyjson.com`)

## What I learned building these

- Forcing structured JSON output from LLMs to make downstream nodes deterministic
- Combining hard logic (filters, IFs) with AI reasoning in the same pipeline
- Using `Merge` to keep original data alongside enriched data when an LLM only returns its own output
- Designing scheduled, autonomous pipelines (no human in the loop)
- Routing data to different destinations based on AI classification

---

Built by **Joel Fayad** — Frontend Developer & Automation Engineer based in Colombia.
