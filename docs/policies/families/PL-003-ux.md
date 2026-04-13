# PL-003 — UX Policies

## Objective
Kullanıcıya açıklanabilir, güvenli, zengin seçimli ve cihaz uyumlu deneyim sunulmasını zorunlu kılmak.

## Primary Subjects
- option sets
- navigation
- interaction patterns
- previews

## Mandatory Checks
1. Kullanıcıyı sessiz kararla kilitleme yapılmamalı.
2. Kritik aksiyonlar yeterli friction ve feedback taşımalı.
3. Mobile ve tablet davranışı ayrıca gözden geçirilmeli.

## Enforcement
- allow
- allow_with_warning
- require_user_choice
- require_review

## Exception Path
Yalnız documented UX risk acceptance ile, sınırlı scope için.

## Evidence
- option refs
- preview captures
- diagnostics
- user feedback refs

## Review Cadence
Her yeni UX surface eklendiğinde ve release öncesi.
