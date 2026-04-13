# RP-07 — Secret Exposure Response Extended Spec v1

## Purpose
Secret exposure response prosedürünü yalnız kısa containment akışı olmaktan çıkarıp operasyonel karar ve kayıt çerçevesiyle genişletmek.

## Roles
- security owner
- affected surface owner
- runtime or platform owner when config/runtime involved
- communications owner if external/user impact exists
- audit recorder

## Required Inputs
- suspected secret class
- exposure channel or surface
- first detection timestamp
- current containment status
- affected environments
- evidence refs

## Decision Tree
1. If secret class cannot yet be confirmed but exposure is plausible -> open active review state and continue containment.
2. If secret is confirmed on public or shared surface -> escalate immediately and mark high or critical review path.
3. If exposure is confined to low-risk internal non-production path -> still record and evaluate rotation necessity.
4. If the secret may grant privileged or tenant-wide access -> require immediate containment and follow-up review.
5. If exposure is disproven -> close as false positive with evidence.

## Default Timelines
- first detection time must be recorded immediately
- containment decision should not remain implicit beyond the active review window
- rotation decision must be explicitly recorded, even if deferred with reason
- follow-up validation should be scheduled before closure

## Required Records
- exposure review record
- affected secret class note
- environment scope note
- containment actions record
- rotation decision record
- validation completion record
- audit ref

## Example Scenarios
### Scenario 1
A token appears in preview logs visible to an internal shared surface. The event is not ignored as "non-production"; containment and rotation decision are still recorded.

### Scenario 2
A credential appears only in a transient local-only log with no sharing and no reuse. It may still close as low-risk after evidence-backed review, but cannot be silently discarded.

## Closure Criteria
- exposure disproven with evidence, or
- containment completed, or
- rotation/mitigation path documented and validated
