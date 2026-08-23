<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**언어:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · **한국어** · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

AI 지원 소프트웨어 개발을 위한 최소 구성의 vendor-neutral(벤더 중립) 기반입니다. 이동 가능한 정책/컨텍스트 레이어와 작고 재사용 가능한 절차 집합으로 구성됩니다. agent runtime(에이전트 실행 환경), orchestrator(오케스트레이터), installer(설치 도구), framework(소프트웨어 프레임워크)가 아닙니다.

## 파일

- `AGENTS.md` — 공유 always-on(항상 활성) 엔지니어링 기준.
- `MODEL_ROUTING.md` — 안정적인 품질/비용 및 capability tier(역량 수준) 정책.
- `MODEL_CATALOG.md` — 시간에 따라 갱신되는 runtime(실행 환경)/모델 카탈로그.
- `CLAUDE.md` — Claude Code에서 `AGENTS.md`를 가리키는 가벼운 연결부.
- `skills/` — Harness-owned(Harness 소유), canonical(유일한 기준 원본에서 온), on-demand(필요할 때 로드되는) 절차.
- `i18n/` — README 현지화 요약.

## 규칙과 스킬: 네 개 레이어

여기서 rules(규칙)는 항상 적용되는 지침을, skills(스킬)는 특정 작업에 사용하는 절차를 뜻합니다.

| | 항상 활성 | 필요 시 |
| --- | --- | --- |
| **공유** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **프로젝트 전용** | 프로젝트 자체 규칙/정책 메커니즘 | 프로젝트 자체 스킬 |

AI Engineering Harness는 별도의 `rules/` 디렉터리를 제공하지 않습니다. 공유 always-on(항상 활성) 규칙 레이어의 canonical source(유일한 기준 원본)는 이미 `AGENTS.md`에 있고, model routing(모델 라우팅) 정책은 `MODEL_ROUTING.md`에 있습니다. 항상 활성인 두 번째 원본을 만들면 중복과 충돌 위험이 생깁니다.

Domain rules(도메인 규칙), environment/deployment topology(환경/배포 토폴로지), vendor/model preferences(벤더/모델 선호), product behavior(제품 동작), business rules(비즈니스 규칙), infrastructure paths(인프라 경로)는 프로젝트 전용으로 유지합니다. 새로운 지침을 어느 레이어에 둘지는 `continuous-improvement` 스킬의 safeguard(지속 가능한 보호 장치) 선택 방식을 사용해 결정합니다.

## 공유 스킬

Skills(스킬)는 task-specific procedures(작업별 절차)이며 always-on policy(항상 활성 정책)가 아닙니다. progressive disclosure(점진적 표시)에서는 일반적으로 discovery metadata(탐색 메타데이터)만 노출되고, 전체 `SKILL.md` 본문은 현재 작업과 실제로 일치할 때만 로드됩니다.

Harness-owned skills(Harness 소유 스킬)의 canonical source(유일한 기준 원본)는 `skills/`입니다. ownership marker(소유권 표시)는 다음과 같습니다.

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

같은 이름의 skill(스킬)에 이 키가 없다면 Harness-owned(Harness 소유)가 아니며 adoption(도입)이나 update(업데이트)에서 덮어쓰면 안 됩니다.

v2에는 14개 스킬이 있습니다.

- `backup-and-recovery-review` — backup(백업), restore(복원), recovery(복구) 준비.
- `interface-qa` — web, mobile, desktop, CLI, API 인터페이스 검증.
- `calculation-model-validation` — 수식과 의사결정 모델 검증.
- `change-review` — 완료된 변경의 review(리뷰), 회귀, 위험 검토.
- `compatibility-and-rollout` — compatibility(호환성), migration(마이그레이션), rollout(단계적 배포), rollback(되돌리기).
- `high-risk-change-review` — 영향이 큰 변경에 대한 추가 규율.
- `delegation-strategy` — 검증된 delegation(위임)과 parallelism(병렬 처리)의 안전한 사용.
- `dependency-change` — dependency(의존성) 추가·삭제·upgrade(버전 상향) 평가.
- `documentation-sync` — 장기 문서를 실제 상태와 동기화.
- `environment-release-safety` — release(릴리스)/deployment(배포) 영향과 approval(승인) 안전성.
- `continuous-improvement` — 반복 실패를 지속 가능한 safeguards(보호 장치)로 전환.
- `root-cause-debug` — root cause(근본 원인)를 식별하고 입증.
- `secret-exposure-response` — secret(비밀값)과 credential(인증 정보)의 exposure(노출) 대응.
- `cross-surface-consistency` — 여러 surface(사용자 접점) 사이의 동작 일관성.

공유 집합은 대략 **20개 스킬 이하**로 유지하며 각 `description`은 **300자 이하**로 유지합니다.

우선순위: **project-local rules/policy(프로젝트 전용 규칙/정책) > 공유 `AGENTS.md` 기준 > shared skills(공유 스킬)**. 스킬은 approval boundary(승인 경계), authorized scope(허용 범위), runtime capability(실행 환경 역량), production/live safety(운영/라이브 안전성)를 약화할 수 없습니다.

## 도입과 업데이트

운영용 copy/paste prompts(복사/붙여넣기 프롬프트)는 하나의 canonical source(기준 원본)에만 두고 본문은 번역하지 않습니다.

- [도입 프롬프트(영어)](../README.md#copypaste-adoption-prompt)
- [업데이트 프롬프트(영어)](../README.md#copypaste-update-prompt)

Adoption(도입)은 repository evidence(저장소의 근거)를 통해 실제 사용 runtimes(실행 환경)를 판단합니다. 머신에 CLI가 설치되어 있다는 사실만으로는 충분하지 않습니다. 검증된 project-level skill paths(프로젝트 수준 스킬 경로)는 Cursor/Antigravity/Codex의 `.agents/skills/`, Claude Code의 `.claude/skills/`입니다. Cursor는 `.claude/skills/`도 읽을 수 있습니다. 하나의 검증된 root(루트 디렉터리)가 모든 실행 환경을 포함하면 한 복사본만 사용합니다. native activation(네이티브 활성화)을 검증할 수 없으면 `harness/skills/`를 neutral fallback(중립 대안)으로 사용하고 네이티브 활성화가 되었다고 주장하지 않습니다.

어떤 스킬도 쓰기 전에 모든 canonical names(기준 원본의 이름)를 모든 target roots(대상 루트 디렉터리)에서 collision(이름 충돌) 여부로 검사합니다. 변경되는 managed files(관리 대상 파일)는 repository(저장소) 밖에 byte-for-byte(바이트 단위 완전 일치) 백업을 만듭니다. Harness-owned(Harness 소유) 복사본은 canonical source(기준 원본)와 verbatim(완전 동일) 상태를 유지합니다. update(업데이트)는 기존 배치를 이동하지 않습니다. upstream(상위 원본)에서 제거된 managed skill(관리 대상 스킬)도 자동 삭제하지 않고 orphaned(상위 원본에 없는 상태)로 보고합니다.

## 제거와 테스트

자동 uninstaller(제거 도구)는 없습니다. ownership marker(소유권 표시) `metadata.ai-engineering-harness`가 있는 managed skills(관리 대상 스킬)만 제거하고, project-local skills/rules(프로젝트 전용 스킬/규칙)는 건드리지 않습니다. [공유 스킬 제거(영어)](../README.md#remove-the-shared-skills)를 참고하세요.

native skill activation(스킬의 네이티브 활성화)을 검증할 수 없다면 agent(에이전트)는 해당 스킬이 active(활성)라고 주장해서는 안 됩니다. 관련 없는 작업에서는 모든 skill bodies(스킬 본문)를 context(컨텍스트)에 로드하지 않고 discovery metadata(탐색 메타데이터)만 보이게 해야 합니다. [도입 테스트(영어)](../README.md#how-to-test-an-installation)를 참고하세요.

`SKILL.md` 파일은 번역하지 않고 canonical English copy(유일한 기준 영어 복사본) 하나만 유지합니다. 자세한 maintenance(유지보수), adoption/update behavior(도입/업데이트 동작), scope boundaries(범위 경계)는 [영어 README](../README.md)를 기준으로 합니다.
