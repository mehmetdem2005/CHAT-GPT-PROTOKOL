# PL-014 — Deployment & Release Management Policies

## Objective
Deployment, rollout, approval ve rollback güvenliğini zorunlu kılmak.

## Primary Subjects
- deployment requests
- release candidates
- pipeline runs
- rollout plans

## Mandatory Checks
1. Production deployment approval zinciriyle bağlı olmalı.
2. Rollback readiness görünür olmalı.
3. Rollout stratejisi açık seçilmeli.

## Enforcement
- require_approval
- release_hold
- hard_block

## Exception Path
Yalnız documented acil durum yolu ve audit kaydı ile.

## Evidence
- pipeline refs
- rollout refs
- approval refs
- rollback refs

## Review Cadence
Her production path değişikliğinde.
