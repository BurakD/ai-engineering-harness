<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Diller:** [English](../README.md) · **Türkçe** · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

AI destekli yazılım geliştirme için minimal, vendor-neutral bir politika/bağlam katmanı ve küçük bir yeniden kullanılabilir prosedür setidir. Bir agent runtime, orchestrator, installer veya framework değildir.

## Dosyalar

- `AGENTS.md` — paylaşılan always-on mühendislik tabanı.
- `MODEL_ROUTING.md` — kararlı kalite/maliyet ve capability-tier politikası.
- `MODEL_CATALOG.md` — zaman duyarlı runtime/model kataloğu.
- `CLAUDE.md` — Claude Code için ince `AGENTS.md` köprüsü.
- `skills/` — Harness-owned canonical on-demand prosedürler.
- `i18n/` — yerelleştirilmiş README özetleri.

## Rules ve skills: dört katman

| | Always-on | On-demand |
| --- | --- | --- |
| **Paylaşılan** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Projeye özel** | Projenin kendi rule/policy mekanizması | Projenin kendi skill'leri |

Harness ayrı bir `rules/` dizini sunmaz: paylaşılan always-on kural katmanının canonical kaynağı zaten `AGENTS.md`'dir; model yönlendirme politikası `MODEL_ROUTING.md`'dedir. İkinci bir always-on kaynak tekrar ve çelişki üretirdi.

Domain kuralları, ortam/deployment topolojisi, vendor/model tercihleri, ürün davranışı, iş kuralları ve altyapı yolları projeye özel kalır. Yeni bir rehberliğin hangi katmana ait olduğuna karar verirken `continuous-improvement` skill'indeki safeguard tercih yaklaşımını kullanın.

## Paylaşılan skills

Skill'ler task-specific prosedürlerdir; always-on policy değildir. Normalde yalnız metadata discovery bağlamında görünür, tam `SKILL.md` gövdesi yalnız görev gerçekten eşleştiğinde yüklenir.

Harness-owned skill'lerin canonical kaynağı `skills/` dizinidir ve ownership marker'ı şudur:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Aynı isimli bir skill bu anahtarı taşımıyorsa Harness-owned değildir ve adoption/update sırasında üzerine yazılmaz.

v2 seti 14 skill içerir:

- `backup-and-recovery-review` — backup/restore/recovery hazırlığı.
- `interface-qa` — web, mobil, desktop, CLI ve API arayüz doğrulaması.
- `calculation-model-validation` — formül ve karar modeli doğrulaması.
- `change-review` — tamamlanmış değişikliklerin risk ve regresyon incelemesi.
- `compatibility-and-rollout` — uyumluluk, migration, rollout ve rollback.
- `high-risk-change-review` — yüksek etkili değişikliklerde ek disiplin.
- `delegation-strategy` — doğrulanmış delegation/parallelism kullanımı.
- `dependency-change` — dependency ekleme, kaldırma ve upgrade incelemesi.
- `documentation-sync` — kalıcı dokümantasyonu gerçekle senkron tutma.
- `environment-release-safety` — release/deployment etkisi ve approval güvenliği.
- `continuous-improvement` — tekrarlanan hataları kalıcı safeguard'a dönüştürme.
- `root-cause-debug` — belirti yerine kök nedeni bulup kanıtlama.
- `secret-exposure-response` — secret/credential exposure müdahalesi.
- `cross-surface-consistency` — çoklu yüzeylerde davranış tutarlılığı.

Set yaklaşık **20 skill veya altında** tutulmalıdır; `description` alanları **300 karakter veya daha kısa** olmalıdır.

Öncelik: **project-local rules/policy > paylaşılan `AGENTS.md` tabanı > shared skills**. Skill approval boundary, scope, runtime capability veya production/live safety kuralını gevşetemez.

## Adoption ve update

Operasyonel copy/paste prompt'lar tek canonical kaynakta tutulur ve çevrilmez:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

Adoption runtime kullanımını repository kanıtından tespit eder; makinede CLI kurulu olması tek başına yeterli değildir. Doğrulanmış project-level skill yolları: Cursor/Antigravity/Codex için `.agents/skills/`, Claude Code için `.claude/skills/`; Cursor ayrıca `.claude/skills/` okuyabilir. Tek doğrulanmış root tüm kullanılan runtime'ları kapsıyorsa tek kopya kullanılır. Doğrulanamayan native activation için neutral `harness/skills/` kullanılır ve native aktif olduğu iddia edilmez.

Herhangi bir skill yazılmadan önce tüm canonical isimler tüm hedef root'larda collision açısından taranır. Managed mevcut skill değişecekse repo dışında byte-for-byte yedek alınır. Update mevcut skill yerleşimini taşımaz; upstream'den kaldırılmış managed skill otomatik silinmez, orphan olarak raporlanır.

## Kaldırma ve test

Otomatik uninstaller yoktur. Yalnız `metadata.ai-engineering-harness` marker'ı taşıyan managed skill'ler kaldırılır; project-local skill/rule'lara dokunulmaz. Ayrıntı için [Remove the shared skills](../README.md#remove-the-shared-skills).

Kurulum testinde runtime native activation doğrulanamıyorsa agent aktif olduğunu söylememelidir. Alakasız bir görevde tüm skill gövdeleri context'e girmemeli; yalnız discovery metadata'sı görünmelidir. Ayrıntı için [How to test an installation](../README.md#how-to-test-an-installation).

`SKILL.md` dosyaları çevrilmez; tek canonical İngilizce kopya korunur. Ayrıntılı bakım, adoption/update davranışı ve kapsam sınırları için [English README](../README.md) esas kaynaktır.
