<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Языки:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · **Русский** · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Минимальная, независимая от конкретного вендора основа для разработки ПО с ИИ: переносимый слой политик/контекста плюс небольшой набор переиспользуемых инженерных процедур. Это не runtime агентов, не оркестратор, не установщик и не framework.

## Файлы

- `AGENTS.md` — общая always-on инженерная база.
- `MODEL_ROUTING.md` — стабильная политика качества/стоимости и capability tiers.
- `MODEL_CATALOG.md` — изменяемый во времени каталог runtime/моделей.
- `CLAUDE.md` — минимальный мост Claude Code к `AGENTS.md`.
- `skills/` — канонические Harness-owned процедуры по требованию.
- `i18n/` — локализованные сводки README.

## Rules и skills: четыре слоя

| | Always-on | On-demand |
| --- | --- | --- |
| **Общий** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Проектный** | Собственный механизм rules/policy проекта | Собственные skills проекта |

Harness намеренно не поставляет отдельный каталог `rules/`: канонический общий always-on слой уже находится в `AGENTS.md`, а модельная routing-политика — в `MODEL_ROUTING.md`. Второй канонический источник правил создавал бы дублирование и риск противоречий.

Доменные правила, топология environments/deployments, предпочтения вендоров и моделей, поведение продукта, бизнес-правила и инфраструктурные пути остаются локальными для проекта. При выборе слоя для новой guidance используйте skill `continuous-improvement` и его принцип выбора минимального долговечного safeguard.

## Общие skills

Skills — это процедуры для конкретных задач, а не always-on policy. Обычно в discovery должна быть видна только metadata; полный текст `SKILL.md` загружается, когда текущая задача действительно соответствует skill.

Канонический источник Harness-owned skills — каталог `skills/`. Маркер ownership:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Skill с тем же именем без этого ключа не принадлежит Harness и никогда не должен перезаписываться при adoption или update.

Набор v2 содержит 14 skills:

- `backup-and-recovery-review` — готовность backup, restore и recovery.
- `interface-qa` — проверка web, mobile, desktop, CLI и API интерфейсов.
- `calculation-model-validation` — проверка формул и моделей принятия решений.
- `change-review` — review завершённых изменений, регрессий и рисков.
- `compatibility-and-rollout` — совместимость, миграции, rollout и rollback.
- `high-risk-change-review` — усиленная дисциплина для высокорисковых изменений.
- `delegation-strategy` — безопасное использование подтверждённой delegation/parallelism.
- `dependency-change` — оценка добавления, удаления и обновления зависимостей.
- `documentation-sync` — синхронизация долговечной документации с реальностью.
- `environment-release-safety` — безопасность release/deployment и approval boundaries.
- `continuous-improvement` — превращение повторяющихся ошибок в долговечные safeguards.
- `root-cause-debug` — поиск и доказательство корневой причины.
- `secret-exposure-response` — реагирование на утечку secrets/credentials.
- `cross-surface-consistency` — согласованность поведения между несколькими поверхностями.

Общий набор должен оставаться примерно **20 skills или меньше**; каждый `description` — **не более 300 символов**.

Приоритет: **project-local rules/policy > общая база `AGENTS.md` > shared skills**. Skill не может ослаблять approval boundaries, разрешённый scope, runtime capabilities или production/live safety.

## Adoption и update

Операционные copy/paste prompts хранятся в одном каноническом источнике и не переводятся:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

Adoption определяет используемые runtime по доказательствам в repository; сам факт установки CLI недостаточен. Проверенные project-level пути: `.agents/skills/` для Cursor, Antigravity и Codex; `.claude/skills/` для Claude Code. Cursor также читает `.claude/skills/`. Если один проверенный root покрывает все обнаруженные runtime, используется одна копия. Если native activation нельзя подтвердить, используется нейтральный `harness/skills/`, и агент не заявляет о native activation.

До любой записи skill все канонические имена проверяются на collisions во всех target roots. Изменяемые managed-файлы получают byte-for-byte backup вне repository. Update не переносит существующее размещение skills; managed skill, удалённый upstream, автоматически не удаляется и отмечается как orphaned.

## Удаление и тестирование

Автоматического uninstaller нет. Удаляться как Harness-owned могут только skills с `metadata.ai-engineering-harness`; project-local rules и skills не трогаются. См. [Remove the shared skills](../README.md#remove-the-shared-skills).

Если native activation нельзя подтвердить, агент не должен утверждать, что skill активен. Для нерелевантной задачи тела всех skills не должны попадать в context; может быть видна только discovery metadata. См. [How to test an installation](../README.md#how-to-test-an-installation).

Файлы `SKILL.md` не переводятся; сохраняется единственная каноническая английская копия. Подробности по maintenance, adoption/update и scope boundaries находятся в [английском README](../README.md).
