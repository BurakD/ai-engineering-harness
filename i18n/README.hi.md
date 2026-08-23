<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**भाषाएँ:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · **हिन्दी**

AI-सहायित सॉफ़्टवेयर विकास के लिए एक छोटा, vendor-neutral baseline: portable policy/context layer के साथ पुनः उपयोग योग्य engineering procedures का सीमित सेट। यह agent runtime, orchestrator, installer या framework नहीं है।

## फ़ाइलें

- `AGENTS.md` — shared, always-on engineering baseline.
- `MODEL_ROUTING.md` — स्थिर quality/cost और capability-tier policy.
- `MODEL_CATALOG.md` — समय-संवेदनशील runtime/model catalog.
- `CLAUDE.md` — Claude Code से `AGENTS.md` का पतला bridge.
- `skills/` — Harness-owned canonical on-demand procedures.
- `i18n/` — localized README summaries.

## Rules और skills: चार layers

| | Always-on | On-demand |
| --- | --- | --- |
| **Shared** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Project-specific** | प्रोजेक्ट का अपना rule/policy mechanism | प्रोजेक्ट के अपने skills |

Harness अलग `rules/` directory जानबूझकर नहीं देता। Shared always-on rule layer का canonical source पहले से `AGENTS.md` है और model-routing policy `MODEL_ROUTING.md` में है। दूसरा canonical always-on source duplication और conflict risk पैदा करेगा।

Domain rules, environment/deployment topology, vendor/model preferences, product behavior, business rules और infrastructure paths project-local रहते हैं। नई guidance किस layer में होनी चाहिए, यह तय करने के लिए `continuous-improvement` skill में दिए “सबसे छोटा durable safeguard चुनें” दृष्टिकोण का उपयोग करें।

## Shared skills

Skills task-specific procedures हैं, always-on policy नहीं। सामान्यतः discovery के लिए केवल metadata उपलब्ध होनी चाहिए; पूरा `SKILL.md` body तभी load होना चाहिए जब वर्तमान task वास्तव में skill से मेल खाए।

Harness-owned skills का canonical source `skills/` है। Ownership marker:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

इसी नाम का कोई skill यदि यह key नहीं रखता, तो वह Harness-owned नहीं है और adoption/update के दौरान उसे overwrite नहीं किया जाना चाहिए।

v2 में 14 skills हैं:

- `backup-and-recovery-review` — backup/restore/recovery readiness.
- `interface-qa` — web, mobile, desktop, CLI और API interface validation.
- `calculation-model-validation` — formulas और decision models का validation.
- `change-review` — completed changes, regressions और risks का review.
- `compatibility-and-rollout` — compatibility, migration, rollout और rollback.
- `high-risk-change-review` — high-risk changes के लिए अतिरिक्त discipline.
- `delegation-strategy` — verified delegation/parallelism का सुरक्षित उपयोग.
- `dependency-change` — dependency add/remove/upgrade evaluation.
- `documentation-sync` — durable documentation को वास्तविकता के साथ sync रखना.
- `environment-release-safety` — release/deployment और approval-boundary safety.
- `continuous-improvement` — recurring failures को durable safeguards में बदलना.
- `root-cause-debug` — root cause पहचानना और प्रमाणित करना.
- `secret-exposure-response` — secret/credential exposure response.
- `cross-surface-consistency` — कई surfaces/channels में behavior consistency.

Shared set को लगभग **20 skills या उससे कम** रखा जाना चाहिए; हर `description` **300 characters या कम** होना चाहिए।

Precedence: **project-local rules/policy > shared `AGENTS.md` baseline > shared skills**. कोई skill approval boundary, authorized scope, runtime capability या production/live safety को कमजोर नहीं कर सकता।

## Adoption और update

Operational copy/paste prompts एक ही canonical source में रहते हैं और translate नहीं किए जाते:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

Adoption runtimes को repository evidence से detect करता है; मशीन पर CLI installed होना अकेले पर्याप्त evidence नहीं है। Verified project-level skill paths: Cursor/Antigravity/Codex के लिए `.agents/skills/`, Claude Code के लिए `.claude/skills/`; Cursor `.claude/skills/` भी पढ़ सकता है। यदि एक verified root सभी detected runtimes को cover करता है, तो केवल एक copy उपयोग होती है। यदि native activation verify नहीं किया जा सके, neutral `harness/skills/` उपयोग होता है और native activation का दावा नहीं किया जाता।

किसी भी skill को लिखने से पहले सभी canonical names को सभी target roots में collisions के लिए scan किया जाता है। बदले जाने वाले managed files का repository के बाहर byte-for-byte backup लिया जाता है। Update existing skill placement को move नहीं करता; upstream से हटाया गया managed skill अपने-आप delete नहीं होता, उसे orphaned के रूप में report किया जाता है।

## Removal और tests

Automatic uninstaller नहीं है। केवल `metadata.ai-engineering-harness` वाले skills को Harness-owned removal candidate माना जाता है; project-local rules/skills untouched रहते हैं। देखें [Remove the shared skills](../README.md#remove-the-shared-skills)।

यदि native skill activation verify नहीं की जा सके, agent को यह दावा नहीं करना चाहिए कि skill active है। किसी unrelated task में सभी skill bodies context में नहीं आने चाहिए; केवल discovery metadata दिखाई दे सकती है। देखें [How to test an installation](../README.md#how-to-test-an-installation)।

`SKILL.md` files translate नहीं किए जाते; एक canonical English copy ही रखी जाती है। Detailed maintenance, adoption/update और scope boundaries के लिए [English README](../README.md) authoritative source है।
