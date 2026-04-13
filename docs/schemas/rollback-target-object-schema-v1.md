# Rollback Target Object Schema v1

## Purpose
Rollback hedefini, kapsamını ve doğrulama bağını taşıyan ortak nesneyi tanımlamak.

## Required Fields
- rollbackTargetId
- targetSnapshotRef
- rollbackScope
- affectedRefs
- createdAt

## Optional Fields
- approvalRef
- validationPlanRef
- reasonSummary

## Rollback Scope Values
- single_artifact
- module_scope
- turn_scope
- release_candidate_scope
- workspace_scope

## Validation Rules
- targetSnapshotRef boş olamaz
- affectedRefs en az bir ref içermeli
- rollbackScope normalize enum değerinden biri olmalı
