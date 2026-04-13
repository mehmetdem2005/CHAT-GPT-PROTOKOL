# PL-018 — Documentation & Knowledge Management Policies

## Objective
Ajan, protokol, politika ve release kararlarının dokümantasyon disiplinini korumak.

## Primary Subjects
- agent packages
- protocol changes
- policy changes
- release packages

## Mandatory Checks
1. Kritik değişiklikler release note ve rationale taşımalı.
2. Minimum agent ve protocol docs eksik olmamalı.
3. Karar gerekçeleri kalıcı refs ile saklanmalı.

## Enforcement
- allow_with_warning
- require_review
- release_hold

## Exception Path
Yalnız kısa süreli acil değişiklikte, sonradan tamamlama şartıyla.

## Evidence
- docs refs
- release notes
- rationale refs
- review comments

## Review Cadence
Her major change setinde.
