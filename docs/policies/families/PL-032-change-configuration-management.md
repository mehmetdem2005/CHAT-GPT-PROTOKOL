# PL-032 — Change & Configuration Management Policies

## Objective
Değişiklik etkisini, config kontrolünü ve geri alınabilirlik beklentisini görünür kılmak.

## Primary Subjects
- config changes
- schema changes
- deployments
- hotfix changes

## Mandatory Checks
1. Kritik değişiklikler impact summary taşımalı.
2. Config ve hızlı düzeltmeler onay akışına bağlı olmalı.
3. Geri dönüş veya düzeltme yolu görünür olmalı.

## Enforcement
- require_review
- require_approval
- release_hold
- hard_block

## Exception Path
Yalnız documented acil durum yolu ve sonradan tam review ile.

## Evidence
- change refs
- approval refs
- rollback refs
- deployment refs

## Review Cadence
Her kritik değişiklikte.
