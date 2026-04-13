# RP-06 — Tenant Isolation Verification Procedure

## Trigger
Auth, storage, cache, preview veya topology değişikliği tenant sınırını etkileyebilir.

## Steps
1. Tenant scope boundaries listesini çıkar.
2. Cross-tenant read ve write risklerini kontrol et.
3. Cache, namespace ve preview ayrımını doğrula.
4. Bulguları severity ile kaydet.
5. Gerekirse blocking review veya hold sonucu üret.

## Completion
- isolation_verified
- isolation_needs_review
- isolation_blocked
