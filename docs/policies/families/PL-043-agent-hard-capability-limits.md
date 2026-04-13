# PL-043 — Agent Hard Capability Limits Policy

## Objective
Ajanların hangi sınırlara kadar davranabileceğini ve hangi aksiyonları tek başına yapamayacağını sabitlemek.

## Scope
- autonomous generation
- structural changes
- override attempts
- cross-module mutations
- privileged actions

## Mandatory Checks
1. Hard boundary aşan agent aksiyonları human/governance kontrolüne gitmeli.
2. Cross-scope mutation açık izin olmadan yapılamamalı.
3. Agent capability declaration olmayan aksiyonlar yetkisiz kabul edilmeli.

## Enforcement
- turn_block
- require_approval
- hard_block

## Evidence
- capability refs
- task refs
- override refs
- audit refs

## Review Cadence
Her yeni agent capability ve orchestration change setinde.
