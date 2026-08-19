# Project learning-state contract

Read this reference only when inspecting, proposing, creating, or updating persistent learning state.

## Location and precedence

All learner-specific state lives under the current project's `learning/` directory:

- `learning/profile.md`
- `learning/progress.md`
- `learning/sessions/YYYY-MM-DD-HHmm-<topic>.md`
- `learning/evidence.md`

Existing project state is the source of truth. An explicit correction from the learner overrides it, but propose the corresponding file update so the conflict does not persist. Never carry a learner profile or progress record from another project. Do not use global memory as a substitute for project state.

When `learning/` is absent, operate session-only. Offer initialization only when it would help, and create nothing without explicit authorization. Use the matching template from `assets/` when initialization is requested.

## Authorization protocol

Reading existing state is allowed when relevant to the request. For any write:

1. show a concise proposed change or patch;
2. distinguish observed evidence from inference;
3. ask for explicit authorization in the current interaction;
4. apply only the approved state change;
5. report the affected file and validation performed.

Do not treat a request for coaching, reflection, or assessment as permission to persist state.

## `profile.md`

Keep the profile sanitized and learning-specific:

- goals and intended depth;
- evidence-backed strengths;
- current gaps and uncertainty;
- language, teaching, and pacing preferences;
- date and provenance of the latest diagnostic.

Exclude names, contact details, account identifiers, precise location, resume text, and unrelated experience. Mark unverified self-report as provisional. New direct diagnostic evidence may supersede the baseline.

## `progress.md`

Include:

- course offering and official repository commit locks;
- current unit and core learning objectives;
- the four gate states for each objective;
- evidence references, open misconceptions, blockers, and next action.

Allowed gate values are exactly:

- `not_assessed`: no direct evidence;
- `in_progress`: partial, indirect, or unverified evidence;
- `passed`: direct evidence satisfies that gate.

An objective is mastered only when explanation, derivation, implementation, and transfer are all `passed`. Never infer a gate from another gate, average statuses, or lower the rule to preserve a schedule.

Evidence references should resolve to a note section, derivation, test output, commit, experiment record, profiler report, or session assessment. A bare self-rating is not sufficient.
Record every gate as its own row or with its own evidence field. Never use one undifferentiated evidence value for all four gates.

## Session records

Create a session record only after authorization. Keep it brief and factual:

- timestamp, active mode, objective, and relevant course lock;
- evidence observed in the session;
- misconception or uncertainty exposed;
- gate transitions proposed or applied;
- next action.

Use local project time and a filesystem-safe topic slug. Do not store full chat transcripts or sensitive data.

## `evidence.md`

Export only passed, traceable capabilities. Each entry includes:

- neutral capability statement;
- demonstrated scope and environment/version when material;
- evidence links;
- limitations or untested boundaries;
- validation date.

This file is an evidence handoff, not a resume. Do not add promotional adjectives, role targeting, or claims broader than the source evidence.
