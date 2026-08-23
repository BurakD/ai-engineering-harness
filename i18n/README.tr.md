<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Diller:** [English](../README.md) · **Türkçe** · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

AI destekli yazılım geliştirme için minimal, vendor-neutral (sağlayıcıdan bağımsız) bir politika/bağlam katmanı ve küçük bir yeniden kullanılabilir prosedür kümesidir. Bir agent runtime (ajan çalışma ortamı), orchestrator (orkestrasyon sistemi), installer (kurulum aracı) veya framework (yazılım çerçevesi) değildir.

## Dosyalar

- `AGENTS.md` — paylaşılan always-on (sürekli etkin) mühendislik tabanı.
- `MODEL_ROUTING.md` — kararlı kalite/maliyet ve capability tier (yetenek seviyesi) politikası.
- `MODEL_CATALOG.md` — zamanla değişen runtime (çalışma ortamı)/model kataloğu.
- `CLAUDE.md` — Claude Code için `AGENTS.md` dosyasına yönlendiren ince köprü.
- `skills/` — Harness-owned (Harness'a ait), canonical (tek yetkili kaynaktan gelen), on-demand (gerektiğinde yüklenen) prosedürler.
- `i18n/` — yerelleştirilmiş README özetleri.

## Kurallar ve beceriler: dört katman

Burada rules (kurallar) sürekli geçerli yönlendirmeyi, skills (beceriler) ise belirli görevlerde kullanılan prosedürleri ifade eder.

| | Sürekli etkin | Gerektiğinde |
| --- | --- | --- |
| **Paylaşılan** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Projeye özel** | Projenin kendi kural/politika mekanizması | Projenin kendi becerileri |

AI Engineering Harness ayrı bir `rules/` dizini sunmaz: paylaşılan always-on (sürekli etkin) kural katmanının canonical source (tek yetkili kaynak) zaten `AGENTS.md`'dir; model routing (model yönlendirme) politikası `MODEL_ROUTING.md`'dedir. İkinci bir sürekli etkin kaynak tekrar ve çelişki riski doğururdu.

Domain rules (alan kuralları), environment/deployment topology (ortam/dağıtım topolojisi), vendor/model preferences (sağlayıcı/model tercihleri), product behavior (ürün davranışı), business rules (iş kuralları) ve infrastructure paths (altyapı yolları) projeye özel kalır. Yeni bir rehberliğin hangi katmana ait olduğuna karar verirken `continuous-improvement` becerisindeki safeguard (koruyucu önlem) tercih yaklaşımını kullanın.

## Paylaşılan beceriler

Skills (beceriler), task-specific procedures (göreve özgü prosedürler) olup always-on policy (sürekli etkin politika) değildir. Progressive disclosure (kademeli gösterim) yaklaşımında normalde yalnız discovery metadata (keşif üst verisi) görünür; tam `SKILL.md` gövdesi yalnız görev gerçekten eşleştiğinde yüklenir.

Harness-owned skills (Harness'a ait beceriler) için canonical source (tek yetkili kaynak) `skills/` dizinidir. Ownership marker (sahiplik işareti) şudur:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Aynı isimli bir skill (beceri) bu anahtarı taşımıyorsa Harness-owned (Harness'a ait) değildir ve adoption (kurulum) ya da update (güncelleme) sırasında üzerine yazılmaz.

v2 kümesi 14 beceri içerir:

- `backup-and-recovery-review` — backup (yedekleme), restore (geri yükleme) ve recovery (kurtarma) hazırlığı.
- `interface-qa` — web, mobil, masaüstü, CLI ve API arayüz doğrulaması.
- `calculation-model-validation` — formül ve karar modeli doğrulaması.
- `change-review` — tamamlanmış değişikliklerin risk ve regresyon incelemesi.
- `compatibility-and-rollout` — compatibility (uyumluluk), migration (geçiş), rollout (aşamalı yayına alma) ve rollback (geri dönüş).
- `high-risk-change-review` — yüksek etkili değişikliklerde ek disiplin.
- `delegation-strategy` — delegation (görev devri) ve parallelism (paralel çalışma) kullanımının doğrulanması.
- `dependency-change` — dependency (bağımlılık) ekleme, kaldırma ve upgrade (sürüm yükseltme) incelemesi.
- `documentation-sync` — kalıcı dokümantasyonu gerçekle senkron tutma.
- `environment-release-safety` — release (yayın)/deployment (dağıtım) etkisi ve approval (onay) güvenliği.
- `continuous-improvement` — tekrarlanan hataları kalıcı safeguard'lara (koruyucu önlemlere) dönüştürme.
- `root-cause-debug` — belirti yerine root cause'u (kök nedeni) bulup kanıtlama.
- `secret-exposure-response` — secret (sır) ve credential (kimlik bilgisi) exposure'ına (açığa çıkmasına) müdahale.
- `cross-surface-consistency` — birden çok surface'te (arayüzde) davranış tutarlılığı.

Paylaşılan küme yaklaşık **20 beceri veya altında** tutulmalıdır; `description` alanları **300 karakter veya daha kısa** olmalıdır.

Öncelik: **project-local rules/policy (projeye özgü kurallar/politika) > paylaşılan `AGENTS.md` tabanı > shared skills (paylaşılan beceriler)**. Bir beceri; approval boundary (onay sınırı), authorized scope (yetkili kapsam), runtime capability (çalışma ortamı yeteneği) veya production/live safety (üretim/canlı sistem güvenliği) kuralını gevşetemez.

## Kurulum ve güncelleme

Operasyonel copy/paste prompts (kopyala/yapıştır prompt'ları) tek canonical source'ta (tek yetkili kaynakta) tutulur ve çevrilmez:

- [Kurulum prompt'u (İngilizce)](../README.md#copypaste-adoption-prompt)
- [Güncelleme prompt'u (İngilizce)](../README.md#copypaste-update-prompt)

Adoption (kurulum), runtime (çalışma ortamı) kullanımını repository evidence'dan (kod deposu kanıtından) tespit eder; makinede CLI kurulu olması tek başına yeterli değildir. Doğrulanmış project-level skill paths (proje düzeyindeki beceri yolları): Cursor/Antigravity/Codex için `.agents/skills/`, Claude Code için `.claude/skills/`; Cursor ayrıca `.claude/skills/` okuyabilir. Tek doğrulanmış root (kök dizin) tüm kullanılan çalışma ortamlarını kapsıyorsa tek kopya kullanılır. Doğrulanamayan native activation (yerel etkinleştirme) için `harness/skills/` neutral fallback (tarafsız alternatif) olarak kullanılır ve yerel etkinleştirmenin gerçekleştiği iddia edilmez.

Herhangi bir beceri yazılmadan önce tüm canonical names (tek yetkili kaynak adları), tüm target roots'ta (hedef kök dizinlerde) collision (ad çakışması) açısından taranır. Managed (yönetilen) mevcut beceri değişecekse repository (kod deposu) dışında byte-for-byte (bayt bayt birebir) yedek alınır. Harness-owned (Harness'a ait) kopyalar canonical source (tek yetkili kaynak) ile verbatim (birebir) tutulur. Update (güncelleme) mevcut beceri yerleşimini taşımaz; upstream'den (üst kaynaktan) kaldırılmış managed skill (yönetilen beceri) otomatik silinmez, orphaned (kaynakta olmayan) olarak raporlanır.

## Kaldırma ve test

Otomatik uninstaller (kaldırma aracı) yoktur. Yalnız `metadata.ai-engineering-harness` ownership marker'ını (sahiplik işaretini) taşıyan managed skills (yönetilen beceriler) kaldırılır; project-local skills/rules'a (projeye özgü beceri/kurallara) dokunulmaz. Ayrıntı için [Paylaşılan becerileri kaldırma (İngilizce)](../README.md#remove-the-shared-skills).

Kurulum testinde native skill activation (yerel beceri etkinleştirmesi) doğrulanamıyorsa agent (ajan), becerinin active (etkin) olduğunu söylememelidir. Alakasız bir görevde tüm skill bodies (beceri gövdeleri) context'e (bağlama) girmemeli; yalnız discovery metadata (keşif üst verisi) görünmelidir. Ayrıntı için [Kurulumu test etme (İngilizce)](../README.md#how-to-test-an-installation).

`SKILL.md` dosyaları çevrilmez; tek canonical English copy (tek yetkili İngilizce kopya) korunur. Ayrıntılı maintenance (bakım), adoption/update behavior (kurulum/güncelleme davranışı) ve scope boundaries (kapsam sınırları) için [İngilizce README](../README.md) esas kaynaktır.
