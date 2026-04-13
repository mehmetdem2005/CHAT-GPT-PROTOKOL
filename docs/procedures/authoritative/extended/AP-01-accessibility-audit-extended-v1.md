# AP-01 — Accessibility Audit Extended Spec v1

## Purpose
Accessibility audit prosedürünü yalnız checklist değil, release ve remediation kararlarını besleyen bir denetim akışı olarak ayrıntılandırmak.

## Roles
- audit owner
- route or surface owner
- remediation owner
- release owner when blocking finding exists

## Required Inputs
- target routes
- target viewports
- keyboard/navigation matrix
- previous findings refs
- release candidate refs if applicable
- evidence storage refs for captures and notes

## Decision Tree
1. If route is user-facing and not yet audited for current release -> audit required.
2. If blocking issue affects core interaction, form completion, focus visibility or essential semantics -> release impact must be recorded.
3. If issue is non-blocking but repeated across surfaces -> group remediation review required.
4. If finding appears environment-specific -> capture evidence before closure.
5. If no issues found -> audit still records evidence and scope.

## Default Timelines
- release-blocking findings should be addressed in the current release window
- non-blocking findings should receive target remediation window and owner
- repeated findings should not remain ungrouped across consecutive audits

## Required Records
- route audit scope list
- viewport evidence refs
- finding classification summary
- release impact note
- remediation assignment
- closure or defer note

## Example Scenarios
### Scenario 1
A checkout form is keyboard inaccessible on tablet viewport. This is not a cosmetic issue; it is release-impacting for that route.

### Scenario 2
A marketing page has a minor heading hierarchy inconsistency with no navigation impact. It may be non-blocking but still must be recorded.

## Closure Criteria
- all blocking findings resolved, or
- explicit defer decision with owner, target date and release impact note
