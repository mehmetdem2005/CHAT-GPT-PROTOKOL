# PL-009 — Architecture & Contract Policies

## Objective
Protocol, schema, artifact ownership ve versioning disiplinini korumak.

## Primary Subjects
- task contracts
- task graphs
- api contracts
- data schemas
- code patches
- manifests

## Mandatory Checks
1. Contract değişiklikleri görünür işaretlenmeli.
2. Artifact ownership ve contract refs açık olmalı.
3. Sessiz contract drift kabul edilmemeli.

## Enforcement
- allow_with_warning
- require_review
- release_hold

## Exception Path
Migration notu, owner review ve gerekiyorsa approval ile sınırlı istisna açılabilir.

## Evidence
- contract test refs
- schema refs
- manifest refs
- patch refs

## Review Cadence
Her contract veya schema değişikliğinde.
