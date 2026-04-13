# PL-035 — Data Migration & Schema Change Policy

## Objective
Şema ve migration değişikliklerinin etkili analiz, review ve geri dönüş planı ile yürütülmesini sağlamak.

## Scope
- relational schema changes
- document schema changes
- migration scripts
- data backfill jobs

## Mandatory Checks
1. Schema change impact summary zorunlu olmalı.
2. Data migration change rollback veya forward-fix yolu taşımalı.
3. Migration riskleri release kararına bağlanmalı.

## Enforcement
- require_review
- require_approval
- release_hold

## Evidence
- schema refs
- migration refs
- change request refs
- rollback or mitigation notes

## Review Cadence
Her schema-affecting release öncesi.
