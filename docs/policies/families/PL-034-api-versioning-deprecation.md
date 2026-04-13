# PL-034 — API Versioning & Deprecation Policy

## Objective
API sürümlerinin kontrollü evrilmesini ve eski sürümlerin sessizce bozulmadan kaldırılmasını sağlamak.

## Business Rationale
API yüzeyleri dış entegrasyonlar ve iç modüller için contract yüzeyidir. Sessiz veya plansız değişiklikler sistem çapında kırılma üretir.

## Scope
- public APIs
- internal service APIs
- versioned endpoint contracts
- API lifecycle notices

## Non-Scope
- purely internal function signatures
- draft experimental payloads not yet published

## Primary Subjects
- API contracts
- release candidates
- deprecation notices
- migration plans

## Mandatory Checks
1. Breaking API change major version veya explicit compatibility note taşımalı.
2. Deprecated yüzey replacement ref ve sunset tarihi taşımalı.
3. Migration guidance olmadan deprecation tamamlanmış sayılmamalı.

## Enforcement
- require_review
- release_hold
- hard_block

## Metrics
- undocumented deprecation count
- API break without migration note count
- deprecated surface overage beyond sunset date

## Evidence
- api contract refs
- deprecation notice refs
- migration notes
- release refs

## Review Cadence
Her API breaking veya deprecation change setinde.
