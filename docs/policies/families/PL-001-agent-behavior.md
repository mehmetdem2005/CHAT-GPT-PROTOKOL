# PL-001 — Agent Behavior Policies

## Objective
Ajanların contract-first, izlenebilir, kontrollü ve minimum gerekli değişiklik ilkesiyle çalışmasını zorunlu kılmak.

## Primary Subjects
- task contracts
- task graphs
- agent outputs
- code patches

## Mandatory Checks
1. Görev resmi protokol ve schema ile tanımlanmış olmalı.
2. Ajan, lock veya policy sınırını sessizce ezmemeli.
3. Üretilen patch için reason ve affected refs görünür olmalı.

## Enforcement
- warn
- require_review
- turn_block

## Exception Path
Sadece yetkili operator veya approval-bound governance kararıyla geçici istisna açılabilir.

## Evidence
- task refs
- patch refs
- trace id
- audit record

## Review Cadence
Quarterly veya major agent behavior change sonrası.
