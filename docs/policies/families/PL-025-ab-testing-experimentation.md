# PL-025 — A/B Testing & Experimentation Policies

## Objective
Deneylerin kontrollü, adil, ölçülebilir ve geri çekilebilir olmasını zorunlu kılmak.

## Primary Subjects
- experiment configs
- traffic assignments
- release candidates

## Mandatory Checks
1. Her deneyin hipotezi ve başarı ölçütü yazılı olmalı.
2. Trafik dağılımı ve geri çekilme koşulları açık olmalı.
3. Zararlı deney sonucu hızlı retreat yoluna bağlı olmalı.

## Enforcement
- require_review
- require_approval
- hard_block

## Exception Path
Yalnız sınırlı internal experiment ve owner approval ile.

## Evidence
- experiment configs
- metrics refs
- rollout refs
- retreat refs

## Review Cadence
Her production experiment öncesi.
