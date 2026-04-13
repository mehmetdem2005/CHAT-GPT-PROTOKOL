# AP-01 — Accessibility Audit Procedure

## Trigger
Release candidate, major UX surface change veya recurring accessibility concern.

## Roles
- audit owner
- surface owner
- remediation owner

## Inputs
- target routes
- target viewports
- previous a11y findings
- release refs

## Steps
1. Audit scope ve target surfaces listesini sabitle.
2. Keyboard, focus, semantics, contrast ve form behavior kontrol setini çalıştır.
3. Findings'i severity ve blocking flag ile sınıflandır.
4. Route ve viewport bazlı kanıt ekle.
5. Remediation owner ve target date ata.
6. Release impact kararını kaydet.

## Default Timelines
- blocking findings same release window içinde çözülmeli
- non-blocking findings next scheduled remediation window'a atanmalı

## Completion
- audit_passed
- audit_passed_with_findings
- audit_blocked_release
