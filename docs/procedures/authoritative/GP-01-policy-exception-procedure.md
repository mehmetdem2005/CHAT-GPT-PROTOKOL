# GP-01 — Policy Exception Procedure

## Trigger
Bir kural geçici olarak aşılamadan ilerlenemiyor.

## Prerequisites
- ilgili policy ref
- risk summary
- owner bilgisi
- affected scope

## Steps
1. Exception request oluştur.
2. Policy ref ve affected scope ekle.
3. Risk ve gerekçeyi yaz.
4. Expiry tarihi belirle.
5. Gerekli approver zincirini çalıştır.
6. Audit kaydını bağla.

## Completion
- allow_with_exception
- denied
- needs_more_evidence
