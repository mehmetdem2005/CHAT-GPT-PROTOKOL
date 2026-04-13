# Preview Runtime Protocol Spec v1

Bu belge, üretilen kodun yerel preview/runtime panelinde nasıl build edileceğini, ayağa kaldırılacağını, doğrulanacağını ve gözlemleneceğini tanımlar.

## Amaç
- her tur sonrası üretilen kodun çalıştırılabilir olmasını sağlamak
- masaüstü, tablet ve mobil önizlemeyi aynı panelden göstermek
- route, render, health, viewport ve build durumlarını standartlaştırmak
- preview başarısızlıklarını izlenebilir ve müdahale edilebilir hale getirmek

## Tasarım İlkeleri
- preview first-class artifact’tır
- run what was generated
- fast feedback, bounded execution
- route-aware validation
- viewport-aware rendering
- failure isolation
- human visibility
- intervention friendly

## Kapsam
Bu protokol şunları kapsar:
- build orchestration
- runtime startup
- preview session lifecycle
- port and URL management
- readiness and health checks
- route discovery and validation
- viewport rendering
- snapshot capture
- runtime diagnostics
- panel synchronization
- partial rebuild and rerun logic
- timeout and failure recovery

## Temel Kavramlar
- Preview Session
- Runtime Instance
- Preview Target
- Viewport Profile
- Readiness Gate
- Render Capture
- Diagnostic Layer

## Üst Düzey Akış
1. Input Resolution
2. Build Preparation
3. Build Execution
4. Runtime Startup
5. Health and Readiness Validation
6. Route Discovery
7. Route Validation
8. Viewport Rendering
9. Snapshot Capture
10. Panel Synchronization
11. Continuous Monitoring
12. Teardown or Reuse Decision

## Input Resolution
Zorunlu girdiler:
- workspaceId
- turnId
- manifestRef
- buildRef
- entryPoints
- affectedRoutes
- viewportProfiles
- runtimeMode

Runtime mode değerleri:
- full_preview
- route_subset_preview
- module_preview
- qa_preview
- safe_rerun

## Build Preparation
Hazırlık görevleri:
- çalışma dizinini çöz
- bağımlılık manifestini doğrula
- entry point’leri eşleştir
- env descriptor’ları yükle
- preview-safe config uygula
- build hedeflerini belirle
- kaynak sınırlarını ata

Preview-safe config ilkeleri:
- production yan etkileri kapalı olmalı
- destructive jobs devre dışı olmalı
- sandbox veya sahte entegrasyon modu kullanılmalı
- preview telemetry açık olmalı
- debug yüzeyi kontrollü olmalı

## Build Execution
Build durumları:
- not_started
- preparing
- building
- build_succeeded
- build_failed
- cancelled
- timed_out

Failure category değerleri:
- dependency_resolution_failure
- syntax_failure
- type_failure
- config_failure
- missing_entry_failure
- resource_limit_failure
- unknown_build_failure

Kural:
- build başarısızsa runtime startup fazına geçilmez

## Runtime Startup
Runtime status değerleri:
- not_started
- starting
- running
- degraded
- failed
- stopped
- reused

Kurallar:
- runtime instance izole port bağlamında çalışmalıdır
- startup tamamlanmadan preview URL aktif sayılmaz

## Health and Readiness Validation
Zorunlu health sinyalleri:
- process alive
- port listening
- root or entry route responds
- critical asset serving works
- error boundary crash yok

Readiness seviyeleri:
- booting
- partially_ready
- ready
- degraded
- unready

Ready olmak için minimum:
- runtime process aktif olmalı
- belirlenen preview entry yanıt vermeli
- en az bir kritik route render edebilmeli
- panel senkronizasyonu kurulmuş olmalı

## Route Discovery
Route kaynakları:
- entry point map
- artifact manifest route impacts
- frontend architecture route map
- explicit user request
- QA target list

Route kategorileri:
- marketing
- authenticated_app
- admin
- automation
- settings
- system

## Route Validation
Her route için:
- routeRef
- routeCategory
- requiresAuth
- navigationReachable
- directLoadSuccess
- renderStatus
- httpStatus
- errorSummary
- validatedAt

Render status değerleri:
- not_tested
- loaded
- partially_loaded
- render_failed
- redirected
- blocked_by_auth
- missing

## Viewport Profiles
Minimum profiller:
- desktop_default
- tablet_default
- mobile_default

Ek profiller:
- desktop_wide
- mobile_small
- mobile_large
- tablet_landscape

Interaction mode değerleri:
- mouse_keyboard
- touch
- hybrid

## Viewport Rendering
Her render için:
- renderId
- routeRef
- viewportId
- renderStartedAt
- renderCompletedAt
- status
- layoutIntegrity
- interactionIntegrity
- captureRef
- issues

Render status değerleri:
- queued
- rendering
- rendered
- rendered_with_warnings
- failed
- timed_out

Layout integrity değerleri:
- clean
- minor_shift
- major_break
- unusable

Interaction integrity değerleri:
- not_checked
- basic_ok
- degraded
- broken

## Snapshot Capture
Snapshot türleri:
- baseline_snapshot
- turn_snapshot
- comparison_snapshot
- failure_snapshot
- release_candidate_snapshot

## Panel Synchronization
Panelde görülecek alanlar:
- build durumu
- runtime durumu
- health/readiness durumu
- available route listesi
- selected route
- viewport switch state
- latest snapshots
- critical warnings
- blocking errors
- rerun, rollback, review aksiyonları

Available action değerleri:
- rerun_preview
- rerun_route_subset
- switch_viewport
- open_logs
- compare_snapshot
- request_fix
- rollback
- approve_turn

## Continuous Monitoring
İzlenecek sinyaller:
- process liveness
- route response continuity
- render crash detection
- unexpected restart
- console/runtime error bursts
- asset serving failures

Monitoring outcome değerleri:
- stable
- warning
- degraded
- unstable
- failed

## Teardown or Reuse Decision
Reuse decision değerleri:
- reuse_runtime
- restart_runtime
- destroy_runtime

## Timeout ve Sınırlar
Timeout alanları:
- buildTimeoutMs
- startupTimeoutMs
- routeValidationTimeoutMs
- renderTimeoutMs
- panelSyncTimeoutMs

Timeout sonucu değerleri:
- retry_same_phase
- retry_with_safe_mode
- degrade_preview
- fail_preview

## Hata Sınıflandırması
Build level:
- build_dependency_error
- build_syntax_error
- build_type_error
- build_config_error

Startup level:
- runtime_port_conflict
- runtime_boot_error
- runtime_env_error
- runtime_crash_on_start

Route level:
- route_missing
- route_redirect_loop
- route_auth_blocked
- route_render_exception

Render level:
- layout_break
- asset_load_failure
- hydration_error
- interaction_break

Panel sync level:
- panel_sync_failure
- stale_preview_state
- snapshot_publish_failure

Recovery level:
- auto_recovered
- manual_intervention_required
- rollback_recommended

## Recovery Stratejileri
- retry_phase
- rerun_route_subset
- restart_runtime
- safe_mode_runtime
- last_good_snapshot_fallback
- rollback_candidate_prompt
- manual_fix_required

## Güvenlik ve İzolasyon Kuralları
- production secret’larla çalışmamalı
- destructive external action’lar sandbox veya kapalı modda olmalı
- debug yüzeyi herkese açık olmamalı
- runtime logs hassas veri sızdırmamalı
- auth simülasyonları gerçek kullanıcı verisiyle karışmamalı

İzolasyon seviyeleri:
- light_isolation
- module_isolation
- full_session_isolation

## Preview Readiness Kuralları
Ready olmak için minimum:
- build başarılı olmalı
- runtime process çalışıyor olmalı
- en az bir entry route uyumlu render vermeli
- panel sync kurulmuş olmalı
- en az bir viewport render kaydı oluşmuş olmalı

Partially ready olabilir eğer:
- bazı route’lar hazır ama tüm kritik route’lar değil
- yalnızca desktop render başarılı
- auth simülasyonu eksik

Failed olur eğer:
- build başarısızsa
- runtime hiç ayağa kalkmazsa
- root entry route render vermezse
- panel senkronizasyonu kurulamayıp kullanıcı görünümü oluşmazsa

## Minimum Çekirdek Gereksinimler
- build çalıştırma
- runtime başlatma
- tek entry route doğrulama
- desktop, tablet, mobile viewport render
- en az bir snapshot üretimi
- panel status senkronizasyonu
- logs referansı
- rerun action
- request fix action

## Sonuç
Bu belge, canlı preview ve yerel çalışma panelinin resmi çalışma omurgasını tanımlar.
