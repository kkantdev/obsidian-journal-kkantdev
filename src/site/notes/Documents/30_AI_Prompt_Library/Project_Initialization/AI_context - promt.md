---
{"dg-publish":true,"permalink":"/documents/30-ai-prompt-library/project-initialization/ai-context-promt/","tags":["promt","aicontext","antigravity","ClaudeCode"],"dg-note-properties":{"tags":["promt","aicontext","antigravity","ClaudeCode"]}}
---

hey


PROMT

````
Initialize Project Context Governance Protocol.

Your task is to create a folder named `.ai_context` at the root of this project. Inside this folder, you must initialize and maintain exactly five Markdown files. These files will act as our source of truth, memory, and guardrails to prevent context drift and optimize token usage. 

Please create the folder and generate the following five files immediately using the templates provided below. Ensure you replace any placeholder bracket text (like [Your Project Name]) with the actual details of this repository.

---

### File 1: `.ai_context/README.md`
```markdown
# 🤖 Project Memory & Context Index
> **CRITICAL RULE FOR THE AI:** Read this file FIRST before touching any code or files. This is your onboarding map. Do not load the other `.md` files in this directory unless your specific task requires them.

## 📂 Context Directory Map

| File Name | What it Contains | WHEN YOU SHOULD READ IT |
| :--- | :--- | :--- |
| `README.md` | This index and onboarding rules. | **Always read first** on a new session. |
| `completed_features.md` | A historical log of what is 100% built and working. | Read *only* if you are debugging an existing feature or checking how a past feature was implemented. |
| `future_roadmap.md` | A structured backlog of what to build next. | Read *only* when the user says "What's next?" or asks you to build a new feature. |
| `architecture_map.md` | The visual folder tree and app data flow. | Read *only* if you are creating new routes, folders, or changing how data moves. |
| `secrets_manifest.md` | Tracking map for environment variables. | Read *only* when setting up a new API key, OAuth, or backend service. |

## 📜 Global AI Execution Rules
1. **Never guess:** If the current code state doesn't match `completed_features.md`, stop and ask the user for clarification.
2. **Update on Completion:** When you finish a task, you are responsible for updating the relevant specific file (e.g., moving a task from roadmap to completed).
3. **Protect Secrets:** Never hardcode actual API strings. Check `secrets_manifest.md` for variable naming conventions.
````

---

### File 2: `.ai_context/completed_features.md`

Markdown

```
# Completed Features Log
> **AI GOVERNANCE RULE:** This file is READ-ONLY for future AI sessions regarding historical context. New entries must only be appended upon 100% feature completion and verification.

## 📜 System Rules for AI
1. When a feature passes local verification, remove it from `future_roadmap.md` and append it here.
2. Include the implementation date, core files modified, and verification steps.

---

## 🛠️ Implemented Features & Core Stack
- [AI Instructions]: Scan the root files (like package.json or config files) and list the current core technologies, frameworks, and existing foundation features below as the initial entry.
```

---

### File 3: `.ai_context/future_roadmap.md`

Markdown

```
# Future Roadmap & Backlog
> **AI GOVERNANCE RULE:** This file is the source of truth for the project's next steps. Do not invent features out of scope unless explicitly prompted by the user.

## 📜 System Rules for AI
1. Always prioritize items from **Phase 1** from top to bottom.
2. Do not jump to a later phase until the current phase items are marked complete and migrated to `completed_features.md`.

---

## 🚀 Near-Term Backlog

### Phase 1: Current Objectives
- [ ] **Task 1:** [AI Instructions: Leave an empty task item here for the user to define their immediate next step]
```

---

### File 4: `.ai_context/architecture_map.md`

Markdown

```
# Architecture Map & Data Flow
> **AI GOVERNANCE RULE:** Update this map immediately whenever you introduce new directories, permanent page routes, API endpoints, or database tables.

## 📜 System Rules for AI
1. Maintain the visual file tree below to match the physical repository structure exactly.
2. Document high-level data flow changes when new infrastructure elements are added.

---

## 📂 Directory Tree
- [AI Instructions]: Generate a high-level visual ASCII text folder tree of the current project structure right here, including this new `.ai_context` folder.
```

---

### File 5: `.ai_context/secrets_manifest.md`

Markdown

```
# Secrets Manifest & Environment Mapping
> **AI GOVERNANCE RULE:** **CRITICAL SECURITY RISK.** NEVER write actual production or local secret values (strings) in this file, any code files, or commit them to GitHub. This file tracks *where* keys are expected, not what they are.

## 📜 System Rules for AI
1. If an AI agent introduces an external API or service provider, it **must** register the required variable name below first.
2. Ensure environment files (like `.env`, `.env.local`, `.dev.vars`) are verified in the project's `.gitignore` before writing code for the feature.

---

## 🔑 Required Environment Variables

| Variable Name | Provider / Service | Environment / Scope | Purpose / Location Used |
| :--- | :--- | :--- | :--- |
| (Example: DATABASE_URL) | (DB Provider) | Private / Server-side | (Database connection string) |

## 🛡️ Security Check Verification Status
- [ ] Environment file added to `.gitignore`
```