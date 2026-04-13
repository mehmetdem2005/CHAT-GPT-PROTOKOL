# RP-14 — Auth Incident Response Procedure

## Trigger
Authentication, authorization, session veya privileged access yüzeyinde ciddi bozulma veya şüphe.

## Roles
- auth owner
- operations owner
- review approver if needed

## Steps
1. Incident scope ve affected surfaces'i tanımla.
2. Session, token veya access path etkisini sınıflandır.
3. Immediate containment ihtiyacını belirle.
4. Audit ve event refs aç.
5. User impact ve next action özetini yaz.
6. Follow-up remediation owner ata.

## Default Timelines
- high or critical auth issue immediate triage gerektirir
- medium issues same review window içinde atanmalı

## Completion
- contained
- escalated
- false_positive
