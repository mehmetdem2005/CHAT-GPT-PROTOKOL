# PL-006 — Security Policies

## Objective
Auth, authorization, input validation, secret handling ve least-privilege sınırlarını zorunlu kılmak.

## Primary Subjects
- auth actions
- deployments
- previews
- API contracts
- integrations

## Mandatory Checks
1. Kritik yüzeylerde kimlik ve yetki sınırı doğrulanmalı.
2. Secret, token ve hassas config preview veya public surface’a sızmamalı.
3. Zararlı girdi ve injection yolları filtrelenmeli.

## Enforcement
- require_review
- release_hold
- hard_block

## Exception Path
Yalnız security owner ve gerekli approver zinciriyle, süreli ve audit-linked istisna açılabilir.

## Evidence
- auth audit logs
- security scans
- secret scan results
- deployment evidence

## Review Cadence
Continuous ve her kritik değişiklikte zorunlu.
