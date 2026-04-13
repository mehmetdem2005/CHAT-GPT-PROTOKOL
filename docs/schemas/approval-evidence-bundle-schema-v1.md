# Approval Evidence Bundle Schema v1

## Purpose
Approval kararına bağlanan kanıt paketinin ortak yapısını tanımlamak.

## Required Fields
- evidenceBundleId
- subjectRef
- evidenceRefs
- summary
- createdAt

## Optional Fields
- blockingFindings
- waiverRefs
- previewRefs
- qaRefs
- policyDecisionRefs

## Validation Rules
- subjectRef boş olamaz
- evidenceRefs en az bir ref içermeli
- summary boş olamaz
