# Engineering Notes

Short, practical notes from building business web applications. They are general patterns, not descriptions of any specific system.

| Note | In one line |
|---|---|
| [Fail-closed authorization](fail-closed-authorization.md) | When access cannot be decided, return nothing, not everything |
| [Safe changes to a live database](safe-live-database-changes.md) | Small, guarded, verifiable scripts instead of full schema syncs |
| [Template / instance data modeling](template-instance-modeling.md) | Keep history correct when checklists and forms change |
| [Approval workflows as state machines](approval-workflows.md) | Explicit states, append-only audit rows, a controlled bypass |
| [Modernizing a legacy app](modernizing-legacy-apps.md) | Analysis first, parallel run, a parity checklist |
| [Working with AI coding agents](ai-assisted-development.md) | Context, guardrails and traceable releases |

Related: [ai-agent-guardrails-starter](https://github.com/gHAZALehkanani/ai-agent-guardrails-starter)
