# PL-027 — Open Source & Licensing Policies

## Objective
Third-party dependency lisans uyumu ve repository lisans açıklığını korumak.

## Primary Subjects
- dependencies
- release packages
- repository metadata

## Mandatory Checks
1. Lisans uyumu release öncesi gözden geçirilmeli.
2. Repository lisansı ve contribution şartları görünür olmalı.
3. Uyuşmazlık release blocking signal üretebilmeli.

## Enforcement
- allow_with_warning
- release_hold
- hard_block

## Exception Path
Yalnız legal review ve documented acceptance ile.

## Evidence
- dependency manifests
- license scan refs
- repository license refs
- legal notes

## Review Cadence
Her dependency değişikliğinde ve release öncesi.
