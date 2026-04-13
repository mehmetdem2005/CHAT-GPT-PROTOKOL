# Option Card Schema v1

## Purpose
Kullanıcıya sunulan seçilebilir seçenek kartlarının ortak şeklini tanımlamak.

## Required Fields
- optionId
- optionType
- title
- summary
- selectable

## Optional Fields
- previewRef
- tradeoffs
- tags
- recommendedFor
- blockedReason

## Option Types
- navigation_pattern
- layout
- automation_model
- visual_direction
- architecture_variant

## Validation Rules
- title boş olamaz
- selectable false ise blockedReason bulunmalı
- previewRef varsa erişilebilir ref formatında olmalı
