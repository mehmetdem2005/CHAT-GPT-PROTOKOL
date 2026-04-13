# RP-04 — Rollback Validation Procedure

## Trigger
Rollback tamamlandı ve doğrulama gerekiyor.

## Steps
1. Artifact integrity kontrol et.
2. Route availability ve preview durumunu ölç.
3. Temel QA smoke sonuçlarını topla.
4. Release gate etkisini yeniden değerlendir.
5. Validation outcome kaydı üret.

## Completion
- rollback_validated
- rollback_needs_review
- rollback_invalid
