# DRISHT1

### Digital Risk & Intelligence System for Threat Investigation

> **Connecting Telecom, Financial & Social Intelligence to Uncover Hidden Patterns, Detect Anomalies, and Generate Explainable, Actionable Insights.**

---

## 🛡️ About DRISHT1

**DRISHT1** is a unified, AI-powered digital intelligence and analytics platform designed to correlate multiple digital footprints into a single investigative view.

The platform brings together:

- 📞 **Telecom CDR/IPDR Data**
- 🏦 **Bank Statements & Financial Transactions**
- 🌐 **Social Media Activity**
- 🔗 **Cross-Domain Entity Resolution**
- 🕸️ **Relationship & Graph Analysis**
- 📊 **Behavioral & Temporal Analytics**
- 🚨 **Anomaly & Risk Detection**
- 🤖 **LLM-Based Explainable Intelligence**

Instead of analyzing each source independently, DRISHT1 focuses on the harder problem: **entity resolution + cross-source correlation**. The goal is to connect a phone number, bank account identifier, and social handle to a unified digital identity and then analyze relationships, behavior, and anomalies across the resulting network.

The LLM is deliberately not responsible for deciding what is anomalous. Deterministic and statistical analytics identify the anomaly first; the LLM explains the evidence in grounded, investigator-readable language.

---

## 🎯 Problem Statement

Investigators today often work with three siloed data sources when building a case or profile:

| Source | What it contains | Typical current practice |
|---|---|---|
| **Telecom CDR/IPDR** | Call logs, durations, tower IDs, IP session logs, data volume, ports | Manually reviewed in spreadsheets |
| **Bank statements** | Transactions, counterparties, UPI/NEFT/RTGS, amounts, timestamps | Manually reconciled, PDF-based |
| **Social media activity** | Posts, connections, sentiment, geo-tags, engagement | Rarely correlated with the other two |

Telecom records, financial transactions, and social-media activity can individually provide useful information, but important relationships may only become visible when multiple sources are correlated.

### DRISHT1 aims to address this challenge by providing:

> **A single analytics platform that ingests Telecom CDR/IPDR data, financial transactions, and user-provided social-media exports; resolves cross-domain entities; detects anomalies; analyzes relationships; and generates grounded, explainable intelligence for investigators.**

The hard problem is not simply parsing three file formats. It is **building the identity-resolution and relationship layer that ties them together**, while ensuring anomalies remain explainable and traceable to evidence.

---

# 🧠 Core Concept

DRISHT1 follows a **cross-domain intelligence approach**:

```text
                    ┌──────────────────────┐
                    │     TELECOM DATA     │
                    │      CDR / IPDR      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │                      │
                    │       DRISHT1        │
                    │                      │
                    │ Digital Intelligence │
                    │      Platform        │
                    │                      │
                    └──────────┬───────────┘
                               ▲
                               │
              ┌────────────────┴────────────────┐
              │                                 │
     ┌────────┴─────────┐              ┌────────┴─────────┐
     │  FINANCIAL DATA  │              │  SOCIAL MEDIA    │
     │ Transactions /   │              │ Posts / Handles  │
     │ Bank Statements  │              │ / Activity       │
     └────────┬─────────┘              └────────┬─────────┘
              │                                 │
              └────────────────┬────────────────┘
                               ▼
                    ┌──────────────────────┐
                    │ Entity Resolution &  │
                    │ Cross-Source Linking │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Relationship / Graph │
                    │      Analysis        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Anomaly Detection &  │
                    │ Pattern Discovery     │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Risk Scoring &       │
                    │ Explainable Insights │
                    └──────────────────────┘
```

---

# 🔍 What DRISHT1 Does

## 1. Multi-Source Data Analysis

DRISHT1 processes and normalizes structured and semi-structured data from multiple digital domains.

### 📞 Telecom — CDR/IPDR

**CDR fields**

- Caller number
- Callee number
- Timestamp
- Duration
- Cell tower ID
- IMEI / IMSI

**IPDR fields**

- Source IP
- Destination IP
- Port
- Protocol
- Timestamp
- Data volume
- NAT-mapped mobile number

**Processing**

```text
Parse
  ↓
Validate
  ↓
Normalize numbers to E.164
  ↓
Resolve tower ID to latitude/longitude
  ↓
Create relationship edges
```

**Potential anomaly signals**

- Burst calling
- Odd-hour activity
- Tower-hopping inconsistent with claimed location
- Contact with numbers already flagged elsewhere in a case
- Sudden increase in IPDR data volume
- Activity potentially consistent with file transfer or VPN tunneling

---

### 🏦 Financial Data

**Fields**

- Transaction date
- Amount
- Debit / credit
- Counterparty account/name
- Transaction mode
- UPI / NEFT / RTGS / cash
- Narration text

**Processing**

```text
PDF / CSV
  ↓
Table extraction
  ↓
Normalize transaction data
  ↓
Counterparty entity resolution
  ↓
Create financial relationship edges
```

**Potential anomaly signals**

- Multiple transactions near a reporting threshold
- Round-number transfers
- Sudden large inflows or outflows
- High-frequency transfers to newly seen counterparties
- Income vs. spend mismatch

---

### 🌐 Social Media Activity

**Fields**

- Post text
- Timestamp
- Engagement counts
- Mentioned handles
- Geo-tags where available

**Processing**

```text
User-provided export
  ↓
NER for names / locations / organizations
  ↓
Sentiment scoring
  ↓
Entity linking
  ↓
Relationship analysis
```

Social processing is designed around **user-provided data exports rather than unrestricted live scraping**.

**Potential anomaly signals**

- Sudden change in posting behavior
- Coordinated posting patterns
- Sentiment spikes
- Geo-tags inconsistent with other sources

---

## 2. Cross-Domain Entity Resolution

Entity resolution is one of the primary differentiators of DRISHT1.

A single real-world entity may appear differently across multiple datasets:

```text
                  ┌───────────────┐
                  │    ENTITY     │
                  │    Person A   │
                  └───────┬───────┘
                          │
             ┌────────────┼────────────┐
             │            │            │
             ▼            ▼            ▼
       Phone Number   Bank Account   Social Handle
             │            │            │
             ▼            ▼            ▼
            CDR        Transactions    Posts
```

### Resolution Strategy

**1. Deterministic matching**

- Exact phone numbers
- Exact account identifiers where authorized
- Known identifier relationships

**2. Probabilistic matching**

- Name similarity
- Shared contacts
- Temporal co-occurrence
- Cross-source behavioral similarity

**3. Confidence scoring**

Every inferred relationship is surfaced with a confidence value. Entities are not silently merged without evidence.

Every resolved entity becomes a node, while calls, transactions, and social links become relationship edges.

---

## 3. Relationship & Graph Intelligence

DRISHT1 models connected entities as a relationship network.

```text
                     Entity B
                        │
                        │ CDR
                        ▼
Entity A ─────────── Entity C
   │                    │
   │ Transaction        │ Social
   ▼                    ▼
Account X            Entity D
   │
   ▼
Account Y
```

The system can analyze:

- Communication relationships
- Financial relationships
- Social relationships
- Indirect connections
- High-degree entities
- Communities / clusters
- Shortest paths between entities
- Network centrality

For the current project scale, the graph is represented through relational edges in **Supabase PostgreSQL**, while **NetworkX** is used for in-memory graph analysis.

A separate Neo4j database is not required for the initial implementation.

---

## 4. Anomaly Detection

DRISHT1 uses two analytical tiers.

### Tier 1 — Statistical / Rule-Based

Fast and explainable detection without requiring training data.

- Z-score / IQR outlier detection
- Transaction amount anomalies
- Call-frequency anomalies
- Data-volume anomalies
- Odd-hour bursts
- Structuring-like transaction patterns
- Other threshold-based red flags

### Tier 2 — ML / Graph-Based

Machine-learning and graph features identify more complex deviations.

- Isolation Forest
- Local Outlier Factor
- DBSCAN
- Community detection
- Centrality analysis
- Shortest-path analysis

Example feature vector:

```text
Call Frequency
Transaction Volatility
Network Centrality
Communication Volume
Sentiment Volatility
Temporal Activity
```

### Evidence-Based Anomaly Object

Every anomaly raised by the engine should contain:

```text
Anomaly
│
├── Entity
├── Type
├── Tier
├── Severity
├── Raw Score
├── Confidence
├── Trigger
├── Evidence References
└── Timestamp
```

The structured anomaly object is passed to the LLM. The LLM should **never invent anomalies from raw data**.

---

# 🤖 LLM Intelligence Layer

DRISHT1 uses **Qwen3.5-9B** as its language-model layer.

The model is responsible for:

- Explaining detected anomalies
- Generating investigative narratives
- Answering free-text case questions through RAG
- Converting structured analytical output into readable summaries

### Critical Design Principle

> **The LLM explains what the analytical engine already found; it does not determine what counts as an anomaly.**

This separation improves:

- Explainability
- Auditability
- Reproducibility
- Reliability
- Human verification

---

## Qwen Fine-Tuning Strategy

The fine-tuning approach is **last-layer / LoRA-on-final-block fine-tuning**.

Full fine-tuning of a 9B model requires significant GPU memory and a sufficiently large dataset. DRISHT1 has a narrower objective, so the proposed strategy freezes most of the model and adapts only the final transformer block / LM head through LoRA.

### Why this approach fits

- Smaller GPU / VRAM footprint
- Lower risk of losing general capabilities
- Faster iteration
- Better fit for a narrow structured-to-narrative task

### What the fine-tuned model should learn

**1. Structured-to-narrative generation**

Convert an anomaly JSON object into a concise investigative note in a consistent output style.

**2. Free-text case Q&A**

This is primarily a **RAG problem**, not a fine-tuning problem. Case documents and anomaly summaries are retrieved at query time and supplied as context to the base model.

---

## Fine-Tuning Dataset

No public dataset exists for this exact task, so the training set will be created from generated or authorized data.

Proposed process:

- Generate real or synthetic anomaly objects from Tier 1 / Tier 2 detection
- Hand-write approximately **150–300 examples** covering anomaly types
- Format examples as instruction pairs
- Augment through controlled paraphrasing
- Human-review generated examples

Example:

```json
{
  "input": "<anomaly JSON + minimal context>",
  "output": "<grounded investigative narrative>"
}
```

---

## Training Setup

- **Framework:** Hugging Face `transformers` + `peft`
- **LoRA:** targeting the final transformer block
- **Suggested rank:** `r=8–16`
- **LM head:** `modules_to_save` can be limited to the LM head where appropriate
- **Hardware:** a single 24 GB GPU class machine such as RTX 3090/4090 or rented A10G/L4
- **Evaluation:** hold out 15–20% of handwritten examples
- **Evaluation criteria:** factual grounding + fluency, not loss alone

---

# 🔎 RAG & Case Intelligence

DRISHT1 uses PostgreSQL with **pgvector** so structured case data and embeddings can remain in the same managed database.

```text
Case Data
   ↓
Chunk / Normalize
   ↓
Generate Embeddings
   ↓
Supabase pgvector
   ↓
Similarity Retrieval
   ↓
Relevant Case Context
   ↓
Qwen
   ↓
Grounded Answer
```

Example questions:

```text
Which entities are connected to Entity A?

Show unusual financial activity around Entity B.

Are there communication and transaction relationships
between these two entities?

Summarize the strongest anomalies in this case.
```

---

# 🏗️ High-Level Architecture

```text
┌─────────────────────────────────────────────────────────────┐
│                     NEXT.JS FRONTEND                       │
│                                                             │
│ Dashboard | Entity Explorer | Network Graph | Timeline      │
│ Alerts | Case Management | Investigation Chat              │
└──────────────────────────────┬──────────────────────────────┘
                               │
                         REST / WebSocket
                               │
┌──────────────────────────────▼──────────────────────────────┐
│                 DJANGO + DRF API LAYER                     │
│                                                             │
│ Supabase JWT Verification | Case Management | Uploads      │
│ Entity APIs | Analytics APIs | Insight APIs                │
└──────────────┬──────────────┬───────────────┬───────────────┘
               │              │               │
        ┌──────▼─────┐ ┌──────▼────────┐ ┌────▼─────────────┐
        │ INGESTION  │ │  ANALYTICS &  │ │  LLM INFERENCE   │
        │   + ETL    │ │    ANOMALY    │ │     SERVICE      │
        │            │ │    ENGINE     │ │                  │
        │   Celery   │ │ scikit-learn  │ │ Qwen3.5-9B       │
        │   Workers  │ │ NetworkX      │ │ vLLM / Ollama    │
        └──────┬─────┘ └──────┬────────┘ └────────┬─────────┘
               │               │                   │
               └───────────────┼───────────────────┘
                               │
                ┌──────────────▼────────────────┐
                │            SUPABASE            │
                │                                │
                │ PostgreSQL                     │
                │ + pgvector                     │
                │ + Storage                      │
                │                                │
                │ Entities                       │
                │ CDR / IPDR                     │
                │ Transactions                   │
                │ Social Posts                   │
                │ Relationships                  │
                │ Anomalies                      │
                │ Cases                          │
                │ Embeddings                     │
                └──────────────┬─────────────────┘
                               │
                        ┌──────▼──────┐
                        │    Redis    │
                        │ Celery      │
                        │ Broker/Cache│
                        └─────────────┘
```

### Why this architecture?

The anomaly engine and LLM inference service are deliberately separated from Django.

- Anomaly detection remains deterministic/statistical and does not depend on the LLM being available.
- The LLM is used to explain already-detected anomalies and answer grounded case questions.
- The LLM can be fine-tuned or redeployed independently.
- Investigators can trace generated insights back to the originating analytical trigger.

---

# 🧩 Technology Stack

## Backend

- **Django 5.x + Django REST Framework**
  - API and compute layer
  - File-parsing orchestration
  - Entity resolution
  - Anomaly detection orchestration
  - LLM orchestration
  - Case/entity models

- **Celery + Redis**
  - Async processing for file parsing
  - Anomaly-analysis jobs
  - LLM inference jobs

- **Django Channels** *(optional)*
  - Live progress updates
  - Streaming LLM responses over WebSocket

---

## Database & Storage

### Supabase PostgreSQL

Supabase provides the managed PostgreSQL foundation for DRISHT1.

It provides:

- Structured relational data
- `pgvector` for embeddings
- Storage for raw uploaded files
- Web dashboard for inspecting data

This replaces the need to self-manage separate infrastructure for:

- PostgreSQL
- Vector database
- S3 / MinIO-style raw-file storage

Django connects to Supabase exactly like a normal PostgreSQL database using the Supabase connection string.

---

## Authentication

DRISHT1 uses **Supabase Auth** as the authentication provider, while Django handles request-level authorization.

```text
Next.js
   ↓
Supabase Auth
   ↓
Supabase JWT
   ↓
Django JWT Verification
   ↓
Django Authorization / RBAC
```

Users can authenticate through:

- Email/password
- Magic link
- OAuth

Django does not issue competing auth tokens. It verifies the incoming Supabase JWT and maps it to the required Django user/role for permission checks.

---

## Graph Storage Strategy

A separate graph database is intentionally avoided in the initial architecture.

The current relationship graph consists mainly of:

- Entities
- CDR relationships
- Transaction relationships
- Social relationships

These can be represented using PostgreSQL relational edges, recursive CTEs, and adjacency-list queries.

For analytical graph operations, DRISHT1 loads the required edges into **NetworkX** at analysis time.

PostgreSQL remains the source of truth.

---

## Frontend

- **Next.js 15 (App Router)**
- **TypeScript**
- **TailwindCSS**
- **shadcn/ui**
- **react-force-graph / Cytoscape.js**
- **Recharts / D3.js**
- **TanStack Query**

### Core frontend views

- Case Dashboard
- Entity Explorer
- Network Graph
- Timeline
- Alerts
- Investigation Chat

---

## ML / Data Processing

- **Python**
- **Pandas**
- **NumPy**
- **scikit-learn**
- **NetworkX**
- **pdfplumber**
- **camelot-py**
- **spaCy**
- **Hugging Face Transformers**
- **PEFT**

---

## LLM

- **Qwen3.5-9B**
- **LoRA / final-block fine-tuning**
- **vLLM**
- **Ollama**

The proposed Qwen model is intended to be self-hosted behind an internal-only service rather than exposed directly to the frontend.

---

# 🗄️ Suggested Database Schema

The core data model is built around a canonical entity and its identifiers.

```text
Entity (id, canonical_name, confidence_score, created_at)
  ├── PhoneIdentifier (entity_id, number, first_seen, last_seen)
  ├── BankIdentifier (entity_id, account_number_hash, bank_name)
  └── SocialIdentifier (entity_id, platform, handle)

CDRRecord
(id, caller_entity_id, callee_entity_id, timestamp, duration, tower_id)

IPDRRecord
(id, entity_id, src_ip, dst_ip, port, timestamp, data_volume)

Transaction
(id, from_entity_id, to_entity_id, amount, mode, timestamp, narration)

SocialPost
(id, entity_id, platform, text, timestamp, sentiment_score, geo_tag)

Anomaly
(id, entity_id, type, tier, severity, evidence_refs[], raw_score, created_at)

Insight
(id, anomaly_id, narrative_text, generated_by_model, reviewed_by_human)

Case
(id, name, investigator_id, entities[], status)
```

### Relationship Representation

```text
Entity A ──CDR────────────► Entity B
Entity A ──Transaction────► Account C
Entity A ──Social─────────► Entity D
```

---

# 🔄 Complete Intelligence Pipeline

```text
               DATA INGESTION
                     │
                     ▼
        DATA CLEANING & NORMALIZATION
                     │
                     ▼
              ENTITY RESOLUTION
                     │
                     ▼
          CROSS-SOURCE CORRELATION
                     │
                     ▼
          RELATIONSHIP / GRAPH DATA
                     │
                     ▼
             FEATURE ENGINEERING
                     │
                     ▼
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
       TIER 1                 TIER 2
     Statistical               ML
       Rules                Algorithms
          │                     │
          └──────────┬──────────┘
                     ▼
             ANOMALY OBJECT
                     │
                     ▼
              EVIDENCE LAYER
                     │
                     ▼
              RAG RETRIEVAL
                     │
                     ▼
                 QWEN LLM
                     │
                     ▼
          EXPLAINABLE INSIGHT
                     │
                     ▼
             INVESTIGATOR UI
```

---

# 📊 Potential Intelligence Views

## Entity Profile

```text
┌────────────────────────────────────────┐
│             ENTITY PROFILE             │
├────────────────────────────────────────┤
│ Entity ID:        E102                 │
│ Confidence:       0.94                 │
│                                        │
│ Telecom Links:    24                   │
│ Financial Links:  8                    │
│ Social Links:     13                   │
│                                        │
│ Anomalies:        5                    │
│ Relationships:    37                   │
└────────────────────────────────────────┘
```

---

## Relationship Graph

```text
                  ┌───────────┐
                  │ Entity B  │
                  └─────┬─────┘
                        │
                        │ CDR
                        │
┌───────────┐      ┌────▼─────┐      ┌───────────┐
│ Account A │──────│ Entity A │──────│ Entity C  │
└───────────┘      └────┬─────┘      └───────────┘
                        │
                    Social Link
                        │
                        ▼
                  ┌───────────┐
                  │ Entity D  │
                  └───────────┘
```

---

## Risk & Anomaly Dashboard

The platform can surface:

- Severity
- Confidence
- Triggering evidence
- Related entities
- Timeline
- Source records
- Cross-domain correlations
- Communication anomalies
- Financial anomalies
- Relationship anomalies

---

## Investigator Timeline

A unified timeline can combine:

```text
CDR Events
    +
IPDR Events
    +
Financial Transactions
    +
Social Activity
    +
Detected Anomalies
```

This enables investigators to examine changes in behavior over time and correlate events that would otherwise appear disconnected.

---

# 🚨 Responsible Intelligence

DRISHT1 is intended as an **investigative decision-support system**, not an autonomous decision-maker.

The platform is designed with an emphasis on:

- 🔐 Authorized data access
- 🔒 Data privacy
- ⚖️ Responsible AI
- 🧠 Explainable analytics
- 👤 Human-in-the-loop investigation
- 📋 Auditability
- 🎯 Evidence-based conclusions
- 🚫 Minimizing false positives

The system should operate only on **lawfully obtained and authorized data**.

Social-media processing is designed around user-provided exports rather than unrestricted live scraping.

Any intelligence generated by DRISHT1 should be treated as:

> **An analytical lead requiring appropriate human verification and lawful investigative procedures.**

---

# 🎯 Objectives

DRISHT1 aims to:

- **Unify** fragmented digital intelligence
- **Correlate** information across multiple data sources
- **Resolve** entities across heterogeneous datasets
- **Detect** statistical and ML-based anomalies
- **Analyze** complex relationships
- **Visualize** digital networks
- **Prioritize** significant patterns
- **Explain** anomalies using grounded LLM output
- **Reduce** manual analysis of large datasets
- **Maintain** a traceable and auditable analytical pipeline

---

# 🗺️ Development Roadmap

The architecture is planned as a **12-week implementation path**, with the option to compress it to approximately 4–6 weeks for a hackathon or extend it across a full semester.

| Phase | Weeks | Focus |
|---|---:|---|
| **0. Setup & Design** | 1 | Repository scaffolding, Django + DRF, Next.js, Supabase project, DB schema, review of CDR/fraud analytics tools |
| **1. Ingestion Pipeline (CDR first)** | 2 | CDR CSV parser, Celery pipeline, Django models against Supabase Postgres, file uploads to Supabase Storage |
| **2. Entity Graph MVP** | 2 | Deterministic entity resolution, relational graph queries, NetworkX analysis, basic graph visualization |
| **3. Anomaly Engine — Tier 1** | 1 | Statistical/rule-based CDR detectors wired to the Anomaly model and API |
| **4. Bank Statement + IPDR** | 2 | Extend parsers, anomaly detectors, and relationship analysis |
| **5. Social Media Module** | 1 | Export-based ingestion, NER, sentiment, and entity linking |
| **6. Tier 2 ML Detection** | 1 | Isolation Forest and graph algorithms across all sources |
| **7. Qwen3.5-9B Fine-Tuning** | 1.5 | Dataset construction, LoRA/last-layer training, evaluation, vLLM serving |
| **8. RAG + Insight API** | 1 | pgvector indexing in Supabase, retrieval pipeline, `/api/insights/`, `/api/case-chat/` |
| **9. Frontend Polish** | 1.5 | Dashboard, timeline, graph interaction, alerts, case chat |
| **10. Testing + Demo Prep** | 1.5 | End-to-end testing, architecture diagrams, report, demo using a synthetic realistic dataset |

### Recommended Development Strategy

The ordering matters.

A complete slice should work end-to-end before parallelizing across every source:

```text
One Data Source
      ↓
Ingestion
      ↓
Entity Resolution
      ↓
Visible Anomaly
      ↓
Evidence
      ↓
LLM Narrative
      ↓
Investigator UI
```

### Critical Path Risks

The two areas most likely to consume additional time are:

1. **Entity resolution**
2. **Fine-tuning dataset construction**

Fine-tuning examples should therefore be collected from the beginning of anomaly-engine development rather than waiting until the dedicated fine-tuning phase.

---

# 🏆 What Will Actually Impress Evaluators

### 1. Cross-Source Entity Resolution

Many projects can parse CSV files and show dashboards.

DRISHT1's stronger differentiator is:

> **Connecting three different digital domains to the same canonical entity with confidence scoring.**

---

### 2. Explainable Anomaly Detection

A working, explainable Tier-1 anomaly detector is more useful in a demonstration than a black-box ML model that cannot clearly explain why it generated a result.

---

### 3. Evidence-Grounded LLM

A fine-tuned model that reliably produces grounded narratives is more useful than a larger model that occasionally invents facts.

The evaluation should explicitly test:

- Factual grounding
- Evidence consistency
- Narrative fluency
- Absence of hallucinated facts

---

### 4. Unified Analytical View

The investigator should be able to move from:

```text
Entity
  ↓
Relationships
  ↓
Timeline
  ↓
Anomalies
  ↓
Evidence
  ↓
Explainable Insight
```

without manually switching between disconnected systems.

---

# 🚀 Vision

> **Transform fragmented digital footprints into connected, explainable intelligence.**

DRISHT1 envisions a future where investigators can move from:

```text
Millions of Records
        ↓
Data Correlation
        ↓
Entity Resolution
        ↓
Meaningful Relationships
        ↓
Anomalies
        ↓
Evidence
        ↓
Explainable Intelligence
```

without manually examining every individual record.

---

# 🏆 Built For

**Chandigarh Police Hackathon**

Developed as a collaborative team project focused on applying:

**Artificial Intelligence × Data Analytics × Graph Intelligence × Responsible AI**

to modern digital-investigation challenges.

---

# 👥 Team

**DRISHT1 Development Team**

Building technology at the intersection of:

**Artificial Intelligence × Data Analytics × Digital Intelligence × Law Enforcement**

---

# 📌 Project Status

🚧 **Currently under active development**

The architecture, analytical models, data pipelines, fine-tuning strategy, and investigator interfaces are evolving throughout development.

Current focus areas include:

- Data ingestion
- Entity resolution
- Anomaly detection
- Graph analytics
- Risk scoring
- Qwen fine-tuning
- RAG
- Supabase data layer
- Investigator dashboard
- Case management
- Security and audit controls

---

# ⭐ DRISHT1

### *See the connections. Detect the anomalies. Explain the intelligence.*
