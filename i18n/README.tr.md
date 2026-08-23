<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Diller:** [English](../README.md) · **Türkçe** · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

AI destekli yazılım geliştirme için minimal, vendor-neutral (sağlayıcıdan bağımsız) bir politika/bağlam katmanı ve küçük bir yeniden kullanılabilir prosedür setidir. Bir agent runtime (ajan çalışma ortamı), orchestrator, installer veya framework değildir.

## Dosyalar

- `AGENTS.md` — paylaşılan always-on (sürekli etkin) mühendislik tabanı.
- `MODEL_ROUTING.md` — kararlı kalite/maliyet ve capability-tier (yetenek seviyesi) politikası.
- `MODEL_CATALOG.md` — zaman duyarlı runtime (çalışma ortamı)/model kataloğu.
- `CLAUDE.md` — Claude Code için ince `AGENTS.md` köprüsü.
- `skills/` — Harness-owned (Harness'a ait), canonical (tek yetkili kaynak), on-demand (gerektiğinde) prosedürler.
- `i18n/` — yerelleştirilmiş README özetleri.

## Rules (kurallar) ve skills (beceriler): dört katman

| | Always-on | On-demand |
| --- | --- | --- |
| **Paylaşılan** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Projeye özel** | Projenin kendi rule/policy mekanizması | Projenin kendi skill'leri |

Harness ayrı bir `rules/` dizini sunmaz: paylaşılan always-on kural katmanının canonical kaynağı zaten `AGENTS.md`'dir; model yönlendirme politikası `MODEL_ROUTING.md`'dedir. İkinci bir always-on kaynak tekrar ve çelişki üretirdi.

Alan kuralları, ortam/deployment topolojisi, sağlayıcı/model tercihleri, ürün davranışı, iş kuralları ve altyapı yolları projeye özel kalır. Yeni bir rehberliğin hangi katmana ait olduğuna karar verirken `continuous-improvement` skill'indeki safeguard (koruyucu önlem) tercih yaklaşımını kullanın.

## Paylaşılan skills

Skill'ler göreve özgü prosedürlerdir; always-on policy değildir. Progressive disclosure (kademeli gösterim) yaklaşımında normalde yalnız keşif metadata'sı görünür; tam `SKILL.md` gövdesi yalnız görev gerçekten eşleştiğinde yüklenir.

Harness-owned skill'lerin canonical kaynağı `skills/` dizinidir ve ownership marker (sahiplik işareti) şudur:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Aynı isimli bir skill bu anahtarı taşımıyorsa Harness-owned değildir ve adoption (benimseme)/update sırasında üzerine yazılmaz.

v2 seti 14 skill içerir:

- `backup-and-recovery-review` — backup, restore ve recovery hazırlığı.
- `interface-qa` — web, mobil, desktop, CLI ve API arayüz doğrulaması.
- `calculation-model-validation` — formül ve karar modeli doğrulaması.
- `change-review` — tamamlanmış değişikliklerin risk ve regresyon incelemesi.
- `compatibility-and-rollout` — uyumluluk, migration, aşamalı yayına alma ve geri dönüş.
- `high-risk-change-review` — yüksek etkili değişikliklerde ek disiplin.
- `delegation-strategy` — doğrulanmış görev devri ve paralel çalışma kullanımı.
- `dependency-change` — dependency ekleme, kaldırma ve sürüm yükseltme incelemesi.
- `documentation-sync` — kalıcı dokümantasyonu gerçekle senkron tutma.
- `environment-release-safety` — release/deployment etkisi ve onay güvenliği.
- `continuous-improvement` — tekrarlanan hataları kalıcı koruyucu önlemlere dönüştürme.
- `root-cause-debug` — belirti yerine kök nedeni bulup kanıtlama.
- `secret-exposure-response` — secret ve credential açığa çıkmasına müdahale.
- `cross-surface-consistency` — çoklu yüzeylerde davranış tutarlılığı.

Set yaklaşık **20 skill veya altında** tutulmalıdır; `description` alanları **300 karakter veya daha kısa** olmalıdır.

Öncelik: **project-local (projeye özgü) rules/policy > paylaşılan `AGENTS.md` tabanı > shared skills**. Skill, approval boundary (onay sınırı), scope, runtime capability veya production/live safety kuralını gevşetemez.

## Adoption ve update

Operasyonel copy/paste prompt'lar tek canonical kaynakta tutulur ve çevrilmez:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

Adoption, runtime kullanımını repository kanıtından tespit eder; makinede CLI kurulu olması tek başına yeterli değildir. Doğrulanmış proje düzeyindeki skill yolları: Cursor/Antigravity/Codex için `.agents/skills/`, Claude Code için `.claude/skills/`; Cursor ayrıca `.claude/skills/` okuyabilir. Tek doğrulanmış root tüm kullanılan runtime'ları kapsıyorsa tek kopya kullanılır. Doğrulanamayan native activation (yerel etkinleştirme) için `harness/skills/` neutral fallback (tarafsız alternatif) olarak kullanılır ve native activation gerçekleşmiş gibi gösterilmez.

Herhangi bir skill yazılmadan önce tüm canonical isimler tüm hedef root'larda collision (ad çakışması) açısından taranır. Managed (yönetilen) mevcut skill değişecekse repo dışında byte-for-byte yedek alınır. Harness-owned kopyalar canonical kaynakla verbatim (birebir) tutulur. Update mevcut skill yerleşimini taşımaz; upstream'den kaldırılmış managed skill otomatik silinmez, orphaned (kaynakta olmayan) olarak raporlanır.

## Kaldırma ve test

Otomatik uninstaller yoktur. Yalnız `metadata.ai-engineering-harness` marker'ı taşıyan managed skill'ler kaldırılır; project-local skill/rule'lara dokunulmaz. Ayrıntı için [Remove the shared skills](../README.md#remove-the-shared-skills).

Kurulum testinde runtime native activation doğrulanamıyorsa agent skill'in aktif olduğunu söylememelidir. Alakasız bir görevde tüm skill gövdeleri context'e girmemeli; yalnız discovery metadata görünmelidir. Ayrıntı için [How to test an installation](../README.md#how-to-test-an-installation).

`SKILL.md` dosyaları çevrilmez; tek canonical İngilizce kopya korunur. Ayrıntılı bakım, adoption/update davranışı ve kapsam sınırları için [English README](../README.md) esas kaynaktır.
