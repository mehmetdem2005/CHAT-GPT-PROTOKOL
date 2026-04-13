# RP-01 — Preview Failure Triage Procedure

## Trigger
Preview failed, degraded veya unstable.

## Steps
1. Failure domain belirle: build, startup, route, render, panel.
2. Son başarılı state'i bul.
3. Etkilenen routes ve viewports'u listele.
4. Rerun, safe mode veya fix path seç.
5. Turn state ve diagnostics refs güncelle.

## Completion
- triage_complete
- fix_requested
- rerun_authorized
