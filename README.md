# Qodo (qodo-gen)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
