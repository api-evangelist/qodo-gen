# Qodo (qodo-gen)

Qodo (formerly **CodiumAI**, rebranded in 2024) is an AI code quality and integrity platform spanning the software development lifecycle. Its products include **Qodo Gen** (an AI coding assistant IDE plugin for VS Code and JetBrains - code generation, chat, and AI test generation), **Qodo Merge** (an agentic pull request review app for GitHub, GitLab, Bitbucket, and Azure DevOps, built on the open-source PR-Agent project), **Qodo Command / Qodo Gen CLI** (a terminal agent runner installed via npm that can serve agents as HTTP APIs or MCP services), **Qodo Cover** (test coverage automation), and **Qodo Aware** (codebase context).

## Access model (read this first)

Qodo does **not** publish a single documented public REST API for its hosted platform, and it does **not** expose a public WebSocket API. Qodo's developer-facing surfaces are:

- **IDE plugin (Qodo Gen)** - code generation, chat, and test generation inside VS Code / JetBrains.
- **Git application (Qodo Merge)** - reviews pull requests, invoked with **PR comment commands** (`/review`, `/describe`, `/improve`, `/ask`, `/add_docs`, `/update_changelog`) and driven by a **Git webhook**. Single-tenant installs expose a real, documented webhook receiver at `https://qodo-merge.<tenant>.st.qodo.ai/api/v1/webhook`.
- **CLI (Qodo Command / Qodo Gen CLI)** - `npm install -g @qodo/command`; runs agents defined in `agents.toml`, and can serve an agent as a **local HTTP API** (`--webhook`) or an **MCP service** (`--mcp`).
- **Open source (PR-Agent, MIT)** - [github.com/qodo-ai/pr-agent](https://github.com/qodo-ai/pr-agent) is the engine behind Qodo Merge, self-hostable as a CLI (`pip install pr-agent`), a GitHub Action, or a webhook server.

Because there is no single vendor-published REST contract, the APIs below are catalogued as **capability areas**. The OpenAPI in this repo marks every operation with `x-modeled: true` **except** the single real webhook endpoint (`x-modeled: false`). Do not treat the modeled paths as a stable, guaranteed API.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/qodo-gen/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/qodo-gen/refs/heads/main/apis.yml)

## Tags

- AI Coding Assistant
- Code Review
- Test Generation
- Developer Tools
- LLM
- AI
- Pull Request Review
- Code Quality
- Agents
- Open Source

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs (capability areas)

### Qodo Merge PR Review

Agentic pull request review. Qodo Merge is a hosted Git app (GitHub, GitLab, Bitbucket, Azure DevOps) that reviews PRs automatically and on demand via the `/review` PR comment command. Driven by a Git webhook (single-tenant path `/api/v1/webhook`), not a public REST API; modeled from the open-source PR-Agent engine.

- **Human URL:** [https://docs.qodo.ai/code-review](https://docs.qodo.ai/code-review)
- **Base URL:** `https://qodo-merge.st.qodo.ai/api/v1`

### Qodo Merge Code Suggestions

Committable, ranked code-improvement suggestions for a PR, invoked with `/improve`. Modeled from the PR-Agent improve tool.

- **Human URL:** [https://qodo-merge-docs.qodo.ai/tools/improve/](https://qodo-merge-docs.qodo.ai/tools/improve/)

### Qodo Merge PR Description

Automatic PR title, summary, walkthrough, and labels, invoked with `/describe`. Modeled from the PR-Agent describe tool.

- **Human URL:** [https://qodo-merge-docs.qodo.ai/tools/describe/](https://qodo-merge-docs.qodo.ai/tools/describe/)

### Qodo Merge Ask and Chat

Free-text question answering about a PR or specific lines, invoked with `/ask`. Modeled from the PR-Agent ask tool.

- **Human URL:** [https://qodo-merge-docs.qodo.ai/tools/ask/](https://qodo-merge-docs.qodo.ai/tools/ask/)

### Qodo Gen Test Generation

AI test generation - the capability CodiumAI was founded on - surfaced through the Qodo Gen IDE plugin (VS Code, JetBrains) and Qodo Cover. Delivered through the IDE plugin and CLI rather than a documented public REST endpoint; modeled as a capability area.

- **Human URL:** [https://docs.qodo.ai/qodo-documentation/qodo-gen](https://docs.qodo.ai/qodo-documentation/qodo-gen)

### Qodo Command Agent API

The Qodo Command / Qodo Gen CLI (`npm @qodo/command`) runs configurable agents (`agents.toml`). With `--webhook` an agent is served as a local HTTP API; with `--mcp` an agent becomes a callable MCP service for orchestrators such as LangChain. Self-hosted; endpoints modeled from the CLI docs.

- **Human URL:** [https://docs.qodo.ai/qodo-documentation/qodo-command](https://docs.qodo.ai/qodo-documentation/qodo-command)

## Properties per API

- [OpenAPI](openapi/qodo-gen-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/qodo-gen.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/qodo-gen.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Source Code (PR-Agent)](https://github.com/qodo-ai/pr-agent) — MIT-licensed engine behind Qodo Merge

## Pricing (summary)

- **Trial** - 14 days free, unlimited credits and reviews.
- **Pro Team** - $30/month per seat, up to 30 users; pooled monthly credit packs (2,500 / 5,000 / 20,000 credits, ~$0.012/credit); a 2,500-credit pack is ~18 reviews/month; customer-set overage cap.
- **Enterprise** - custom; SSO/SAML, audit logs, advanced analytics, BYOK, single-tenant SaaS or on-premises, dedicated CSM.
- **PR-Agent (open source, MIT)** - free to self-host; you pay only your own LLM API usage and infrastructure.

Qodo states it has no permanent free tier, but open source projects can qualify for free access through a separate program. See [plans/qodo-gen-plans-pricing.yml](plans/qodo-gen-plans-pricing.yml).

## Common Properties

- [Authentication](authentication/qodo-gen-authentication.yml)
- [Domain Security](security/qodo-gen-domain-security.yml)
- [GitHub Organization](https://github.com/qodo-ai)
- [LinkedIn](https://www.linkedin.com/company/qodoai)
- [Website](https://www.qodo.ai)
- [Documentation](https://docs.qodo.ai)
- [Plans](plans/qodo-gen-plans-pricing.yml)
- [Rate Limits](rate-limits/qodo-gen-rate-limits.yml)
- [Fin Ops](finops/qodo-gen-finops.yml)
- [Blog](https://www.qodo.ai/blog/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
