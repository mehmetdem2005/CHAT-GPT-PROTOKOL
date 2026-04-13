# RP-11 — Data Breach Notification Extended Spec v1

## Purpose
Data breach notification prosedürüne zaman, rol ve karar ayrıntısı eklemek.

## Roles
- privacy owner
- legal or compliance reviewer
- incident owner
- communications owner

## Required Inputs
- detection timestamp
- affected data classes
- suspected scope
- containment status
- jurisdiction notes
- evidence refs

## Decision Tree
1. If sensitive or personal data scope unknown -> escalate immediately for privacy review.
2. If breach suspicion disproven -> close with false positive record.
3. If notification required -> prepare internal and external notices.
4. If notification timing window applies -> track deadline explicitly.
5. If scope changes materially -> refresh notice decision.

## Default Timelines
- detection time must be recorded immediately
- decision on notification necessity should not remain implicit
- notification deadlines must be tracked as explicit due items

## Required Records
- breach review record
- legal/compliance review ref
- notice drafts
- sent notice refs
- post-event review ref

## Example
If exported user data may have been exposed and scope is not yet bounded, privacy and compliance review cannot be deferred silently; the uncertainty itself is a tracked condition.
