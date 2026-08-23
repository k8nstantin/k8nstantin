# Constantin Alexander

**[SuperX](https://github.com/k8nstantin/superx)** · **[swindex](https://swindex.ai)** · **[KungFu](https://github.com/k8nstantin/kungfu)** · **[go-leiden](https://github.com/k8nstantin/go-leiden)** · **[LinkedIn](https://www.linkedin.com/in/constantin-alexander/)** (30K+) · **[dedomena.io](https://dedomena.io)**

---

I build the layer underneath autonomous agents: the operating system that governs them, and the graph index that makes their memory navigable. Twenty-five years of data architecture — Oracle, Apple, Walmart, ProxySQL, Iceberg lakehouses — now pointed at the problem of making AI agents accountable, durable, and directable.

---

## The thesis

**Agents are powerful and ungovernable.** They forget everything between sessions, hallucinate completion, drift from instructions, and give you no honest account of what they did or what it cost. The fix is not a better prompt — it is an operating system: capture everything they emit, model the work as a graph, schedule that graph, dispatch agents against it, and write the results back where the next agent will find them. Every fact an insert, nothing overwritten, all of it queryable.

**Graphs at scale are the other half.** Once the substrate remembers everything, the question becomes "what is related to this, three hops out, right now" — and that question is where property graphs fall over. So I built the index for it separately: hierarchical communities plus hub-routed traversal, answering multi-hop queries in microseconds without moving your data.

One system remembers and directs. The other makes the memory navigable. Both are Rust, both are open.

---

## Currently building

### [SuperX](https://github.com/k8nstantin/superx) — the agentic OS

**[k8nstantin.github.io/superx](https://k8nstantin.github.io/superx/)** · Rust + SurrealDB · v1.1.0 · Apache-2.0

Your coding agents already run all day. SuperX captures every one of them — full conversations, tool calls, token usage, history backfilled and then tailed live — with no agent-side configuration to install. Then it puts them to work.

![The SuperX dashboard](https://raw.githubusercontent.com/k8nstantin/superx/main/superx-mod-website/img/dashboard.png)

**The loop:** capture everything → model the work as a graph → schedule the graph → agents execute it → results land back in the graph.

- **Total capture.** Claude Code, Gemini CLI and Claude Desktop, read straight from their transcripts. Sessions identified `agent/uuid7`, the raw transcript line kept beside every message, cursor checkpoints so nothing is lost across restarts. On the machine this was written on: 46k events and 19k messages across 28 sessions.
- **The product graph.** Typed entities as nodes — product, task, rag, model, document, text, repo, credential, 18 kinds seeded and extensible at runtime — joined by native graph edges. Long-form text is itself a node linked by role edges, so every description, instruction and comment carries its own version history. Files attach as document nodes.
- **The runner.** A schedule row says only "at this time, kick this entity"; everything else already lives in the graph. It layers tasks over their `depends_on` edges and dispatches waves — independent work in parallel, dependants after their dependencies succeed. Each task spawns an agent with a prompt assembled from its instructions and its neighbourhood; output writes back as a `produced` node. Every run pins the exact instruction version it dispatched with, and the graph is re-read at every wave — so editing it mid-run steers everything not yet dispatched.
- **Modules all the way down.** The kernel does capture and the substrate; everything else is a module with its own database and service account, its own directory, log, CLI namespace, parameters, uuid7 identity and optionally its own UI — enable or disable them on a live OS.

![A SuperX product graph](https://raw.githubusercontent.com/k8nstantin/superx/main/superx-mod-website/img/graph.png)

**Design commitments:** append-only SCD-2 throughout — updates insert versions, unlinks insert retractions, cancels append rows, and "current" is computed rather than stored. Time-ordered UUIDv7 everywhere, so the substrate is its own historical log. No hardcoded policy: every tunable is a substrate parameter, and the agent executor has no default at all — until you set it, dispatch refuses loudly.

### [swindex](https://github.com/k8nstantin/swindex) — hierarchical small-world graph index

**[swindex.ai](https://swindex.ai)** · Rust · v0.1.0 · 142 tests

Multi-hop property-graph queries in microseconds. swindex builds and persists a layered structure over your graph — Leiden communities, then a hub graph over them — and answers "what is related to X" by routing through hubs the way HNSW routes through vectors, instead of walking edges.

**It is an index, not a database.** Your data stays wherever it already lives — MySQL, Postgres, Iceberg, Parquet, Arrow, an HTTP API — and swindex sits alongside as a sidecar that narrows a multi-hop question to a small bounded set of UUIDv7 ids. Your application then goes back to its own store for the rows. Persistence is Fjall; the design target and the measured numbers are both published in the repo rather than implied.

### [KungFu](https://github.com/k8nstantin/kungfu) — agent-native version control

Rust · Loro CRDTs

Git assumes humans working sequentially; agents work concurrently, and the merge tax is paid in branch graveyards. KungFu drops branches entirely: agents splice fine-grained mutations into one stream and CRDTs merge them, every mutation signed with Ed25519, with "Ghost State" isolating an agent's work mathematically until it is ready to be seen. Exposes an MCP server so agents use it natively.

### [go-leiden](https://github.com/k8nstantin/go-leiden) — the first native Go Leiden

Go · zero dependencies

The Go ecosystem had Louvain and no Leiden. This is a clean-room port of [graspologic-native](https://github.com/graspologic-org/graspologic-native) (Microsoft Research), the same implementation behind Microsoft GraphRAG — Leiden guarantees the well-connected communities Louvain cannot.

It is also the case study: **written end to end by autonomous agents, with no human code commits**, driven by OpenPraxis through five manifests of chained tasks, each with a cascading prompt and a feedback loop that rewrote its own scaffold when tasks failed.

### [Alan](https://github.com/k8nstantin/writing-system-for-ai) — a universal writing system for the age of AI

**[Live prototype](https://k8nstantin.github.io/writing-system-for-ai/)**

Meaning leaks at every hand-off: human to model, model to RAG, agent to agent. Natural language is too loose and code is too low-level, so nothing carries pure intent across the loop. Alan is a spatial-geometric notation where one meaning has exactly one written form — Leibniz's *characteristica universalis*, attempted now that there is finally both a need and an engine for it.

### [mcps](https://github.com/k8nstantin/mcps) — MCP servers for databases

Model Context Protocol servers that let agents manage real databases directly.

---

## [OpenPraxis](https://github.com/k8nstantin/OpenPraxis) — the predecessor to SuperX

Go · 19k+ lines · superseded, kept public as prior art

OpenPraxis was the first attempt at the same thesis: a spec-driven platform where products decompose into manifests and task DAGs, and agents execute them in isolated git worktrees, commit, push and open PRs autonomously. A single Go binary with an MCP server, an HTTP dashboard, mDNS peer discovery and Automerge CRDT sync.

**What it proved:** agents cannot be trusted to self-govern, and the fix is structural. Rules the agent must acknowledge and cannot override. An audit it cannot see or skip. Every dollar and turn attributed to the spec that caused it. Memory that survives the session. Products as graphs rather than tickets.

**What it taught me, and what SuperX does differently:** one node table and one edge table with kinds as data, instead of five entity tables that had to be collapsed later. Lifecycle derived from an append-only event log rather than a status column that drifts. A verdict as typed data rather than free text. The instruction stream — not a template table — as the surface where prompts actually evolve. And insert-only as a hard rule, so that history cannot be destroyed by a migration.

SuperX is that rewrite, in Rust, on an append-only substrate.

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
