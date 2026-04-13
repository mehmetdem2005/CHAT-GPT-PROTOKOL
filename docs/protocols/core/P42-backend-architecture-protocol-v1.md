# P42 — Backend Architecture Protocol v1

## Purpose
Service topology, job model, state ownership ve integration boundary yapısını standartlaştırmak.

## Producers
- backend architecture agents

## Consumers
- implementation planning
- deployment topology
- runtime and observability planning

## Required Fields
- protocolVersion
- backendArchitectureId
- serviceMap
- jobTypes
- stateOwnership
- integrationBoundaries
- traceId
- turnId

## Optional Fields
- storageMap
- deploymentHints
- failureDomains
- externalDependencies

## Validation Rules
- serviceMap boş olamaz
- stateOwnership kritik state alanlarını kapsamalı
- integrationBoundaries service refs ile uyumlu olmalı
- jobTypes background or sync role işaretlemeli

## Example Shape
{
  "backendArchitectureId": "ba_001",
  "serviceMap": [],
  "jobTypes": [],
  "stateOwnership": {},
  "integrationBoundaries": []
}

## Error Modes
- missing_service_map
- unowned_state
- invalid_integration_boundary
- undefined_job_type
