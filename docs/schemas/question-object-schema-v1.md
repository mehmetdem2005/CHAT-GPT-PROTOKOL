# Question Object Schema v1

## Purpose
Sistem tarafından kullanıcıya yöneltilen soru nesnesinin ortak şeklini tanımlamak.

## Required Fields
- questionId
- questionType
- prompt
- isBlocking
- turnId

## Optional Fields
- helperText
- optionRefs
- defaultValue
- validationHints
- sourceProtocolRef

## Question Types
- free_text
- single_select
- multi_select
- ranked_choice
- visual_choice
- confirm_or_reject

## Validation Rules
- prompt boş olamaz
- questionType desteklenen enum değerlerinden biri olmalı
- optionRefs select sınıflarında bulunmalı
