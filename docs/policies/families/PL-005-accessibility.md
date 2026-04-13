# PL-005 — Accessibility Policies

## Objective
Tüm kritik yüzeylerde erişilebilirlik baseline’ını zorunlu kılmak.

## Primary Subjects
- rendered previews
- navigation
- forms
- release candidates

## Mandatory Checks
1. Focus visibility ve keyboard erişimi doğrulanmalı.
2. Kontrast, form labeling ve semantics baseline’ı geçilmeli.
3. Reduced motion ve uyarlanabilirlik desteği düşünülmeli.

## Enforcement
- allow_with_warning
- turn_block
- release_hold

## Exception Path
Blocking accessibility issue için kalıcı istisna verilmez; yalnız geçici internal review sınırı olabilir.

## Evidence
- a11y QA
- viewport captures
- form audits
- release gate refs

## Review Cadence
Her release candidate ve her büyük UX değişikliği sonrası.
