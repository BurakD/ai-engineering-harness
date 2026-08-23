<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**اللغات:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · **العربية** · [हिन्दी](README.hi.md)

خط أساس صغير لتطوير البرمجيات بمساعدة AI، بمنهج ⁦vendor-neutral⁩ (محايد تجاه المورّد): طبقة محمولة للسياسات/السياق مع مجموعة محدودة من الإجراءات القابلة لإعادة الاستخدام. ليس ⁦agent runtime⁩ (بيئة تشغيل للوكلاء)، ولا ⁦orchestrator⁩ (منظّم تنسيق)، ولا ⁦installer⁩ (أداة تثبيت)، ولا ⁦framework⁩ (إطار برمجي).

## الملفات

- `AGENTS.md` — خط أساس هندسي مشترك ⁦always-on⁩ (دائم التفعيل).
- `MODEL_ROUTING.md` — سياسة مستقرة للجودة/الكلفة و⁦capability tier⁩ (مستوى القدرة).
- `MODEL_CATALOG.md` — كتالوج ⁦runtime⁩ (بيئات التشغيل)/النماذج المتغير مع الزمن.
- `CLAUDE.md` — جسر خفيف من Claude Code إلى `AGENTS.md`.
- `skills/` — إجراءات ⁦Harness-owned⁩ (مملوكة للـ Harness)، و⁦canonical⁩ (قادمة من المصدر المرجعي الوحيد)، و⁦on-demand⁩ (تُحمّل عند الحاجة).
- `i18n/` — ملخصات README مترجمة.

## القواعد والمهارات: أربع طبقات

المقصود بـ ⁦rules⁩ (القواعد) هنا هو التوجيه الدائم، وبـ ⁦skills⁩ (المهارات) الإجراءات المستخدمة لمهام محددة.

| | دائم التفعيل | عند الحاجة |
| --- | --- | --- |
| **مشتركة** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **خاصة بالمشروع** | آلية القواعد/السياسات الخاصة بالمشروع | مهارات المشروع الخاصة |

لا يوزّع AI Engineering Harness مجلد `rules/` منفصلاً عمداً. طبقة القواعد المشتركة ⁦always-on⁩ (دائمة التفعيل) لها بالفعل ⁦canonical source⁩ (مصدر مرجعي وحيد) في `AGENTS.md`، بينما توجد سياسة ⁦model routing⁩ (توجيه النماذج) في `MODEL_ROUTING.md`. إنشاء مصدر دائم ثانٍ سيؤدي إلى التكرار واحتمال التعارض.

تبقى ⁦domain rules⁩ (قواعد المجال)، و⁦environment/deployment topology⁩ (طوبولوجيا البيئات/النشر)، و⁦vendor/model preferences⁩ (تفضيلات المورّد/النموذج)، و⁦product behavior⁩ (سلوك المنتج)، و⁦business rules⁩ (قواعد العمل)، و⁦infrastructure paths⁩ (مسارات البنية التحتية) خاصة بالمشروع. لتحديد الطبقة المناسبة لتوجيه جديد، استخدم منهج ⁦safeguard⁩ (إجراء حماية دائم) في المهارة `continuous-improvement`.

## المهارات المشتركة

⁦Skills⁩ (المهارات) هي ⁦task-specific procedures⁩ (إجراءات خاصة بالمهمة)، وليست ⁦always-on policy⁩ (سياسة دائمة التفعيل). مع ⁦progressive disclosure⁩ (العرض التدريجي)، تظهر عادةً فقط ⁦discovery metadata⁩ (بيانات الاكتشاف الوصفية)، ولا يُحمّل النص الكامل في `SKILL.md` إلا عندما تتطابق المهمة فعلاً.

المصدر ⁦canonical source⁩ (المرجعي الوحيد) للمهارات ⁦Harness-owned⁩ (المملوكة للـ Harness) هو `skills/`. و⁦ownership marker⁩ (علامة الملكية) هو:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

أي ⁦skill⁩ (مهارة) بالاسم نفسه من دون هذا المفتاح ليست ⁦Harness-owned⁩ (مملوكة للـ Harness)، ولا يجوز استبدالها أثناء ⁦adoption⁩ (التثبيت) أو ⁦update⁩ (التحديث).

تحتوي v2 على 14 مهارة:

- `backup-and-recovery-review` — جاهزية ⁦backup⁩ (النسخ الاحتياطي)، و⁦restore⁩ (الاستعادة)، و⁦recovery⁩ (التعافي).
- `interface-qa` — التحقق من واجهات الويب والجوال وسطح المكتب وCLI وAPI.
- `calculation-model-validation` — التحقق من الصيغ ونماذج القرار.
- `change-review` — ⁦review⁩ (مراجعة) التغييرات المكتملة والانحدارات والمخاطر.
- `compatibility-and-rollout` — ⁦compatibility⁩ (التوافق)، و⁦migration⁩ (الترحيل)، و⁦rollout⁩ (النشر التدريجي)، و⁦rollback⁩ (الرجوع للإصدار السابق).
- `high-risk-change-review` — انضباط إضافي للتغييرات عالية التأثير.
- `delegation-strategy` — الاستخدام الآمن لـ ⁦delegation⁩ (تفويض المهام) و⁦parallelism⁩ (التنفيذ المتوازي) بعد التحقق.
- `dependency-change` — تقييم إضافة/حذف ⁦dependencies⁩ (التبعيات) و⁦upgrade⁩ (ترقية الإصدارات).
- `documentation-sync` — إبقاء التوثيق الدائم متوافقاً مع الواقع.
- `environment-release-safety` — أمان ⁦release⁩ (الإصدار)/⁦deployment⁩ (النشر) و⁦approval⁩ (الموافقة).
- `continuous-improvement` — تحويل الإخفاقات المتكررة إلى ⁦safeguards⁩ (إجراءات حماية دائمة).
- `root-cause-debug` — تحديد ⁦root cause⁩ (السبب الجذري) وإثباته.
- `secret-exposure-response` — الاستجابة لـ ⁦exposure⁩ (انكشاف) ⁦secrets⁩ (الأسرار) و⁦credentials⁩ (بيانات الاعتماد).
- `cross-surface-consistency` — اتساق السلوك عبر عدة ⁦surfaces⁩ (واجهات استخدام).

ينبغي إبقاء المجموعة المشتركة عند نحو **20 مهارة أو أقل**، وأن يكون كل `description` **300 حرف أو أقل**.

الأولوية: **⁦project-local rules/policy⁩ (قواعد/سياسات المشروع المحلية) > خط أساس `AGENTS.md` المشترك > ⁦shared skills⁩ (المهارات المشتركة)**. لا يجوز لأي مهارة أن تخفف ⁦approval boundary⁩ (حدود الموافقة)، أو ⁦authorized scope⁩ (النطاق المصرّح)، أو ⁦runtime capability⁩ (قدرات بيئة التشغيل)، أو ⁦production/live safety⁩ (أمان الإنتاج/النظام الحي).

## التثبيت والتحديث

تبقى ⁦copy/paste prompts⁩ (أوامر النسخ/اللصق) التشغيلية في ⁦canonical source⁩ (مصدر مرجعي واحد) ولا يُترجم نصها:

- [أمر التثبيت (بالإنجليزية)](../README.md#copypaste-adoption-prompt)
- [أمر التحديث (بالإنجليزية)](../README.md#copypaste-update-prompt)

تحدد ⁦adoption⁩ (عملية التثبيت) بيئات ⁦runtime⁩ (التشغيل) المستخدمة من ⁦repository evidence⁩ (أدلة المستودع)؛ وجود CLI مثبت على الجهاز وحده لا يكفي. مسارات المهارات ⁦project-level⁩ (على مستوى المشروع) التي تم التحقق منها هي `.agents/skills/` لـ Cursor/Antigravity/Codex و`.claude/skills/` لـ Claude Code؛ ويستطيع Cursor أيضاً قراءة `.claude/skills/`. إذا كان ⁦root⁩ (مجلد جذر) واحد موثوق يغطي كل البيئات المكتشفة، تُستخدم نسخة واحدة فقط. إذا تعذر التحقق من ⁦native activation⁩ (التفعيل الأصلي)، يُستخدم `harness/skills/` كـ ⁦neutral fallback⁩ (بديل محايد) ولا يُدّعى أن التفعيل الأصلي قد تم.

قبل كتابة أي مهارة، تُفحص كل ⁦canonical names⁩ (أسماء المصدر المرجعي) في جميع ⁦target roots⁩ (المجلدات الجذرية المستهدفة) بحثاً عن ⁦collision⁩ (تعارض أسماء). كل ⁦managed file⁩ (ملف مُدار) سيتغير يحصل على نسخة احتياطية ⁦byte-for-byte⁩ (مطابقة بايتاً ببايت) خارج ⁦repository⁩ (المستودع). تبقى النسخ ⁦Harness-owned⁩ (المملوكة للـ Harness) ⁦verbatim⁩ (مطابقة حرفياً) مع ⁦canonical source⁩ (المصدر المرجعي). لا ينقل ⁦update⁩ (التحديث) مكان التثبيت الحالي؛ وإذا حُذفت ⁦managed skill⁩ (مهارة مُدارة) من ⁦upstream⁩ (المصدر الأعلى) فلا تُحذف تلقائياً، بل يُبلغ عنها كـ ⁦orphaned⁩ (غير موجودة في المصدر).

## الإزالة والاختبار

لا يوجد ⁦uninstaller⁩ (أداة إزالة) آلي. لا تُزال إلا ⁦managed skills⁩ (المهارات المُدارة) التي تحمل ⁦ownership marker⁩ (علامة الملكية) `metadata.ai-engineering-harness`؛ ولا تُمس ⁦project-local skills/rules⁩ (مهارات/قواعد المشروع المحلية). راجع [إزالة المهارات المشتركة (بالإنجليزية)](../README.md#remove-the-shared-skills).

إذا تعذر التحقق من ⁦native skill activation⁩ (التفعيل الأصلي للمهارة)، فلا يجوز للـ ⁦agent⁩ (الوكيل) الادعاء بأن المهارة ⁦active⁩ (نشطة). وفي مهمة غير مرتبطة لا ينبغي تحميل كل ⁦skill bodies⁩ (نصوص المهارات) إلى ⁦context⁩ (السياق)؛ يمكن أن تظهر فقط ⁦discovery metadata⁩ (بيانات الاكتشاف الوصفية). راجع [اختبار التثبيت (بالإنجليزية)](../README.md#how-to-test-an-installation).

لا تُترجم ملفات `SKILL.md`؛ تبقى ⁦canonical English copy⁩ (نسخة إنجليزية مرجعية وحيدة). ولتفاصيل ⁦maintenance⁩ (الصيانة)، و⁦adoption/update behavior⁩ (سلوك التثبيت/التحديث)، و⁦scope boundaries⁩ (حدود النطاق)، راجع [README الإنجليزي](../README.md).
