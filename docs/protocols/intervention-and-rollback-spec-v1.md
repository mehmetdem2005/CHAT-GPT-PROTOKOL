# Intervention & Rollback Spec v1

Bu belge, insan müdahalesi, karar kilitleme, override, durdurma, yeniden yönlendirme ve rollback süreçlerinin resmi spesifikasyonudur.

## Amaç
- kullanıcı ve operatörün sistem kararlarına kontrollü biçimde müdahale etmesini sağlamak
- kritik değişikliklerde sessiz ilerlemeyi engellemek
- güvenli geri dönüş noktaları tanımlamak
- ajan üretimini denetlenebilir ve geri alınabilir hale getirmek
- approval, audit, risk ve preview sistemleriyle uyumlu müdahale katmanı oluşturmak

## Tasarım İlkeleri
- human authority on critical boundaries
- explicit intervention only
- minimal-scope correction
- rollback is a governed action
- locked choices are protected
- intervention is traceable
- recovery before destruction

## Kapsam
Bu spesifikasyon şunları kapsar:
- user lock
- operator lock
- override
- halt and pause
- reroute
- require review
- regeneration request
- reject output
- rollback planning
- rollback execution
- rollback validation
- intervention audit linking
- approval coupling
- risk escalation

## Temel Kavramlar
- Intervention
- Lock
- Override
- Halt
- Reroute
- Regeneration
- Rollback
- Safe Point
- Approval Boundary

## Intervention Sınıfları
### Choice-level
- lock choice
- unlock choice
- reject option
- force selection review

### Task-level
- pause task
- cancel task
- reroute task
- change priority
- require human review

### Agent-level
- suspend agent
- limit agent scope
- force critic review
- replace producer agent path

### Artifact-level
- reject patch
- freeze artifact
- restrict mutation scope
- request targeted fix

### Turn-level
- halt turn
- reopen turn
- mark awaiting approval
- mark awaiting fix

### Runtime-level
- rerun preview
- rerun affected routes only
- safe-mode runtime
- restart runtime

### Recovery interventions
- suggest rollback
- execute rollback
- partial rollback
- full turn rollback
- release candidate rollback

## Müdahale Yetki Modeli
### User
Kullanıcı şunları yapabilir:
- option seçme
- option reddetme
- lock choice
- regenerate request
- preview fix request
- route bazlı inceleme isteme
- onaya konu görsel ve yapısal tercihi değiştirme

### Operator
Operatör şunları yapabilir:
- override decision
- halt generation
- reroute task
- force review
- unlock certain non-user-critical locks
- execute approved rollback
- require approval

### System Governance
Yönetişim katmanı şunları tetikleyebilir:
- hard block
- soft block
- require approval
- suggest rollback
- freeze release decision
- mark risk escalation

## Müdahale Yetki Matrisi
User-allowed:
- lock_choice
- request_regeneration
- reject_output
- request_fix
- approve
- decline

Operator-allowed:
- unlock_choice
- override_decision
- reroute_task
- halt_generation
- force_review
- execute_partial_rollback
- execute_turn_rollback

Governance-only:
- policy_block
- release_freeze
- critical_risk_hold
- mandatory_security_review
- mandatory_approval

Approval-bound actions:
- major structural override
- unlock user-locked architecture choice
- auth/data schema rollback
- release candidate rollback
- cross-module forced mutation

## Lock Modeli
Lock türleri:
- user_lock
- operator_lock
- policy_lock
- approval_lock
- release_lock

Lock subject türleri:
- option
- decision
- artifact
- module
- route
- workflow
- token_pack
- navigation_model
- architecture_variant

Lock nesnesi alanları:
- lockId
- lockType
- subjectType
- subjectRef
- scope
- lockedBy
- lockedAt
- reason
- unlockConditions
- approvalRequiredToUnlock
- auditRef

Scope değerleri:
- single_subject
- module_scope
- turn_scope
- workspace_scope

Kurallar:
- user_lock kullanıcı onayı veya yetkili approval olmadan aşılamaz
- policy_lock uygun review veya fix olmadan kaldırılamaz
- release_lock release decision veya rollback akışıyla ilişkilendirilmelidir

## Intervention Nesnesi
Her intervention kaydı için:
- interventionId
- actionType
- initiatedBy
- targetRef
- targetType
- reason
- authorityLevel
- linkedTurnId
- linkedTaskRefs
- linkedAuditRef
- linkedApprovalRef
- executionStatus
- resultSummary

Execution status değerleri:
- pending
- accepted
- running
- completed
- failed
- cancelled

## Override Kuralları
Override yapılabilmesi için:
- açık gerekçe yazılmalı
- yetkili aktör bulunmalı
- etkilenen subject ve scope net olmalı
- audit bağı kurulmalı
- gerekiyorsa approval ref bağlanmalı

Sessiz override yasaktır.

## Halt ve Pause Kuralları
Halt veya pause şu durumlarda kullanılabilir:
- riskli üretim akışı
- preview crash loop
- policy block sonrası bekleme
- kullanıcı açıkça üretimi durdurmak istiyor

Halt sonrası sistem şunlardan birine yönlenmelidir:
- reroute
- require review
- targeted regeneration
- rollback consideration

## Reroute Kuralları
Reroute şu amaçlarla kullanılabilir:
- aynı görevi başka ajana devretmek
- aynı ajanı farklı strategy ile tekrar çalıştırmak
- modül kapsamını daraltmak
- critic loop zorlamak

Reroute kaydı şunları içermelidir:
- fromTaskRef
- toTaskRef veya replacementPath
- reason
- scopeImpact
- approvalRequired

## Regeneration Kuralları
Regeneration rollback ile aynı şey değildir.
Regeneration:
- seçili kapsamı yeniden üretir
- mevcut güvenli state’i tamamen geri almaz
- lock ve approval sınırlarına uymak zorundadır

Regeneration türleri:
- option regeneration
- route regeneration
- component regeneration
- module regeneration
- preview-only regeneration

## Rollback Planlama
Rollback düşünülmesi gereken durumlar:
- repeated regression
- build/runtime preview zinciri stabil değil
- yanlış yapısal karar onaylandı
- kritik policy veya QA ihlali hızlı düzeltilemiyor
- son güvenli snapshot daha güvenilir

Rollback planı alanları:
- rollbackId
- targetSnapshotId
- rollbackScope
- reason
- createdBy
- createdAt
- affectedArtifacts
- affectedRoutes
- approvalRequired
- approvedBy
- validationPlanRef

Rollback scope değerleri:
- single_artifact
- module_scope
- turn_scope
- release_candidate_scope
- workspace_scope

## Safe Point Kuralları
Safe point şu özellikleri taşımalıdır:
- snapshot doğrulanmış olmalı
- gerekli artifact refs mevcut olmalı
- manifest bağı kurulmuş olmalı
- QA veya en az temel preview doğrulaması yapılmış olmalı
- audit ve trace bağı mevcut olmalı

## Rollback Execution
Rollback çalıştırılırken minimum:
- hedef snapshot çözülür
- etki kapsamı netleştirilir
- approval gereksinimi doğrulanır
- artifact/manifest eşleme güncellenir
- preview rerun veya validation planı tetiklenir
- audit event yazılır

Rollback execution status değerleri:
- planned
- awaiting_approval
- executing
- validated
- failed
- abandoned

## Rollback Validation
Rollback sonrası doğrulama:
- artifact integrity
- manifest consistency
- route availability
- preview readiness
- QA smoke checks
- release gate re-evaluation

Validation başarısızsa sistem:
- rollback_failed state üretir
- operator review ister
- daha dar veya farklı rollback hedefi önerebilir

## Approval Coupling
Şu müdahaleler approval-bound kabul edilir:
- major structural override
- unlock user-locked architecture choice
- auth or schema rollback
- release candidate rollback
- cross-module forced mutation

## Audit ve Trace Kuralları
Her kritik intervention veya rollback için minimum:
- audit record
- trace id
- turn ref
- actor ref
- affected subject refs
- result summary

## Turn State Entegrasyonu
Bu protokol şu alanlarla ilişkilidir:
- lockedChoices
- interventionEvents
- rollbackOptions
- approvalRequests
- completionState
- releaseGateState

## Manifest Entegrasyonu
Rollback veya artifact-level intervention durumunda şu alanlar güncellenmelidir:
- patchRefs
- traceLinks
- snapshot refs
- rollback targets
- status

## Minimum Çekirdek Gereksinimler
İlk sürüm için minimum:
- user lock
- request regeneration
- request fix
- operator reroute
- force review
- rollback suggestion
- approved rollback execution
- audit-linked intervention records

## Sonuç
Bu belge, sistemin human-in-the-loop kontrol ve geri dönüş omurgasını resmi hale getirir.
