# PL-016 — Energy Efficiency & Sustainability Policies

## Objective
Gereksiz ajan işi, boşta preview süreçleri ve tekrar eden pahalı işlemleri azaltmak.

## Primary Subjects
- preview sessions
- task graphs
- scheduled jobs

## Mandatory Checks
1. Idle preview süreçleri teardown edilmeli.
2. Tekrarlayan iş tekrar üretimi azaltılmalı.
3. Batch uygun işlerde öncelikli tercih olmalı.

## Enforcement
- advisory
- allow_with_warning
- require_review

## Exception Path
Yalnız performans veya test zorunluluğu açıkça belgelendiğinde.

## Evidence
- idle runtime metrics
- duplicate invocation patterns
- batch job summaries

## Review Cadence
Quarterly.
