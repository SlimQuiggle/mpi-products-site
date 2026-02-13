# Development Team

## Overview
This is a coordinated dev team managed by the main agent (coordinator). Each sub-agent has a defined role, personality, and set of responsibilities. They are spawned via `sessions_spawn` with their role file loaded as the task preamble.

## How It Works
1. **Coordinator (Main Agent)** — That's me. I receive tasks from the human, break them down, assign work to the right agents, and integrate results.
2. **Sub-agents** — Spawned on demand using `sessions_spawn`. Each gets their role prompt from `team/<role>.md`.
3. **Workspace** — All agents share `/srv/OpenClaw1` as the workspace. They read/write files here.
4. **Communication** — Sub-agents report back when done. I review, merge, and coordinate.

## Spawning Pattern
```
Read team/<role>.md → Inject as preamble to the task → sessions_spawn with label "<role>-agent"
```

## The Team

| Role | File | Label | Specialty |
|------|------|-------|-----------|
| 🏗️ Architect | `architect.md` | `architect-agent` | System design, architecture, tech decisions |
| 🎨 Frontend | `frontend.md` | `frontend-agent` | UI/UX, HTML/CSS/JS, React, responsive design |
| ⚙️ Backend | `backend.md` | `backend-agent` | APIs, databases, server logic, Node/Python |
| 🧪 QA | `qa.md` | `qa-agent` | Testing, code review, bug hunting, quality |
| 🚀 DevOps | `devops.md` | `devops-agent` | Infrastructure, CI/CD, Docker, deployment |
| 📝 Writer | `writer.md` | `writer-agent` | Copy, docs, README, content, humor |

## Rules
- Sub-agents do NOT talk to the human directly — everything goes through the coordinator
- Sub-agents should write output to files, not just return text
- Each agent should announce what files they created/modified
- Agents can read each other's output files for integration work
- Use `opus` model for complex tasks, `openrouter/auto` for routine work

## Project Structure Convention
```
/srv/OpenClaw1/
├── team/              # Agent role definitions (this dir)
├── projects/          # Active project directories
│   └── <project>/     # Each project gets its own folder
├── mpi-site/          # Example: MPI Products website
└── memory/            # Agent memory logs
```
