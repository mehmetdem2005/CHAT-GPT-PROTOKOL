# PL-008 — Compliance & Legal Routing Policies

## Objective
Hukuki belirsizlik, jurisdiction farkları ve high-risk feature’ların doğru review zincirine yönlendirilmesini zorunlu kılmak.

## Primary Subjects
- release candidates
- legal-sensitive features
- data flows
- regulated surfaces

## Mandatory Checks
1. Regülasyon duyarlı değişiklikler doğru review kanalına yönlenmeli.
2. Belirsiz hukuki alanlarda otomatik kesin karar verilmemeli.
3. High-risk domain’lerde explicit approval veya hold mekanizması çalışmalı.

## Enforcement
- require_review
- require_approval
- hard_block

## Exception Path
Sadece documented legal review ve owner sign-off ile.

## Evidence
- compliance maps
- legal notes
- jurisdiction refs
- approval refs

## Review Cadence
Her regulated feature ve release candidate öncesi.
