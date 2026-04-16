# Constantin Alexander

**[LinkedIn](https://www.linkedin.com/in/constantin-alexander/)** (30K+) | **[OpenLoom](https://github.com/k8nstantin/openloom)** | **[dedomena.io](https://dedomena.io)**

---

I design data systems and build AI tools that make them smarter. Two decades of databases at enterprise scale, now applying that depth to autonomous AI agent development.

At **Gryphon AI** I built three things that connect: a serverless data lakehouse on GCP (Iceberg + BigLake + Dataproc Serverless, zero idle costs), an AI-powered schema intelligence chatbot that makes 17,000+ database objects searchable by natural language (Gemini + Vector Search + RAG), and **OpenLoom** — a framework where AI agents build software from specifications while machines audit every commit, track every dollar, and enforce engineering rules the agent can't override.

At **SpringbokSQL** I benchmarked storage hardware for MySQL/MariaDB workloads (Virident vs Fusion IO), consulted on high-availability architectures, and published technical comparisons that the community still references.

At **AccelerationDB** I worked on MySQL replication at scale — MHA vs Continuent Tungsten, multi-source replication, failover automation. The kind of infrastructure that keeps data flowing when things break at 3am.

---

## Deep Technical Knowledge

This is what I actually know, from building it and writing about it:

**Replication & High Availability** — MySQL GTID vs MariaDB domain-based GTIDs and why they're incompatible. PostgreSQL streaming replication with WAL archiving, synchronous standby, cascading replicas. Patroni for automated failover with etcd clustering, HAProxy load balancing, split-brain prevention. I've configured all of these in production and written the guides people use to learn them.

**Database Internals** — How SQL actually executes: the 9-step pipeline from FROM to LIMIT. Why nested loop joins are O(n*m) while hash joins are O(n+m). Reading EXPLAIN plans — buffer hits vs disk reads, cardinality estimates, sargable predicates. The difference between knowing SQL syntax and understanding what the engine does with it.

**Change Data Capture** — PostgreSQL logical replication into Apache Flink for real-time streaming. CDC pipeline design with Kafka sinks, Iceberg sinks, tumbling window aggregations. Checkpoint configuration, backpressure management, schema evolution. End-to-end from database WAL to analytics warehouse.

**Data Lakehouse** — Apache Iceberg table maintenance: compaction (40-60% storage reduction), snapshot expiration, orphan file cleanup, Z-ordering for query optimization. Orchestration with Airflow DAGs and Kubernetes CronJobs. Cost modeling per file, per snapshot, per compute job.

**Backup & Recovery** — PostgreSQL pg_dump, pg_basebackup, WAL archiving, PITR. Size-specific strategies from 10GB to multi-terabyte. Automated validation frameworks that verify referential integrity after restore. Cloud-native backup across AWS RDS, GCP Cloud SQL, Azure PostgreSQL.

**AI Agent Orchestration** — Building OpenLoom taught me how to make AI agents productive: spec-driven task decomposition, dependency chains, autonomous execution with MCP protocol, server-side auditing that agents can't game, cost tracking per task per turn per line of code, shared memory across sessions, peer-to-peer sync with Automerge CRDTs.

---

## OpenLoom

The project I'm most focused on. A spec-driven development framework for autonomous coding agents.

You define products as hierarchies of specifications. The framework spawns agent sessions, feeds them the spec and context from every previous session, and they work independently — branch, code, commit, PR. A watcher audits every task: commits exist? Code compiles? Deliverables addressed? The agent doesn't know it's being watched.

Every conversation recorded. Every tool call captured. Every dollar tracked. Productivity scoring shows completion rates, first-attempt success, cost per task, 7-day trends.

19,000+ lines of Go. 40+ MCP tools. 70+ API endpoints. 16-tab dashboard. Single binary.

**[github.com/k8nstantin/openloom](https://github.com/k8nstantin/openloom)**

---

## Published

| Date | Article | Likes |
|------|---------|-------|
| Oct 2025 | [MySQL and MariaDB so similar, alas so different](https://www.linkedin.com/pulse/mysql-mariadb-so-similar-alas-different-constantin-alexander--ifu9e) — GTID incompatibilities, replication gotchas, migration strategies | 71 |
| Oct 2025 | [Demystify SQL](https://www.linkedin.com/pulse/demystify-sql-constantin-alexander--7lyoe) — How SQL actually executes: the 9-step pipeline, join algorithms, EXPLAIN plans | 16 |
| Oct 2025 | [PostgreSQL + Apache Flink CDC](https://www.linkedin.com/pulse/postgresql-apache-flink-cdc-integration-constantin-alexander--qhnle) — Real-time streaming from PostgreSQL WAL to analytics via Flink | 24 |
| Oct 2025 | [Apache Iceberg Maintenance](https://www.linkedin.com/pulse/easy-apache-iceberg-maintenance-guide-constantin-alexander-oq8ve) — Compaction, snapshot expiry, orphan cleanup, 40-60% storage reduction | 9 |
| Sep 2025 | [PostgreSQL Patroni Integration](https://www.linkedin.com/pulse/easy-postgresql-patroni-intergration-constantin-alexander-tc8je) — Automated HA with etcd, HAProxy, split-brain prevention | 35 |
| Sep 2025 | [Terraform Modules](https://www.linkedin.com/pulse/easy-terraform-modules-constantin-alexander-9hlne) — Modular infrastructure as code patterns | 7 |
| Sep 2025 | [Apache Paimon + Iceberg](https://www.linkedin.com/pulse/apache-paimon-iceberg-constantin-alexander-jey5e) — Comparing lakehouse table formats | 6 |
| Sep 2025 | [PostgreSQL Physical Replication](https://www.linkedin.com/pulse/postgresql-physical-replication-easy-guide-constantin-alexander-sh5ie) — WAL streaming, synchronous standby, cascading replicas, failover | 49 |
| Sep 2025 | [PostgreSQL Logical Replication](https://www.linkedin.com/pulse/postgresql-logical-replication-constantin-alexander-hzlae) — Publication/subscription, selective table replication | 42 |
| Sep 2025 | [PostgreSQL Backup Strategies](https://www.linkedin.com/pulse/easy-postgresql-backup-strategies-complete-guide-constantin-alexander-uvlye) — pg_dump to PITR, size-specific strategies, cloud-native backup | 48 |
| Oct 2014 | Virident vs Fusion IO — MySQL/MariaDB storage benchmarks (SpringbokSQL) | |
| May 2012 | MySQL MHA vs Continuent Tungsten replication comparison (AccelerationDB) | |

---

> *"Constantin is the data whisperer! Everything started looking up and information became both accessible and reliable."*

> *"Exceptionally technically skilled with great manager/architect potential."*

Organizer, **The Silicon Valley MySQL Meetup** | English, Russian, Spanish — all native
