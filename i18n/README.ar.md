<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**اللغات:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · **العربية** · [हिन्दी](README.hi.md)

خط أساس صغير ومحايد تجاه المورّد لتطوير البرمجيات بمساعدة الذكاء الاصطناعي: طبقة محمولة للسياسات/السياق مع مجموعة محدودة من الإجراءات الهندسية القابلة لإعادة الاستخدام. ليس runtime للوكلاء، ولا orchestrator، ولا installer، ولا framework.

## الملفات

- `AGENTS.md` — خط أساس هندسي مشترك يعمل دائماً.
- `MODEL_ROUTING.md` — سياسة مستقرة للجودة/الكلفة ومستويات القدرة.
- `MODEL_CATALOG.md` — كتالوج runtime/model يتغير مع الزمن.
- `CLAUDE.md` — جسر خفيف من Claude Code إلى `AGENTS.md`.
- `skills/` — إجراءات canonical مملوكة للـ Harness وتُحمّل عند الحاجة.
- `i18n/` — ملخصات README مترجمة.

## القواعد والـ skills: أربع طبقات

| | Always-on | On-demand |
| --- | --- | --- |
| **مشتركة** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **خاصة بالمشروع** | آلية rules/policy الخاصة بالمشروع | skills الخاصة بالمشروع |

لا يوزّع Harness مجلد `rules/` منفصلاً عمداً. المصدر canonical للطبقة المشتركة always-on موجود بالفعل في `AGENTS.md`، بينما سياسة model routing في `MODEL_ROUTING.md`. إنشاء مصدر canonical ثانٍ للقواعد سيؤدي إلى التكرار واحتمال التعارض.

قواعد المجال، وطوبولوجيا البيئات وعمليات النشر، وتفضيلات المورّد/النموذج، وسلوك المنتج، وقواعد العمل، ومسارات البنية التحتية تبقى خاصة بالمشروع. لتحديد الطبقة المناسبة لأي guidance جديد، استخدم skill `continuous-improvement` ومنهجه في اختيار أصغر safeguard دائم مناسب.

## Shared skills

الـ skills إجراءات مرتبطة بمهمة محددة وليست always-on policy. عادةً يجب أن تكون metadata فقط متاحة للاكتشاف، ويُحمّل جسم `SKILL.md` الكامل فقط عندما تتطابق المهمة فعلاً مع skill.

المصدر canonical للـ Harness-owned skills هو `skills/`. علامة ownership:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

أي skill بالاسم نفسه من دون هذا المفتاح ليس مملوكاً للـ Harness ويجب ألا يُستبدل أثناء adoption أو update.

تحتوي v2 على 14 skills:

- `backup-and-recovery-review` — جاهزية backup/restore/recovery.
- `interface-qa` — التحقق من واجهات web/mobile/desktop/CLI/API.
- `calculation-model-validation` — التحقق من الصيغ ونماذج القرار.
- `change-review` — مراجعة التغييرات المكتملة ومخاطر regression.
- `compatibility-and-rollout` — compatibility وmigration وrollout وrollback.
- `high-risk-change-review` — انضباط إضافي للتغييرات عالية المخاطر.
- `delegation-strategy` — الاستخدام الآمن لـ delegation/parallelism بعد التحقق.
- `dependency-change` — تقييم إضافة/حذف/ترقية dependencies.
- `documentation-sync` — إبقاء التوثيق الدائم متوافقاً مع الواقع.
- `environment-release-safety` — أمان release/deployment وحدود الموافقة.
- `continuous-improvement` — تحويل الإخفاقات المتكررة إلى safeguards دائمة.
- `root-cause-debug` — تحديد root cause وإثباتها.
- `secret-exposure-response` — الاستجابة لانكشاف secrets/credentials.
- `cross-surface-consistency` — اتساق السلوك عبر عدة surfaces/channels.

ينبغي إبقاء المجموعة المشتركة عند نحو **20 skill أو أقل**، وأن يكون كل `description` **300 حرف أو أقل**.

الأولوية: **project-local rules/policy > shared `AGENTS.md` baseline > shared skills**. لا يجوز لأي skill أن يخفف حدود الموافقة أو النطاق المصرّح أو قدرات runtime أو أمان production/live.

## Adoption و update

تبقى prompts التشغيلية القابلة للنسخ واللصق في مصدر canonical واحد ولا تُترجم:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

تحدد adoption الـ runtimes المستخدمة من أدلة داخل repository؛ وجود CLI مثبت على الجهاز وحده لا يكفي. المسارات project-level التي تم التحقق منها: `.agents/skills/` لـ Cursor وAntigravity وCodex، و`.claude/skills/` لـ Claude Code. يستطيع Cursor أيضاً قراءة `.claude/skills/`. إذا كان root واحد موثوق يغطي كل runtimes المكتشفة، تُستخدم نسخة واحدة فقط. إذا تعذر التحقق من native activation، يستخدم `harness/skills/` كموقع محايد ولا يُدّعى أن الـ skill مفعّل native.

قبل كتابة أي skill، تُفحص جميع الأسماء canonical بحثاً عن collisions في جميع target roots. أي managed file سيُعدّل يحصل على backup byte-for-byte خارج repository. لا ينقل update مكان تثبيت skill الحالي؛ وإذا حُذف managed skill من upstream فلا يُحذف تلقائياً بل يُبلغ عنه كـ orphaned.

## الإزالة والاختبار

لا يوجد uninstaller آلي. لا تُزال باعتبارها Harness-owned إلا skills التي تحمل `metadata.ai-engineering-harness`؛ ولا تُمس project-local rules/skills. راجع [Remove the shared skills](../README.md#remove-the-shared-skills).

إذا تعذر التحقق من native skill activation فلا يجوز للوكيل الادعاء بأن skill نشط. وفي مهمة غير مرتبطة لا ينبغي تحميل أجسام جميع skills إلى context؛ يمكن أن تظهر discovery metadata فقط. راجع [How to test an installation](../README.md#how-to-test-an-installation).

لا تُترجم ملفات `SKILL.md`؛ تبقى نسخة canonical إنجليزية واحدة. للتفاصيل الكاملة عن maintenance وadoption/update وحدود النطاق، راجع [English README](../README.md).
