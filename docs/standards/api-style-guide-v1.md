# API Style Guide v1

## Purpose
API endpoint isimlendirme, versioning, pagination, error davranışı ve compatibility beklentilerini standartlaştırmak.

## Naming Rules
- resource names plural olmalı
- paths kebab-case kullanmalı
- verbs route yerine action objects veya sub-resources ile temsil edilmeli

## Versioning Rules
- breaking API changes explicit version signal taşımalı
- deprecation replacement ve sunset tarihi ile duyurulmalı

## Request Rules
- requestId ve traceId mümkünse taşınmalı
- validation hataları field-based details içermeli

## Response Rules
- success ve error envelope tutarlı olmalı
- pagination varsa page info alanları normalize olmalı

## Error Rules
- codes Global Error Code Registry ile uyumlu olmalı
- internal secrets veya stack trace response içine yazılmamalı

## Review Requirements
- API style deviation documented review gerektirir
