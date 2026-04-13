# Approval Object Schema v1

## Purpose
Approval-bound kararlar için ortak approval nesnesinin şeklini tanımlamak.

## Required Fields
- approvalId
- subjectRef
- status
- requiredApprovers
- requestedAt

## Optional Fields
- resolvedAt
- resolutionReason
- evidenceRefs
- selfApprovalAllowed

## Status Values
- pending
- approved
- rejected
- expired

## Validation Rules
- subjectRef boş olamaz
- requiredApprovers en az bir approver içermeli
- approved veya rejected durumunda resolvedAt bulunmalı
