# PL-038 — Code Review Policy

## Objective
Kod değişikliklerinin yeterli gözden geçirme, kapsam görünürlüğü ve kritik yüzeylerde ek kontrol ile ilerlemesini sağlamak.

## Scope
- code patches
- pull requests
- critical surface changes
- generated code acceptance

## Mandatory Checks
1. Her change set review owner taşımalı.
2. Kritik yüzeylerde ek reviewer veya approval gerekebilmeli.
3. Review olmadan merge edilen değişiklikler görünür istisna sayılmalı.

## Enforcement
- require_review
- require_approval
- release_hold

## Evidence
- review refs
- patch refs
- critical surface tags
- exception refs

## Review Cadence
Continuous.
