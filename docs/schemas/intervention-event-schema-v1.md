# Intervention Event Schema v1

## Purpose
Lock, override, reroute, halt ve related governance müdahaleleri için ortak olay nesnesini tanımlamak.

## Required Fields
- interventionId
- actionType
- initiatedBy
- targetRef
- targetType
- reason
- linkedTurnId
- executionStatus

## Optional Fields
- approvalRef
- auditRef
- resultSummary
- affectedTaskRefs
- affectedArtifactRefs

## Action Types
- lock_choice
- unlock_choice
- override_decision
- reroute_task
- halt_generation
- force_review
- request_regeneration
- reject_output

## Validation Rules
- targetRef boş olamaz
- actionType normalize enum değerinden biri olmalı
- executionStatus pending, accepted, running, completed, failed veya cancelled olmalı
