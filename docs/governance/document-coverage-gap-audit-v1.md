# Document Coverage Gap Audit v1

Bu belge, mevcut repo belge setinin kapsamını ve halen eksik olan alanları görünür kılmak için hazırlanmıştır.

## Sonuç Özeti
Repo artık güçlü bir çekirdek omurga içeriyor; ancak "her şey dahil" durumda değildir.

Aşağıdaki ana katmanlar kısmen veya tamamen eksik olabilir:
- ayrı prosedür ve runbook dosyaları
- bazı alt şema paketleri
- adı geçen ama resmi registry kaydı eksik protokoller
- operasyonel incident / release / hotfix / waiver prosedürleri
- panel, question-card ve diagnostics gibi türev modeller

## Mevcut Güçlü Kapsam
- master protocol omurgası
- protocol registry v1
- policy registry ve 33 policy family split
- turn state schema
- artifact manifest schema
- preview runtime spec
- intervention and rollback spec
- protocol clarification ve governance belgeleri

## Açık Boşluklar
### 1. Adı geçen ama ayrı authoritative belge bekleyen setler
- system module registry
- global error code registry
- event catalog
- api style guide
- security policy standard
- observability standard
- testing standard
- deployment and environment contract
- core 18 agent execution order
- studio panel state model
- question and option card schema pack
- preview diagnostics taxonomy
- patch mutation rules

### 2. Alt şema paketleri
- question object schema
- option card schema
- decision object schema
- agent execution record schema
- artifact change schema
- preview snapshot schema
- qa report attachment schema
- approval object schema
- intervention event schema
- turn summary schema
- artifact object schema
- dependency edge schema
- entry point object schema
- contract impact object schema
- preview impact schema
- qa coverage object schema
- snapshot object schema
- trace link schema
- module ownership schema

### 3. Operasyonel prosedür boşlukları
- release approval procedure
- rollback execution procedure
- rollback validation procedure
- incident declaration procedure
- postmortem procedure
- hotfix procedure
- change request procedure
- policy exception procedure
- protocol change procedure
- tenant isolation verification procedure

## Kural
Bu belge, mevcut omurgayı küçümsemez; yalnız hâlâ ayrı authoritative doküman gerektiren alanları görünür kılar.
