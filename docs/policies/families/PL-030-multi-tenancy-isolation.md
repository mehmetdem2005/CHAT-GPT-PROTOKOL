# PL-030 — Multi-Tenancy & Isolation Policies

## Objective
Tenant bazlı veri, cache, preview ve runtime izolasyonunu zorunlu kılmak.

## Primary Subjects
- preview sessions
- storage namespaces
- cache strategy
- auth actions
- topology config

## Mandatory Checks
1. Cross-tenant veri ve runtime karışımı engellenmeli.
2. Namespace ve scope doğrulaması görünür olmalı.
3. Convenience uğruna isolation gevşetilmemeli.

## Enforcement
- require_review
- hard_block

## Exception Path
Genel exception yok; yalnız açık governance kararı ve süreli mitigasyon olabilir.

## Evidence
- tenant scope checks
- topology refs
- auth logs
- isolation evidence

## Review Cadence
Her auth, preview veya topology değişikliğinde.
