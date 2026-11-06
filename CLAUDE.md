# CLAUDE.md

Follow every rule in AGENTS.md. It is shared with Codex and other tools, so the whole team works from one set of rules:

@AGENTS.md

## Additional notes for Claude
- **Database work:** use the Supabase connection for the **Move Me** project. Inspect existing tables and functions before changing them. Apply schema changes as named migrations, and keep them additive (AGENTS.md §4).
- **Ask before anything destructive.** Get the owner's explicit OK before any `DELETE`, `DROP`, `TRUNCATE` or account removal. Show what would be affected first, such as row counts or bookings.
- **Test without leaving traces.** When testing database functions with real accounts, roll the test back, or clean up the test data afterwards, and say what was created.
- **Hand-off:** finish by giving the user the updated `index.html` (and any other changed files) to upload, with a one-line note of what changed and what you couldn't test.
