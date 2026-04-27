# Fraser Eye Scheduling MVP Data Model

## Overview

The initial schema is designed to support CSV imports, rule storage, schedule generation, and later UI review. It favors clear relational tables over premature optimization.

## Entity summary

### locations

Clinic or work locations where staff can be assigned.

Key fields:

- `id`
- `code`
- `name`
- `address_line1`
- `city`
- `state`
- `is_active`

### employees

Development roster of employees. For this milestone, records must be fake/sample data only.

Key fields:

- `id`
- `employee_code`
- `first_name`
- `last_name`
- `default_location_id`
- `employment_status`
- `default_weekly_hours`
- `can_float`
- `notes`

### skills

Reusable staff skills or role qualifications.

Examples:

- front_desk
- technician
- scribe
- testing
- surgical_counseling
- phone_triage

### employee_skills

Many-to-many mapping between employees and skills.

Key fields:

- `employee_id`
- `skill_id`
- `proficiency_level`
- `verified_on`
- `expires_on`

### accommodations

Employee-specific scheduling limitations or preferences.

Examples:

- no late shifts
- no inter-location travel
- maximum hours per day
- preferred location

Fields include severity so rules can be handled as hard blocks or soft preferences.

### training_rules

Defines training or certification requirements for specific skills or roles.

Examples:

- skill requires annual renewal
- new staff must shadow for a number of sessions
- role requires supervisor signoff

### travel_times

Location-to-location travel durations in minutes.

Used later to detect impossible same-day assignments across locations.

### lunch_slots

Defines lunch coverage windows by location and weekday/session.

Used to ensure enough coverage remains while employees take lunch.

### doctor_staffing_rules

Defines required staffing around a doctor, location, weekday, and session.

Examples:

- Dr. Avery at East clinic Monday AM needs 2 technicians and 1 scribe.
- Dr. Morgan at West clinic Tuesday PM needs 1 front desk and 2 technicians.

### time_off_requests

Imported or manually entered staff time off constraints.

Tracks date range, reason category, and approval status.

### import_batches

Metadata for import operations so future UI can show source, status, row counts, and errors.

### schedule_runs

Represents an attempt to generate or revise a schedule for a date range.

### schedule_assignments

Stores generated or manually entered staff assignments for a schedule run.

### schedule_conflicts

Stores warnings and hard conflicts found during schedule generation or validation.

## Important relationships

- Employees may belong to a default location but can float if `can_float = true`.
- Employees may have many skills.
- Doctor staffing rules reference a location and required skill.
- Time off and accommodations constrain assignment eligibility.
- Travel times constrain multi-location assignments.
- Schedule runs have many assignments and conflicts.

## MVP status values

### employee employment_status

- active
- inactive
- leave

### rule severity

- hard
- soft

### schedule run status

- draft
- generated
- reviewed
- finalized
- failed

### assignment source

- generated
- manual
- imported

## Design notes

- Import templates use human-readable codes, but relational tables store UUIDs.
- Unique constraints protect import idempotency for common lookup data.
- Timestamps are included on operational tables for auditability.
- RLS is enabled in the initial migration, but broad authenticated policies are left for later app-specific security design.
