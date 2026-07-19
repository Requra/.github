<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/hero-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/hero-light.svg">
  <img src="./assets/hero-light.svg" alt="Requra.AI turns scattered project context into evidence-grounded requirements and review-ready delivery artifacts." width="100%">
</picture>

<p align="center">
  <a href="https://requra-demo-rust.vercel.app/demo"><strong>Open Live Demo</strong></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Requra/frontend"><strong>Explore Frontend</strong></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Requra/ai-pipeline"><strong>Explore AI Pipeline</strong></a>
  &nbsp;·&nbsp;
  <a href="https://vrqplen1gy.apidog.io/"><strong>View API Docs</strong></a>
  &nbsp;·&nbsp;
  <a href="https://www.figma.com/design/t3LvbLJ0QiAynzr6mxsifi/UI-Shared?node-id=0-1&t=3JyWES2RjWpm9pKi-1"><strong>Open Figma</strong></a>
</p>

## What Requra.AI does

Requra.AI turns fragmented project knowledge—documents, notes, transcripts, meeting audio, and stakeholder context—into structured requirements, user stories, acceptance criteria, executive summaries, evidence, quality findings, and delivery-ready export data.

Unlike a generic LLM wrapper, the AI workflow retrieves source support and then performs a separate grounding step that verifies final evidence quotes against the original chunks. Business analysts and product teams can review the result, invite stakeholders, resolve feedback, and keep delivery artifacts connected to their source.

<table>
<tr>
<td width="33%" valign="top">

### Unstructured context

- PDF and DOCX files
- Notes and text
- Meeting transcripts
- Audio when STT is configured
- Project and meeting context

</td>
<td width="34%" valign="top">

### Grounded intelligence

- Parsing and chunking
- Requirement extraction
- Deduplication and classification
- BM25 or optional hybrid retrieval
- Evidence grounding and quality gates

</td>
<td width="33%" valign="top">

### Delivery artifacts

- Structured requirements
- User stories and criteria
- Executive summaries
- Source references and coverage
- Jira-compatible and spreadsheet-ready rows

</td>
</tr>
</table>

## Product experience

| Surface | Current experience |
| --- | --- |
| **Project workspaces** | Create, organize, search, inspect, edit, and remove project workspaces. |
| **Asynchronous analysis** | Submit source documents, follow queued/processing/terminal states, retry, and render normalized results. |
| **Evidence and traceability** | Review source quotes, document references, requirement confidence, coverage, and quality findings. |
| **Stakeholder review** | Invite viewers or commenters through focused public review experiences and collect feedback. |
| **Meeting workflows** | Schedule, invite, join, manage participants and consent, orchestrate recording, and review summaries. |
| **Delivery exports** | Produce browser-generated CSV and Jira-compatible structures; remote Jira/Azure issue creation is not implemented. |

> The recruiter demo is an explicit synthetic runtime. Its meeting media and transcription are simulated and isolated from production services.

## Platform architecture

<img src="./assets/platform-architecture.svg" alt="Requra.AI platform architecture showing the React application, external .NET backend, FastAPI AI API, durable PostgreSQL state, Redis RQ worker execution, providers, pgvector artifacts, optional callback, emergency direct AI fallback, and planned mobile client." width="100%">

The normal production boundary is **React frontend → external .NET backend → internal AI service**.

- The **backend** owns end-user authentication, project authorization, original source binaries, meetings, application persistence, and AI orchestration.
- The backend contract is visible through frontend adapters and current API documentation; its implementation repository is not published in this organization.
- The **AI service** owns request validation, deterministic fingerprinting, job execution, retrieval, grounding, quality controls, and the V1 result contract.
- The **mobile client** is planned or external; no mobile repository is currently published. It should consume authenticated backend APIs rather than internal AI routes.
- The direct browser-to-AI processor is an explicit two-flag emergency/demo fallback, not the normal customer path.

Editable source: [`profile/diagrams/platform-architecture.mmd`](./diagrams/platform-architecture.mmd)

## Asynchronous analysis lifecycle

<img src="./assets/analysis-sequence.svg" alt="Sequence showing frontend and backend job submission, FastAPI validation and fingerprinting, durable job persistence, Redis RQ dispatch, worker execution, result persistence, authoritative polling, and optional callback." width="100%">

1. The user starts analysis in the web application.
2. The frontend calls the backend's project-scoped analysis contract.
3. The backend submits an internal AI job.
4. FastAPI validates the request and computes a deterministic fingerprint.
5. The job is persisted and dispatched through Redis/RQ when production infrastructure is configured.
6. A worker recovers the source and executes the graph.
7. Chunks, evidence, requirements, stories, coverage, quality data, events, and the final result are persisted.
8. The backend polls durable status/result state and returns normalized data to the frontend.
9. A callback may notify the backend after persistence, but callback delivery is optional and best effort.

**Polling is authoritative. Callback failure does not invalidate an already persisted result.**

Editable source: [`profile/diagrams/analysis-sequence.mmd`](./diagrams/analysis-sequence.mmd)

## AI intelligence pipeline

<img src="./assets/ai-pipeline.svg" alt="Fifteen-node Requra.AI LangGraph workflow with audio routing through transcription, document and text routing through chunking, rejection short circuit, retrieval and grounding, generation, quality validation, bounded repair, summary, and formatting." width="100%">

The current graph contains 15 nodes:

`detect_file_type` → `ingest` → `transcribe` when audio → `parse_to_chunks` → `build_source_index` → `extract` → `dedupe_requirements` → `retrieve_evidence` → `classify` → `evidence_grounding` → `generate` → `quality_gate` → `repair_stories` when eligible → `summarize` → `format`

Key implementation characteristics:

- PDF, DOCX, text, and backend transcripts converge on the same graph.
- Accepted audio routes through configured Groq or Deepgram speech-to-text.
- Rejected or failed input short-circuits to formatting.
- BM25 is the deterministic primary retriever; pgvector-backed hybrid retrieval is optional.
- Evidence grounding verifies that attached quotes occur in source chunks.
- The only loop is the bounded `quality_gate → repair_stories → quality_gate` cycle.
- Chat providers are configurable through OpenRouter, OpenAI, or Groq; no single model is hard-coded as the product identity.

Editable source: [`profile/diagrams/ai-pipeline.mmd`](./diagrams/ai-pipeline.mmd)

## Evidence and traceability

<img src="./assets/traceability-chain.svg" alt="Traceability chain from a source document or meeting to provenance-aware chunks, grounded evidence, requirements, classification, user stories, acceptance criteria, source references, and quality coverage." width="100%">

**Retrieval improves recall; grounding verifies that the final quote exists in the source.** Final results can preserve document identity, page/speaker/timestamp-aware chunks, quotes, requirement confidence, story coverage, acceptance criteria, and aggregate quality findings.

## Product gallery

<p align="center">
  <img src="https://raw.githubusercontent.com/Requra/frontend/main/docs/readme/screenshots/dashboard.png" alt="Requra.AI dashboard showing portfolio activity and project workspaces." width="49%">
  <img src="https://raw.githubusercontent.com/Requra/frontend/main/docs/readme/screenshots/projects.png" alt="Requra.AI searchable projects workspace." width="49%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/Requra/frontend/main/docs/readme/screenshots/ai-results.png" alt="Requra.AI analysis results with requirements, stories, summaries, and quality metrics." width="49%">
  <img src="https://raw.githubusercontent.com/Requra/frontend/main/docs/readme/screenshots/evidence.png" alt="Requra.AI evidence view connecting generated artifacts to source references." width="49%">
</p>

The gallery reuses the current privacy-safe frontend showcase assets. Open the [interactive demo](https://requra-demo-rust.vercel.app/demo) for the complete synthetic recruiter workspace.

## Repository landscape

<table>
<tr>
<td width="50%" valign="top">

### [`Requra/frontend`](https://github.com/Requra/frontend)

React 19 · TypeScript · Vite · React Router · TanStack Query · Zustand · Axios · Tailwind CSS · Radix UI · Zod · React Hook Form · Vitest · MSW

Owns projects, analysis/result experiences, evidence views, stakeholder review, meeting surfaces, responsive UI, and the isolated recruiter-demo runtime.

</td>
<td width="50%" valign="top">

### [`Requra/ai-pipeline`](https://github.com/Requra/ai-pipeline)

Python · FastAPI · LangGraph · PostgreSQL · pgvector · Redis · RQ · BM25 · optional hybrid retrieval · Docker Compose

Owns durable asynchronous AI jobs, source preparation, requirement intelligence, evidence grounding, story generation, quality scoring, structured summaries, and the V1 result contract.

</td>
</tr>
<tr>
<td width="50%" valign="top">

### Backend — external contract

**External .NET service**

Contract represented through frontend adapters and API documentation. Expected ownership includes auth, projects, source files, meetings, persistence, and the bridge to the internal AI service.

**Repository not currently published in the organization.**

</td>
<td width="50%" valign="top">

### Mobile — planned / external

Expected to consume the same authenticated backend contracts and avoid direct access to protected internal AI routes.

**Repository not currently published; framework and release status are unverified.**

</td>
</tr>
</table>

## Capability status

| Capability | Status | Current truth |
| --- | --- | --- |
| PDF, DOCX, text, and transcript ingestion | ✅ Implemented | Parsed, normalized, chunked, and carried through the graph. |
| Audio transcription | ⚙️ Conditional | Requires audio enablement and configured Groq or Deepgram STT. |
| Requirement extraction, classification, and deduplication | ✅ Implemented | Includes structured schemas, confidence, and deterministic fallbacks. |
| BM25 evidence retrieval and quote grounding | ✅ Implemented | Retrieval and proof are separate steps. |
| Embeddings and hybrid retrieval | ⚙️ Conditional | Requires provider, database, and feature configuration. |
| Requirement-to-story traceability and coverage | ✅ Implemented | Source references and coverage mappings are in the result contract. |
| Story quality scoring and bounded repair | ⚙️ Conditional | Quality scoring is implemented; repair is configuration-controlled. |
| Semantic conflict candidates | ⚙️ Conditional | Depends on feature and provider/embedding availability. |
| Stakeholder review and feedback surfaces | ✅ Implemented | Current frontend experiences and contracts exist. |
| Meeting management | ✅ Implemented | Scheduling, invitations, lifecycle, consent, recording contracts, and summaries exist. |
| Recruiter demo | 🧪 Demo / simulated | Synthetic deterministic workspace; meeting media and transcription are simulated. |
| Direct remote Jira or Azure DevOps creation | 🛣️ Planned / incomplete | Current outputs are import-compatible structures only. |
| Real-time meeting AI suggestions | 🛣️ Planned / incomplete | Post-meeting and real-time analysis must not be conflated. |
| Backend implementation and deployment topology | 🔍 External / unverified | No backend source repository was available for inspection. |
| Mobile application | 🔍 Unverified / unpublished | No mobile repository was found. |

## Engineering credibility

- **Separated API and worker execution:** request handling does not perform the long-running graph inline.
- **Idempotent submission:** production-relevant request identity is fingerprinted so retries do not silently become different jobs.
- **Durable lifecycle state:** jobs, attempts, events, chunks, evidence, results, quality findings, and terminal state can persist in PostgreSQL.
- **Tenant/project scoping:** ownership identifiers flow through jobs and retrieval filters; authorization remains a backend responsibility.
- **Structured validation:** FastAPI/Pydantic contracts and typed frontend adapters bound transport shapes.
- **Evidence grounding:** retrieved support is not treated as proof until the quote is checked against source chunks.
- **Quality gates:** coverage, source mapping, story structure, acceptance criteria, duplicates, and aggregate scores are validated.
- **Safe observability:** request IDs, lifecycle events, redaction defaults, and provider metadata avoid raw production prompt logging.
- **Source retrieval controls:** the backend client applies origin restrictions, unsafe-address checks, size limits, and optional SHA-256 verification.
- **Honest operating modes:** in-memory and in-process fallbacks are for local/test use; production-shaped durability requires PostgreSQL and Redis/RQ.

Current gaps include AI-service rate limiting, a durable callback outbox, scheduled retention cleanup, and a complete prompt-injection defense. Reliability controls reduce risk but do not guarantee perfect correctness or zero hallucinations.

## Quick access and local development

| Resource | Link |
| --- | --- |
| Interactive demo | [requra-demo-rust.vercel.app/demo](https://requra-demo-rust.vercel.app/demo) |
| Product design | [Figma UI Shared](https://www.figma.com/design/t3LvbLJ0QiAynzr6mxsifi/UI-Shared?node-id=0-1&t=3JyWES2RjWpm9pKi-1) |
| API documentation | [Apidog](https://vrqplen1gy.apidog.io/) |
| Frontend source | [`Requra/frontend`](https://github.com/Requra/frontend) |
| AI source | [`Requra/ai-pipeline`](https://github.com/Requra/ai-pipeline) |

```bash
git clone https://github.com/Requra/frontend.git
cd frontend
npm ci
cp .env.example .env
npm run dev
```

```bash
git clone https://github.com/Requra/ai-pipeline.git
cd ai-pipeline
docker compose up --build
```

Use each repository's README and environment template for complete setup, safety gates, tests, and production configuration.

## Team and project context

Requra.AI is a coordinated multidisciplinary graduation project spanning frontend and product UI, backend and integrations, mobile client planning, AI and data intelligence, and shared testing and quality work. Historical role assignments are preserved in the project proposal; current code ownership should be taken from repository settings and contribution history rather than inferred from old documentation.

---

<p align="center">
  <strong>Capture context. Verify evidence. Align stakeholders. Deliver clearly.</strong>
</p>

<p align="center">
  Proprietary software · All rights reserved by the Requra.AI team
</p>
