<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

اللغات: [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · العربية · [हिन्दी](README.hi.md)

طبقة سياسات/سياق صغيرة ومحايدة تجاه المورّد (vendor-neutral) لتطوير البرمجيات بمساعدة AI، مع مجموعة محدودة من الإجراءات القابلة لإعادة الاستخدام. ليست agent runtime (بيئة تشغيل للوكلاء)، ولا orchestrator (نظام تنسيق)، ولا installer (أداة تثبيت)، ولا framework (إطار برمجي).

## الملفات

- `AGENTS.md` — خط أساس هندسي مشترك always-on (دائم التفعيل).
- `MODEL_ROUTING.md` — سياسة مستقرة للجودة/الكلفة و capability tier (مستوى القدرة).
- `MODEL_CATALOG.md` — كتالوج runtime (بيئة التشغيل) والنماذج المتغير مع الزمن.
- `CLAUDE.md` — جسر خفيف من Claude Code إلى `AGENTS.md`.
- `skills/` — إجراءات قادمة من مصدر Harness-owned (مملوك للـ Harness)، canonical (وحيد ومرجعي)، وتُحمّل on-demand (عند الحاجة).
- `i18n/` — ملخصات مترجمة من `README.md`.

## Rules (القواعد) و skills (المهارات): أربع طبقات

Rules هي التوجيهات المستمرة، وskills هي الإجراءات التي تدخل حيز الاستخدام في مهام محددة.

| | Always-on (دائم التفعيل) | On-demand (عند الحاجة) |
| --- | --- | --- |
| مشتركة | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| خاصة بالمشروع | آلية rules/policy الخاصة بالمشروع | skills الخاصة بالمشروع |

لا يوفّر Harness مجلد `rules/` منفصلاً: المصدر canonical source (المرجعي الوحيد) لطبقة القواعد المشتركة always-on هو بالفعل `AGENTS.md`، بينما توجد سياسة توجيه النماذج في `MODEL_ROUTING.md`. إنشاء مصدر always-on ثانٍ سيؤدي إلى التكرار واحتمال التعارض.

تبقى قواعد المجال، وطوبولوجيا البيئة و deployment (النشر)، وتفضيلات المورّد/النموذج، وسلوك المنتج، وقواعد العمل، ومسارات البنية التحتية خاصة بالمشروع. لتحديد الطبقة المناسبة لتوجيه جديد، استخدم منهج اختيار أصغر safeguard (إجراء حماية) دائم في skill `continuous-improvement`.

## skills (المهارات) المشتركة

Skills هي إجراءات خاصة بالمهمة وليست always-on policy. مع progressive disclosure (العرض التدريجي)، تظهر عادةً فقط discovery metadata (بيانات الاكتشاف الوصفية)، ولا يُحمّل النص الكامل في `SKILL.md` إلا عندما تتطابق المهمة فعلاً.

المصدر canonical source للـ Harness-owned skills هو `skills/`، و ownership marker (علامة الملكية) هو:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

أي skill بالاسم نفسه من دون هذا المفتاح ليست Harness-owned؛ ولا يجوز استبدالها أثناء adoption (التثبيت) أو update (التحديث).

تحتوي v2 على 14 skills:

- `backup-and-recovery-review` — مراجعة جاهزية backup (النسخ الاحتياطي)، restore (الاستعادة)، و recovery (التعافي).
- `interface-qa` — التحقق من واجهات الويب والجوال وسطح المكتب وCLI وAPI.
- `calculation-model-validation` — التحقق من الصيغ ونماذج القرار.
- `change-review` — مراجعة الانحدارات والمخاطر في التغييرات المكتملة.
- `compatibility-and-rollout` — التوافق، migration (ترحيل البيانات/المخطط)، rollout (النشر التدريجي)، و rollback (الرجوع).
- `high-risk-change-review` — انضباط إضافي للتغييرات عالية التأثير.
- `delegation-strategy` — استخدام delegation (تفويض المهام) والعمل المتوازي بعد التحقق.
- `dependency-change` — مراجعة إضافة dependency (تبعية)، وحذفها، وترقية إصدارها.
- `documentation-sync` — إبقاء التوثيق الدائم متزامناً مع الواقع.
- `environment-release-safety` — أثر release (الإصدار) و deployment (النشر) مع أمان الموافقة.
- `continuous-improvement` — تحويل الأخطاء المتكررة إلى safeguards (إجراءات حماية) دائمة.
- `root-cause-debug` — العثور على السبب الجذري وإثباته بدلاً من الاكتفاء بالعرض.
- `secret-exposure-response` — الاستجابة لتسرب secret (سر) و credential (بيانات اعتماد).
- `cross-surface-consistency` — اتساق السلوك عبر عدة واجهات.

ينبغي إبقاء المجموعة المشتركة عند نحو 20 skills أو أقل، وأن يكون كل حقل `description` 300 حرف أو أقل.

ترتيب الأولوية: rules/policy الخاصة بالمشروع > خط أساس `AGENTS.md` المشترك > skills المشتركة. لا يجوز لأي skill أن تخفف approval boundary (حدود الموافقة)، أو authorized scope (النطاق المصرّح)، أو runtime capability (قدرات بيئة التشغيل)، أو production/live safety (أمان الإنتاج/النظام الحي).

## Adoption (التثبيت) و update (التحديث)

تبقى prompts النسخ/اللصق في مصدر canonical واحد ولا تُترجم:

- [أمر التثبيت (بالإنجليزية)](../README.md#copypaste-adoption-prompt)
- [أمر التحديث (بالإنجليزية)](../README.md#copypaste-update-prompt)

تحدد Adoption بيئات runtime المستخدمة من repository evidence (أدلة المستودع)؛ وجود CLI مثبت على الجهاز وحده لا يكفي. مسارات skills التي تم التحقق منها على مستوى المشروع هي: `.agents/skills/` لـ Cursor وAntigravity وCodex؛ و`.claude/skills/` لـ Claude Code. يستطيع Cursor أيضاً قراءة `.claude/skills/`. إذا كان root (مجلد جذر) واحد موثوق يغطي كل بيئات runtime المستخدمة، تُستخدم نسخة واحدة فقط. إذا تعذر التحقق من native activation (التفعيل الأصلي)، يُستخدم `harness/skills/` كـ neutral fallback (بديل محايد) ولا يُدّعى أن native activation قد تم.

قبل كتابة أي skill، تُفحص جميع الأسماء canonical في كل الجذور المستهدفة بحثاً عن collision (تعارض أسماء). إذا كان سيجري تغيير skill managed (مُدارة)، تؤخذ خارج repository نسخة احتياطية byte-for-byte (مطابقة بايتاً ببايت). تبقى النسخ Harness-owned متطابقة verbatim (حرفياً) مع المصدر canonical. لا ينقل Update موضع skill الحالي؛ وإذا حُذفت managed skill من upstream (المصدر الأعلى) فلا تُحذف تلقائياً، بل يُبلغ عنها كـ orphaned (غير موجودة في المصدر).

## الإزالة والاختبار

لا يوجد uninstaller (أداة إزالة) آلي. لا تُزال إلا managed skills التي تحمل علامة الملكية `metadata.ai-engineering-harness`؛ ولا تُمس skills وrules الخاصة بالمشروع. راجع [إزالة skills المشتركة (بالإنجليزية)](../README.md#remove-the-shared-skills).

إذا تعذر التحقق من native activation أثناء اختبار التثبيت، فلا يجوز للـ agent الادعاء بأن skill نشطة. وفي مهمة غير مرتبطة لا ينبغي تحميل نصوص skills إلى context (السياق)؛ ينبغي أن تظهر discovery metadata فقط. راجع [اختبار التثبيت (بالإنجليزية)](../README.md#how-to-test-an-installation).

لا تُترجم ملفات `SKILL.md`؛ تبقى نسخة إنجليزية canonical واحدة. ولتفاصيل الصيانة، وسلوك adoption/update، وحدود النطاق، يكون [ملف `README.md` الإنجليزي](../README.md) هو المصدر الأساسي.
