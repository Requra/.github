# Requra.AI

> AI-Powered Requirements Engineering Platform

Requra.AI transforms meetings, documents, transcripts, and stakeholder discussions into structured software requirements, agile user stories, and export-ready backlogs using advanced AI workflows.

Built for Business Analysts, Product Managers, Agile Teams, and Software Companies to streamline the requirements engineering lifecycle.

---

# ✨ Features

## 🤖 AI-Powered Requirement Extraction

Extract requirements from:

* PDF files
* DOCX documents
* Meeting transcripts
* Audio recordings
* Live meetings (MVP)

The platform automatically identifies:

* Actors
* Goals
* Business needs
* Functional Requirements
* Non-Functional Requirements
* Business Rules

---

## 📋 Agile User Story Generation

Automatically generates standardized user stories:

```text
As a [User],
I want [Goal],
So that [Benefit]
```

---

## ✅ Acceptance Criteria Generation

Generate:

* Acceptance Criteria
* Definition of Done (DoD)
* Suggested validations for each requirement

---

## 🧠 Executive Summaries

AI-generated summaries that include:

* Key project decisions
* Requirement insights
* Missing information
* Pending questions
* Potential ambiguities

---

## 👥 Stakeholder Collaboration

* Invite stakeholders via email or shareable links
* Permission-based access:

  * Viewer
  * Commenter
* Requirement discussions & feedback
* Comment tracking workflow

---

## 📊 Interactive Dashboard

Review and edit:

* User stories
* Requirements
* Acceptance criteria
* Tags & categories
* Requirement classifications

---

## 📤 Export Ready for Jira & Azure DevOps

Export outputs as:

* Excel (.xlsx)
* CSV (.csv)

Structured specifically for:

* Jira imports
* Azure DevOps workflows

---

# 🎯 Problem Requra.AI Solves

Requirement gathering is often:

* Manual
* Time-consuming
* Fragmented
* Hard to track
* Error-prone

Teams lose valuable project information inside:

* Meetings
* PDFs
* Voice notes
* Emails
* Stakeholder discussions

Requra.AI centralizes and transforms all project inputs into structured engineering outputs ready for development teams.

---

# 🏗️ System Architecture

## Frontend

The frontend follows a scalable feature-based architecture using React and TypeScript.

```bash
src/
├── assets/
├── components/
│   └── ui/
├── features/
│   ├── auth/
│   ├── projects/
│   ├── requirements/
│   ├── stakeholders/
│   └── exports/
├── hooks/
├── layouts/
├── routes/
├── services/
├── store/
├── types/
└── utils/
```

### Frontend Stack

* React.js
* TypeScript
* Tailwind CSS
* Framer Motion
* GSAP
* React Query
* React Router

---

## Backend

Backend services are built using:

* ASP.NET Core (.NET)

The backend is responsible for:

* Authentication & authorization
* Project management
* File handling
* Export generation
* Collaboration workflows
* Notifications
* API orchestration

---

## AI Engine

The AI system is heavily powered by:

* LangGraph
* FastAPI
* LLM APIs
* NLP Pipelines
* Speech-to-Text Processing

The AI architecture is designed to be modular, scalable, and extensible.

---

# 🧠 AI Pipeline Flow

Requra.AI uses a graph-based AI workflow powered by LangGraph.

## Pipeline Nodes

```text
__start__

ingest

transcribe

extract

classify

generate

summarize

format

__end__
```

---

## Main Sequential Flow

```text
__start__ ➔ ingest

transcribe ➔ extract

extract ➔ classify

classify ➔ generate

generate ➔ summarize

summarize ➔ format

format ➔ __end__
```

---

## Conditional / Alternative Flows

Depending on the input type and workflow requirements, the pipeline supports dynamic routing:

```text
ingest ➔ transcribe

ingest ➔ extract

ingest ➔ format
```

This allows the AI engine to intelligently skip unnecessary stages for optimized processing.

---

# ⚙️ Core Functionalities

## 📂 Project Management

* Create and manage projects
* Workspace organization
* Role-based access control

---

## 📥 Input Ingestion

Supports:

* PDFs
* DOCX
* Text transcripts
* Audio files
* Live meeting sessions (MVP)

---

## 🧠 Requirement Engineering

Generate:

* Functional Requirements
* Non-Functional Requirements
* Business Rules
* User Stories
* Acceptance Criteria

---

## 👥 Stakeholder Workflow

* Invite stakeholders
* Review generated outputs
* Add comments & feedback
* Track feedback status

---

## 📤 Export Layer

Export requirements directly into:

* Excel
* CSV
* Jira-ready structures

---

# 🔒 Security & Privacy

Requra.AI includes:

* Authentication & Authorization
* Role-Based Access Control (RBAC)
* Secure document storage
* Permission-based sharing
* Tokenized project links
* Protected stakeholder access

---

# 📈 Scalability & Maintainability

The system is designed for:

* Modular AI workflows
* High scalability
* Multi-project support
* Concurrent collaboration
* Cross-platform compatibility
* Future AI feature expansion

---

# 🚀 Future Roadmap

## Phase 2+

* Conflict & ambiguity detection
* Requirement traceability mapping
* Direct Jira integration
* Real-time AI meeting analysis
* AI-generated wireframes
* Arabic language support
* Smart follow-up question generation

---

# 🧪 Example Workflow

## 1. Create Project

Business Analyst creates a new workspace.

---

## 2. Upload Inputs

Upload:

* PDFs
* DOCX files
* Meeting transcripts
* Audio files

---

## 3. AI Processing

Requra.AI extracts:

* Requirements
* User stories
* Acceptance criteria
* Business rules

---

## 4. Review & Edit

The BA/PM reviews generated outputs inside the dashboard.

---

## 5. Stakeholder Feedback

Stakeholders can:

* Review outputs
* Add comments
* Suggest changes

---

## 6. Finalize & Export

Export finalized requirements directly into Jira-ready formats.

---

# 🌍 Vision

> “From conversations to clear requirements — instantly.”

Requra.AI aims to modernize requirements engineering using AI-first workflows and collaborative stakeholder experiences.

---

# 👨‍💻 Team

Built with passion by the Requra.AI team.

---

# 📄 License

Proprietary Software — All Rights Reserved © Requra.AI
