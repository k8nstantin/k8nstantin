# Constantin Alexander

**[OpenPraxis](https://github.com/k8nstantin/OpenPraxis)** | **[go-leiden](https://github.com/k8nstantin/go-leiden)** | **[KungFu](https://github.com/k8nstantin/kungfu)** | **[LinkedIn](https://www.linkedin.com/in/constantin-alexander/)** (30K+) | **[dedomena.io](https://dedomena.io)**

---

AI expert specializing in **autonomous agent governance**, **deployment control**, and **AI-powered data intelligence**. Creator of OpenPraxis. Builder of production AI systems that give organizations real control over how AI agents work, what they cost, and what they produce.

---

## Currently Building

### [OpenPraxis](https://github.com/k8nstantin/OpenPraxis) — Autonomous Agent Workflow Engine

A peer-to-peer workflow engine for autonomous coding agents. Single Go binary: MCP server + HTTP dashboard + mDNS peer discovery + Automerge CRDT sync. Products break into specs (manifests) with task DAGs. Agents execute tasks sequentially in isolated git worktrees, commit, push, open PRs — autonomously. Full cost, quality, and compliance visibility.

**What makes it different:** Agents don't self-govern. OpenPraxis enforces visceral rules the agent cannot override, runs an independent server-side audit the agent cannot see, tracks every dollar and turn, and persists memory across sessions and machines.

19,000+ lines of Go · 40+ MCP tools · 70+ API endpoints · 16-tab dashboard · Single binary

→ The engine that builds everything below.

---

### [go-leiden](https://github.com/k8nstantin/go-leiden) — First Native Go Leiden Algorithm

**The first and only Go implementation of the Leiden community detection algorithm.** Zero external dependencies. Port of [graspologic-native](https://github.com/graspologic-org/graspologic-native) (Microsoft Research, MIT) — the same Rust implementation used in production by Microsoft GraphRAG.

The Go ecosystem has Louvain (`gonum/graph/community`). It has no Leiden. Leiden fixes Louvain's fundamental flaw: it guarantees well-connected communities where Louvain cannot.

**How it's built:** Entirely by autonomous AI agents on OpenPraxis. No human code commits. Five manifests, five tasks, sequential execution chain. Every task gets a cascading prompt: product context → manifest context → implementation spec → coding standards. The [Trace-Grounded Feedback Loop](https://github.com/k8nstantin/OpenPraxis) auto-improves prompts when tasks fail — agents learn from their own failures.

```
M1: Core data structures (CompactNetwork, Clustering, Edge)
  ↓
M2: Algorithm phases (local-move, refinement, aggregation)
  ↓
M3: Quality functions (Modularity, CPM)
  ↓
M4: Public API (Leiden, HierarchicalLeiden, go.mod)
  ↓
M5: Tests, benchmarks, fuzz
```

This is the case study: **can autonomous agents build a production-quality open-source Go library from algorithm spec to published package without human code commits?**

→ [go-leiden on GitHub](https://github.com/k8nstantin/go-leiden) · [Build process & prompts](https://github.com/k8nstantin/go-leiden/tree/main/docs)

---

### [KungFu](https://github.com/k8nstantin/kungfu) — Next-Generation Version Control for AI Agents

Git was built for humans working sequentially. KungFu is built for AI agents working concurrently. CRDT-based version control (Loro library) where agents stream fine-grained mutations that merge automatically — no branches, no merge conflicts, no sequential commits. Every mutation is signed with Ed25519. The "Ghost State" concept isolates agent work mathematically until it's ready to expose.

Built in Rust. Exposes an MCP server so AI coding agents interact with it natively. Designed to replace Git for high-concurrency agentic workflows.

→ [KungFu on GitHub](https://github.com/k8nstantin/kungfu)

---

## OpenPraxis — Deep Dive

**The core problem:** AI coding agents are powerful but ungovernable. They hallucinate completion, deviate from instructions, start every session from zero, and give you no visibility into cost, quality, or compliance.

**OpenPraxis fixes this:**

- **Visceral Rules** — Non-negotiable constraints agents must acknowledge before starting. Violations detected and flagged automatically. You set the rules once, every agent follows them.
- **Product DAGs** — Products → Manifests → Tasks with `owns` and `depends_on` edges in a relationship table. Tasks execute in dependency order. Agents spawn autonomously into isolated git worktrees.
- **Trace-Grounded Feedback Loop** — Every agent run sees its own execution history. Pass rates tracked per task and manifest. Autonomous proposer fires on failure streaks and improves prompts without intervention.
- **Independent Auditing** — Server-side watcher the agent cannot see or bypass checks every task: committed? builds? deliverables addressed?
- **Full Cost & Productivity Tracking** — Every dollar, turn, line of code tracked per task, agent, day.
- **Persistent Memory** — Decisions, patterns, bugs carry across sessions and machines. Peer-to-peer sync via Automerge CRDTs.

---

## Schema Intelligence — Semantic Search Across Your Entire Database

At **Gryphon AI**, built an AI knowledge network that lets you **search 17,000+ database objects by natural language**.

17,000+ tables, stored procedures, views, events, and triggers across 27 databases and 5 servers — each summarized by Gemini 2.5 Pro with PII detection and index analysis. Embedded with text-embedding-005 and indexed in Vertex AI Vector Search.

Ask "what tables handle customer billing?" and it searches every object semantically, enriches from BigQuery, and answers with source citations. Three modes: **explore**, **impact analysis**, **migration planning**. Multi-turn chat with session persistence. Deployed serverless on Cloud Run.

Full pipeline — parsing, AI summarization, embedding, knowledge graph, categorization — runs as a single atomic Dataproc Serverless job. Rebuilds for ~$30.

---

## Data Platform Experience

**Gryphon AI** — Lead Data Architect. Serverless Apache Iceberg lakehouse on GCP (BigLake, BigQuery, Dataproc Serverless, Apache Doris, Terraform). Schema intelligence chatbot. OpenPraxis.

**ProxySQL** — MySQL/PostgreSQL connection pooling, query routing, and caching at scale.

**O'Reilly Auto Parts** — GCP/Azure cloud migration. Snowflake + Apache Kafka + FiveTran/Informatica. Apache Iceberg across Snowflake and BigQuery. 6,000+ PostgreSQL to AlloyDB migration. Alation data catalog for GDPR/CCPA. GCP Data Lake with DataPlex, DataFusion, Pub/Sub.

**CareRev** — Confluent Kafka as unified data pipeline. PostgreSQL CDC via Debezium to S3/Snowflake. KsqlDB for inflight analytics. Full Heroku to AWS migration.

**Everflow** — Live-migrated GCP CloudSQL MySQL 5.6→5.7 with zero downtime when Google said it required multi-day outage.

**365 Retail Markets** — On-premise to AWS migration. Snowflake, Kafka CDC, streaming data lake. MySQL with ProxySQL. Hadoop EMR/Spark pipelines.

**Telmate** — MySQL/MariaDB HA on PCI Flash/ZFS. ScaleArc. AWS Aurora/RDS. Redshift. Snowflake DSS pilot.

**Walmart eCommerce** — MySQL Galera architecture and deployment at scale.

**SpringbokSQL** — Founded. MySQL/MariaDB appliances on FusionIO PCI Flash. Synchronous replication. Columnar DSS analytics. Postgres-XL.

**Ultimate Gaming** — 99.999% uptime on synchronous replication. Virident PCI Flash. Reports from hours to minutes. Cassandra for gaming messaging.

**AccelerationDB** — MySQL at scale. MHA vs Tungsten. Silicon Valley MySQL Meetup organizer.

**Akiban Technologies** — Lead Database Architect. AkibanDB group index. Product roadmap. First customer deployment.

**Apple** — Databases Architect, iAd platform.

**Continuent** — Architect. Tungsten carrier-grade replication for MySQL, PostgreSQL, Oracle.

**HubSpot** — MySQL multi-master replication. Pentaho DW.

**Xerox Global Services** — Oracle Applications 11i, Data Guard, ERP management.

**24 Hour Fitness** — Oracle Applications, PeopleSoft. SOX compliance.

**GE** — Server consolidation. Oracle Financials.

**Texas Instruments** — Oracle Applications ERP deployment.

**Oracle Corporation** — Managing/Principal Consultant. Applications architecture.

**JBS Corporation** — Principal Consultant. ERP implementations.

---

## Published

| Date | Article | Likes |
|------|---------|-------|
| Oct 2025 | [MySQL and MariaDB so similar, alas so different](https://www.linkedin.com/pulse/mysql-mariadb-so-similar-alas-different-constantin-alexander--ifu9e) | 71 |
| Oct 2025 | [Demystify SQL](https://www.linkedin.com/pulse/demystify-sql-constantin-alexander--7lyoe) | 16 |
| Oct 2025 | [PostgreSQL + Apache Flink CDC](https://www.linkedin.com/pulse/postgresql-apache-flink-cdc-integration-constantin-alexander--qhnle) | 24 |
| Oct 2025 | [Apache Iceberg Maintenance](https://www.linkedin.com/pulse/easy-apache-iceberg-maintenance-guide-constantin-alexander-oq8ve) | 9 |
| Sep 2025 | [PostgreSQL Patroni HA](https://www.linkedin.com/pulse/easy-postgresql-patroni-intergration-constantin-alexander-tc8je) | 35 |
| Sep 2025 | [Terraform Modules](https://www.linkedin.com/pulse/easy-terraform-modules-constantin-alexander-9hlne) | 7 |
| Sep 2025 | [Apache Paimon + Iceberg](https://www.linkedin.com/pulse/apache-paimon-iceberg-constantin-alexander-jey5e) | 6 |
| Sep 2025 | [PostgreSQL Physical Replication](https://www.linkedin.com/pulse/postgresql-physical-replication-easy-guide-constantin-alexander-sh5ie) | 49 |
| Sep 2025 | [PostgreSQL Logical Replication](https://www.linkedin.com/pulse/postgresql-logical-replication-constantin-alexander-hzlae) | 42 |
| Sep 2025 | [PostgreSQL Backup Strategies](https://www.linkedin.com/pulse/easy-postgresql-backup-strategies-complete-guide-constantin-alexander-uvlye) | 48 |
| 2014 | Virident vs Fusion IO — MySQL/MariaDB benchmarks (SpringbokSQL) | |
| 2012 | MySQL MHA vs Continuent Tungsten (AccelerationDB) | |

---

> *"Constantin is the data whisperer! Everything started looking up and information became both accessible and reliable."*

> *"Exceptionally technically skilled with great manager/architect potential."*

English, Russian, Spanish — all native | Organizer, **The Silicon Valley MySQL Meetup** | City University of Seattle
