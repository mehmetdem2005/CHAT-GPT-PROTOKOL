# PL-017 — Localization & Internationalization Policies

## Objective
Locale, fallback language, RTL ve formatlama davranışlarını kontrollü hale getirmek.

## Primary Subjects
- rendered previews
- locale config
- option outputs

## Mandatory Checks
1. Varsayılan locale ve fallback dili net tanımlanmalı.
2. RTL gereken yüzeylerde bozulma kontrol edilmeli.
3. Tarih, saat, para ve sayı formatları bölgeye uygun olmalı.

## Enforcement
- allow_with_warning
- require_review
- release_warning

## Exception Path
Yalnız geçici eksik çeviri veya sınırlı beta yüzeyi için.

## Evidence
- locale maps
- preview captures
- rtl checks
- formatting samples

## Review Cadence
Her yeni locale ve büyük UX revizyonunda.
