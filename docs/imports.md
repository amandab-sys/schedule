# Fraser Eye Scheduling CSV Imports

## Purpose

CSV imports let the MVP load fake sample data and, later, validated operational data without hard-coding rules in the app.

## General import conventions

- CSV files should include a header row.
- Codes should be stable and human-readable.
- Dates should use `YYYY-MM-DD`.
- Times should use 24-hour `HH:MM` format.
- Weekdays should use uppercase names: `MONDAY`, `TUESDAY`, `WEDNESDAY`, `THURSDAY`, `FRIDAY`, `SATURDAY`, `SUNDAY`.
- Sessions should use `AM`, `PM`, or `FULL_DAY`.
- Boolean values should use `true` or `false`.
- Empty optional values should be left blank.

## Templates

### employees.csv

Creates or updates employee roster records.

Required columns:

- employee_code
- first_name
- last_name
- employment_status

Optional columns:

- default_location_code
- default_weekly_hours
- can_float
- notes

### employee_skills.csv

Assigns skills to employees.

Required columns:

- employee_code
- skill_code

Optional columns:

- proficiency_level
- verified_on
- expires_on
- notes

### accommodations.csv

Stores employee-specific scheduling constraints or preferences.

Required columns:

- employee_code
- accommodation_type
- severity
- description

Optional columns:

- starts_on
- ends_on
- active

### training_rules.csv

Defines training requirements by skill.

Required columns:

- rule_code
- skill_code
- rule_name
- requirement_type

Optional columns:

- renewal_interval_months
- minimum_shadow_sessions
- requires_signoff
- active
- notes

### travel_times.csv

Defines travel time between two clinic locations.

Required columns:

- from_location_code
- to_location_code
- minutes

Optional columns:

- notes

### lunch_slots.csv

Defines lunch windows and required coverage.

Required columns:

- location_code
- weekday
- session
- starts_at
- ends_at
- minimum_coverage_count

Optional columns:

- notes

### doctor_staffing_rules.csv

Defines staffing requirements for doctor sessions.

Required columns:

- doctor_code
- doctor_name
- location_code
- weekday
- session
- skill_code
- minimum_count

Optional columns:

- ideal_count
- active
- notes

### time_off_import.csv

Imports staff time off constraints.

Required columns:

- employee_code
- starts_on
- ends_on
- status

Optional columns:

- reason_category
- notes

## Validation rules for future UI

- Unknown employee, location, or skill codes should be flagged before import commit.
- Duplicate rows should be identified and shown to the scheduler.
- Date ranges must have `ends_on >= starts_on`.
- Travel time minutes must be non-negative.
- Minimum counts must be greater than or equal to zero.
- Ideal counts should be greater than or equal to minimum counts.

## Import batch tracking

Every import should eventually create an `import_batches` record with:

- import type
- source filename
- status
- started/completed timestamps
- row count
- error count
- notes

For this milestone, templates and schema are created first; full import UI and validation flow comes later.
