# Constantin Alexander

What happens when you stop asking AI to help you code — and start giving it the entire job?

That's the question I've been obsessing over. After 20 years of building data platforms — migrating databases, designing lakehouses, tuning systems at scale — I realized the next leap isn't better tools for developers. It's developers that are tools themselves.

So I built [OpenLoom](https://github.com/k8nstantin/openloom) — a framework where you write a spec, and AI agents do the rest. They pick up the task, create a branch, write the code, commit, push, open a PR. A server-side auditor checks their work — did they actually commit? Does it compile? Did they address the spec? The agent doesn't even know it's being watched.

Every conversation is recorded. Every tool call captured. Every dollar tracked. You can see exactly what each agent did, what it cost, and whether it followed the rules.

It's early. It's messy. And it's the most exciting thing I've ever worked on.

> *"Constantin is the data whisperer! Everything started looking up and information became both accessible and reliable."*

> *"Exceptionally technically skilled with great manager/architect potential."*

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

## 20 Years, 7 Cities

I've built data systems at enterprise scale across Miami, Los Angeles, San Francisco, New York, Boston, Las Vegas, and Carlsbad. Telecom, finance, healthcare, SaaS — different industries, same obsession: making data reliable, fast, and accessible.

Currently at **Gryphon AI** in Miami, where I designed the serverless data lakehouse, built the schema intelligence chatbot, and created OpenLoom.

**City University of Seattle** (1993-1997) | Becker CPA Academic Achievement (1996)

## What I Can Help With

IT consulting, database development, application development, data recovery, team building, leadership development, change management, digital marketing strategy, and brand marketing.

Or if you're trying to figure out how to make AI agents actually productive in your engineering org — that's where things get interesting.

## Published Work

| Article | Likes |
|---------|-------|
| [MySQL and MariaDB so similar, alas so different](https://www.linkedin.com/pulse/mysql-mariadb-so-similar-alas-different-constantin-alexander--ifu9e) | 71 |
| [PostgreSQL Physical Replication, Easy Guide](https://www.linkedin.com/pulse/postgresql-physical-replication-easy-guide-constantin-alexander-sh5ie) | 49 |
| [Easy PostgreSQL Backup Strategies: Complete Guide](https://www.linkedin.com/pulse/easy-postgresql-backup-strategies-complete-guide-constantin-alexander-uvlye) | 48 |
| [PostgreSQL Logical Replication](https://www.linkedin.com/pulse/postgresql-logical-replication-constantin-alexander-hzlae) | 42 |
| [Easy PostgreSQL Patroni Integration](https://www.linkedin.com/pulse/easy-postgresql-patroni-intergration-constantin-alexander-tc8je) | 35 |
| [PostgreSQL and Apache Flink CDC Integration](https://www.linkedin.com/pulse/postgresql-apache-flink-cdc-integration-constantin-alexander--qhnle) | 24 |
| [Demystify SQL](https://www.linkedin.com/pulse/demystify-sql-constantin-alexander--7lyoe) | 16 |
| [Easy Apache Iceberg Maintenance Guide](https://www.linkedin.com/pulse/easy-apache-iceberg-maintenance-guide-constantin-alexander-oq8ve) | 9 |
| [Easy Terraform Modules](https://www.linkedin.com/pulse/easy-terraform-modules-constantin-alexander-9hlne) | 7 |
| [Apache Paimon + Apache Iceberg](https://www.linkedin.com/pulse/apache-paimon-iceberg-constantin-alexander-jey5e) | 6 |
| Battle of the Titans — Virident vs Fusion IO in MySQL/MariaDB tests (2014) | - |
| MySQL MHA vs Continuent Tungsten comparison (2012) | - |

## Community

Organizer of **The Silicon Valley MySQL Meetup**. 30K+ followers on [LinkedIn](https://www.linkedin.com/in/constantin-alexander/). Published author on database architecture and distributed systems.

## Connect

[LinkedIn](https://www.linkedin.com/in/constantin-alexander/) | [dedomena.io](https://dedomena.io) | English, Russian, Spanish (all native)
