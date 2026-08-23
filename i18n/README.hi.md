<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**भाषाएँ:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · **हिन्दी**

AI-सहायित सॉफ़्टवेयर विकास के लिए एक छोटा आधार, जिसमें vendor-neutral (प्रदाता-स्वतंत्र) दृष्टिकोण अपनाया गया है: एक पोर्टेबल नीति/संदर्भ परत और पुनः उपयोग योग्य प्रक्रियाओं का सीमित समूह। यह agent runtime (एजेंट निष्पादन परिवेश), orchestrator (समन्वयक), installer (स्थापना उपकरण) या framework (सॉफ़्टवेयर ढाँचा) नहीं है।

## फ़ाइलें

- `AGENTS.md` — साझा always-on (हमेशा सक्रिय) इंजीनियरिंग आधार।
- `MODEL_ROUTING.md` — स्थिर गुणवत्ता/लागत और capability tier (क्षमता स्तर) नीति।
- `MODEL_CATALOG.md` — समय के साथ बदलने वाला runtime (निष्पादन परिवेश)/मॉडल कैटलॉग।
- `CLAUDE.md` — Claude Code से `AGENTS.md` तक हल्का सेतु।
- `skills/` — Harness-owned (Harness के स्वामित्व वाली), canonical (एकमात्र प्रामाणिक स्रोत से आने वाली), on-demand (ज़रूरत पर लोड होने वाली) प्रक्रियाएँ।
- `i18n/` — README के स्थानीयकृत सारांश।

## नियम और कौशल: चार परतें

यहाँ rules (नियम) से आशय हमेशा लागू रहने वाले निर्देशों से है और skills (कौशल) से उन प्रक्रियाओं से है जो विशिष्ट कार्यों में उपयोग होती हैं।

| | हमेशा सक्रिय | ज़रूरत पर |
| --- | --- | --- |
| **साझा** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **प्रोजेक्ट-विशिष्ट** | प्रोजेक्ट का अपना नियम/नीति तंत्र | प्रोजेक्ट के अपने कौशल |

AI Engineering Harness अलग `rules/` डायरेक्टरी नहीं देता। साझा always-on (हमेशा सक्रिय) नियम परत का canonical source (एकमात्र प्रामाणिक स्रोत) पहले से `AGENTS.md` है, जबकि model routing (मॉडल रूटिंग) नीति `MODEL_ROUTING.md` में है। दूसरा हमेशा-सक्रिय स्रोत दोहराव और टकराव का जोखिम बढ़ाएगा।

Domain rules (डोमेन नियम), environment/deployment topology (परिवेश/डिप्लॉयमेंट टोपोलॉजी), vendor/model preferences (प्रदाता/मॉडल प्राथमिकताएँ), product behavior (उत्पाद व्यवहार), business rules (व्यावसायिक नियम) और infrastructure paths (इन्फ्रास्ट्रक्चर पथ) प्रोजेक्ट-विशिष्ट रहते हैं। नई मार्गदर्शिका किस परत में रखनी है, यह तय करने के लिए `continuous-improvement` कौशल के safeguard (स्थायी सुरक्षा उपाय) चयन दृष्टिकोण का उपयोग करें।

## साझा कौशल

Skills (कौशल) task-specific procedures (कार्य-विशिष्ट प्रक्रियाएँ) हैं, always-on policy (हमेशा सक्रिय नीति) नहीं। progressive disclosure (क्रमिक प्रदर्शन) में सामान्यतः केवल discovery metadata (खोज मेटाडेटा) दिखाई देती है; पूरा `SKILL.md` पाठ तभी लोड होता है जब वर्तमान कार्य वास्तव में मेल खाता हो।

Harness-owned skills (Harness के स्वामित्व वाले कौशल) का canonical source (एकमात्र प्रामाणिक स्रोत) `skills/` है। ownership marker (स्वामित्व चिह्न) यह है:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

इसी नाम का कोई skill (कौशल) यदि यह कुंजी नहीं रखता, तो वह Harness-owned (Harness के स्वामित्व वाला) नहीं है और adoption (स्थापना) या update (अद्यतन) के दौरान उसे overwrite (ऊपर से लिखना) नहीं किया जाता।

v2 में 14 कौशल हैं:

- `backup-and-recovery-review` — backup (बैकअप), restore (पुनर्स्थापन) और recovery (पुनर्प्राप्ति) की तैयारी।
- `interface-qa` — web, mobile, desktop, CLI और API इंटरफ़ेस सत्यापन।
- `calculation-model-validation` — सूत्रों और निर्णय मॉडलों का सत्यापन।
- `change-review` — पूरे हो चुके परिवर्तनों का review (समीक्षा), regression (प्रतिगमन) और जोखिम जाँच।
- `compatibility-and-rollout` — compatibility (अनुकूलता), migration (माइग्रेशन), rollout (चरणबद्ध जारी करना) और rollback (वापसी)।
- `high-risk-change-review` — उच्च-प्रभाव वाले परिवर्तनों के लिए अतिरिक्त अनुशासन।
- `delegation-strategy` — सत्यापित delegation (कार्य सौंपना) और parallelism (समानांतर निष्पादन) का सुरक्षित उपयोग।
- `dependency-change` — dependency (निर्भरता) जोड़ने, हटाने और upgrade (संस्करण उन्नयन) की समीक्षा।
- `documentation-sync` — दीर्घकालिक दस्तावेज़ को वास्तविक स्थिति के साथ समकालिक रखना।
- `environment-release-safety` — release (रिलीज़)/deployment (डिप्लॉयमेंट) प्रभाव और approval (अनुमोदन) सुरक्षा।
- `continuous-improvement` — दोहराई जाने वाली विफलताओं को स्थायी safeguards (सुरक्षा उपायों) में बदलना।
- `root-cause-debug` — root cause (मूल कारण) को पहचानना और प्रमाणित करना।
- `secret-exposure-response` — secrets (गोपनीय मान) और credentials (प्रमाण-पत्र) के exposure (उजागर होने) पर प्रतिक्रिया।
- `cross-surface-consistency` — कई surfaces (इंटरफ़ेस सतहों) में व्यवहार की एकरूपता।

साझा समूह को लगभग **20 कौशल या उससे कम** रखा जाना चाहिए; हर `description` **300 अक्षर या कम** होना चाहिए।

प्राथमिकता: **project-local rules/policy (प्रोजेक्ट-विशिष्ट नियम/नीति) > साझा `AGENTS.md` आधार > shared skills (साझा कौशल)**। कोई कौशल approval boundary (अनुमोदन सीमा), authorized scope (अधिकृत दायरा), runtime capability (निष्पादन परिवेश क्षमता) या production/live safety (प्रोडक्शन/लाइव सुरक्षा) को कमजोर नहीं कर सकता।

## स्थापना और अद्यतन

ऑपरेशनल copy/paste prompts (कॉपी/पेस्ट प्रॉम्प्ट) एक ही canonical source (प्रामाणिक स्रोत) में रखे जाते हैं और उनका मूल पाठ अनूदित नहीं किया जाता:

- [स्थापना प्रॉम्प्ट (अंग्रेज़ी)](../README.md#copypaste-adoption-prompt)
- [अद्यतन प्रॉम्प्ट (अंग्रेज़ी)](../README.md#copypaste-update-prompt)

Adoption (स्थापना) repository evidence (रिपॉज़िटरी साक्ष्य) से उपयोग हो रहे runtimes (निष्पादन परिवेशों) का पता लगाता है; मशीन पर CLI स्थापित होना अकेले पर्याप्त नहीं है। सत्यापित project-level skill paths (प्रोजेक्ट-स्तरीय कौशल पथ): Cursor/Antigravity/Codex के लिए `.agents/skills/` और Claude Code के लिए `.claude/skills/`; Cursor `.claude/skills/` भी पढ़ सकता है। यदि एक सत्यापित root (मूल डायरेक्टरी) सभी पाए गए परिवेशों को कवर करता है, तो केवल एक कॉपी उपयोग होती है। यदि native activation (मूल सक्रियण) सत्यापित नहीं किया जा सके, तो `harness/skills/` को neutral fallback (तटस्थ विकल्प) के रूप में उपयोग किया जाता है और मूल सक्रियण का दावा नहीं किया जाता।

किसी कौशल को लिखने से पहले सभी canonical names (प्रामाणिक स्रोत के नाम) को सभी target roots (लक्षित मूल डायरेक्टरियों) में collision (नाम टकराव) के लिए जाँचा जाता है। बदले जाने वाले managed files (प्रबंधित फ़ाइलों) का repository (रिपॉज़िटरी) के बाहर byte-for-byte (बाइट-दर-बाइट) बैकअप लिया जाता है। Harness-owned (Harness के स्वामित्व वाली) कॉपियाँ canonical source (प्रामाणिक स्रोत) से verbatim (हूबहू) रखी जाती हैं। update (अद्यतन) मौजूदा स्थान नहीं बदलता; upstream (ऊपरी स्रोत) से हटाया गया managed skill (प्रबंधित कौशल) अपने-आप नहीं मिटता, बल्कि orphaned (स्रोत में अनुपस्थित) के रूप में रिपोर्ट होता है।

## हटाना और परीक्षण

कोई automatic uninstaller (स्वचालित हटाने का उपकरण) नहीं है। केवल ownership marker (स्वामित्व चिह्न) `metadata.ai-engineering-harness` वाले managed skills (प्रबंधित कौशल) हटाए जाते हैं; project-local skills/rules (प्रोजेक्ट-विशिष्ट कौशल/नियम) को नहीं छुआ जाता। देखें [साझा कौशल हटाना (अंग्रेज़ी)](../README.md#remove-the-shared-skills)।

यदि native skill activation (कौशल का मूल सक्रियण) सत्यापित नहीं हो सके, तो agent (एजेंट) को यह दावा नहीं करना चाहिए कि कौशल active (सक्रिय) है। किसी असंबंधित कार्य में सभी skill bodies (कौशल पाठ) context (संदर्भ) में लोड नहीं होने चाहिए; केवल discovery metadata (खोज मेटाडेटा) दिखाई दे सकती है। देखें [स्थापना का परीक्षण (अंग्रेज़ी)](../README.md#how-to-test-an-installation)।

`SKILL.md` फ़ाइलें अनूदित नहीं की जातीं; केवल एक canonical English copy (एकमात्र प्रामाणिक अंग्रेज़ी प्रति) रखी जाती है। विस्तृत maintenance (रखरखाव), adoption/update behavior (स्थापना/अद्यतन व्यवहार) और scope boundaries (दायरा सीमाएँ) के लिए [अंग्रेज़ी README](../README.md) देखें।
