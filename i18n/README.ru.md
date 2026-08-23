<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Языки:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · **Русский** · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Минимальная основа для разработки ПО с AI, построенная по принципу vendor-neutral (независимость от поставщика): переносимый слой политик/контекста и небольшой набор переиспользуемых процедур. Это не agent runtime (среда выполнения агентов), не orchestrator (оркестратор), не installer (установщик) и не framework (программный каркас).

## Файлы

- `AGENTS.md` — общая always-on (постоянно действующая) инженерная база.
- `MODEL_ROUTING.md` — стабильная политика качества/стоимости и capability tier (уровней возможностей).
- `MODEL_CATALOG.md` — изменяемый со временем каталог runtime (сред выполнения)/моделей.
- `CLAUDE.md` — тонкий мост Claude Code к `AGENTS.md`.
- `skills/` — Harness-owned (принадлежащие Harness), canonical (идущие из единственного авторитетного источника), on-demand (загружаемые по требованию) процедуры.
- `i18n/` — локализованные сводки README.

## Правила и навыки: четыре слоя

Здесь rules (правила) — это постоянно действующие указания, а skills (навыки) — процедуры для конкретных задач.

| | Постоянно действует | По требованию |
| --- | --- | --- |
| **Общий** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Проектный** | Собственный механизм правил/политик проекта | Собственные навыки проекта |

AI Engineering Harness намеренно не поставляет отдельный каталог `rules/`: общий always-on (постоянно действующий) слой правил уже имеет canonical source (единственный авторитетный источник) в `AGENTS.md`, а политика model routing (маршрутизации моделей) находится в `MODEL_ROUTING.md`. Второй постоянно действующий источник создал бы дублирование и риск противоречий.

Domain rules (доменные правила), environment/deployment topology (топология сред/развёртывания), vendor/model preferences (предпочтения поставщика/модели), product behavior (поведение продукта), business rules (бизнес-правила) и infrastructure paths (инфраструктурные пути) остаются проектными. Для выбора слоя новой инструкции используйте подход safeguard (долговременная защита) из навыка `continuous-improvement`.

## Общие навыки

Skills (навыки) — это task-specific procedures (процедуры для конкретных задач), а не always-on policy (постоянно действующая политика). При progressive disclosure (постепенном раскрытии) обычно видна только discovery metadata (метаданные обнаружения); полный текст `SKILL.md` загружается только тогда, когда текущая задача действительно соответствует навыку.

Canonical source (единственный авторитетный источник) Harness-owned skills (навыков, принадлежащих Harness) — каталог `skills/`. Ownership marker (маркер принадлежности):

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Одноимённый skill (навык) без этого ключа не является Harness-owned (принадлежащим Harness) и никогда не перезаписывается во время adoption (установки) или update (обновления).

Набор v2 содержит 14 навыков:

- `backup-and-recovery-review` — готовность к backup (резервному копированию), restore (восстановлению) и recovery (аварийному восстановлению).
- `interface-qa` — проверка web-, mobile-, desktop-, CLI- и API-интерфейсов.
- `calculation-model-validation` — проверка формул и моделей принятия решений.
- `change-review` — review (ревью) завершённых изменений, регрессий и рисков.
- `compatibility-and-rollout` — compatibility (совместимость), migration (миграция), rollout (поэтапное внедрение) и rollback (откат).
- `high-risk-change-review` — дополнительная дисциплина для изменений с высоким риском.
- `delegation-strategy` — безопасное использование подтверждённых delegation (делегирования) и parallelism (параллелизма).
- `dependency-change` — оценка добавления, удаления и upgrade (обновления версии) dependencies (зависимостей).
- `documentation-sync` — поддержание долговременной документации в соответствии с реальностью.
- `environment-release-safety` — безопасность release (выпуска)/deployment (развёртывания) и approval (одобрения).
- `continuous-improvement` — превращение повторяющихся ошибок в долговременные safeguards (защитные меры).
- `root-cause-debug` — поиск и доказательство root cause (корневой причины).
- `secret-exposure-response` — реагирование на exposure (раскрытие) secrets (секретов) и credentials (учётных данных).
- `cross-surface-consistency` — согласованность поведения между несколькими surfaces (поверхностями).

Общий набор должен оставаться примерно **20 навыков или меньше**; каждый `description` — **не более 300 символов**.

Приоритет: **project-local rules/policy (проектные правила/политика) > общая база `AGENTS.md` > shared skills (общие навыки)**. Навык не может ослаблять approval boundaries (границы одобрения), authorized scope (разрешённый охват), runtime capabilities (возможности среды выполнения) или production/live safety (безопасность продакшена/живой системы).

## Установка и обновление

Операционные copy/paste prompts (промпты для копирования/вставки) хранятся в одной canonical source (авторитетной исходной точке) и не переводятся:

- [Промпт установки (на английском)](../README.md#copypaste-adoption-prompt)
- [Промпт обновления (на английском)](../README.md#copypaste-update-prompt)

Adoption (установка) определяет используемые runtimes (среды выполнения) по repository evidence (доказательствам в репозитории); сам факт установки CLI недостаточен. Проверенные project-level skill paths (пути навыков на уровне проекта): `.agents/skills/` для Cursor/Antigravity/Codex и `.claude/skills/` для Claude Code; Cursor также читает `.claude/skills/`. Если один проверенный root (корневой каталог) покрывает все обнаруженные среды, используется одна копия. Если native activation (нативную активацию) нельзя подтвердить, применяется `harness/skills/` как neutral fallback (нейтральный запасной вариант), и нативная активация не заявляется.

До записи любого навыка все canonical names (имена из авторитетного источника) проверяются во всех target roots (целевых корневых каталогах) на collision (конфликт имён). Изменяемые managed files (управляемые файлы) получают byte-for-byte (побайтовую) резервную копию вне repository (репозитория). Harness-owned (принадлежащие Harness) копии остаются verbatim (полностью идентичными) canonical source (авторитетному источнику). Update (обновление) не переносит существующее размещение; managed skill (управляемый навык), удалённый upstream (в вышестоящем источнике), автоматически не удаляется и отмечается как orphaned (отсутствующий в источнике).

## Удаление и тестирование

Автоматического uninstaller (деинсталлятора) нет. Удаляются только managed skills (управляемые навыки) с ownership marker (маркером принадлежности) `metadata.ai-engineering-harness`; project-local skills/rules (проектные навыки/правила) не изменяются. См. [Удаление общих навыков (на английском)](../README.md#remove-the-shared-skills).

Если native skill activation (нативную активацию навыка) нельзя подтвердить, agent (агент) не должен утверждать, что навык active (активен). Для нерелевантной задачи все skill bodies (тексты навыков) не должны попадать в context (контекст); может быть видна только discovery metadata (метаданные обнаружения). См. [Проверка установки (на английском)](../README.md#how-to-test-an-installation).

Файлы `SKILL.md` не переводятся; сохраняется одна canonical English copy (единственная авторитетная английская копия). Подробности по maintenance (сопровождению), adoption/update behavior (поведению установки/обновления) и scope boundaries (границам охвата) находятся в [английском README](../README.md).
