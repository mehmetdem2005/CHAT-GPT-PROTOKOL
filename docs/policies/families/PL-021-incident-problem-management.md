# PL-021 — Incident & Problem Management Policies

## Objective
Severity, notification, containment, postmortem ve RCA disiplinini zorunlu kılmak.

## Primary Subjects
- incidents
- escalations
- postmortems
- problem records

## Mandatory Checks
1. P1–P4 sınıflandırması görünür olmalı.
2. Kritik olaylarda notification ve owner zinciri açık olmalı.
3. P1/P2 olaylar postmortem ve RCA olmadan kapanmamalı.

## Enforcement
- require_review
- release_hold

## Exception Path
Kritik olaylarda exception yok; yalnız sınıflandırma düzeltmesi yapılabilir.

## Evidence
- incident records
- communications log
- timeline
- RCA refs

## Review Cadence
Her P1/P2 sonrası ve quarterly trend review.
