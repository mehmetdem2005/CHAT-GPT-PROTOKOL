# PL-029 — Model Output Censorship & Safety Policies

## Objective
Yasaklı çıktı kategorilerini ve güvenli fallback davranışını enforce etmek.

## Primary Subjects
- generated text
- option copy
- recommendations
- templates

## Mandatory Checks
1. Yasaklı içerik sınıfları engellenmeli veya güvenli fallback kullanılmalı.
2. Moderation katmanı kritik yüzeylerde görünür olmalı.
3. Unsafe output release veya user surface’a taşınmamalı.

## Enforcement
- allow
- allow_with_warning
- turn_block
- hard_block

## Exception Path
Genel exception verilmez; yalnız internal review ve controlled redaction mümkündür.

## Evidence
- moderation refs
- output logs
- safety decisions
- audit refs

## Review Cadence
Her output surface değişikliğinde.
