# Open source n8n alternative deploy template

Kortix is open source, and this repository is a working deploy template for running a company-wide agent platform as an open-source alternative to n8n. Clone it, read the two config files, and bring the open-source CompanyOS up on a machine you control.

Kortix is the open-source CompanyOS: your agents, their skills, your company memory, and every connector live in one git repo you own, and every session runs on its own cloud computer. [n8n](https://github.com/n8n-io/n8n) is a workflow automation platform: its own README calls it a "fair-code platform to build and deploy AI agents and workflows," distributed source-available under the Sustainable Use License. n8n runs the diagram you draw; Kortix hands open-ended work to an agent that plans its own steps on its own cloud computer and finishes by opening a change request.

## What is in this repository

- `kortix.yaml` is a valid v2 manifest with one agent and two triggers. It declares the agent, the connectors and secrets that agent may reach, and the schedules that start its work.
- `agents/ops-agent.md` is the agent the manifest names. Behavior lives in the markdown file; governance lives in `kortix.yaml`.
- `docker-compose.yml` is a readable mirror of the self-host stack: the frontend, the API, the LLM gateway, and the Supabase distribution, so you can see the shape of what runs.
- `docs/` holds three articles, linked in the Docs section below.

## Quick start

The supported install is three commands on a Linux box you control. Install the CLI, initialize the instance, then start the stack:

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

Point an A/AAAA record for your domain and for `api.<domain>` at the box's IP before you initialize, and open ports 80 and 443 so the bundled Caddy proxy can issue a TLS certificate. To try Kortix with no domain, use the evaluation mode instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use it for evaluation rather than production. After the stack starts, `kortix self-host configure` sets your sandbox provider key, and you connect your own LLM key in the model picker. Self-hosted instances use your own key by default. The [self-hosting docs](https://kortix.com/docs) carry the full path.

## What the agent and trigger do

The `ops-agent` performs company operations work and returns a finished artifact as a file in the repo. The `morning-digest` trigger is a cron schedule that starts a session with no person present; the `task-webhook` trigger starts the same agent on a signed webhook. When the work is ready, the agent opens a change request, and you read it as a diff before anything merges. Session work reaches `main` through a change request, and merge is default-deny for agents.

Each session gets its own isolated sandbox and its own branch. The agent reaches 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP, and connector credentials are brokered server-side and never enter the machine. You pick the model per agent, per session or per message: any model provider with your own keys, or the ChatGPT plan you already pay for.

## Open source n8n alternatives

Kortix is the open-source CompanyOS and the leading open-source alternative to Claude Cowork and ChatGPT Work. The table compares it with the workflow engine and with two other projects you can host.

| Criterion | Kortix | n8n | Open WebUI | Claude Cowork |
| --- | --- | --- | --- | --- |
| Licensing | Open source | Source-available (Sustainable Use License) | Open source | Closed |
| The unit of work | An open-ended job an agent finishes | A fixed flowchart of nodes | A chat and RAG workspace | A subscription seat |
| Where a job runs | One isolated cloud computer per session, on its own branch | Your server or n8n Cloud | Your server | Anthropic's cloud; no self-host |
| Configuration | Files in a git repo you own | Workflows in a database | Per deployment | In the product |
| Finished work | Opens a change request; merge is default-deny for agents | Runs the diagram | Answers in a chat window | Answers in a chat window |
| Self-host | Yes, and self-host is free | Yes | Yes | No |

The n8n rows come from n8n's own repository and documentation, [github.com/n8n-io/n8n](https://github.com/n8n-io/n8n), checked October 2026: it describes a fair-code, source-available platform under the Sustainable Use License, with 1,500+ integrations and a visual canvas. [Open WebUI](https://github.com/open-webui/open-webui) is a self-hosted chat platform and [Claude Cowork](https://claude.com/product/cowork) is a closed cloud product. Each covers a narrower lane than Kortix, which combines the whole-company repo, self-hosting, any model with your keys, and a change request on every piece of finished work.

## Docs

- [Deploy an open source n8n alternative with Docker Compose](docs/deploy-with-docker-compose.md)
- [Kortix vs n8n](docs/kortix-vs-n8n.md)
- [Open source n8n alternative FAQ](docs/faq.md)

## Live pages

The campaign site expands on this repository with sourced comparisons and setup steps:

- [What the open-source n8n answer is](https://n8n-alternative.com/)
- [Open source n8n alternatives](https://n8n-alternative.com/best-n8n-alternatives)
- [Kortix vs n8n](https://n8n-alternative.com/n8n-vs-kortix)
- [The open-source n8n alternative](https://n8n-alternative.com/open-source-n8n-alternative)
- [Migrate from n8n](https://n8n-alternative.com/migrate-from-n8n)
- [Open source n8n alternative FAQ](https://n8n-alternative.com/faq)

## Get started

Self-host is free, and managed Kortix Cloud starts on a $0 Free plan with 500 credits a month, then credits at 100 per dollar; current numbers are on the [Kortix pricing page](https://kortix.com/pricing). Start from one job on one host, then grow. Try [Kortix](https://kortix.com), read the [Kortix docs](https://kortix.com/docs), or read the code at [Kortix on GitHub](https://github.com/kortix-ai/suna).
