# MP-01 — Input Capture Protocol

## Purpose
Ham kullanıcı cevaplarını, seçimleri ve upload referanslarını normalize edilmeden önce taşımak.

## Producers
- Studio UI
- intake surfaces
- A03

## Consumers
- A06
- A10
- downstream normalization flows

## Required Fields
- captureId
- sourceSurface
- rawInputs
- uploadRefs
- capturedAt
- turnId
- workspaceId
- traceId

## Optional Fields
- locale
- deviceHints
- validationWarnings
- sourceActorRef

## Validation Rules
- rawInputs boş olamaz
- uploadRefs varsa erişilebilir ref formatında olmalı
- turnId ve traceId bulunmalı

## Error Modes
- invalid_input_shape
- oversized_payload
- missing_capture_context
