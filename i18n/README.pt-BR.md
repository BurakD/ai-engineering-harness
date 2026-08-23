<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Idiomas:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · **Português (Brasil)** · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Uma base mínima e neutra em relação a fornecedores para desenvolvimento de software assistido por IA: uma camada portátil de políticas/contexto mais um pequeno conjunto de procedimentos reutilizáveis. Não é um agent runtime (ambiente de execução de agentes), orquestrador, instalador nem framework.

## Arquivos

- `AGENTS.md` — baseline compartilhada de engenharia always-on (sempre ativa).
- `MODEL_ROUTING.md` — política estável de qualidade/custo e capability-tier (nível de capacidade).
- `MODEL_CATALOG.md` — catálogo de runtime (ambiente de execução)/modelos sensível ao tempo.
- `CLAUDE.md` — ponte mínima do Claude Code para `AGENTS.md`.
- `skills/` — procedimentos Harness-owned (pertencentes ao Harness), canonical (fonte autoritativa) e on-demand (sob demanda).
- `i18n/` — resumos localizados do README.

## Regras e skills (habilidades): quatro camadas

| | Always-on | On-demand |
| --- | --- | --- |
| **Compartilhada** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Específica do projeto** | Mecanismo próprio de regras/políticas | Skills próprios do projeto |

O Harness não distribui um diretório `rules/` separado: a fonte canonical da camada compartilhada always-on já é `AGENTS.md`, com a política de routing em `MODEL_ROUTING.md`. Uma segunda fonte always-on autoritativa criaria duplicação e risco de conflito.

Regras de domínio, topologia de ambientes/deployments, preferências de fornecedor/modelo, comportamento do produto, regras de negócio e caminhos de infraestrutura permanecem no projeto. Para decidir onde uma nova orientação deve ficar, use o skill `continuous-improvement` e sua abordagem de escolher o menor safeguard (proteção) durável adequado.

## Skills compartilhados

Skills são procedimentos específicos de tarefa, não política always-on. Com progressive disclosure (exposição gradual), normalmente apenas a metadata fica disponível para discovery; o corpo completo de `SKILL.md` é carregado quando a tarefa realmente corresponde ao skill.

A fonte canonical dos skills Harness-owned é `skills/`. O ownership marker (marcador de propriedade) é:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Um skill com o mesmo nome sem essa chave não pertence ao Harness e nunca deve ser sobrescrito durante adoption (adoção) ou update.

O conjunto v2 contém 14 skills:

- `backup-and-recovery-review` — prontidão de backup, restore e recovery.
- `interface-qa` — validação de interfaces web, mobile, desktop, CLI e API.
- `calculation-model-validation` — validação de fórmulas e modelos de decisão.
- `change-review` — revisão de mudanças concluídas, regressões e riscos.
- `compatibility-and-rollout` — compatibilidade, migração, liberação gradual e reversão.
- `high-risk-change-review` — disciplina extra para mudanças de alto impacto.
- `delegation-strategy` — uso seguro de delegação e paralelismo verificados.
- `dependency-change` — revisão de adição, remoção e atualização de dependências.
- `documentation-sync` — manter documentação durável alinhada à realidade.
- `environment-release-safety` — segurança de release/deployment e aprovações.
- `continuous-improvement` — transformar falhas recorrentes em proteções duráveis.
- `root-cause-debug` — identificar e comprovar a causa raiz.
- `secret-exposure-response` — resposta a exposição de segredos/credenciais.
- `cross-surface-consistency` — consistência de comportamento entre superfícies.

O conjunto deve permanecer em aproximadamente **20 skills ou menos**; cada `description` deve ter **300 caracteres ou menos**.

Precedência: **regras/política locais do projeto > baseline compartilhada de `AGENTS.md` > skills compartilhados**. Um skill nunca pode afrouxar limites de aprovação, escopo autorizado, capacidades do runtime ou segurança production/live.

## Adoption e update

Os prompts operacionais copy/paste ficam em uma única fonte canonical e não são traduzidos:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

A adoption detecta runtimes por evidência do repositório; um CLI instalado na máquina não basta. Caminhos de projeto verificados: `.agents/skills/` para Cursor, Antigravity e Codex; `.claude/skills/` para Claude Code. Cursor também lê `.claude/skills/`. Se uma única raiz verificada cobrir todos os runtimes detectados, usa-se uma única cópia. Se a native activation (ativação nativa) não puder ser verificada, usa-se `harness/skills/` como neutral fallback (alternativa neutra) e não se afirma ativação nativa.

Antes de escrever qualquer skill, todas as raízes-alvo são verificadas contra collisions (colisões) para todos os nomes canonical. Arquivos managed (gerenciados) que serão alterados recebem backup byte a byte fora do repositório. As cópias Harness-owned permanecem verbatim (idênticas) à fonte canonical. Update não move a instalação existente; um skill gerenciado removido upstream não é apagado automaticamente, é reportado como orphaned (sem equivalente upstream).

## Remoção e testes

Não há uninstaller automático. Apenas skills com `metadata.ai-engineering-harness` podem ser removidos como parte do Harness; regras e skills locais permanecem intactos. Veja [Remove the shared skills](../README.md#remove-the-shared-skills).

Se o runtime não permitir verificar ativação nativa, o agente não deve afirmar que o skill está ativo. Em tarefa não relacionada, os corpos dos skills irrelevantes não devem entrar no contexto; apenas metadata de discovery pode permanecer visível. Veja [How to test an installation](../README.md#how-to-test-an-installation).

Os arquivos `SKILL.md` não são traduzidos; existe uma única cópia canonical em inglês. Para manutenção detalhada, adoption/update e limites de escopo, consulte o [README em inglês](../README.md).
