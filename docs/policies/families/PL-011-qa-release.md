# PL-011 — QA & Release Policies

## Objective
Release kararını zorunlu QA, security, accessibility ve contract kapılarına bağlamak.

## Primary Subjects
- QA reports
- preview sessions
- release candidates
- deployment requests

## Mandatory Checks
1. Preview olmadan release ilerlememeli.
2. Blocking QA bulguları görünür tutulmalı.
3. Release kararı evidence refs ile desteklenmeli.

## Enforcement
- allow_with_warning
- release_hold
- hard_block

## Exception Path
Sadece documented release waiver ve yetkili approver zinciriyle.

## Evidence
- QA reports
- preview refs
- policy decisions
- release decision refs

## Review Cadence
Her release candidate için zorunlu.
