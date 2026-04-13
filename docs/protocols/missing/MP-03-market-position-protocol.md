# MP-03 — Market Position Protocol

## Purpose
Ürün fikrinin segment, rakip bağlamı ve değer önerisi çerçevesini taşımak.

## Producers
- A08

## Consumers
- A21
- A22
- A31

## Required Fields
- marketPositionId
- targetSegments
- valueHypotheses
- differentiationNotes
- riskNotes
- turnId
- traceId

## Optional Fields
- competitorRefs
- evidenceRefs
- marketConstraints

## Validation Rules
- targetSegments boş olamaz
- valueHypotheses en az bir öğe içermeli
- differentiationNotes kısa slogan değil açıklayıcı olmalı

## Error Modes
- ambiguous_positioning
- missing_segment_context
- unsupported_market_scope
