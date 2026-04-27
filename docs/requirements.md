# Fraser Eye Scheduling Platform MVP Requirements

## Purpose

The MVP should help Fraser Eye organize clinic staffing information, import operational rules, and prepare for schedule generation. This milestone focuses on the foundation: documentation, import templates, database schema, and fake sample data.

## MVP goals

- Maintain a roster of fictional/sample employees for development.
- Track staff skills and eligibility for different roles.
- Track accommodations and availability constraints.
- Import time off requests and training requirements.
- Define doctor staffing needs by location, weekday, and session.
- Define lunch coverage expectations.
- Define travel times between clinic locations.
- Store generated schedule runs and assignment results for later UI review.

## Non-goals for this milestone

- No production employee data.
- No final optimization engine yet.
- No payroll integration.
- No live EMR/PM integration.
- No final UI workflow until schema and rules are documented.

## Primary users

- Scheduling/admin user: imports data, reviews rules, generates schedules, adjusts assignments, and exports final schedules.
- Manager/reviewer: reviews coverage gaps, staffing conflicts, and exceptions.
- Future staff user: may eventually view assignments or submit availability/time off, but this is not required for the first milestone.

## Core records

- Employees
- Locations
- Skills
- Employee skill mappings
- Accommodations
- Training rules
- Travel times
- Lunch slots
- Doctor staffing rules
- Time off requests/imports
- Schedule runs
- Schedule assignments
- Schedule conflicts
- Import batches

## Functional requirements

### Imports

The MVP should support CSV templates for:

- employees
- employee_skills
- accommodations
- training_rules
- travel_times
- lunch_slots
- doctor_staffing_rules
- time_off_import

Each import should be traceable to an import batch record. Import validation should report row-level errors before data is committed in future UI work.

### Scheduling rules

The system should represent:

- Skills required for a shift or doctor/session.
- Employee-specific accommodations.
- Time off by employee and date range.
- Location-to-location travel times.
- Lunch coverage windows.
- Minimum and ideal staffing counts.
- Hard vs soft rules.

### Schedule generation readiness

The database should support generated schedule runs with:

- Run metadata.
- Input date range.
- Status.
- Assignments.
- Conflict/warning records.
- Manual override flag on assignments.

## Data safety requirements

- Use fake sample employee data only.
- Do not disable RLS without approval.
- Do not drop tables or wipe data without approval.
- Keep migrations in source control.

## Success criteria for this milestone

- Repo contains project guidance, requirements, data model, scheduling rules, and import documentation.
- Repo contains CSV templates for all requested import types.
- Repo contains initial Supabase migration files.
- Repo contains fake development seed data.
- Schema is described clearly before UI implementation begins.
