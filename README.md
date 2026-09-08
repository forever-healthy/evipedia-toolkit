[![Forever Healthy](https://img.shields.io/badge/(c)_2026-Forever_Healthy-573D7D.svg)](https://forever-healthy.org)
[![Content CC BY 4.0](https://img.shields.io/badge/Content-CC_BY_4.0-blue.svg)](https://creativecommons.org/licenses/by/4.0/)
![evipedia.ai](./docs/evipedia-header.png)

# Evipedia Toolkit

[Evipedia](https://evipedia.ai) is a comprehensive, continuously updated online encyclopedia that provides much-needed, accurate, and up-to-date information on a wide range of health and longevity-related interventions.

We build it as a backbone tool for the whole longevity and rejuvenation community. It will always be free, and we actively encourage and support its use in any way and on any project that helps people live longer, healthier lives.

Everything Evipedia knows is open to build on. No API keys, no sign-up, no SDK — plain HTTP, open CORS, and a ready-made tool for every common way of using it.

All content is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): use it freely, credit evipedia.ai, and link back to a review where practical.


### Start Here

* **I want Evipedia in my browser** → the [browser extension](#browser-extension)
* **I want my AI agent to use Evipedia** → the [MCP server](#mcp-server), [AI plugin](#ai-plugin), [Grok Bot](#grok-bot), or [Custom GPT](#custom-gpt)
* **I want Evipedia on my own website** → the [JavaScript widget](#javascript-widget) — one script tag
* **I want to query the data myself** → the [HTTP API](#http-api) — every review as Markdown or JSON
* **I want the whole corpus** → the [full corpus](#http-api) as JSONL — the entire library in one file


---


### Browser Extension

Brings Evipedia hover cards to every site you visit, and turns supplement labels and ingredient lists into links to the evidence.

[Install & details](https://evipedia.ai/extension) · [Source](https://github.com/forever-healthy/evipedia-extension)


---


### MCP Server

Connects any [Model Context Protocol](https://modelcontextprotocol.io) client — Claude, Cursor, Grok, and others — straight to evipedia.ai. Your agent can search reviews, read conclusions or full Markdown, pull structured medical metadata, and suggest new interventions. No API key.

```json
{ "mcpServers": { "evipedia": { "type": "http", "url": "https://mcp.evipedia.ai/mcp" } } }
```

[Source](https://github.com/forever-healthy/evipedia-mcp) · [npm](https://www.npmjs.com/package/evipedia-mcp) · [Local install & all clients](https://evipedia.ai/integration#evipedia-mcp-server)


### AI Plugin

The fastest route for Claude and Grok Build users — wires in the MCP server plus a `/demo` skill in one install, from the Forever Healthy plugin marketplace.

```
/plugin marketplace add forever-healthy/fh-plugins
/plugin install evipedia@forever-healthy
```

[Marketplace](https://github.com/forever-healthy/fh-plugins) · [Claude Desktop & Grok Build steps](https://evipedia.ai/integration#evipedia-ai-plugin)


### Grok Bot

Turns Grok into a specialized assistant giving evidence-based second opinions, grounded in the Evipedia catalogue and the AI4L persona. Set up by pointing a new bot at one URL.

```
Set yourself up from https://evipedia.ai/grokbot.md
```

[Details](https://evipedia.ai/grokbot)


### Custom GPT

The same evidence inside ChatGPT with zero setup — a wrapper over the public API, no install and no key.

[Open in ChatGPT](https://chatgpt.com/g/g-6a58ce5b317481919396d0a558a4c031-evipedia) · [Details](https://evipedia.ai/integration#evipedia-custom-gpt)


---

### JavaScript Widget

Highlights intervention names on any web page and shows an evidence-review hover card. One script tag, no build step, no data of its own — it reads from evipedia.ai.

```html
<script src="https://evipedia.ai/widget.js"></script>
<script>evipedia.init()</script>
```

[Source & demo](https://github.com/forever-healthy/evipedia-widget) · [Full options](https://evipedia.ai/api#website-integration)

### HTTP API

Every endpoint is a plain `GET` with open CORS (`Access-Control-Allow-Origin: *`), so browser-side code can fetch it directly. Replace `{permalink}` with any review's short URL, e.g. `rapamycin`.

| Endpoint | What you get | Example |
|---|---|---|
| `/{permalink}` | The review page — a short, stable URL that never changes | [`/rapamycin`](https://evipedia.ai/rapamycin) |
| `/{permalink}_er#{anchor}` | A fixed section of any review; anchors are identical across the catalogue | [`/rapamycin_er#conclusion`](https://evipedia.ai/rapamycin_er#conclusion) |
| `/{permalink}.md` | The complete review as raw Markdown, no HTML to parse | [`/rapamycin.md`](https://evipedia.ai/rapamycin.md) |
| `/{permalink}.meta.json` | Dates and primary-source citations with PMIDs, flat JSON | [`/rapamycin.meta.json`](https://evipedia.ai/rapamycin.meta.json) |
| `/reviews.json` | The full catalogue — name, synonyms, category, permalink, conclusion | [`/reviews.json`](https://evipedia.ai/reviews.json) |
| `/search.json` | Search index, one entry per review; resolves brand names, synonyms and drug classes | [`/search.json`](https://evipedia.ai/search.json) |
| `mcp.evipedia.ai/search?q=` | Hosted search — ranked matches without running the query yourself (60 req/min per IP) | [`?q=rapamycin`](https://mcp.evipedia.ai/search?q=rapamycin) |
| `/evipedia-corpus.jsonl` | The entire library, one JSON object per line with full Markdown (~25 MB) | [`/evipedia-corpus.jsonl`](https://evipedia.ai/evipedia-corpus.jsonl) |
| `/updates.json` | Every review newest first, each flagged `new` or `updated` | [`/updates.json`](https://evipedia.ai/updates.json) |
| `/feed.xml` · `/feed-new.xml` | RSS — new and refreshed reviews, or newly published only | [`/feed.xml`](https://evipedia.ai/feed.xml) · [`/feed-new.xml`](https://evipedia.ai/feed-new.xml) |
| `/llms.txt` | Machine-readable signpost to everything above, for agents | [`/llms.txt`](https://evipedia.ai/llms.txt) |
| `/openapi.yaml` | OpenAPI 3.1 spec — point a generator at it for a typed client | [`/openapi.yaml`](https://evipedia.ai/openapi.yaml) |
| `/persona.md` | System prompt for conversations in Evipedia's and AI4L's style | [`/persona.md`](https://evipedia.ai/persona.md) |

Every review page also carries [schema.org](https://schema.org/MedicalWebPage) `MedicalWebPage` JSON-LD, including primary-source citations as structured `ScholarlyArticle` / `MedicalStudy` entries — so an agent can traverse straight to the underlying evidence without scraping prose.

Full reference, with the reasoning behind each format: [the API page](https://evipedia.ai/api).


---

### Open Source

Everything we build on top of Evipedia is public. Issues and pull requests welcome.

* **[evipedia-mcp](https://github.com/forever-healthy/evipedia-mcp)** — the MCP server, local and hosted
* **[evipedia-widget](https://github.com/forever-healthy/evipedia-widget)** — the embeddable hover-card widget
* **[evipedia-extension](https://github.com/forever-healthy/evipedia-extension)** — the browser extension
* **[fh-plugins](https://github.com/forever-healthy/fh-plugins)** — the Forever Healthy plugin marketplace
* **[AI4L](https://github.com/forever-healthy/AI4L)** — the open framework Evipedia itself is built on, including the "Audit-Driven Prompting" approach behind every review


---

### Crawlers & Agents Welcome

Evipedia places no barriers to automated access. Our crawler policy is fully open — every agent and crawler is welcome, whether it's an AI assistant, a search engine, or a research tool. No special arrangements, no negotiated access, no robots.txt games.


---

### Limitations

Please be aware of the "[Limitations of Evipedia, AI4L & AI](https://evipedia.ai/disclaimer)"
