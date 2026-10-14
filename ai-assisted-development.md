# Working with AI Coding Agents

**Principle:** the agent is fast and literal. Give it the context a good colleague would have, and the walls a good process would have.

## 1. Context the agent can read

| Artifact | Purpose |
|---|---|
| README as an **index** | What the system does, how to run it, where details live. Points, does not repeat. |
| System guide | Business rules that cannot be guessed from code. |
| **Glossary** | Terms that look alike but mean different things. |
| Architecture rules | Layering, where queries may live, how errors flow. |
| Process diagrams | The intended behavior, next to the implementation. |
| Rules file (`CLAUDE.md`) | Behavior rules for the agent. |

## 2. Guardrails from real incidents

Write a rule only when something taught you it was needed, and keep the story short: what happened, why it was possible, the rule, how to verify it. Example themes: no full schema syncs on a live database, never loosen authorization to pass a test, never commit secrets, fail closed.

## 3. Work tracking connected to code

- Every task is an issue before work starts.
- Commits reference the issue ID, with a **closing** keyword when the work is complete and a **linking** keyword when it is partial.
- A CI workflow can label the issue as deployed when a commit carries a deploy marker.

Reusable version: [ai-agent-guardrails-starter](https://github.com/gHAZALehkanani/ai-agent-guardrails-starter).

## 4. Review and parallel work

- Independent tasks run in separate **git worktrees**.
- I read the diff, run the tests and inspect generated SQL. The agent proposes; I merge.

## 5. Where I keep control

Authorization rules, live database changes, secrets, and the interpretation of ambiguous business rules (confirmed with the owner, then written down).
