# PL-040 — Rate Limiting & Throttling Policy

## Objective
API ve runtime yüzeylerinde adil kullanım, kaynak korunumu ve abuse azaltımı için limitlerin uygulanmasını sağlamak.

## Scope
- public APIs
- internal high-cost actions
- preview-heavy surfaces
- tenant-scoped consumption

## Mandatory Checks
1. Kritik yüzeyler documented rate controls taşımalı.
2. Tenant ve actor bazlı aşırı kullanım görünür sinyal üretmeli.
3. Limit davranışı sessiz veri kaybı yerine anlaşılır hata üretmeli.

## Enforcement
- allow_with_warning
- require_review
- turn_block
- hard_block for abusive patterns

## Evidence
- rate limit configs
- usage metrics
- abuse findings
- exception refs

## Review Cadence
Monthly ve trafik modeli değiştiğinde.
