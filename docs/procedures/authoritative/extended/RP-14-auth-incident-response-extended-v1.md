# RP-14 — Auth Incident Response Extended Spec v1

## Purpose
Auth incident response prosedürünü daha operasyonel hale getirmek.

## Roles
- auth owner
- platform operations owner
- security reviewer
- communications owner if user impact exists

## Required Inputs
- affected auth surface
- suspected issue class
- impacted actor classes
- containment status
- evidence refs

## Decision Tree
1. If privileged access path may be compromised -> escalate immediately.
2. If scope is uncertain -> keep review open and record uncertainty.
3. If only non-critical session issue exists -> route to standard remediation unless repeated.
4. If user-facing impact exists -> produce communication decision.

## Default Timelines
- high-severity auth issues require same-window triage
- medium issues require explicit follow-up scheduling

## Required Records
- incident/event ref
- auth review ref
- containment notes
- remediation owner and due item

## Example
A missing authorization check on an admin-like route is not a simple bug; it requires auth incident handling and review outcome even before permanent fix is merged.
