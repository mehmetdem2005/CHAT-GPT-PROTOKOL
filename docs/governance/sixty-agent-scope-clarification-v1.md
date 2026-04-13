# 60-Agent Scope Clarification v1

## Purpose
Bu belge, repo içindeki protokol ve politika çalışmalarının 60 agent'li sistem hedefiyle hazırlandığını, ancak her agent için detay seviyesinin henüz eşit olmadığını netleştirir.

## Scope Statement
Evet, bu repo çok ajanlı ve yaklaşık 60 agent'li bir ürün stüdyosu hedefini desteklemek üzere tasarlanmaktadır.

## Current Reality
Şu anki belge setinin büyük bölümü:
- agent-agnostic çekirdek protokoller
- governance ve policy omurgası
- preview, rollback, approval ve release mekanizmaları
- shared schema ve registry başlangıçları
şeklindedir.

## What Is Already 60-Agent Oriented
- task contract ve task graph mantığı çok ajanlı orkestrasyonu destekler
- capability declaration ve module boundary yönü bu hedefe uygundur
- intervention, rollback, approval ve audit sistemleri çok ajanlı çatışma ve kontrol ihtiyacını düşünür
- policy family seti geniş agent yüzeyi için hazırlanmıştır

## What Is Not Fully Done Yet
Henüz tam bitmemiş alanlar:
- 60 agent'in tamamı için bireysel capability dosyaları
- agent-by-agent input/output fixture setleri
- conflict matrix
- execution order registry for all agents
- per-agent hard capability limits
- per-agent quality scorecards

## Canonical Interpretation
Bu repo şu anda 60 agent sistemi için:
- omurgayı kuruyor
- sözleşmeleri ve governance'i hazırlıyor
- ama bütün agent katalog derinliğini henüz tamamlamış değil

## Next Recommended Work
1. system module registry sonrası agent registry v2
2. per-agent capability declaration files
3. agent input/output examples
4. agent conflict matrix
5. execution order and dependency registry
