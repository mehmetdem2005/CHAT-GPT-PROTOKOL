# PL-044 — AI Hallucination & Accuracy Policy

## Objective
Model output doğruluğu, belirsizlik işaretleme ve kritik alanlarda yanlış kesinlik üretimini azaltmak.

## Scope
- generated recommendations
- structured outputs
- summaries
- user-facing explanations

## Mandatory Checks
1. Düşük güvenli veya belirsiz output açık uncertainty sinyali taşımalı.
2. Kritik alanlarda doğrulanmamış kesin dil minimize edilmeli.
3. Repeated accuracy failure review ve remediation üretmeli.

## Enforcement
- allow_with_warning
- require_review
- hard_block for critical unsafe certainty patterns

## Evidence
- confidence refs
- output review refs
- incident or escalation refs
- evaluation notes

## Review Cadence
Her kritik output surface ve model revision sonrası.
