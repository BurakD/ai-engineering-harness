<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**언어:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · **한국어** · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

AI 지원 소프트웨어 개발을 위한 최소·벤더 중립 기준입니다. 휴대 가능한 policy/context 레이어와 작고 재사용 가능한 engineering procedures 집합으로 구성됩니다. Agent runtime, orchestrator, installer, framework가 아닙니다.

## 파일

- `AGENTS.md` — 공유 always-on engineering baseline.
- `MODEL_ROUTING.md` — 안정적인 품질/비용 및 capability-tier policy.
- `MODEL_CATALOG.md` — 시간에 따라 갱신되는 runtime/model catalog.
- `CLAUDE.md` — Claude Code에서 `AGENTS.md`를 가리키는 얇은 bridge.
- `skills/` — Harness-owned canonical on-demand procedures.
- `i18n/` — README 현지화 요약.

## Rules와 skills: 네 개 레이어

| | Always-on | On-demand |
| --- | --- | --- |
| **Shared** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Project-specific** | 프로젝트 자체 rule/policy mechanism | 프로젝트 자체 skills |

Harness는 별도의 `rules/` 디렉터리를 제공하지 않습니다. 공유 always-on 규칙의 canonical source는 이미 `AGENTS.md`이며 model routing policy는 `MODEL_ROUTING.md`에 있습니다. 두 번째 canonical always-on source는 중복과 충돌 위험만 만듭니다.

Domain rules, environment/deployment topology, vendor/model preferences, product behavior, business rules, infrastructure paths는 project-local로 유지합니다. 새로운 guidance가 어느 레이어에 속해야 하는지는 `continuous-improvement` skill의 “가장 작은 durable safeguard 선택” 접근을 사용해 결정합니다.

## Shared skills

Skills는 task-specific procedures이며 always-on policy가 아닙니다. 일반적으로 discovery에서는 metadata만 노출되고, 전체 `SKILL.md` body는 현재 작업과 실제로 일치할 때만 로드되어야 합니다.

Harness-owned skills의 canonical source는 `skills/`입니다. Ownership marker:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

같은 이름의 skill에 이 key가 없다면 Harness-owned가 아니며 adoption/update에서 절대 덮어쓰면 안 됩니다.

v2에는 14개 skills가 있습니다:

- `backup-and-recovery-review` — backup/restore/recovery readiness.
- `interface-qa` — web, mobile, desktop, CLI, API interface validation.
- `calculation-model-validation` — formula 및 decision-model validation.
- `change-review` — 완료된 변경의 regression/risk review.
- `compatibility-and-rollout` — compatibility, migration, rollout, rollback.
- `high-risk-change-review` — 고위험 변경에 대한 추가 discipline.
- `delegation-strategy` — 검증된 delegation/parallelism의 안전한 사용.
- `dependency-change` — dependency 추가·삭제·upgrade 평가.
- `documentation-sync` — durable documentation을 실제 상태와 동기화.
- `environment-release-safety` — release/deployment 및 approval boundary 안전성.
- `continuous-improvement` — 반복 failure를 durable safeguard로 전환.
- `root-cause-debug` — root cause 식별 및 입증.
- `secret-exposure-response` — secret/credential exposure 대응.
- `cross-surface-consistency` — 여러 surface/channel 간 동작 일관성.

공유 집합은 대략 **20 skills 이하**로 유지하며 각 `description`은 **300자 이하**로 유지합니다.

우선순위: **project-local rules/policy > shared `AGENTS.md` baseline > shared skills**. Skill은 approval boundary, authorized scope, runtime capability, production/live safety를 약화할 수 없습니다.

## Adoption과 update

운영용 copy/paste prompt는 하나의 canonical source에만 두고 번역하지 않습니다:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

Adoption은 repository evidence를 통해 실제 사용 runtime을 판단합니다. 머신에 CLI가 설치되어 있다는 사실만으로는 충분하지 않습니다. 검증된 project-level skill paths: Cursor/Antigravity/Codex는 `.agents/skills/`, Claude Code는 `.claude/skills/`. Cursor는 `.claude/skills/`도 읽을 수 있습니다. 하나의 검증된 root가 모든 runtime을 커버하면 한 복사본만 사용합니다. Native activation을 검증할 수 없으면 neutral `harness/skills/`를 사용하고 native active라고 주장하지 않습니다.

어떤 skill도 쓰기 전에 모든 canonical skill names를 모든 target roots에서 collision scan합니다. 변경되는 managed file은 repository 밖에 byte-for-byte backup을 만듭니다. Update는 기존 skill placement를 이동하지 않으며, upstream에서 제거된 managed skill도 자동 삭제하지 않고 orphaned로 보고합니다.

## 제거와 테스트

자동 uninstaller는 없습니다. `metadata.ai-engineering-harness`를 가진 skills만 Harness-owned 제거 대상으로 취급하며 project-local rules/skills는 건드리지 않습니다. [Remove the shared skills](../README.md#remove-the-shared-skills) 참고.

Native skill activation을 검증할 수 없다면 agent는 skill이 active라고 주장해서는 안 됩니다. 관련 없는 작업에서는 모든 skill body가 context에 들어가면 안 되며 discovery metadata만 보이는 것이 정상입니다. [How to test an installation](../README.md#how-to-test-an-installation) 참고.

`SKILL.md` 파일은 번역하지 않고 하나의 canonical English copy만 유지합니다. 자세한 maintenance, adoption/update, scope boundaries는 [English README](../README.md)를 기준으로 합니다.
