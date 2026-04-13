# PL-015 — Cost & Resource Management Policies

## Objective
Ajan çağrıları, preview kaynakları, pipeline maliyeti ve depolama büyümesini kontrollü tutmak.

## Primary Subjects
- task graphs
- preview sessions
- pipeline runs
- storage usage

## Mandatory Checks
1. Kaynak sınırları görünür tanımlanmalı.
2. Aşırı tüketim uyarı ve review üretmeli.
3. Maliyet optimizasyonu kalite veya güvenliği sessizce ezmemeli.

## Enforcement
- allow_with_warning
- require_review
- turn_block

## Exception Path
Yalnız sınırlı süreli ve owner onaylı kapasite artışı ile.

## Evidence
- runtime metrics
- pipeline usage refs
- storage reports
- task volume signals

## Review Cadence
Aylık ve büyük kullanım sıçramalarında.
