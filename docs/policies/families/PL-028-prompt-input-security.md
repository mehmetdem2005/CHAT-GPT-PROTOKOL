# PL-028 — Prompt & Input Security Policies

## Objective
Zararlı girdi, prompt injection, system prompt sızıntısı ve input size risklerini azaltmak.

## Primary Subjects
- user inputs
- fetched external text
- model invocation setup

## Mandatory Checks
1. Harmful input filtering uygulanmalı.
2. Prompt secrecy ve escaping kuralları korunmalı.
3. Büyük veya dengesiz input’lar kontrollü ele alınmalı.

## Enforcement
- allow
- turn_block
- hard_block

## Exception Path
Güvenlik sahibi onayı olmadan exception verilmez.

## Evidence
- input gateway logs
- safety filters
- moderation refs
- policy decisions

## Review Cadence
Her input surface ve model invocation değişikliğinde.
