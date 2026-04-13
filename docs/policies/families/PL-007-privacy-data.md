# PL-007 — Privacy & Data Policies

## Objective
Veri minimizasyonu, hassas veri sınıflandırması ve privacy-by-default yaklaşımını enforce etmek.

## Primary Subjects
- schemas
- analytics payloads
- manifests
- API contracts

## Mandatory Checks
1. Gerekli olmayan kişisel veya hassas veri tutulmamalı.
2. Retention, deletion ve correction davranışı belgelenmeli.
3. Analytics ve export yüzeyleri anonimleştirme sınırına uymalı.

## Enforcement
- require_review
- require_approval
- hard_block

## Exception Path
Süreli, documented ve privacy owner onaylı istisna dışında izin verilmez.

## Evidence
- schema refs
- data maps
- retention rules
- analytics evidence

## Review Cadence
Her data model veya analytics değişikliğinde.
