# AI Engineering Harness

**Diller:** [English](README.md) · **Türkçe** · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

AI destekli yazılım geliştirme için minimal ve araçtan bağımsız bir temel.

AI kodlama araçları veya modeller arasında geçiş yapmak çoğu zaman projenin mühendislik bağlamını kaybetmek ve aynı şeyleri yeniden anlatmak anlamına gelir. AI Engineering Harness bunu önlemek için küçük, taşınabilir bir politika ve bağlam katmanı sağlar. Bir agent runtime'ı veya orkestratör değildir. Cursor, Claude Code, Codex ve Antigravity kendi yürütme ve orkestrasyon yeteneklerini sağlar; bu repository onların yanında çalışmak için tasarlanmıştır.

Harness üç pratik problemi çözmeyi amaçlar:

1. Araç veya model değiştirirken proje bağlamını ve mühendislik disiplinini kalıcı tutmak.
2. Daha güçlü reasoning'i yalnızca işin karmaşıklığı veya riski gerektirdiğinde kullanarak kalite ve maliyeti dengelemek.
3. Kısa ömürlü vendor model adlarını kararlı mühendislik politikasına sabitlemeden model/runtime seçimlerini güncel tutmak.

Yapı özellikle küçük tutulur. Zorunlu installer, orchestrator, model gateway veya projeye özel framework yoktur.

## Dosyalar

- `AGENTS.md` — uyumlu coding agent'lar için ortak mühendislik temeli.
- `MODEL_ROUTING.md` — kararlı FAST / STANDARD / REASONING / FRONTIER kalite-maliyet yönlendirme politikası.
- `MODEL_CATALOG.md` — zamanla değişen model/runtime kataloğu ve güncel başlangıç önerileri.
- `CLAUDE.md` — Claude Code'un `AGENTS.md` içeriğini kullanmasını sağlayan ince adapter.
- `README.md` — kurulum, güncelleme, test ve bakım rehberi.
- `LICENSE` — Apache License 2.0.
- `CONTRIBUTING.md` — katkı rehberi.

## Bu nedir, ne değildir?

Asıl ortak değer dosya düzeni değil politika içeriğidir: repository-first bağlam, model-routing tier'ları, fail-closed runtime capability yaklaşımı, etkisine göre insan onayı, scope disiplini, kalıcı handoff ve güvenli adoption/update davranışı.

Bu proje bir spec-driven workflow engine, multi-agent framework, runtime, rule-sync generator veya tool-native rule/skill mekanizmalarının yerine geçen bir sistem değildir. Tool-native özellikler runtime'a özel activation için kullanılmaya devam eder; Harness taşınabilir politikanın tek bir araca hapsolmasını önler.

## Runtime uyumluluğu ve native köprüler

`AGENTS.md`, bu repository'nin icat ettiği bir format değil, araçlar arasında kullanılabilen dış bir convention'dır. Doğrudan `AGENTS.md` okuyabilen runtime'lar Harness'a özel adapter gerektirmez.

Claude Code `CLAUDE.md` kullandığı için repository yalnızca minimal köprüyü içerir: `CLAUDE.md`, `@AGENTS.md` dosyasını import eder.

Antigravity'ye özgü `.agents/skills/` ve `.agents/workflows/` gibi yapılar tool-native ve project-local kalır. Harness bunları kopyalamaz, üretmez veya başka araçlara mirror etmez.

## Lisans

Proje **Apache License 2.0** ile açık kaynak olarak sunulur. Lisans koşulları çerçevesinde kullanabilir, değiştirebilir, yeniden dağıtabilir ve ticari olarak kullanabilirsiniz.

## 3 adımda mevcut projeye ekleme

1. Projeyi normalde çalıştığınız repository ve branch üzerinde açın.
2. İngilizce README'deki güncel adoption prompt'unu yetenekli bir coding agent'a verin.
3. Her şeyi kabul veya commit etmeden önce Git status, diff, backup konumları ve project-readiness bulgularını inceleyin.

Sırf Harness eklemek için yeni branch, worktree, proje kopyası, installer veya geçici clone oluşturmayın; yalnızca kullanıcı açıkça isterse veya repository politikası bunu gerektirirse izolasyon kullanın.

**Tam copy/paste adoption prompt'u:** [English README](README.md#copypaste-adoption-prompt)

## Temel ilkeler

### Model değişse de repository gerçeği yaşar

Yeni bir model veya agent, önceki chat geçmişine bağımlı olmadan repository'den mevcut durumu yeniden kurabilmelidir. Kod, testler, dokümantasyon, ADR'ler, CI/release convention'ları, repository-local talimatlar ve güncel Git durumu source of truth'tur.

### Ekle; yerine geçme

Harness mevcut projeyi kendi yapısına zorlamaz. `.cursor/rules/`, `.cursor/skills/`, `.agents/skills/`, `.agents/workflows/`, `.claude/skills/` ve benzeri tool-native varlıklar yerinde kalır. Shared truth yalnızca bir tool-native klasörde yaşamamalıdır; kalıcı bilgi docs, ADR, test, script, code/config ve `AGENTS.md` gibi herkesin okuyabildiği yerlere konmalıdır.

Bir runtime başka bir tool'un model/subagent/skill adını okuyabilir, ancak aktif session gerçekten desteklemiyorsa onu çağırabildiğini iddia edemez. Benzer niyeti mevcut gerçek capability ile korumak mümkündür; sahte cross-tool delegation yasaktır.

### Kararlı politika, güncellenebilir katalog

`MODEL_ROUTING.md` kararlı tier politikasını taşır. `MODEL_CATALOG.md` zaman duyarlıdır. Model adı, plan erişimi, fiyat, picker içeriği veya vendor sürümü değiştiğinde normalde katalog güncellenir; tier tanımları değiştirilmez. Aktif runtime gerçekte çağırabildiği şey konusunda son otoritedir.

### Projeye özel bilgi projede kalır

Ürün adları, iş kuralları, mimari kararlar, environment ayrıntıları, release prosedürleri, dil tercihleri, credentials ve domain bilgisi shared Harness repository'sine taşınmaz.

### Deterministic korumaları tercih et

Aynı kuralı güvenilir biçimde enforce edebiliyorsa test, type/schema constraint, analyzer, linter, build, CI check ve script'ler tekrar tekrar model yargısına tercih edilir.

### İnsan onayı araca göre değil etkiye göre belirlenir

Yüksek etkili işlemler Cursor, Claude Code, Codex, Antigravity, CLI, IDE veya başka bir agent üzerinden yapılmasına bakılmadan açık onay gerektirir. Environment isimleri varsayılmaz; customer-facing/live yayın sınırı işlemin etkisine göre değerlendirilir.

## Mevcut projeye adoption ayrıntıları

Önerilen yaklaşım: **incele, koru, backup al, sonra ekle — mevcut repository içinde**.

1. Mevcut repository ve branch'te kal.
2. Değişiklikten önce branch ve working-tree durumunu incele.
3. `AGENTS.md`, `CLAUDE.md`, tool-native rules/skills, docs, ADR, test, CI/release ve deployment dokümanlarını keşfet.
4. Environment/release topolojisini ve validation komutlarını repository kanıtından çıkar; isim veya akış uydurma.
5. Harness adoption için gerçekten gerekli fakat çözülemeyen bir bilgi varsa yalnızca odaklı soruyu sor; diğer belirsizlikleri Project readiness bölümünde raporla.
6. Değiştirilecek her mevcut dosyanın repository dışında byte-for-byte backup'ını al.
7. `AGENTS.md` yoksa shared dosyayı verbatim kopyala; varsa yalnızca belgelenmiş shared marker bloğunu ekle/güncelle.
8. Harness-owned `MODEL_ROUTING.md` ve `MODEL_CATALOG.md` dosyalarını upstream ile verbatim tut.
9. Claude Code kullanılıyorsa ince `CLAUDE.md` adapter'ını ekle; mevcut Claude-specific değeri koru.
10. Sırf Harness var diye `.ai/`, `.agents/`, installer, manifest, skill veya ekstra adapter oluşturma.
11. Project-local policy conflict'lerini sessizce düzeltme; raporla ve onay bekle.
12. Son diff'i incele; açık onay olmadan commit, push, deploy veya publish yapma.

## Kurulu Harness'ı güncelleme

Güncelleme yalnızca Harness-owned shared içeriği yeniler ve project-local değeri korur.

1. Target repository ile güncel upstream Harness'ı incele.
2. Uygulanan upstream commit'i kaydet.
3. Değiştirilecek mevcut dosyaların repository dışında byte-for-byte backup'ını al.
4. `AGENTS.md` shared marker'ları varsa yalnızca marker içini güncelle.
5. Harness-owned `MODEL_ROUTING.md` ve `MODEL_CATALOG.md` içeriklerini upstream'den verbatim yenile.
6. Catalog değişikliği nedeniyle project-local model tercihini otomatik değiştirme.
7. Gerekiyorsa yalnızca `CLAUDE.md` shared adapter kısmını yenile.
8. Runtime'lar arasında rule/skill/model mapping kopyalama veya senkronizasyon yapma.
9. Semantic conflict veya stale local rule'ları otomatik düzeltmek yerine raporla.
10. Exact diff'i incele ve uygulanabilir installation testlerini çalıştır.
11. Sırf Harness update için application code, deploy/release policy değiştirme; commit/push/deploy/publish yapma.

**Tam copy/paste update prompt'u:** [English README](README.md#copypaste-update-prompt)

## Manuel alternatif

Yeni bir projede `AGENTS.md` yoksa shared dosyalar normal dosya kopyalama yöntemiyle proje köküne alınabilir. `CLAUDE.md` yalnızca Claude Code kullanılacaksa gereklidir. Mevcut projede dosyaları körlemesine overwrite etmeyin; yukarıdaki backup ve preservation kurallarını uygulayın.

## Kurulumu test etme

Testleri önceki kurulum sohbetine bağımlı olmamak için **fresh agent session** üzerinde çalıştırın.

1. **Structural smoke test:** Agent repository kurallarını, Git durumunu, deployment/release topolojisini, routing tier'ını, catalog guidance'ını, validation komutlarını ve approval boundary'lerini doğru keşfetmeli.
2. **Real-task behavior test:** Küçük ama non-trivial bir işi önce yalnız analiz etmesini isteyin; mevcut implementasyonu ve kuralları incelemeden çözüm önermemeli.
3. **Approval-boundary test:** Customer-facing/live yayını tetikleyen bir repository işlemi varsa bunun explicit human approval gerektirdiğini söylemeli; yoksa production modeli uydurmamalı.
4. **Cross-tool runtime-capability test:** Her kullandığınız runtime'da fresh session açın. Agent yalnızca aktif runtime'ın gerçekten çağırabildiği model/agent/subagent/mode/delegation mekanizmalarını adlandırmalı; başka tool'un native mekanizmasını kendisininmiş gibi göstermemeli.

Exact test prompt'ları için: [English README — How to test an installation](README.md#how-to-test-an-installation)

## Model routing ve catalog bakımı

`MODEL_ROUTING.md` dört kararlı capability tier tanımlar:

- **FAST** — küçük/mekanik işler.
- **STANDARD** — normal implementation ve sınırlı düzeltmeler.
- **REASONING** — zor, belirsiz, mimari, security-sensitive, compatibility-sensitive veya release-sensitive işler.
- **FRONTIER** — istisnai en zor durumlar; yalnızca manual escalation.

`MODEL_CATALOG.md` runtime'a özgü güncel seçenekleri kaydeder ve daha sık değişmesi beklenir. Project-specific kurallar hassas bir alan için minimum tier'ı yükseltebilir veya başka güncel modeller seçebilir; bu override'lar shared catalog'da değil project-local olarak tutulur.

## AI hatalarından kalıcı öğrenme

Bir düzeltmenin tekrar önemli olması muhtemelse chat memory yerine kalıcı test/check, code/schema invariant, linter/build/CI rule veya project-local rule/documentation iyileştirmesi tercih edin.

## Bakım

Kararlı süreç `AGENTS.md` içinde, kararlı tier tanımları `MODEL_ROUTING.md` içinde, değişken runtime/model bilgisi `MODEL_CATALOG.md` içinde tutulur. Kurulu projeler ayrı bir sync mekanizması yerine upstream README'deki güncel update prosedürünü kullanır.

## Olası gelecek genişletmeleri

Templates, project overlays, reusable skills, additional adapters, automated installation ve orchestration ancak tekrar eden gerçek adoption maliyeti veya riski bunları gerekli kılarsa eklenmelidir. v1'de bilinçli olarak uygulanmamıştır.