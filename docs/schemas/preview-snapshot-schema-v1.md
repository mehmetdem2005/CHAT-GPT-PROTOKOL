# Preview Snapshot Schema v1

## Purpose
Preview çıktılarının capture ve comparison amaçlı ortak nesne yapısını tanımlamak.

## Required Fields
- snapshotId
- previewSessionRef
- routeRef
- viewportId
- snapshotType
- captureRef
- createdAt

## Optional Fields
- layoutIntegrity
- interactionIntegrity
- relatedDiagnosticRefs
- comparisonBaseRef

## Snapshot Types
- baseline_snapshot
- turn_snapshot
- comparison_snapshot
- failure_snapshot
- release_candidate_snapshot

## Validation Rules
- routeRef bulunmalı
- viewportId desteklenen profile işaret etmeli
- captureRef erişilebilir ref formatında olmalı
- comparisonBaseRef varsa mevcut snapshot ref olmalı
