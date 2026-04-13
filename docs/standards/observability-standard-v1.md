# Observability Standard v1

## Purpose
Trace, log ve metric alanlarında minimum zorunlu standardı belirlemek.

## Required Correlation Fields
- traceId
- requestId where applicable
- turnId where applicable
- workspaceId where applicable
- sourceRef

## Log Rules
- structured logs kullanılmalı
- severity normalize olmalı
- secret ve hassas veri log’a yazılmamalı

## Trace Rules
- kritik akışlar distributed trace taşımalı
- parent-child ilişkileri korunmalı

## Metric Rules
- metric names anlamlı ve stable olmalı
- units görünür olmalı
- SLO taşıyan metrikler ayrı işaretlenmeli

## Review Requirements
- yeni kritik servis veya runtime yüzeyi observability review gerektirir
