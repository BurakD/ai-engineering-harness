# AI Engineering Harness

**Языки:** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · **Русский** · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

Минимальная, независимая от поставщика основа для разработки ПО с помощью ИИ.

При переходе между AI-инструментами или моделями часто теряется инженерный контекст проекта и приходится объяснять его заново. AI Engineering Harness — это небольшая переносимая прослойка политик и контекста, которая предотвращает это. Это не runtime агентов и не оркестратор; Cursor, Claude Code, Codex и Antigravity предоставляют собственные механизмы выполнения.

## Какие задачи решает

1. Сохраняет контекст проекта и инженерную дисциплину при смене инструмента или модели.
2. Балансирует качество и стоимость, используя более мощное reasoning только там, где это оправдано сложностью или риском.
3. Позволяет поддерживать выбор моделей/runtime актуальным, не закрепляя краткоживущие названия моделей в стабильной политике.

## Файлы

- `AGENTS.md` — общая инженерная база для совместимых coding agents.
- `MODEL_ROUTING.md` — стабильная политика FAST / STANDARD / REASONING / FRONTIER.
- `MODEL_CATALOG.md` — изменяемый со временем каталог моделей/runtimes и текущих рекомендаций.
- `CLAUDE.md` — минимальный адаптер, позволяющий Claude Code импортировать `AGENTS.md`.
- `README.md` — основной документ по adoption, обновлению, тестированию и сопровождению.

## Что это — и чем не является

Главная ценность — политика: repository-first контекст, routing tiers, fail-closed проверка возможностей runtime, человеческое одобрение по эффекту действия, дисциплина scope, устойчивый handoff и безопасное обновление.

Это не workflow engine, не multi-agent framework, не runtime, не генератор синхронизации правил и не замена нативным rules/skills конкретных инструментов.

## Совместимость

`AGENTS.md` — внешняя cross-tool конвенция. Runtime, который читает её напрямую, не требует Harness-специфичного адаптера. Claude Code использует `CLAUDE.md`, поэтому в репозитории есть только минимальный мост `@AGENTS.md`. Специфичные для Antigravity механизмы вроде `.agents/skills/` и `.agents/workflows/` остаются локальными для проекта.

## Подключение к существующему проекту

1. Оставайтесь в текущем repository и branch.
2. До изменений поручите подходящему агенту изучить правила, docs, Git-состояние, deployment-топологию и команды валидации.
3. Перед изменением существующего файла создайте byte-for-byte backup вне repository.
4. Сохраните весь project-specific контент и добавляйте только shared-контент Harness.
5. Не создавайте branch, worktree, installer, manifest, adapter или sync-механику только ради Harness.
6. Не выполняйте commit, push, deploy или publish без явного одобрения.

**Полный adoption prompt:** [английский README](README.md#copypaste-adoption-prompt)

## Обновление

Обновление затрагивает только shared-контент Harness. `AGENTS.md`, `MODEL_ROUTING.md`, `MODEL_CATALOG.md` и shared-часть `CLAUDE.md` обновляются из upstream с сохранением project-local правил, моделей, skills, docs, кода и незакоммиченной работы.

**Полный update prompt:** [английский README](README.md#copypaste-update-prompt)

## Ключевые принципы

- Истина repository должна переживать смену модели или агента.
- Добавлять, а не заменять: tool-native правила остаются на месте.
- `MODEL_ROUTING.md` стабилен; `MODEL_CATALOG.md` намеренно зависит от времени.
- Активный runtime — источник истины о реально доступных моделях/агентах.
- Обнаружение проблемы не даёт разрешения исправлять её вне запрошенного scope.
- High-impact действия требуют человеческого одобрения по эффекту, а не по имени инструмента или среды.
- Tests, linters, types, CI и другие детерминированные safeguards предпочтительнее повторного model judgment, если они могут надёжно enforce ту же норму.

## Проверка установки

Проверяйте в новых sessions: structural smoke test, real-task behavior test, approval-boundary test и cross-tool runtime-capability test. Агент должен корректно обнаруживать контекст и никогда не заявлять возможности, которые активный runtime не может подтвердить.

Точные prompts: [How to test an installation](README.md#how-to-test-an-installation)

## Лицензия

Открытый исходный код под **Apache License 2.0**.