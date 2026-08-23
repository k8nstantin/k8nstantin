# Constantin Alexander

**[SuperX](https://github.com/k8nstantin/superx)** · **[swindex](https://swindex.ai)** · **[KungFu](https://github.com/k8nstantin/kungfu)** · **[go-leiden](https://github.com/k8nstantin/go-leiden)** · **[LinkedIn](https://www.linkedin.com/in/constantin-alexander/)** (30K+) · **[dedomena.io](https://dedomena.io)**

---

**Let's build intelligent data.**

Data systems have always been able to store and serve. What they have not been able to do is *mean* anything — to carry their own semantics, so that a person, or now an agent, can ask a real question and get an answer that is grounded rather than plausible. That seam is where I work: making data infrastructure intelligent, and building the execution layer that lets autonomous agents act on it with a record of what they did.

Four threads, all running at once.

**Retrieval that understands structure.** Vector search finds text that reads similar; it does not find entities that are actually related. The moment a question needs two or three hops of context, embeddings alone start returning confident nonsense — which is the failure mode behind most disappointing RAG deployments. So the retrieval work is graph-shaped: community detection to give a graph its natural neighbourhoods ([go-leiden](https://github.com/k8nstantin/go-leiden), the algorithm behind Microsoft GraphRAG), and a hierarchical small-world index that answers multi-hop questions in microseconds without moving the underlying data ([swindex](https://swindex.ai)). Alongside it, verification: "the retrieval is good" is a claim that should be measured against ground truth — read the source, interrogate the system, log every gap — not asserted.

**An operating system for agents.** Coding agents forget everything between sessions, cannot be asked what they did or what it cost, and report their own completion. [SuperX](https://github.com/k8nstantin/superx) is the substrate that fixes those three: it captures every agent on the machine from their own transcripts, records the work as an append-only graph, schedules that graph, dispatches agents against it in dependency order, and writes results back where the next agent will find them. Insert-only throughout — nothing is overwritten, so the history is evidence rather than a story.

**Autonomous agent development.** The point of an agent OS is agents that ship. [go-leiden](https://github.com/k8nstantin/go-leiden) is the controlled experiment: a production library — the first native Leiden implementation in Go — written end to end by autonomous agents with no human code commits, driven through chained specs with a feedback loop that rewrote its own prompt scaffold when tasks stalled. [OpenPraxis](https://github.com/k8nstantin/OpenPraxis) was the platform that ran it, and what it exposed about agent governance is what SuperX was rebuilt to solve.

**Version control for agents.** Git assumes one author at a time, working in sequence; that assumption is what turns concurrent agents into merge conflicts and abandoned branches. [KungFu](https://github.com/k8nstantin/kungfu) removes branching entirely: agents splice fine-grained mutations into a single stream and CRDT semantics (Loro) merge them without a reconciliation step, every mutation signed with Ed25519, with "Ghost State" keeping an agent's work mathematically isolated until it is ready to be seen. It exposes an MCP server, so an agent drives version control natively rather than shelling out to a porcelain built for humans.

**The foundation under all of it.** Twenty-five years of database and distributed-systems architecture: relational engines at scale, synchronous replication and high availability, change-data-capture pipelines, lakehouse platforms, connection pooling and query routing. That background is why the agent substrate looks the way it does — SCD-2 chains, current state computed rather than stored, insert-only audit trails, time-ordered keys, indexes designed for the read path. Agent infrastructure is a data problem wearing a new hat, and much of it is being built by people who have never had to run a system where the history had to be correct.

---

## Currently building

### [SuperX](https://github.com/k8nstantin/superx) — the agentic OS

**[k8nstantin.github.io/superx](https://k8nstantin.github.io/superx/)** · Rust · SurrealDB · v1.1.0 · Apache-2.0

An operating system for the coding agents already running on your machine: it captures everything they emit, models the work they should do as a graph, schedules that graph, dispatches agents against it, and writes the results back into the same substrate.

![The SuperX dashboard](https://raw.githubusercontent.com/k8nstantin/superx/main/superx-mod-website/img/dashboard.png)

**Substrate.** SurrealDB, insert-only. A node is an immutable UUIDv7 anchor row plus an SCD-2 chain of state rows; "current" is the newest row in the chain, computed at read time, never a mutated column. Edges are a native `TYPE RELATION … ENFORCED` table written by `RELATE`, so traversal follows record pointers and costs a node's degree rather than the size of the edge history; unlinking appends a retraction row on the same edge chain instead of deleting. The kernel's service account issues only `SELECT` and `CREATE` — there is no verb in the codebase that can `UPDATE` or `DELETE`, which is what makes the audit trail structural rather than aspirational.

**Capture.** Per-agent adapters tail the transcript files that Claude Code, Gemini CLI and Claude Desktop already write — no hooks, no agent-side configuration, nothing to install into their settings. History is backfilled on first contact, then followed live from per-file byte-offset cursors so a restart resumes exactly where it stopped. Parsing is deliberately tolerant: recognized lines become typed `message` rows with the raw JSON retained alongside, and anything unrecognized still lands as telemetry rather than being dropped. Sessions are identified `agent/uuid7`; token usage, tool calls and context pressure are read from the transcripts rather than estimated.

**The graph.** Eighteen node and edge kinds seeded and extensible at runtime — `product`, `task`, `rag`, `model`, `document`, `text`, `repo`, `credential`, joined by `contains`, `depends_on`, `consults`, `describes`, `instructs`, `produced`, `attached`. Kinds are rows in a registry table, not a Rust enum, so adding one is a command rather than a release. Long-form text is itself a node linked by a role edge, which means a description or a set of instructions has its own version chain independent of the entity it annotates, and one text can serve several entities.

**The runner.** A schedule row carries a time, an entity reference and a recurrence — nothing else; the plan is already in the graph. Firing resolves the target's subgraph, layers its task nodes over `depends_on` with a Kahn topological sort (cycles are refused with the offending path named), and dispatches each wave with a bounded parallelism parameter. Readiness is scoped to the current firing rather than lifetime history, so a re-run is not blocked by a completion from last week. Each run row pins the `valid_from` of the instruction text it dispatched with, and the subgraph is re-read at every frontier re-evaluation, so editing the graph mid-run steers everything not yet dispatched. Output writes back as a `produced` text node linked to the task.

![A SuperX product graph](https://raw.githubusercontent.com/k8nstantin/superx/main/superx-mod-website/img/graph.png)

**Modules.** The kernel owns boot, capture, the telemetry stream and the substrate verbs; everything else is a module registered through a compile-time inventory and given its own database (`superx/<name>`) and service account, its own directory, log target, CLI namespace, substrate parameters, UUIDv7 identity, and optionally its own HTTP UI discovered from the substrate. Modules depend on the kernel and never on each other; cross-module calls go through the kernel's in-process CLI dispatch. They can be enabled and disabled on a running OS, and a module that fails to register does not stop the others from booting.

**Operationally:** one command to a background OS with a self-upgrading schema (`superx --initialize`, then `restart` after a rebuild), typed Rust→TypeScript bindings across both dashboards, and three gates enforced in CI — `cargo test --workspace`, `clippy -D warnings`, and a repository-specific architecture audit that fails the build on hardcoded tunables, DDL outside approved schema files, and mutation verbs in the kernel.

### [swindex](https://github.com/k8nstantin/swindex) — hierarchical small-world graph index

**[swindex.ai](https://swindex.ai)** · Rust · v0.1.0 · 142 tests

An index for property graphs, not a database. It builds and persists a layered structure over a graph — Leiden communities, then a hub graph over those communities — and answers "what is related to X" by routing through hubs rather than walking edges, the way HNSW routes through vectors instead of scanning them.

Data stays in whatever store already holds it: MySQL, Postgres, Iceberg, Parquet, Arrow, an HTTP API. swindex runs alongside as a sidecar, narrows a multi-hop question to a small bounded set of UUIDv7 ids, and hands them back; the application fetches the rows from its own store, so a columnar scan filtered by id replaces a graph traversal.

All four architecture layers are built and persisted. Queries today route through two of them — cluster lookup plus one-hop hub expansion — with region routing and multi-hop hub navigation tracked for v0.2. Persistence is Fjall (LSM). Measured: microsecond queries at 50k-node scale; the design target and the benchmark methodology are both published in the repo rather than asserted.

### [KungFu](https://github.com/k8nstantin/kungfu) — agent-native version control

Rust · Loro CRDTs

Git assumes sequential human authorship; concurrent agents pay for that assumption in merge conflicts and abandoned branches. KungFu removes branching: agents splice fine-grained mutations into a single stream and CRDT semantics merge them without a reconciliation step. Every mutation is signed with Ed25519, and "Ghost State" keeps an agent's work mathematically isolated until it is exposed. Ships an MCP server so agents drive it directly.

### [go-leiden](https://github.com/k8nstantin/go-leiden) — the first native Go Leiden

Go · zero dependencies

The Go ecosystem had Louvain (`gonum/graph/community`) and no Leiden. This is a clean-room port of [graspologic-native](https://github.com/graspologic-org/graspologic-native) (Microsoft Research), the implementation behind Microsoft GraphRAG. Leiden's refinement phase guarantees well-connected communities, which Louvain cannot; the package covers the local-move / refinement / aggregation phases, modularity and CPM quality functions, and hierarchical clustering.

It is also a controlled experiment: **written end to end by autonomous agents with no human code commits**, driven by OpenPraxis as five chained manifests, each task receiving a cascading prompt (product → manifest → spec → coding standards) and a feedback loop that rewrote the prompt scaffold when a task's pass rate stalled.

### [Alan](https://github.com/k8nstantin/writing-system-for-ai) — a universal writing system for the age of AI

**[Live prototype](https://k8nstantin.github.io/writing-system-for-ai/)**

Meaning is re-encoded at every hand-off — human to model, model to retrieval, agent to agent — and each translation loses intent: natural language is ambiguous, code specifies action without purpose. Alan is a spatial-geometric notation in which one meaning has exactly one written form, so an instruction cannot drift as it crosses the loop. Leibniz's *characteristica universalis*, attempted with an engine that can finally read it.

### [mcps](https://github.com/k8nstantin/mcps) — MCP servers for databases

Model Context Protocol servers that give agents direct, typed access to real database instances.

---

## Where to start

These are single-author projects with room for collaborators, and the interesting parts are genuinely unclaimed. Every repo runs the same discipline: an issue defines the work, one short-lived branch per issue, the PR body opens with `Closes #N`, and the gates have to be green before merge. That is the whole ceremony.

**[SuperX](https://github.com/k8nstantin/superx)** — Apache-2.0. The module contract is documented end to end in [`docs/MODULES.md`](https://github.com/k8nstantin/superx/blob/main/docs/MODULES.md), and `superx-mod-hello` exists to be copied: a module is a crate that declares a descriptor, registers itself, and gets its own database, directory, log, CLI namespace and parameters for free. A new **agent adapter** is one trait with two methods — Cursor, Codex, Copilot and Windsurf are all unclaimed, and each one widens what the OS can see. Open work also includes the [entities dashboard epic (#216)](https://github.com/k8nstantin/superx/issues/216), [module-owned parameters (#265)](https://github.com/k8nstantin/superx/issues/265), and an [HTTP verb for task instructions (#248)](https://github.com/k8nstantin/superx/issues/248).

**[swindex](https://github.com/k8nstantin/swindex)** — BSL 1.1, [CONTRIBUTING.md](https://github.com/k8nstantin/swindex/blob/main/CONTRIBUTING.md), [DESIGN.md](https://github.com/k8nstantin/swindex/blob/main/DESIGN.md), [BENCHMARKS.md](https://github.com/k8nstantin/swindex/blob/main/BENCHMARKS.md). The v0.2 questions are open and specific: [hub-corridor navigation against a cluster-adjacency baseline (#72)](https://github.com/k8nstantin/swindex/issues/72) as a measured go/no-go, [region adjacency through the persisted index (#73)](https://github.com/k8nstantin/swindex/issues/73), a [Parquet source and sidecar harness (#74)](https://github.com/k8nstantin/swindex/issues/74), and an [elastic-hashing investigation (#35)](https://github.com/k8nstantin/swindex/issues/35) for the hot path. Benchmarks and adversarial review of the design are as welcome as code — [#44](https://github.com/k8nstantin/swindex/issues/44) is exactly that, an invited database-architect pass.

**[KungFu](https://github.com/k8nstantin/kungfu)** — [CONTRIBUTING.md](https://github.com/k8nstantin/kungfu/blob/main/CONTRIBUTING.md), [DESIGN.md](https://github.com/k8nstantin/kungfu/blob/main/DESIGN.md), roadmap in [#10](https://github.com/k8nstantin/kungfu/issues/10). CRDT semantics, AST-aware validation and agent patching are the live threads.

**[go-leiden](https://github.com/k8nstantin/go-leiden)** — the smallest on-ramp: [`sync.Pool` in the refinement phase (#8)](https://github.com/k8nstantin/go-leiden/issues/8) to cut GC pressure at scale, and a [comparison against newer prior art (#10)](https://github.com/k8nstantin/go-leiden/issues/10).

Useful without writing code: run any of it against a workload it was not designed for and file what breaks. Benchmarks on hardware I do not have. Design critique on the open architecture issues — the graph-index work in particular benefits more from someone finding the flaw early than from another feature. Questions that are not bug reports belong in Discussions — [SuperX](https://github.com/k8nstantin/superx/discussions), [swindex](https://github.com/k8nstantin/swindex/discussions), [KungFu](https://github.com/k8nstantin/kungfu/discussions), [go-leiden](https://github.com/k8nstantin/go-leiden/discussions) — and anything with a reproduction belongs in an issue on that repo. I also read [LinkedIn](https://www.linkedin.com/in/constantin-alexander/).

---

## [OpenPraxis](https://github.com/k8nstantin/OpenPraxis) — the predecessor to SuperX

Go · ~19k lines · superseded, kept public as prior art

A spec-driven platform where products decompose into manifests and task DAGs and agents execute them in isolated git worktrees — commit, push, open a PR — as a single binary carrying an MCP server, an HTTP dashboard, mDNS peer discovery and Automerge CRDT sync.

**What it established:** agents do not reliably self-report completion, so verification has to run server-side where the agent cannot see or skip it; constraints have to be acknowledged before work starts and checked mechanically afterwards; cost and turns have to attribute back to the spec that caused them; and memory has to outlive the session.

**What the rewrite changed.** One node table and one edge table with kinds as data, rather than five entity tables that later had to be collapsed into one. Lifecycle derived from an append-only event log instead of a status column that no code path ever closed. Verdicts as typed records rather than free text — collapsing comment types into one alias silently turned "was this approved" into a question nothing could answer. The per-entity instruction stream, not a template table, as the surface where prompts actually evolve, because that is where every real prompt was written. And insert-only as a hard rule: OpenPraxis dropped sixteen tables at boot as its migration strategy, which is not recoverable.

SuperX is that rewrite, in Rust, on an append-only substrate.

---

## Semantic search over an enterprise data estate

Designed and built a semantic knowledge network that makes an organization's own database estate searchable in natural language — tables, views, stored procedures, events and triggers across many databases and servers, each summarized by an LLM with PII detection and index analysis, embedded and indexed for vector search, enriched from the warehouse, and answered with source citations rather than assertions.

Three working modes: **explore** (what handles this part of the business?), **impact analysis** (what breaks if this changes?), and **migration planning**. Multi-turn chat with session persistence, deployed serverless. The full pipeline — parsing, LLM summarization, embedding, knowledge-graph construction, categorization — runs as a single atomic job so the whole index is rebuildable from source at low cost rather than patched in place.

This is the system that pointed the retrieval work toward graphs: it worked well for "find me things about X" and revealed exactly where vector similarity stops being enough.

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
