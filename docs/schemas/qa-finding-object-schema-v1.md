# QA Finding Object Schema v1

## Purpose
QA bulgularının ortak nesne biçimini tanımlamak.

## Required Fields
- findingId
- findingType
- severity
- summary
- affectedRefs
- blocking

## Optional Fields
- evidenceRefs
- remediationHint
- ownerRef
- targetDate

## Validation Rules
- findingType ve severity normalize enum değerlerinden gelmeli
- summary boş olamaz
- affectedRefs en az bir ref içermeli
- blocking true ise severity düşük olsa bile rationale bulunmalı
