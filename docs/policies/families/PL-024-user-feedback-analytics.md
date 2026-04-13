# PL-024 — User Feedback & Analytics Policies

## Objective
Feedback toplama ve analytics anonimleştirmeyi güvenli ve anlamlı hale getirmek.

## Primary Subjects
- feedback flows
- analytics events
- turn summaries

## Mandatory Checks
1. Feedback toplama akışı görünür olmalı.
2. Analytics veri minimizasyonuna uymalı.
3. Privacy-sensitive telemetry açık review üretmeli.

## Enforcement
- allow_with_warning
- require_review
- hard_block for privacy misuse

## Exception Path
Yalnız owner review ve privacy etkisi düşük olduğunda sınırlı istisna.

## Evidence
- analytics schema refs
- anonymization notes
- feedback refs
- privacy review refs

## Review Cadence
Aylık ve analytics değişikliğinde.
