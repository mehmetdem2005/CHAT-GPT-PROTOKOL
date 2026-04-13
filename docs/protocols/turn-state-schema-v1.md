# Turn State Schema v1

Bu belge, çok turlu çalışan sistemin resmi turn state modelini tanımlar.

## Amaç
Her tur için şunları güvenli biçimde saklamak:
- neden açıldı
- kullanıcıdan ne istendi
- kullanıcı ne seçti
- hangi ajanlar ne yaptı
- hangi kararlar kilitlendi
- hangi artifact ve preview çıktıları üretildi
- hangi risk, policy, approval ve rollback sinyalleri oluştu

## Üst Düzey Bölümler
1. Turn Identity
2. Turn Context
3. User Interaction State
4. Decision State
5. Agent Execution State
6. Artifact and Preview State
7. QA and Governance State
8. Approval and Intervention State
9. Completion State
10. Snapshots and History

## Turn Identity
Zorunlu alanlar:
- turnId
- turnNumber
- sessionId
- workspaceId
- createdAt
- openedBy
- triggerType

Trigger type değerleri:
- initial_request
- followup_question
- user_selection
- regenerate_request
- preview_fix_request
- policy_block_resolution
- approval_request
- rollback_request
- phase_transition

## Turn Context
Zorunlu alanlar:
- stage
- substage
- goalRef
- scopeRef
- activeMode
- traceId

Stage değerleri:
- discovery
- requirements
- ux_architecture
- visual_direction
- generation
- preview_validation
- qa_review
- approval
- release_decision
- maintenance

Active mode değerleri:
- ask_mode
- option_mode
- visual_comparison_mode
- generation_mode
- preview_mode
- review_mode
- approval_mode
- intervention_mode

## User Interaction State
Zorunlu alanlar:
- promptedQuestions
- presentedOptions
- userResponses
- selectionEvents
- lockedChoices
- pendingClarifications

Question type değerleri:
- free_text
- single_select
- multi_select
- ranked_choice
- visual_choice
- style_slider
- layout_picker
- confirm_or_reject
- upload_request

Option type değerleri:
- navigation_pattern
- home_layout
- admin_structure
- automation_model
- font_pairing
- color_direction
- animation_style
- component_variant
- workflow_variant
- architecture_variant

Selection mode değerleri:
- temporary_select
- final_select
- locked_select
- compare_select

## Decision State
Zorunlu alanlar:
- decisionsMade
- decisionSnapshotRef
- activePreferences
- rejectedAlternatives
- decisionConflicts

Decision category değerleri:
- product_scope
- layout
- navigation
- content_structure
- design_direction
- font_selection
- color_selection
- animation_selection
- data_model
- workflow_logic
- security_boundary
- release_gate

Conflict type değerleri:
- agent_agent
- user_agent
- policy_agent
- approval_agent

## Agent Execution State
Zorunlu alanlar:
- invokedAgents
- taskRefs
- executionOrder
- agentOutputs
- executionFailures

Agent status değerleri:
- scheduled
- accepted
- running
- completed
- failed
- blocked
- skipped

## Artifact and Preview State
Zorunlu alanlar:
- artifactChanges
- manifestRef
- buildState
- previewState
- routeState
- viewportSnapshots

Build status değerleri:
- not_started
- building
- build_failed
- build_succeeded
- runtime_starting
- runtime_failed
- runtime_ready

Preview status değerleri:
- unavailable
- starting
- partially_ready
- ready
- degraded
- failed

Viewport değerleri:
- desktop
- tablet
- mobile

## QA and Governance State
Zorunlu alanlar:
- policyEvaluations
- qaReports
- riskState
- releaseGateState

QA report type değerleri:
- code_review
- static_analysis
- responsive_qa
- accessibility_qa
- performance_qa
- security_qa
- regression_qa
- contract_test

Risk band değerleri:
- low
- moderate
- high
- critical

Release gate status değerleri:
- not_evaluated
- allowed
- deferred
- blocked

## Approval and Intervention State
Zorunlu alanlar:
- approvalRequests
- interventionEvents
- rollbackOptions
- operatorNotes

Intervention action değerleri:
- lock_choice
- unlock_choice
- override_decision
- reroute_task
- halt_generation
- force_review
- request_regeneration
- reject_output

## Completion State
Zorunlu alanlar:
- turnStatus
- completionReason
- userVisibleSummary
- nextSuggestedTurnType
- closedAt

Turn status değerleri:
- open
- awaiting_user_input
- awaiting_approval
- awaiting_fix
- completed
- failed
- rolled_back
- abandoned

Completion reason değerleri:
- questions_answered
- selection_locked
- preview_generated
- qa_blocked
- approval_needed
- policy_blocked
- rollback_applied
- user_stopped

Next suggested turn type değerleri:
- ask_more_requirements
- choose_visual_direction
- choose_layout
- generate_preview
- review_preview
- fix_issues
- approve_changes
- release_candidate

## Snapshots and History
Zorunlu alanlar:
- stateSnapshotId
- parentSnapshotId
- snapshotType
- snapshotRef
- historyRefs

Snapshot type değerleri:
- turn_opened
- after_user_input
- after_agent_generation
- after_preview
- after_qa
- after_intervention
- turn_closed

## Bütünlük Kuralları
- lock bütünlüğü korunur
- preview ready ise route ve viewport snapshot bulunmalıdır
- release allowed ise zorunlu QA raporları mevcut olmalıdır
- kritik intervention ve approval olayları audit ile ilişkilendirilebilir olmalıdır
- her completed task en az bir output veya explicit no-output reason taşımalıdır

## Minimum Çekirdek Alan Seti
- turnId
- turnNumber
- sessionId
- createdAt
- triggerType
- context.stage
- context.activeMode
- userInteraction.promptedQuestions
- userInteraction.presentedOptions
- userInteraction.userResponses
- userInteraction.lockedChoices
- decisionState.decisionsMade
- agentExecution.invokedAgents
- artifactPreviewState.buildState
- artifactPreviewState.previewState
- qaGovernanceState.policyEvaluations
- qaGovernanceState.releaseGateState
- approvalInterventionState.interventionEvents
- completionState.turnStatus
- completionState.userVisibleSummary
- history.stateSnapshotId

## Sonuç
Bu belge, sistemin çok turlu konuşma, üretim ve governance hafızasının resmi state omurgasıdır.
