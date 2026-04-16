# Constantin Alexander

I've spent 20+ years building data systems that power enterprises — MySQL fleets, MariaDB migrations, Spark pipelines, serverless lakehouses on GCP. I've done the hard infrastructure work at companies across Miami, LA, San Francisco, New York, and Boston.

But here's what I'm doing now that matters most: I'm building the framework that lets AI agents write production software autonomously.

Not using Copilot to autocomplete lines. Not chatting with Claude for code suggestions. I built a full development platform where you write a spec, and AI agents pick it up, create a branch, write the code, commit it, push it, create a PR — and then a server-side auditor they can't see or override checks every commit, verifies the build passes, and confirms the deliverables were addressed. If any gate fails, the agent's work is rejected. No human babysitting required.

And every dollar spent, every turn taken, every line of code written is tracked. You know exactly what autonomous development costs and what it produces.

That's [OpenLoom](https://github.com/k8nstantin/openloom).

---

## OpenLoom — AI Development Framework

19,000+ lines of Go. 40+ MCP tools. 70+ API endpoints. 16-tab dashboard. Single binary.

**How it works:** You define a product as a hierarchy of specifications (manifests). Each manifest breaks down into tasks with dependency chains. The framework spawns autonomous agent sessions — Claude Code, Cursor, whatever speaks MCP — gives them the spec, the rules, and the context from every previous session. They work independently. When they're done, the watcher audits them. You review the results and approve.

**What makes it different:**

The agents don't grade themselves. A server-side watcher runs three gates — git commits exist, code compiles, deliverables addressed. The agent has no visibility into this process and no way to bypass it. If it claims "done" but didn't commit code, it fails. Period.

Every agent session must acknowledge your visceral rules before doing any work. "Every change gets its own branch." "Daily budget is $100." "Never work around a problem — fix the source." Break a rule and it's flagged automatically.

Productivity scoring gives you real-time metrics — completion rates, first-attempt success, lines committed, cost per task, 7-day trends. You can see whether your agents are getting better or worse.

And all of this persists. Memory carries across sessions. A new agent inherits what every previous agent learned. Multiple machines sync peer-to-peer via Automerge CRDTs. Your knowledge base grows with every session, not resets.

---

## Schema Intelligence Chatbot

Before OpenLoom, I built an AI-powered knowledge network over 17,000+ MySQL database objects across 27 databases and 5 servers at Gryphon AI.

Every table, stored procedure, view, event, and trigger — summarized by Gemini 2.5 Pro with PII detection and index analysis. Embedded with text-embedding-005 and indexed in Vertex AI Vector Search. You ask "what tables store customer data?" and it searches 17,000 objects semantically, enriches results from BigQuery, and generates an answer with source citations.

Three modes: explore (search), impact analysis (what breaks if I change this?), and migration planning. Multi-turn chat with session persistence. Deployed on Cloud Run, serverless.

The entire pipeline — parsing, summarization, embedding, graph building, categorization — runs as a single atomic Dataproc Serverless job. Full rebuild costs about $30.

---

## Serverless Data Lakehouse

Designed and deployed a fully serverless Apache Iceberg lakehouse on GCP. No persistent clusters. Dataproc Serverless for all compute, BigLake REST Catalog for metadata, BigQuery for SQL access. Tables auto-appear in BigQuery UI. Modular Terraform — every component independently rebuildable. Zero idle costs.

---

## The Short Version

I've been building data systems since before most people knew what a data lake was. MySQL replication, MariaDB migrations, high-availability architectures, performance tuning, disaster recovery — I've done it all at enterprise scale.

Now I'm applying all of that experience to the next frontier: making AI agents productive, accountable, and cost-efficient software developers. Not as assistants. As autonomous builders that follow specs, follow rules, and get audited by machines.

If you need someone who can architect your data platform **and** lead your AI enablement — with the hands-on credibility of having built both from scratch — let's talk.

## Published Work

- [MySQL and MariaDB so similar, alas so different](https://www.linkedin.com/pulse/mysql-mariadb-so-similar-alas-different-constantin-alexander--ifu9e) (2025, 71 likes)
- [Demystify SQL](https://www.linkedin.com/pulse/demystify-sql-constantin-alexander--7lyoe) (2025)
- [PostgreSQL and Apache Flink CDC Integration](https://www.linkedin.com/pulse/postgresql-apache-flink-cdc-integration-constantin-alexander--qhnle) (2025)
- Battle of the Titans — Virident vs Fusion IO in MySQL/MariaDB tests (2014)
- MySQL MHA vs Continuent Tungsten comparison (2012)

## Community

Organizer of **The Silicon Valley MySQL Meetup**. 30K+ followers on LinkedIn. Published author on database architecture and distributed systems.

## Connect

[LinkedIn](https://www.linkedin.com/in/constantin-alexander/) | [dedomena.io](https://dedomena.io) | English, Russian, Spanish
