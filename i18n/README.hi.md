<!-- Based on README.md @ v2.0.3 -->
# AI Engineering Harness

भाषाएँ: [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · हिन्दी

AI-सहायित सॉफ़्टवेयर विकास के लिए एक न्यूनतम और प्रदाता-स्वतंत्र (vendor-neutral) नीति/संदर्भ परत और पुनः उपयोग योग्य प्रक्रियाओं का छोटा समूह। यह agent runtime (एजेंट निष्पादन परिवेश), orchestrator (समन्वय प्रणाली), installer (स्थापना उपकरण) या framework (सॉफ़्टवेयर ढाँचा) नहीं है।

## आपको क्या मिलता है

- अलग-अलग tools (उपकरणों) में एक engineering baseline (इंजीनियरिंग आधार)। Cursor, Claude Code, Codex और Antigravity एक ही project context (प्रोजेक्ट संदर्भ) और constraints (सीमाएँ) पढ़ते हैं, इसलिए tool बदलने का मतलब प्रोजेक्ट को फिर से समझाना नहीं है।
- Model choice (मॉडल चयन) आदत नहीं, जोखिम से जुड़ा है। काम capability tiers (क्षमता स्तरों) में वर्गीकृत होता है और सबसे कम पर्याप्त स्तर से शुरू होता है। यह enforcement (तकनीकी बाध्यता) नहीं, policy (नीति) है; वास्तविक बचत active runtime (सक्रिय निष्पादन परिवेश) और आपकी योजना पर निर्भर करती है।
- उन कामों के लिए तैयार प्रक्रियाएँ जिनमें गलती महँगी पड़ती है। Secret exposure (गोपनीय मान का खुलासा), releases (रिलीज़), dependency changes (निर्भरता परिवर्तन), high-risk changes (उच्च-जोखिम परिवर्तन) और recovery (पुनर्प्राप्ति) के लिए साझा प्रक्रियाएँ हैं, और कोई भी प्रक्रिया approval boundary (अनुमोदन सीमा) को कमजोर नहीं कर सकती।
- Discovery (खोज) authorization (अधिकृत अनुमति) नहीं है। कोई agent (एजेंट) अपनी task (कार्य) सीमा से बाहर समस्या देखता है तो वह खुद से ठीक करने के बजाय रिपोर्ट करता है और निर्णय की प्रतीक्षा करता है।
- Capabilities (क्षमताओं) पर fail closed (सत्यापन न हो तो अनुपलब्ध मानना)। Agent किसी model (मॉडल), subagent (उप-एजेंट) या skill activation (कौशल सक्रियण) का दावा नहीं कर सकता जिसे active runtime वास्तव में उपलब्ध नहीं करा सकता।
- Context (संदर्भ) छोटा रहता है। साझा प्रक्रियाएँ हर session (सत्र) को भरने के बजाय तभी लोड होती हैं जब task उनसे मेल खाता है।
- Low lock-in (कम निर्भरता)। आपके repository (रिपॉज़िटरी) में Markdown, बिना installer, runtime या service (सेवा) के। Adoption (स्थापना) और removal (हटाना) दस्तावेज़ित प्रक्रियाएँ हैं, एकतरफा रास्ता नहीं।

## फ़ाइलें

- `AGENTS.md` — साझा always-on (हमेशा सक्रिय) इंजीनियरिंग आधार।
- `MODEL_ROUTING.md` — स्थिर गुणवत्ता/लागत और capability tier (क्षमता स्तर) नीति।
- `MODEL_CATALOG.md` — समय के साथ बदलने वाला runtime (निष्पादन परिवेश) और मॉडल कैटलॉग।
- `CLAUDE.md` — Claude Code से `AGENTS.md` तक हल्का सेतु।
- `skills/` — Harness-owned (Harness के स्वामित्व वाले), canonical (एकमात्र प्रामाणिक) स्रोत से आने वाली और on-demand (ज़रूरत पर लोड होने वाली) प्रक्रियाएँ।
- `i18n/` — `README.md` के स्थानीयकृत सारांश।

## Rules (नियम) और skills (कौशल): चार परतें

Rules वे निर्देश हैं जो लगातार लागू रहते हैं; skills वे प्रक्रियाएँ हैं जो विशिष्ट कार्यों में सक्रिय होती हैं।

| | Always-on (हमेशा सक्रिय) | On-demand (ज़रूरत पर) |
| --- | --- | --- |
| साझा | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| प्रोजेक्ट-विशिष्ट | प्रोजेक्ट का अपना rules/policy तंत्र | प्रोजेक्ट के अपने skills |

Harness अलग `rules/` डायरेक्टरी नहीं देता: साझा always-on नियम परत का canonical source (एकमात्र प्रामाणिक स्रोत) पहले से `AGENTS.md` है, जबकि मॉडल रूटिंग नीति `MODEL_ROUTING.md` में है। दूसरा always-on स्रोत दोहराव और टकराव का जोखिम पैदा करेगा।

डोमेन नियम, परिवेश और deployment (डिप्लॉयमेंट) टोपोलॉजी, प्रदाता/मॉडल प्राथमिकताएँ, उत्पाद व्यवहार, व्यावसायिक नियम और इन्फ्रास्ट्रक्चर पथ प्रोजेक्ट-विशिष्ट रहते हैं। नई मार्गदर्शिका किस परत में होनी चाहिए, यह तय करने के लिए `continuous-improvement` skill में सबसे छोटे स्थायी safeguard (सुरक्षा उपाय) को चुनने वाला दृष्टिकोण अपनाएँ।

## साझा skills (कौशल)

Skills कार्य-विशिष्ट प्रक्रियाएँ हैं, always-on policy नहीं। progressive disclosure (क्रमिक प्रदर्शन) में सामान्यतः केवल discovery metadata (खोज मेटाडेटा) दिखाई देती है; पूरा `SKILL.md` पाठ तभी लोड होता है जब कार्य वास्तव में मेल खाता हो।

Harness-owned skills का canonical source `skills/` है और ownership marker (स्वामित्व चिह्न) यह है:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

इसी नाम का कोई skill यदि यह कुंजी नहीं रखता, तो वह Harness-owned नहीं है; adoption (स्थापना) या update (अद्यतन) के दौरान उसे ऊपर से नहीं लिखा जाता।

v2 में 14 skills हैं:

- `backup-and-recovery-review` — backup (बैकअप), restore (पुनर्स्थापन) और recovery (पुनर्प्राप्ति) तैयारी की समीक्षा।
- `interface-qa` — web, mobile, desktop, CLI और API इंटरफ़ेस सत्यापन।
- `calculation-model-validation` — सूत्रों और निर्णय मॉडलों का सत्यापन।
- `change-review` — पूरे हो चुके परिवर्तनों में regression (प्रतिगमन) और जोखिम की समीक्षा।
- `compatibility-and-rollout` — अनुकूलता, migration (डेटा/स्कीमा माइग्रेशन), rollout (चरणबद्ध जारी करना) और rollback (वापसी)।
- `high-risk-change-review` — उच्च-प्रभाव वाले परिवर्तनों के लिए अतिरिक्त अनुशासन।
- `delegation-strategy` — सत्यापित delegation (कार्य सौंपना) और समानांतर कार्य का उपयोग।
- `dependency-change` — dependency (निर्भरता) जोड़ने, हटाने और संस्करण उन्नयन की समीक्षा।
- `documentation-sync` — दीर्घकालिक दस्तावेज़ को वास्तविक स्थिति के साथ समकालिक रखना।
- `environment-release-safety` — release (रिलीज़) और deployment (डिप्लॉयमेंट) प्रभाव तथा अनुमोदन सुरक्षा।
- `continuous-improvement` — दोहराई जाने वाली त्रुटियों को स्थायी safeguards (सुरक्षा उपायों) में बदलना।
- `root-cause-debug` — लक्षण के बजाय मूल कारण को ढूँढना और प्रमाणित करना।
- `secret-exposure-response` — secret (गोपनीय मान) और credential (प्रमाण-पत्र) के रिसाव पर प्रतिक्रिया।
- `cross-surface-consistency` — कई इंटरफ़ेस में व्यवहार की एकरूपता।

साझा समूह को लगभग 20 skills या उससे कम रखा जाना चाहिए; `description` फ़ील्ड 300 अक्षर या कम होने चाहिए।

प्राथमिकता क्रम: प्रोजेक्ट-विशिष्ट rules/policy > साझा `AGENTS.md` आधार > साझा skills। कोई skill approval boundary (अनुमोदन सीमा), authorized scope (अधिकृत दायरा), runtime capability (निष्पादन परिवेश क्षमता) या production/live safety (प्रोडक्शन/लाइव सुरक्षा) नियमों को कमजोर नहीं कर सकता।

## Adoption (स्थापना) और update (अद्यतन)

कॉपी/पेस्ट prompts एक ही canonical source में रखे जाते हैं और अनूदित नहीं किए जाते:

- [स्थापना prompt (अंग्रेज़ी)](../README.md#copypaste-adoption-prompt)
- [अद्यतन prompt (अंग्रेज़ी)](../README.md#copypaste-update-prompt)

Adoption repository evidence (रिपॉज़िटरी के साक्ष्य) से उपयोग हो रहे runtimes का पता लगाता है; मशीन पर CLI स्थापित होना अकेले पर्याप्त नहीं है। सत्यापित प्रोजेक्ट-स्तरीय skill पथ ये हैं: Cursor, Antigravity और Codex के लिए `.agents/skills/`; Claude Code के लिए `.claude/skills/`। Cursor `.claude/skills/` भी पढ़ सकता है। यदि एक सत्यापित root (मूल डायरेक्टरी) सभी उपयोग हो रहे runtimes को कवर करता है, तो केवल एक कॉपी उपयोग होती है। यदि native activation (मूल सक्रियण) सत्यापित नहीं किया जा सके, तो `harness/skills/` को neutral fallback (तटस्थ विकल्प) के रूप में उपयोग किया जाता है और यह दावा नहीं किया जाता कि native activation हो गया है।

किसी भी skill को लिखने से पहले सभी canonical नामों को सभी लक्षित roots में collision (नाम टकराव) के लिए जाँचा जाता है। यदि किसी managed (प्रबंधित) skill को बदला जाना है, तो repository के बाहर byte-for-byte (बाइट-दर-बाइट समान) बैकअप लिया जाता है। Harness-owned कॉपियाँ canonical स्रोत के साथ verbatim (हूबहू) रखी जाती हैं। Update मौजूदा skill स्थान को नहीं बदलता; upstream (ऊपरी स्रोत) से हटाया गया managed skill अपने-आप नहीं हटता, बल्कि orphaned (स्रोत में अनुपस्थित) के रूप में रिपोर्ट होता है।

## हटाना और परीक्षण

कोई स्वचालित uninstaller (हटाने का उपकरण) नहीं है। केवल `metadata.ai-engineering-harness` स्वामित्व चिह्न वाले managed skills हटाए जाते हैं; प्रोजेक्ट-विशिष्ट skills और rules को नहीं छुआ जाता। देखें [साझा skills हटाना (अंग्रेज़ी)](../README.md#remove-the-shared-skills)।

यदि स्थापना परीक्षण में native activation सत्यापित नहीं हो सके, तो agent को यह दावा नहीं करना चाहिए कि skill सक्रिय है। असंबंधित कार्य में skill निकाय context (संदर्भ) में लोड नहीं होने चाहिए; केवल discovery metadata दिखाई देनी चाहिए। देखें [स्थापना का परीक्षण (अंग्रेज़ी)](../README.md#how-to-test-an-installation)।

`SKILL.md` फ़ाइलें अनूदित नहीं की जातीं; एक canonical अंग्रेज़ी कॉपी रखी जाती है। विस्तृत रखरखाव, adoption/update व्यवहार और दायरा सीमाओं के लिए [अंग्रेज़ी `README.md`](../README.md) मुख्य स्रोत है।
