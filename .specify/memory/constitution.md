<!--
Sync Impact Report
- Version change: unknown -> 1.0.0
- Modified principles: (added) Code Quality, Testing Standards, UX Consistency, Performance Requirements
- Added sections: "Standards & Constraints" (clarifies non-functional requirements)
- Removed sections: none (template placeholders consolidated)
- Templates requiring updates:
	- ✅ /home/markus/development/speckit/.specify/templates/plan-template.md
	- ⚠ /home/markus/development/speckit/.specify/templates/spec-template.md (reviewed, no edits required)
	- ⚠ /home/markus/development/speckit/.specify/templates/tasks-template.md (reviewed, no edits required)
- Follow-up TODOs:
	- TODO(RATIFICATION_DATE): Ratification date unknown; project maintainers to set original adoption date in ISO format YYYY-MM-DD
-->

# Speckit Constitution

## Core Principles

### I. Code Quality (NON-NEGOTIABLE)
All production code MUST be readable, maintainable, and reviewable. Concretely:
- Source files MUST include documentation for public APIs and non-obvious behavior.
- Code MUST pass linting and static analysis configured for the project before merge.
- Complexity MUST be justified in PR descriptions; alternatives considered must be listed.

Rationale: High-quality code reduces long-term maintenance cost, enables safe refactors,
and makes reviews effective.

### II. Testing Standards (NON-NEGOTIABLE)
Testing is mandatory and follows a test-first discipline where practical:
- Unit tests MUST cover critical logic and edge cases. Aim for meaningful coverage, not a
	coverage percentage target alone.
- Integration and contract tests MUST exist for public interfaces and cross-module
	interactions. These tests MUST fail before implementation (TDD ordering in tasks).
- All tests added MUST be automated in CI and execute reliably (flaky tests are tracked and
	quarantined until fixed).

Rationale: Tests are the executable specification; they protect behavior during change and
enable confident releases.

### III. User Experience Consistency
User-facing behaviors and APIs MUST be consistent across the project:
- UX patterns (CLI flags, API response shapes, error codes/messages) MUST follow
	documented conventions in `/docs` or the project README.
- Accessibility and internationalization considerations MUST be included where relevant.
- Breaking UX/API changes require a migration guide, deprecation window, and
	communication plan.

Rationale: Predictable UX reduces user errors, support burden, and integration friction.

### IV. Performance Requirements
Non-functional performance goals MUST be explicit and testable:
- Projects SHOULD declare performance targets in the relevant spec or plan (e.g., p95
	latency, throughput, memory limits) during Phase 0.
- Performance tests MUST be included for any feature with measurable goals and run in CI
	or an agreed benchmarking environment.
- Optimizations MUST be justified with measurements; premature optimization is
	discouraged but regressions are not allowed.

Rationale: Explicit performance requirements prevent regressions and ensure the product
meets operational needs.

## Standards & Constraints
This section captures cross-cutting non-functional requirements and constraints:
- Security: Follow principle of least privilege; encrypt sensitive data at rest and in transit
	where applicable; mark any compliance needs in the spec.
- Observability: Structured logs, error reporting, and basic metrics MUST be provided for
	services and long-running processes.
- Accessibility: UI/UX changes that affect users MUST consider accessibility (WCAG
	guidelines where applicable).
- Resource constraints and targets (example): p95 < 200ms, memory < 200MB for services
	of comparable scope — specifics belong in the feature's Technical Context.

## Development Workflow
Minimum workflow requirements:
- All changes go through a Pull Request with at least one approving reviewer who is
	familiar with the impacted area.
- CI MUST run tests, linters, and basic static checks on every push to a branch.
- Feature branches MUST be named using the convention `###-feature-name` and include
	links to `specs/[###-feature-name]/plan.md`.
- Releases follow semantic versioning; breaking changes MUST be documented and follow
	the migration guidance in Governance.

## Governance
Amendments, versioning, and compliance expectations:
- Amendments: Changes to this constitution MUST be proposed via a Pull Request against
	`.specify/memory/constitution.md` including the reason, migration plan for impacted
	templates, and a test plan for enforcement.
- Approval: A constitution amendment requires approvals from at least two maintainers or
	one maintainer plus one domain owner (e.g., QA for testing rules). If maintainers are
	unavailable, unanimous approval from active contributors in the last 90 days is required.
- Versioning: The constitution uses semantic versioning. Bump rules:
	* MAJOR when removing or redefining principles in a backward-incompatible way.
	* MINOR when adding a new principle or materially expanding guidance.
	* PATCH for clarifications, wording, or typo fixes.
- Compliance: All feature plans (`/plan`) MUST include an explicit "Constitution Check"
	section. CI checks (linters, tests) are the primary enforcement mechanism; policy
	violations are recorded in the complexity tracking table in the plan and must include
	a remediation path.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): set original adoption date | **Last Amended**: 2025-09-21