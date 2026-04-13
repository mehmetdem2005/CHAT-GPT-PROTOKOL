# Legacy Policy Lineage

Bu belge, önceki politika omurgasının unutulmaması için eklenmiştir.

## Amaç
- İlk Policy Registry v1 içindeki çekirdek aileleri korumak
- Yeni 33 ailelik genişleme ile önceki 13 aile arasındaki sürekliliği görünür kılmak
- Repo içinde "eski politika seti kayboldu" durumunu önlemek

## Legacy Core Set
İlk resmi omurga şu 13 aileyi içeriyordu:
1. Agent Behavior Policies
2. Product Quality Policies
3. UX Policies
4. Visual Design Policies
5. Accessibility Policies
6. Security Policies
7. Privacy & Data Policies
8. Compliance & Legal Routing Policies
9. Architecture & Contract Policies
10. Runtime & Reliability Policies
11. QA & Release Policies
12. Auditability & Observability Policies
13. Human Intervention & Governance Policies

## Korunan Global Registry Kuralları
Legacy registry içindeki şu mantık korunur:
- Her politika için `policyId`, `policyName`, `policyFamily`, `version`, `purpose`, `scope`, `appliesToAgents`, `enforcementMode`, `severity`, `passCriteria`, `violationOutcomes`, `overrideRules` alanları düşünülmelidir.
- Enforcement modları: `advisory`, `warn`, `soft-block`, `hard-block`
- Karar sonuçları: `allow`, `allow_with_warning`, `require_review`, `block`
- `critical` + `hard-block` ihlallerinde ilgili tur veya sürüm yayınlanamaz.

## Genişleme Kuralı
Yeni 33 ailelik yapı, legacy 13 aileyi silmez.
Aksine:
- PL-001 ile PL-013 arası çekirdek mirası taşır
- PL-014 ile PL-033 arası ise genişletilmiş operasyon, platform ve yönetişim katmanlarını ekler

## Mapping
- Legacy Agent Behavior -> PL-001
- Legacy Product Quality -> PL-002
- Legacy UX -> PL-003
- Legacy Visual Design -> PL-004
- Legacy Accessibility -> PL-005
- Legacy Security -> PL-006
- Legacy Privacy & Data -> PL-007
- Legacy Compliance & Legal Routing -> PL-008
- Legacy Architecture & Contract -> PL-009
- Legacy Runtime & Reliability -> PL-010
- Legacy QA & Release -> PL-011
- Legacy Auditability & Observability -> PL-012
- Legacy Human Intervention & Governance -> PL-013

## Sonuç
Repo içindeki yeni policy yapısı, legacy çekirdek politika omurgasını temel alır ve onu genişletir. Bundan sonra politika belgeleri yazılırken veya güncellenirken bu soy ağacı korunmalıdır.
