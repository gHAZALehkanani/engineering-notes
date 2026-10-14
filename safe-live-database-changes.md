# Safe Changes to a Live Database

**Rule:** change production schemas with small, guarded, verifiable scripts. Do not let a tool "sync everything".

## The risk

ORM schema-sync commands compare the *whole* database to the schema file. Anything the schema file does not know about (a table made with raw SQL, a legacy table, a hand-added index) can be flagged for deletion. The danger grows quietly as the live database and the schema file drift apart.

## Practice

1. **Mirror every change.** A database change and its schema-file change belong to the same commit.
2. **Guard each script.** Make it safe to run twice:

   ```sql
   IF NOT EXISTS (SELECT 1 FROM sys.columns
                  WHERE object_id = OBJECT_ID('dbo.orders') AND name = 'external_ref')
       ALTER TABLE dbo.orders ADD external_ref NVARCHAR(50) NULL;
   ```

3. **Name and date scripts.** One purpose per file, so history reads like a changelog.
4. **Protect what the ORM cannot model.** Keep a representation of raw tables in the schema file and mark it as ignored when it has no reliable key.
5. **Verify read-only, before and after:**
   - validate the schema file;
   - diff live database vs. schema file; the expected result is an **empty migration**.
6. **Never use a full schema push on production.**

## Why it works

Each step has a small blast radius, can be repeated safely, and produces a yes/no check. That is also what makes it safe to let an AI agent propose database changes: the guardrail is a written rule plus a command anyone can run.
