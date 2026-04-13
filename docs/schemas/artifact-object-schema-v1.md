# Artifact Object Schema v1

## Purpose
Manifest ve patch bağlamında tekrar eden artifact nesnesinin ortak yapısını tanımlamak.

## Required Fields
- artifactId
- artifactType
- path
- status
- moduleRef
- ownedByAgent
- primaryPurpose
- createdInTurnId
- lastModifiedInTurnId

## Optional Fields
- patchRefs
- contractRefs
- policyRefs
- previewRelevance
- qaCoverageRefs
- rollbackEligible

## Artifact Types
- page
- component
- layout
- route_config
- style
- design_token
- schema
- type_definition
- service
- build_config
- runtime_config
- test
- documentation

## Validation Rules
- path boş olamaz
- moduleRef bulunmalı
- artifactType normalize enum değerinden biri olmalı
- lastModifiedInTurnId createdInTurnId ile uyumlu olmalı
