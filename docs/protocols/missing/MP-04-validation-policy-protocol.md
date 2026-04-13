# MP-04 — Validation Policy Protocol

## Purpose
Form, workflow ve input validation kurallarını tek policy taşıyıcısında toplamak.

## Producers
- governance config
- A53

## Consumers
- A14
- A31
- A41

## Required Fields
- validationPolicyId
- ruleSets
- fieldClasses
- failurePresentationRules
- escalationRules
- traceId

## Optional Fields
- localeOverrides
- accessibilityNotes
- severityBands

## Validation Rules
- ruleSets boş olamaz
- fieldClasses desteklenen sınıflarla eşleşmeli
- failure presentation kuralları kullanıcıya gösterim mantığı taşımalı

## Error Modes
- invalid_rule_set
- unsupported_field_class
- missing_failure_presentation
