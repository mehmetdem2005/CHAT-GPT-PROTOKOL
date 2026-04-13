# RP-03 — Rollback Execution Procedure

## Trigger
Approved rollback veya critical regression.

## Steps
1. Target snapshot doğrula.
2. Scope ve affected artifacts listesini sabitle.
3. Approval zorunluluğunu kontrol et.
4. Manifest ve turn refs güncelle.
5. Post-rollback validation başlat.

## Completion
- rollback_executed
- rollback_failed
- approval_missing
