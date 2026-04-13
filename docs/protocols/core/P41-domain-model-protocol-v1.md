# P41 — Domain Model Protocol v1

## Purpose
Domain entity'leri, ilişkileri, invariants ve bounded context ayrımlarını standartlaştırmak.

## Producers
- domain modeling agents
- architecture agents

## Consumers
- backend architecture
- data schema
- workflow and API design

## Required Fields
- protocolVersion
- domainModelId
- boundedContexts
- entities
- relationships
- invariants
- aggregateRoots
- traceId
- turnId

## Optional Fields
- valueObjects
- domainEvents
- glossaryRefs
- deprecatedConcepts

## Validation Rules
- entities boş olamaz
- aggregateRoots entity refs ile uyumlu olmalı
- invariants en az subject ref içermeli
- boundedContexts birbirine karışmamalı

## Example Shape
{
  "domainModelId": "dm_001",
  "boundedContexts": [],
  "entities": [],
  "relationships": [],
  "invariants": [],
  "aggregateRoots": []
}

## Error Modes
- missing_entities
- invalid_aggregate_root
- invariant_without_subject
- overlapping_bounded_contexts
