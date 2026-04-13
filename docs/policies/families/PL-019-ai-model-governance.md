# PL-019 — AI Model Governance Policies

## Objective
Model sürümü, prompt güvenliği, explainability, bias ve tuning dataset güvenliğini kontrollü hale getirmek.

## Primary Subjects
- model invocations
- agent configs
- datasets
- recommendations

## Mandatory Checks
1. Model sürümleri sabitlenebilir ve izlenebilir olmalı.
2. Prompt injection ve fetched input riskleri kontrol edilmeli.
3. Kritik kararlar en azından reason summary ve evidence refs taşımalı.

## Enforcement
- require_review
- require_approval
- hard_block

## Exception Path
Yalnız owner, reviewer ve gerekiyorsa governance approval zinciriyle.

## Evidence
- model version refs
- safety checks
- dataset refs
- evaluation notes

## Review Cadence
Her model veya prompt strategy değişikliğinde.
