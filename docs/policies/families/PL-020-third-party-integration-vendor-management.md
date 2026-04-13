# PL-020 — Third-Party Integration & Vendor Management Policies

## Objective
Vendor güvenliği, veri paylaşım sınırı, SLA yeterliliği ve fallback beklentilerini zorunlu kılmak.

## Primary Subjects
- integrations
- vendors
- external dependencies

## Mandatory Checks
1. Yeni vendor güvenlik ve risk review’undan geçmeli.
2. Outbound data boundary açık tanımlanmalı.
3. Kritik entegrasyonlarda fallback veya failure behavior net olmalı.

## Enforcement
- require_review
- require_approval
- hard_block

## Exception Path
Yalnız documented vendor risk acceptance ve owner approval ile.

## Evidence
- vendor review refs
- data boundary notes
- SLA notes
- fallback refs

## Review Cadence
Her yeni vendor veya kritik entegrasyon değişikliğinde.
