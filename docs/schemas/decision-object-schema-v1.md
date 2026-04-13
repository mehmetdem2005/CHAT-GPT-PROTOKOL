# Decision Object Schema v1

## Purpose
Kullanıcı veya sistem tarafından alınan karar nesnesinin ortak şeklini tanımlamak.

## Required Fields
- decisionId
- decisionCategory
- selectedOptionRef
- madeBy
- reasonSummary
- turnId

## Optional Fields
- affectedArtifactRefs
- locked
- reversible
- evidenceRefs

## Validation Rules
- decisionCategory normalize enum değerinden biri olmalı
- selectedOptionRef bulunmalı
- reasonSummary boş olamaz
- locked true ise unlock path ayrı kayıtta görünmelidir
