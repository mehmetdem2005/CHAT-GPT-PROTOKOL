# MP-02 — Uncertainty Protocol

## Purpose
Eksik bilgi, düşük confidence ve clarification ihtiyacını standartlaştırmak.

## Producers
- A01
- A06
- A07

## Consumers
- A03
- A60
- clarification planners

## Required Fields
- uncertaintyId
- subjectRefs
- uncertaintyScore
- blockingUnknowns
- recommendedClarifications
- turnId
- traceId

## Optional Fields
- evidenceRefs
- confidenceBands
- impactedProtocols

## Validation Rules
- uncertaintyScore tanımlı aralıkta olmalı
- subjectRefs boş olamaz
- blockingUnknowns varsa explanation bulunmalı

## Error Modes
- missing_subjects
- invalid_uncertainty_score
- missing_clarification_path
