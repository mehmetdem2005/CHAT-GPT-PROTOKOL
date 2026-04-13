# Event Catalog v1

Bu belge, sistemdeki temel event sınıflarını ve producer-consumer yönlerini listeler.

## Core Events
- turn.opened
- turn.awaiting_input
- turn.completed
- task.dispatched
- task.completed
- task.failed
- preview.started
- preview.ready
- preview.failed
- approval.requested
- approval.resolved
- rollback.requested
- rollback.executed
- release.reviewed
- release.blocked

## Producer/Consumer Examples
- orchestrator -> task.dispatched -> agents
- preview runtime -> preview.failed -> studio ui, governance
- governance -> approval.requested -> approvers
- rollback executor -> rollback.executed -> manifest store, preview validation

## Required Event Metadata
- eventId
- eventName
- eventVersion
- occurredAt
- producerId
- traceId
- payload
