# Agent Execution Record Schema v1

## Purpose
Bir ajanın bir task üzerinde çalışmasına ait ortak yürütme kaydını tanımlamak.

## Required Fields
- executionId
- agentId
- taskRef
- status
- startedAt
- turnId

## Optional Fields
- completedAt
- outputRefs
- failureRefs
- retryCount
- notes

## Status Values
- scheduled
- accepted
- running
- completed
- failed
- blocked
- skipped

## Validation Rules
- agentId boş olamaz
- taskRef bulunmalı
- completed status için completedAt veya outputRefs bulunmalı
