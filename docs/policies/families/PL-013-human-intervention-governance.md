# PL-013 — Human Intervention & Governance Policies

## Objective
User lock, override, approval, rollback ve görünür change summary disiplinini zorunlu kılmak.

## Primary Subjects
- locks
- approvals
- interventions
- rollbacks

## Mandatory Checks
1. Sessiz override yapılamaz.
2. User lock koruması görünür olmalı.
3. Major structural change için approval sınırı net olmalı.

## Enforcement
- require_user_choice
- require_approval
- turn_block
- rollback_recommended

## Exception Path
Yalnız yetkili governance zinciri ve audit kaydıyla.

## Evidence
- approval refs
- intervention refs
- rollback refs
- audit refs

## Review Cadence
Her intervention modeli değişikliğinde.
