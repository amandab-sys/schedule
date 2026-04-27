# Fraser Eye Scheduling Rules

## Rule philosophy

The MVP should separate hard constraints from soft preferences.

- Hard rules block an assignment or create a conflict that must be fixed.
- Soft rules create a warning or score penalty but can be overridden by a scheduler.

## Core rule categories

### Skill coverage

Each doctor staffing rule defines a required skill, minimum staff count, and ideal staff count for a location, weekday, and session.

Hard rule:

- A staff member cannot fill a role unless they have the required skill and the skill is not expired.

Soft rule:

- Prefer higher proficiency when multiple staff are eligible.

### Employee time off

Approved time off blocks assignments during the requested date range.

Hard rule:

- Do not schedule employees during approved time off.

Soft rule:

- Pending time off should warn the scheduler.

### Accommodations

Accommodations can be hard or soft depending on severity.

Examples:

- Hard: cannot work past 4:00 PM.
- Hard: cannot travel between locations during the same day.
- Soft: prefers East clinic.
- Soft: prefers no Friday PM sessions.

### Travel time

Travel times are stored between locations.

Hard rule:

- Do not schedule an employee at two locations when the gap between assignments is shorter than the required travel time.

Soft rule:

- Prefer minimizing travel even when feasible.

### Lunch coverage

Lunch slots define expected meal windows and coverage requirements.

Hard rule:

- A lunch plan should not reduce active staffing below minimum coverage.

Soft rule:

- Prefer lunch within the employee's usual lunch window when known.

### Doctor staffing

Doctor staffing rules define required roles for a doctor/session.

Hard rule:

- Meet minimum required staff counts for each required skill.

Soft rule:

- Meet ideal counts where possible.

### Weekly hours and workload

Employee weekly hours should be tracked for fairness and compliance.

Hard rule:

- Do not exceed configured maximums when later added.

Soft rule:

- Prefer assignments that keep employees near default weekly hours and distribute undesirable shifts fairly.

## Sessions

The initial schema supports these session values:

- AM
- PM
- FULL_DAY

More granular shift times can be added later through shift templates.

## Conflict severity

Schedule conflicts should be stored with:

- `severity`: info, warning, error
- `conflict_type`: skill_gap, time_off, accommodation, travel, lunch_coverage, overstaffed, understaffed, validation
- `message`: human-readable explanation
- optional assignment or employee reference

## Override behavior

Manual overrides should be allowed later in the UI, but every override should be traceable.

For MVP schema:

- `schedule_assignments.is_manual_override` flags a manual change.
- `schedule_assignments.notes` can explain the override.
- Conflicts can remain attached to finalized schedules if accepted intentionally.

## Open questions for later discovery

- Exact Fraser Eye clinic location list.
- Exact doctor/session patterns.
- Full list of scheduling roles.
- Whether lunch rules differ by department or provider.
- Whether staff availability is recurring or imported from another system.
- Whether overtime, part-time limits, or union rules apply.
