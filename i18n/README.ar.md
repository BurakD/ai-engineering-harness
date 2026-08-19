# AI Engineering Harness

**اللغات:** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · **العربية** · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

طبقة أساسية صغيرة ومحايدة تجاه المورّد لتطوير البرمجيات بمساعدة الذكاء الاصطناعي.

الانتقال بين أدوات أو نماذج البرمجة بالذكاء الاصطناعي يؤدي غالبًا إلى فقدان سياق المشروع الهندسي والحاجة إلى شرحه من جديد. AI Engineering Harness هو طبقة صغيرة وقابلة للنقل من السياسات والسياق لمنع ذلك. ليس Agent Runtime ولا orchestrator؛ إذ توفر Cursor وClaude Code وCodex وAntigravity قدرات التنفيذ والتنظيم الخاصة بها.

## ما الذي يحله؟

1. الحفاظ على سياق المشروع والانضباط الهندسي عند تبديل الأداة أو النموذج.
2. موازنة الجودة والتكلفة باستخدام reasoning أقوى فقط عندما تبرره درجة التعقيد أو المخاطر.
3. إبقاء اختيارات model/runtime محدثة دون تثبيت أسماء نماذج قصيرة العمر داخل السياسة المستقرة.

## الملفات

- `AGENTS.md` — baseline هندسية مشتركة للوكلاء المتوافقين.
- `MODEL_ROUTING.md` — سياسة مستقرة من مستويات FAST / STANDARD / REASONING / FRONTIER.
- `MODEL_CATALOG.md` — كتالوج زمني للنماذج/runtimes والتوصيات الحالية.
- `CLAUDE.md` — adapter بسيط يتيح لـ Claude Code استيراد `AGENTS.md`.
- `README.md` — الدليل الرئيسي للاعتماد والتحديث والاختبار والصيانة.

## ما هو وما ليس هو

القيمة الأساسية في محتوى السياسة: سياق repository-first، مستويات routing، تحقق fail-closed من قدرات runtime، موافقة بشرية حسب أثر الإجراء، انضباط scope، handoff دائم، وتحديث آمن.

ليس workflow engine ولا multi-agent framework ولا runtime ولا مولّدًا لمزامنة القواعد، ولا يستبدل rules/skills الأصلية للأدوات.

## التوافق

`AGENTS.md` convention خارجية وعابرة للأدوات. أي runtime يقرأها مباشرة لا يحتاج adapter خاصًا بالـ Harness. يستخدم Claude Code ملف `CLAUDE.md`، لذلك لا يتضمن هذا المستودع سوى الجسر الأدنى `@AGENTS.md`. وتبقى آليات Antigravity الخاصة مثل `.agents/skills/` و`.agents/workflows/` محلية للمشروع.

## اعتماد Harness في مشروع قائم

1. ابقَ في repository والـ branch الحاليين.
2. قبل التعديل، اجعل agent مناسبًا يفحص rules وdocs وحالة Git وdeployment topology وأوامر validation.
3. قبل تعديل أي ملف موجود، أنشئ نسخة byte-for-byte خارج repository.
4. حافظ على كل المحتوى project-specific وأضف فقط shared content الخاص بالـ Harness.
5. لا تنشئ branch أو worktree أو installer أو manifest أو adapter أو آلية sync لمجرد اعتماد Harness.
6. لا تنفذ commit أو push أو deploy أو publish دون موافقة صريحة.

**نص adoption الكامل:** [README بالإنجليزية](README.md#copypaste-adoption-prompt)

## التحديث

التحديث ينعش فقط shared content المملوك للـ Harness. يتم تحديث `AGENTS.md` و`MODEL_ROUTING.md` و`MODEL_CATALOG.md` والجزء المشترك من `CLAUDE.md` من upstream مع الحفاظ على rules وmodels وskills وdocs وcode والعمل غير الملتزم به داخل المشروع.

**نص update الكامل:** [README بالإنجليزية](README.md#copypaste-update-prompt)

## المبادئ الأساسية

- يجب أن تبقى حقيقة repository متاحة عبر تبديل النماذج أو الوكلاء.
- أضف ولا تستبدل: تبقى tool-native rules في أماكنها.
- `MODEL_ROUTING.md` مستقر؛ `MODEL_CATALOG.md` حساس للزمن عمدًا.
- الـ active runtime هو المرجع النهائي لما يمكن استدعاؤه فعليًا من models/agents.
- اكتشاف مشكلة لا يمنح صلاحية إصلاحها خارج scope المطلوب.
- الإجراءات عالية الأثر تتطلب موافقة بشرية حسب تأثيرها، لا حسب اسم الأداة أو البيئة.
- عندما تستطيع tests وlinters وtypes وCI وغيرها من الضوابط الحتمية فرض القاعدة نفسها بشكل موثوق، تُفضّل على تكرار model judgment.

## اختبار التثبيت

اختبر في sessions جديدة: structural smoke test وreal-task behavior test وapproval-boundary test وcross-tool runtime-capability test. يجب أن يكتشف agent السياق بشكل صحيح وألا يدّعي أي capability لا يستطيع الـ active runtime التحقق منها.

النصوص الدقيقة للاختبارات: [How to test an installation](README.md#how-to-test-an-installation)

## الترخيص

مفتوح المصدر تحت **Apache License 2.0**.