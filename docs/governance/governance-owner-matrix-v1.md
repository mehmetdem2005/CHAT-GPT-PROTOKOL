# Governance Owner Matrix v1

## Purpose
Policy, procedure, protocol ve registry belgelerinde generic owner boşluğunu azaltmak için rol-temelli owner matrisini tanımlamak.

## Role Classes
- platform governance lead
- security owner
- privacy owner
- auth owner
- preview/runtime owner
- release owner
- compliance owner
- data surface owner
- studio ui owner
- protocol owner

## Family-to-Owner Defaults
- PL-001 -> platform governance lead
- PL-006 -> security owner
- PL-007 -> privacy owner
- PL-010 -> preview/runtime owner
- PL-011 -> release owner
- PL-013 -> platform governance lead
- PL-014 -> release owner
- PL-030 -> security owner + platform governance lead
- PL-031 -> compliance owner
- PL-032 -> platform governance lead
- P41/P42/P48/P64 -> protocol owner with architecture reviewer

## Procedure-to-Owner Defaults
- GP procedures -> platform governance lead unless scoped otherwise
- RP auth/security/privacy procedures -> security owner or privacy owner
- preview/runtime procedures -> preview/runtime owner

## Rule
Every new extended spec should reference a concrete role from this matrix until named individuals or teams are formally assigned.
