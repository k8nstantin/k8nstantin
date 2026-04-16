# Constantin Alexander

**AI Pioneer & Data Platform Architect** | 20+ years designing data systems | Building autonomous AI agent systems

---

### Pioneering AI Agent Development

I build systems where AI agents work autonomously — writing code from specs, auditing their own output, and coordinating across sessions. Not prompting AI to help me code. Building AI that codes independently, follows rules, and gets audited by machines — not humans.

**What I've built:**

**OpenLoom** — A spec-driven development platform where you define products as specs, and autonomous AI agents build them. The agents spawn independently, execute against manifests, get audited by a server-side watcher they can't override, and share memory across sessions. 19,000+ lines of Go, 40+ MCP tools, 16-tab dashboard, peer-to-peer sync. *This is what autonomous software development looks like.*

**Schema Intelligence Chatbot** — AI-powered knowledge network over 17,000+ MySQL database objects across 27 databases and 5 servers. Gemini 2.5 Pro summarizes every table, stored procedure, view, event, and trigger. Embeddings power semantic search via Vertex AI Vector Search. A RAG chatbot answers natural language questions about schema architecture, generates impact analysis, and produces migration plans. *Ask it "what tables store customer data?" and it searches 17,000 objects semantically.*

**Serverless Data Lakehouse** — Fully serverless Apache Iceberg lakehouse on GCP. No persistent clusters — all compute is ephemeral Dataproc Serverless (pay-per-job). BigLake REST Catalog for metadata, BigQuery for SQL access, GCS for storage. Tables auto-appear in BigQuery UI. Infrastructure as code via Terraform with modular architecture.

---

### Featured Projects

#### [OpenLoom](https://github.com/k8nstantin/openloom) — Spec-Driven Development Platform for Autonomous Agents

Write specs. Agents build. Watcher audits. Humans approve.

- **Products > Manifests > Tasks** — hierarchical spec-driven development with dependency chains
- **Autonomous Execution** — spawns independent Claude Code / Cursor sessions from specs
- **Watcher** — server-side auditor agents cannot override (git, build, manifest compliance gates)
- **Visceral Rules** — non-negotiable constraints every agent must follow, violations flagged automatically
- **Shared Memory** — decisions, patterns, and context persist across all sessions and agents
- **Peer Sync** — multiple machines discover each other via mDNS and sync via Automerge CRDTs
- **Productivity Scoring** — real-time metrics: lines committed, completion rates, cost per task, 7-day trends
- **Dashboard** — 16-tab UI with task monitoring, cost analytics, DAG visualization, compliance tracking

**Tech:** Go, SQLite, Cytoscape.js, MCP (Model Context Protocol), Automerge CRDT, mDNS

#### Schema Intelligence Chatbot — AI Knowledge Network for Database Architecture

17,000+ database objects made searchable by natural language.

- **AI Summaries** — Gemini 2.5 Pro summarizes every table, procedure, view, event, trigger (5-10 sentences each)
- **Semantic Search** — text-embedding-005 (768-dim) + Vertex AI Vector Search (Tree-AH)
- **RAG Pipeline** — question + vector search + BigQuery enrichment + Gemini answer generation
- **3 Modes** — explore (search), impact analysis (what breaks if I change X), migration planning
- **Cloud Run API** — HTTP endpoints with IAM auth, deployed serverless
- **Chat UI** — multi-turn conversations with annotated sources, code display, session persistence

**Tech:** Python, Gemini 2.5 Pro, Vertex AI Vector Search, BigQuery, Cloud Run, Apache Iceberg, Dataproc Serverless

### Other Projects

| Project | Description |
|---------|-------------|
| [mcps](https://github.com/k8nstantin/mcps) | MCP Servers for managing databases |
| [tengo](https://github.com/k8nstantin/tengo) | Go La Tengo: MySQL automation library (fork) |

---

### Expertise

**AI/Agents:** Autonomous agent orchestration, LLM integration (Claude, Gemini, GPT-4), RAG pipelines, vector search, embeddings, MCP protocol, agent compliance and auditing

**Data:** MySQL, MariaDB, PostgreSQL, Apache Iceberg, BigQuery, Spark, Kafka CDC, Vector Search, schema intelligence

**Cloud:** GCP (Dataproc Serverless, BigLake, Vertex AI, Cloud Run, Vector Search), Terraform, serverless architecture

**Languages:** Go, Python, SQL, JavaScript, Rust

**Infrastructure:** Data lakehouse design, high availability, peer-to-peer systems, CRDT synchronization

### Publications & Community

- Published comparative analyses of MySQL/MariaDB solutions and high-availability systems
- Organizer of **The Silicon Valley MySQL Meetup**
- Active contributor to chaos engineering, data compliance, and distributed systems architecture

### Connect

- [LinkedIn](https://www.linkedin.com/in/constantin-alexander/)
- [dedomena.io](https://dedomena.io)
- Languages: English, Russian, Spanish
