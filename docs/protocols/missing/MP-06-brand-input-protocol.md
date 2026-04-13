# MP-06 — Brand Input Protocol

## Purpose
Marka varlıklarını, ton ve görsel bağlam ipuçlarını normalize biçimde taşımak.

## Producers
- user upload flow
- Studio UI

## Consumers
- A21
- A29

## Required Fields
- brandInputId
- assetRefs
- toneHints
- restrictedElements
- sourceType
- turnId
- traceId

## Optional Fields
- colorHints
- typographyHints
- legalNotes

## Validation Rules
- assetRefs boş olamaz
- restrictedElements varsa uygulanabilir sınıflar içermeli
- sourceType desteklenen giriş türü olmalı

## Error Modes
- invalid_asset_ref
- unsupported_brand_input
- missing_brand_context
