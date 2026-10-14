# Modernizing a Legacy App

**Rule:** write the analysis before the code, and run old and new side by side until the new one proves itself.

## Method

1. **Inventory.** List every file and version. Legacy folders often hold several generations and byte-identical copies; compare them by hash and pick one functional reference.
2. **Extract the data layer from the code.** Tables, columns and the **state machine** of the main entity.
3. **Map every function.** Each page, tab and write action gets a line.
4. **Group findings:** security, data integrity / business rules, performance and code quality.
5. **Decide the target:** not just "port to a new framework", also where the rules live (server, transactions, validation).
6. **List behavior changes explicitly** (old behavior → new behavior) so stakeholders approve behavior, not only looks.
7. **Keep the schema unchanged during the transition** so both systems can run against the same data.
8. **Parity checklist.** Each legacy function gets a status until all are covered.
9. **Record decisions with dates** and keep a list of open questions for the owners.
10. **Name what you are deliberately not migrating** (dead code, unrelated pages), and what debt you are deferring and why.

## Typical fixes that come out of the analysis

- Authentication enforced on every endpoint, with authorization checked on the server.
- Transactions and row locks where two users can claim the same record.
- Server-side pagination, search and sorting instead of loading everything.
- Input validation and validated configuration at startup.
- Rate limiting on login.

## Lesson

Treat the old app as **requirements to understand**, not a specification to copy bug for bug.
