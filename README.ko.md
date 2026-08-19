# AI Engineering Harness

**언어:** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · **한국어** · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

AI 지원 소프트웨어 개발을 위한 최소 구성의 벤더 중립 기반입니다.

AI 코딩 도구나 모델을 바꾸면 프로젝트의 엔지니어링 맥락이 사라져 같은 설명을 반복해야 하는 경우가 많습니다. AI Engineering Harness는 이를 방지하기 위한 작고 이식 가능한 정책/컨텍스트 계층입니다. Agent Runtime이나 오케스트레이터가 아니며, Cursor, Claude Code, Codex, Antigravity는 각자 실행 및 오케스트레이션 기능을 제공합니다.

## 해결하는 문제

1. 도구나 모델을 바꿔도 프로젝트 컨텍스트와 엔지니어링 규율을 유지합니다.
2. 복잡성이나 위험이 정당화할 때만 더 강한 reasoning을 사용해 품질과 비용을 균형 있게 관리합니다.
3. 수명이 짧은 모델 이름을 안정적인 정책에 고정하지 않고 모델/runtime 선택을 최신 상태로 유지합니다.

## 파일

- `AGENTS.md` — 호환되는 coding agent를 위한 공통 엔지니어링 기준.
- `MODEL_ROUTING.md` — 안정적인 FAST / STANDARD / REASONING / FRONTIER 정책.
- `MODEL_CATALOG.md` — 시간에 따라 바뀌는 모델/runtime 카탈로그와 현재 권장사항.
- `CLAUDE.md` — Claude Code가 `AGENTS.md`를 가져오기 위한 최소 어댑터.
- `README.md` — adoption, 업데이트, 테스트, 유지보수의 기본 가이드.

## 무엇이며, 무엇이 아닌가

핵심 가치는 파일 배치가 아니라 정책 내용입니다. repository-first 컨텍스트, routing tier, runtime capability의 fail-closed 검증, 영향 기반의 사람 승인, scope 규율, 지속 가능한 handoff, 안전한 adoption/update를 제공합니다.

workflow engine, multi-agent framework, runtime, rule-sync generator가 아니며 각 도구의 native rules/skills를 대체하지 않습니다.

## 호환성

`AGENTS.md`는 이 repository가 만든 독자 포맷이 아니라 외부의 cross-tool convention입니다. 직접 읽을 수 있는 runtime은 Harness 전용 어댑터가 필요 없습니다. Claude Code는 `CLAUDE.md`를 사용하므로 최소한의 `@AGENTS.md` 브리지만 포함합니다. Antigravity 전용 `.agents/skills/`, `.agents/workflows/` 같은 메커니즘은 project-local로 유지됩니다.

## 기존 프로젝트에 적용

1. 현재 repository와 branch에서 작업합니다.
2. 수정 전에 적절한 agent가 rules, docs, Git 상태, deployment topology, validation 명령을 조사하게 합니다.
3. 기존 파일을 수정하기 전에 repository 밖에 byte-for-byte backup을 만듭니다.
4. project-specific 내용을 모두 보존하고 Harness의 shared content만 추가합니다.
5. Harness 적용만을 위해 branch, worktree, installer, manifest, adapter, sync 메커니즘을 만들지 않습니다.
6. 명시적 승인 없이 commit, push, deploy, publish하지 않습니다.

**전체 adoption prompt:** [영문 README](README.md#copypaste-adoption-prompt)

## 업데이트

업데이트는 Harness-owned shared content만 갱신합니다. `AGENTS.md`, `MODEL_ROUTING.md`, `MODEL_CATALOG.md`, `CLAUDE.md`의 shared 부분을 upstream에서 갱신하면서 project-local rules, models, skills, docs, code, 미커밋 작업을 보존합니다.

**전체 update prompt:** [영문 README](README.md#copypaste-update-prompt)

## 핵심 원칙

- Repository의 진실은 모델이나 agent가 바뀌어도 유지되어야 합니다.
- 교체하지 말고 추가합니다. tool-native rules는 기존 위치에 둡니다.
- `MODEL_ROUTING.md`는 안정적이고 `MODEL_CATALOG.md`는 의도적으로 시간 민감합니다.
- 실제로 호출 가능한 모델/agent에 대해서는 active runtime이 최종 권위입니다.
- 문제를 발견했다고 해서 요청 scope 밖의 수정 권한이 생기지는 않습니다.
- High-impact 작업은 도구나 환경 이름이 아니라 실제 영향에 따라 사람 승인을 요구합니다.
- tests, linters, types, CI 같은 deterministic safeguard가 같은 규칙을 안정적으로 enforce할 수 있다면 반복적인 model judgment보다 우선합니다.

## 설치 테스트

새 session에서 structural smoke test, real-task behavior test, approval-boundary test, cross-tool runtime-capability test를 수행합니다. Agent는 컨텍스트를 정확히 발견하고 active runtime이 검증할 수 없는 capability를 주장해서는 안 됩니다.

정확한 prompts: [How to test an installation](README.md#how-to-test-an-installation)

## 라이선스

**Apache License 2.0**으로 오픈소스 공개됩니다.