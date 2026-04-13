# Testing Standard v1

## Purpose
Schema, unit, integration, preview, accessibility, contract ve release gate testleri için minimum beklentiyi tanımlamak.

## Minimum Test Classes
- schema validation tests
- unit tests
- integration tests
- preview smoke tests
- accessibility checks
- contract tests
- release readiness tests

## Mandatory Rules
- critical protocol changes fixture validation gerektirir
- critical route changes preview smoke gerektirir
- contract-affecting changes contract test gerektirir
- release candidate minimum smoke seti olmadan ilerlememeli

## Evidence
- report refs
- test bundle refs
- CI refs

## Review Requirements
- test class eksikliği documented waiver veya follow-up gerektirir
