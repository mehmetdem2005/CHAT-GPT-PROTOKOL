# PL-010 — Runtime & Reliability Policies

## Objective
Health, timeout, retry safety ve preview/runtime istikrarını zorunlu kılmak.

## Primary Subjects
- preview sessions
- runtime instances
- route validations
- deployments

## Mandatory Checks
1. Health ve readiness sinyalleri görünür olmalı.
2. Retry yan etkileri güvenli sınırda kalmalı.
3. Degraded ve failed modları ayrı ele alınmalı.

## Enforcement
- allow_with_warning
- require_review
- release_hold
- rollback_recommended

## Exception Path
Yalnız documented operational risk acceptance ile, sınırlı süreli.

## Evidence
- health checks
- diagnostics
- route validations
- runtime logs

## Review Cadence
Her runtime surface değişikliğinde ve her release öncesi.
