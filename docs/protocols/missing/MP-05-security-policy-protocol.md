# MP-05 — Security Policy Protocol

## Purpose
Güvenlik gereksinimlerini modül ve feature seviyesinde taşımak.

## Producers
- A52
- security governance config

## Consumers
- A36
- A39
- A46
- A51

## Required Fields
- securityPolicyId
- authRequirements
- secretRules
- inputSecurityRules
- reviewTriggers
- traceId

## Optional Fields
- vendorConstraints
- environmentConstraints
- outputHandlingRules

## Validation Rules
- authRequirements boş olamaz
- secretRules hassas yüzeyleri kapsamalı
- reviewTriggers kritik değişiklik sınıflarını işaretlemeli

## Error Modes
- incomplete_security_policy
- missing_auth_boundary
- missing_secret_rule
