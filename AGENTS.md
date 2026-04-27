# AGENTS.md

Guidance for AI agents and contributors working on the Fraser Eye scheduling platform prototype/MVP.

## Project intent

Build a prototype scheduling platform for Fraser Eye that can import staffing data, model scheduling constraints, and eventually generate, review, and export clinic staffing schedules.

## Ground rules

- Use fake sample data only unless the user explicitly provides real employee data.
- The Supabase development database may be written to, but it must be treated as non-production.
- Ask before dropping tables, deleting all data, disabling RLS, or making destructive changes.
- Keep all schema changes represented as migration files in `supabase/migrations/`.
- Preserve auditability: document schema assumptions and scheduling rules before implementing UI flows.
- Prefer simple, readable MVP code over complex abstractions.

## Current milestone

Before building the UI, establish:

1. Project documentation in `docs/`.
2. CSV import templates in `templates/`.
3. Initial Supabase schema migrations.
4. Fake development seed data.
5. A plain-English schema summary.

## Data principles

- Do not store sensitive real employee information unless explicitly provided by the user.
- Use stable IDs and human-readable codes where helpful for imports.
- Track source files and import batches so bad imports can be reviewed.
- Model rules in data where possible rather than hard-coding them in the UI.

## Scheduling assumptions for MVP

- Staff can work at multiple locations.
- Staff may have multiple skills.
- Doctors can have staffing requirements by location, weekday, and session.
- Accommodations and time off should block or constrain assignments.
- Travel time should be considered when scheduling across locations on the same day.
- Lunch slot coverage should be explicit and auditable.

## Development workflow

- Add or update docs when business rules change.
- Add a new migration for every schema change.
- Add fake seed records when new tables need test coverage.
- Summarize changes in plain English before moving to UI implementation.
