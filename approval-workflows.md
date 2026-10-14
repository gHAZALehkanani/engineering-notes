# Approval Workflows as State Machines

**Idea:** model an approval process as named states with a transition table, not as a pile of `if` statements spread across controllers.

## Design notes

| Concern | Approach |
|---|---|
| States | Explicit and named (`PENDING_REVIEW`, `PENDING_APPROVAL`, `APPROVED`, ...). No boolean flags that combine into hidden states. |
| Transitions | One table: from-state, action, required permission, next state. Easy to test and to draw. |
| Audit | Every transition appends a row (who, when, from, to, note). Never update history. |
| Different entry points | Different request types may start at different states; the table, not the UI, decides. |
| Controlled bypass | An emergency path can exist, but it needs its own permission and writes **one** clear audit record, not fake intermediate approvals. |
| Safety valves | Rejection or rollback at late stages is restricted to a small role. |
| External side effects | Sending to another system is its own state (`PENDING_SYNC`), so a failure there leaves the request waiting instead of lost. |

## Habits that help

- Draw the process in **BPMN** first and keep the file next to the code.
- Test the transition table directly, including the forbidden transitions.
- Keep UI button visibility as a hint; the server validates the transition.
