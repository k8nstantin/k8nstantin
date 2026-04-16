<img src="photo.jpg" width="140" align="right" style="border-radius:50%;margin-left:20px" />

# Constantin Alexander

[LinkedIn](https://www.linkedin.com/in/constantin-alexander/) (30K+) | [OpenLoom](https://github.com/k8nstantin/openloom) | [dedomena.io](https://dedomena.io)

---

Hey — I'm Constantin. I build things at the intersection of data engineering and AI.

For the last 20 years, I've been deep in databases — MySQL, MariaDB, PostgreSQL, migrations, replication, performance, disaster recovery. The kind of work where you're on call at 3am because a replica fell behind. I've done that across telecom, finance, healthcare, and SaaS.

More recently, I got fascinated by what happens when you combine deep data knowledge with modern AI. Not just asking chatbots questions — but building systems where AI actually understands your data and can work with it autonomously.

That led to two things I'm really proud of:

---

## OpenLoom

An AI development framework I built from scratch. The idea is simple: what if you could write a specification and have AI agents build it — with real accountability?

You define a product as a set of specs (manifests). Each spec breaks into tasks with dependencies. OpenLoom spawns autonomous agent sessions — Claude Code, Cursor, whatever speaks MCP — feeds them the spec, your rules, and everything previous agents learned. They work on their own branch, commit their code, and open a PR.

Then the interesting part: a server-side watcher audits every completed task. Did the agent commit code? Does it compile? Did it address the deliverables? The agent can't see the watcher and can't game it. Fail a gate and the work gets flagged.

Everything is tracked — every conversation, every tool call, every dollar spent, lines of code written, productivity trends over time. You get a real picture of what autonomous development costs and produces.

It's 19,000+ lines of Go, 40+ MCP tools, a 16-tab dashboard, and it runs as a single binary. Machines sync peer-to-peer. Memories persist across sessions. I use it every day.

[Check it out](https://github.com/k8nstantin/openloom)

---

## Schema Intelligence

At Gryphon AI, I built a knowledge network over 17,000+ database objects — tables, stored procedures, views, events, triggers — across 27 databases and 5 servers.

Every object gets an AI-generated summary (Gemini 2.5 Pro), embedded for semantic search (Vertex AI Vector Search), and made queryable through a conversational chatbot. You can ask "what tables store customer PII?" and it searches 17,000 objects, pulls context from BigQuery, and gives you a sourced answer.

Three modes: explore (search anything), impact analysis (what breaks if I change this?), and migration planning. The whole pipeline — parsing, summarization, embedding, graph building — runs as a single serverless job on Dataproc. Full rebuild costs about $30.

It's the kind of thing that saves months of tribal knowledge gathering when you're planning a migration or trying to understand a legacy system.

---

## Serverless Data Lakehouse

Also at Gryphon AI — a fully serverless Apache Iceberg lakehouse on GCP. No persistent clusters, no idle costs. Dataproc Serverless for compute, BigLake REST Catalog for metadata, BigQuery for SQL access. Modular Terraform. Tables just show up in BigQuery UI automatically.

---

## The Stuff That Ties It All Together

What I keep coming back to is the blend — deep data platform experience combined with AI that actually does useful work. Not AI as a demo. AI as infrastructure.

OpenLoom came from needing to coordinate multiple AI agents building real software. The schema chatbot came from needing to make 17,000 database objects understandable to humans and machines. The lakehouse came from needing serverless infrastructure that just works.

If any of this resonates — whether you're figuring out AI enablement for your engineering team, planning a database migration, or just curious about autonomous agent development — I'd love to chat.

> *"Constantin is the data whisperer! Everything started looking up and information became both accessible and reliable."*

> *"Exceptionally technically skilled with great manager/architect potential."*

## Published Work

| Article | Likes |
|---------|-------|
| [MySQL and MariaDB so similar, alas so different](https://www.linkedin.com/pulse/mysql-mariadb-so-similar-alas-different-constantin-alexander--ifu9e) | 71 |
| [PostgreSQL Physical Replication, Easy Guide](https://www.linkedin.com/pulse/postgresql-physical-replication-easy-guide-constantin-alexander-sh5ie) | 49 |
| [Easy PostgreSQL Backup Strategies](https://www.linkedin.com/pulse/easy-postgresql-backup-strategies-complete-guide-constantin-alexander-uvlye) | 48 |
| [PostgreSQL Logical Replication](https://www.linkedin.com/pulse/postgresql-logical-replication-constantin-alexander-hzlae) | 42 |
| [Easy PostgreSQL Patroni Integration](https://www.linkedin.com/pulse/easy-postgresql-patroni-intergration-constantin-alexander-tc8je) | 35 |
| [PostgreSQL and Apache Flink CDC](https://www.linkedin.com/pulse/postgresql-apache-flink-cdc-integration-constantin-alexander--qhnle) | 24 |
| [Demystify SQL](https://www.linkedin.com/pulse/demystify-sql-constantin-alexander--7lyoe) | 16 |
| [Easy Apache Iceberg Maintenance](https://www.linkedin.com/pulse/easy-apache-iceberg-maintenance-guide-constantin-alexander-oq8ve) | 9 |
| [Easy Terraform Modules](https://www.linkedin.com/pulse/easy-terraform-modules-constantin-alexander-9hlne) | 7 |
| [Apache Paimon + Apache Iceberg](https://www.linkedin.com/pulse/apache-paimon-iceberg-constantin-alexander-jey5e) | 6 |
| Battle of the Titans — Virident vs Fusion IO in MySQL/MariaDB tests | 2014 |
| MySQL MHA vs Continuent Tungsten comparison | 2012 |

---

Data Platform Architect at **Gryphon AI** | Organizer of **The Silicon Valley MySQL Meetup** | English, Russian, Spanish
