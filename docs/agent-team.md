# Agent team

The Mona's Project Pulse dashboard will be built by a custom agent team orchestrated through GitHub Copilot CLI in a Codespace. Each specialist has a defined responsibility and file scope so planning, design, implementation, and coordination remain clear.

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| **Orchestrator** | Claude Opus 4.7 (copilot) | Coordinates the team, breaks requests into phases, delegates work to specialists, manages dependencies and file ownership, and verifies the integrated result. | `.github/agents/orchestrator.agent.md` |
| **Planner** | Claude Opus 4.7 (copilot) | Researches the repository, documentation, dependencies, edge cases, risks, and validation needs, then produces an ordered implementation plan for the Orchestrator. The Planner does not write code. | `.github/agents/planner.agent.md` |
| **Designer** | Gemini 3.1 Pro (copilot) | Defines and implements the dashboard's UI/UX, accessibility, information hierarchy, interaction flow, responsive behavior, and visual styling. For Project Pulse, this includes project cards, status badges, priority treatment, responsive layout, and deterministic CSS hooks such as `.dashboard` and `.project-card`. | `.github/agents/designer.agent.md` |
| **Coder** | GPT-5.5 (copilot) | Implements application logic and runnable-app support with clear, deterministic, testable code; handles explicit errors and validates assigned changes. For Project Pulse, this includes creating `.vscode/launch.json` when assigned, using `app` as its working directory, and opening `index.html`. | `.github/agents/coder.agent.md` |

The Orchestrator runs the Planner first, uses the resulting plan to sequence or parallelize Designer and Coder work when their file scopes allow it, and then verifies the integrated dashboard. All agents leave staging, commits, and pushes to the learner.
