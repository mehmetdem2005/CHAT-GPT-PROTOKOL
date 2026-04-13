# PL-042 — Data Residency & Sovereignty Policy

## Objective
Veri lokasyonu, saklama bölgesi ve egemenlik gereksinimlerinin görünür ve review-bound olmasını sağlamak.

## Scope
- stored user data
- backups
- exports
- analytics storage
- vendor-hosted regulated data

## Mandatory Checks
1. Regulated veya region-sensitive data class storage region refs taşımalı.
2. Cross-region transfer documented review gerektirmeli.
3. Backup ve archive yüzeyleri aynı sınıflandırma kontrolüne tabi olmalı.

## Enforcement
- require_review
- require_approval
- hard_block

## Evidence
- data class refs
- region maps
- storage refs
- transfer notes

## Review Cadence
Her regulated data flow değişikliğinde.
