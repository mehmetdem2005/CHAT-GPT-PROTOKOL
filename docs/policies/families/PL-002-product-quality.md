# PL-002 — Product Quality Policies

## Objective
Üretilen sistemin ürün amacına, kapsam sınırına ve temel kalite beklentilerine uymasını zorunlu kılmak.

## Primary Subjects
- requirements
- previews
- QA reports
- release candidates

## Mandatory Checks
1. Çıktı açık ürün hedefine bağlanmalı.
2. Scope creep ve amaç kayması görünür işaretlenmeli.
3. Minimum NFR baseline tanımlı olmalı.

## Enforcement
- allow_with_warning
- require_review
- release_hold

## Exception Path
Yalnız documented rationale ve owner onayıyla geçici istisna açılabilir.

## Evidence
- requirement refs
- preview refs
- QA refs
- risk summary

## Review Cadence
Her major release train öncesi.
