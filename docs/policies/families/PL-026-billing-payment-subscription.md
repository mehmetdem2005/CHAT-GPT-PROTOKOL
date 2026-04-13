# PL-026 — Billing, Payment & Subscription Policies

## Objective
Kullanım ölçümü, plan limitleri, ödeme başarısızlığı ve erişim ilişkisini kontrollü hale getirmek.

## Primary Subjects
- usage events
- plan access
- billing actions

## Mandatory Checks
1. Metering davranışı açık ve izlenebilir olmalı.
2. Plan limitleri sessiz değil, görünür uygulanmalı.
3. Payment failure davranışı açık policy ile bağlı olmalı.

## Enforcement
- allow
- allow_with_warning
- turn_block
- require_review

## Exception Path
Yalnız support veya credit süreciyle sınırlı ve audit-linked.

## Evidence
- usage refs
- billing events
- support notes
- plan mappings

## Review Cadence
Aylık ve pricing/plan değişikliklerinde.
