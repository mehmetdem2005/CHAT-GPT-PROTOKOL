# PL-041 — AI Training Data Policy

## Objective
Model tuning, evaluation veya synthetic data üretiminde kullanılacak veri kaynaklarının güvenli ve izinli olmasını sağlamak.

## Scope
- fine-tuning datasets
- evaluation datasets
- synthetic augmentation inputs
- sensitive source material

## Mandatory Checks
1. Eğitim veya evaluation veri kaynağı izin ve sınıflandırma taşımalı.
2. Hassas veri kullanımı explicit review gerektirmeli.
3. Dataset lineage ve retention görünür olmalı.

## Enforcement
- require_review
- require_approval
- hard_block

## Evidence
- dataset refs
- classification refs
- approvals
- lineage notes

## Review Cadence
Her yeni training/evaluation dataset akışında.
