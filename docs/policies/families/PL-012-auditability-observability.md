# PL-012 — Auditability & Observability Policies

## Objective
Kritik kararların, hata akışlarının ve operasyon sinyallerinin izlenebilir olmasını zorunlu kılmak.

## Primary Subjects
- audit events
- traces
- logs
- metrics
- incidents

## Mandatory Checks
1. Kritik eylemler audit kaydı üretmeli.
2. Trace ve log korelasyonu kurulabilmeli.
3. Health ve release kararları evidence ile izlenebilmeli.

## Enforcement
- allow_with_warning
- require_review
- release_hold

## Exception Path
Yalnız kısa süreli operasyonel sınırlama ve açık owner onayıyla.

## Evidence
- audit refs
- trace ids
- log events
- metrics

## Review Cadence
Her observability değişikliği ve incident sonrası.
