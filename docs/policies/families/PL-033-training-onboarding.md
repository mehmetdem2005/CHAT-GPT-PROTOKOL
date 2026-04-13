# PL-033 — Training & Onboarding Policies

## Objective
Yetkili aktörlerin eğitim, yetkinlik ve hazırlık seviyesini görünür ve denetlenebilir hale getirmek.

## Primary Subjects
- operator actions
- approval actions
- rollback actions
- privileged workflows

## Mandatory Checks
1. Kritik yetki verilen roller için minimum hazırlık tanımlanmalı.
2. Canlı kritik aksiyonlardan önce uygun hazırlık kanıtı bulunmalı.
3. Eğitim ve dokümantasyon erişimi görünür olmalı.

## Enforcement
- require_review
- hard_block

## Exception Path
Yalnız açık owner kararı ve sınırlı scope ile.

## Evidence
- training records
- simulation refs
- role mappings
- access reviews

## Review Cadence
Quarterly ve yeni yetkili rol tanımlarında.
