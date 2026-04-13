# PL-045 — User Data Portability Policy

## Objective
Kullanıcı verisinin taşınabilir export ve anlaşılır teslim beklentisini görünür hale getirmek.

## Scope
- user export requests
- portable data bundles
- structured delivery formats

## Mandatory Checks
1. Portable export subject scope ile uyumlu olmalı.
2. Unsupported fields veya exclusions documented reason taşımalı.
3. Export request izlenebilir request and completion refs üretmeli.

## Enforcement
- require_review
- require_approval for sensitive scopes

## Evidence
- export request refs
- completion refs
- exclusion notes
- privacy review refs

## Review Cadence
Her export surface ve format değişikliğinde.
