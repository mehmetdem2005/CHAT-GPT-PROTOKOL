# MP-11 — Code Snapshot Protocol

## Purpose
Belirli bir turn veya patch sonrası codebase snapshot bağını standartlaştırmak.

## Producers
- A40
- A42

## Consumers
- A41
- A46
- A48

## Required Fields
- codeSnapshotId
- snapshotRef
- createdAt
- turnRef
- artifactRefs
- integrityHash
- traceId

## Optional Fields
- baseSnapshotRef
- diffSummary
- manifestRef

## Validation Rules
- snapshotRef bulunmalı
- artifactRefs boş olamaz
- integrityHash hesaplanabilir formatta olmalı

## Error Modes
- snapshot_not_found
- integrity_mismatch
- missing_artifact_refs
