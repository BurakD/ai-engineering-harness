# AI Engineering Harness

**भाषाएँ:** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · **हिन्दी**

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

AI-सहायित सॉफ़्टवेयर विकास के लिए एक न्यूनतम, vendor-neutral आधार।

AI coding tools या models के बीच बदलने पर अक्सर project का engineering context खो जाता है और वही बातें फिर से समझानी पड़ती हैं। AI Engineering Harness एक छोटा, portable policy/context layer है जो इसे रोकता है। यह agent runtime या orchestrator नहीं है; Cursor, Claude Code, Codex और Antigravity अपनी execution और orchestration क्षमताएँ स्वयं प्रदान करते हैं।

## यह किन समस्याओं को हल करता है

1. Tool या model बदलते समय project context और engineering discipline को बनाए रखना।
2. अधिक शक्तिशाली reasoning केवल तभी उपयोग करना जब complexity या risk इसकी आवश्यकता को उचित ठहराए, ताकि quality और cost में संतुलन रहे।
3. Stable engineering policy में अल्पकालिक model names hard-code किए बिना model/runtime choices को वर्तमान रखना।

## फ़ाइलें

- `AGENTS.md` — compatible coding agents के लिए shared engineering baseline।
- `MODEL_ROUTING.md` — स्थिर FAST / STANDARD / REASONING / FRONTIER policy।
- `MODEL_CATALOG.md` — समय के साथ बदलने वाला model/runtime catalog और वर्तमान recommendations।
- `CLAUDE.md` — Claude Code द्वारा `AGENTS.md` import करने के लिए minimal adapter।
- `README.md` — adoption, update, testing और maintenance का मुख्य guide।

## यह क्या है — और क्या नहीं है

मुख्य value policy content में है: repository-first context, routing tiers, runtime capability की fail-closed verification, प्रभाव के आधार पर human approval, scope discipline, durable handoff और सुरक्षित adoption/update।

यह workflow engine, multi-agent framework, runtime, rule-sync generator या tool-native rules/skills का replacement नहीं है।

## Compatibility

`AGENTS.md` इस repository द्वारा बनाया गया निजी format नहीं, बल्कि एक बाहरी cross-tool convention है। जो runtimes इसे सीधे पढ़ते हैं उन्हें Harness-specific adapter की आवश्यकता नहीं होती। Claude Code `CLAUDE.md` उपयोग करता है, इसलिए repository केवल minimal `@AGENTS.md` bridge रखता है। Antigravity-specific `.agents/skills/` और `.agents/workflows/` जैसी व्यवस्थाएँ project-local रहती हैं।

## किसी मौजूदा project में adoption

1. वर्तमान repository और branch में ही रहें।
2. बदलाव से पहले किसी सक्षम agent से rules, docs, Git state, deployment topology और validation commands inspect कराएँ।
3. किसी existing file को बदलने से पहले repository के बाहर उसका byte-for-byte backup बनाएँ।
4. सभी project-specific content को सुरक्षित रखें और केवल shared Harness content जोड़ें।
5. केवल Harness अपनाने के लिए branch, worktree, installer, manifest, adapter या sync mechanism न बनाएँ।
6. Explicit approval के बिना commit, push, deploy या publish न करें।

**पूरा adoption prompt:** [English README](README.md#copypaste-adoption-prompt)

## Update

Update केवल Harness-owned shared content को refresh करता है। `AGENTS.md`, `MODEL_ROUTING.md`, `MODEL_CATALOG.md` और `CLAUDE.md` के shared हिस्से upstream से update किए जाते हैं, जबकि project-local rules, models, skills, docs, code और uncommitted work सुरक्षित रहते हैं।

**पूरा update prompt:** [English README](README.md#copypaste-update-prompt)

## मुख्य सिद्धांत

- Repository की सच्चाई model या agent बदलने के बाद भी बनी रहनी चाहिए।
- Replace नहीं, add करें: tool-native rules वहीं रहें जहाँ वे पहले से हैं।
- `MODEL_ROUTING.md` स्थिर है; `MODEL_CATALOG.md` जानबूझकर time-sensitive है।
- वास्तव में कौन से models/agents invoke किए जा सकते हैं, इस पर active runtime अंतिम authority है।
- किसी problem को discover करना requested scope के बाहर उसे fix करने की authorization नहीं देता।
- High-impact actions को tool या environment name के आधार पर नहीं, उनके वास्तविक प्रभाव के आधार पर human approval चाहिए।
- यदि tests, linters, types, CI और अन्य deterministic safeguards वही rule विश्वसनीय रूप से enforce कर सकते हैं, तो उन्हें बार-बार होने वाले model judgment पर प्राथमिकता दें।

## Installation testing

नई sessions में structural smoke test, real-task behavior test, approval-boundary test और cross-tool runtime-capability test चलाएँ। Agent को context सही तरह discover करना चाहिए और active runtime जिस capability को verify नहीं कर सकता उसका दावा नहीं करना चाहिए।

Exact prompts: [How to test an installation](README.md#how-to-test-an-installation)

## License

**Apache License 2.0** के तहत open source।