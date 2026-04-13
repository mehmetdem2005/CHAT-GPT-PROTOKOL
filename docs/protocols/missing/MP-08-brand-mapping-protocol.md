# MP-08 — Brand Mapping Protocol

## Purpose
Marka girdisinin design token ve art direction sistemine nasıl eşlendiğini taşımak.

## Producers
- A29

## Consumers
- A31
- A33

## Required Fields
- brandMappingId
- brandInputRef
- tokenOverrides
- preservedConstraints
- mappingSummary
- traceId

## Optional Fields
- rejectedMappings
- legalApprovals
- reviewRefs

## Validation Rules
- brandInputRef bulunmalı
- mappingSummary boş olmamalı
- preservedConstraints varsa uygulanabilir tipte olmalı

## Error Modes
- unsafe_brand_override
- missing_brand_input_ref
- invalid_token_override
