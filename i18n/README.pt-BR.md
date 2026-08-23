<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Idiomas:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · **Português (Brasil)** · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Uma base mínima para desenvolvimento de software assistido por AI, com abordagem vendor-neutral (independente de fornecedor): uma camada portátil de políticas/contexto e um pequeno conjunto de procedimentos reutilizáveis. Não é um agent runtime (ambiente de execução de agentes), um orchestrator (orquestrador), um installer (instalador) nem um framework (arcabouço de software).

## Arquivos

- `AGENTS.md` — base compartilhada de engenharia, always-on (sempre ativa).
- `MODEL_ROUTING.md` — política estável de qualidade/custo e capability tier (nível de capacidade).
- `MODEL_CATALOG.md` — catálogo de runtime (ambientes de execução)/modelos sensível ao tempo.
- `CLAUDE.md` — ponte leve do Claude Code para `AGENTS.md`.
- `skills/` — procedimentos Harness-owned (pertencentes ao Harness), canonical (vindos da fonte autorizada) e on-demand (carregados sob demanda).
- `i18n/` — resumos localizados do README.

## Regras e habilidades: quatro camadas

Aqui, rules (regras) significa orientação de aplicação contínua e skills (habilidades) significa procedimentos usados em tarefas específicas.

| | Sempre ativa | Sob demanda |
| --- | --- | --- |
| **Compartilhada** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Específica do projeto** | Mecanismo próprio de regras/políticas | Habilidades próprias do projeto |

O AI Engineering Harness não distribui um diretório `rules/` separado: a camada compartilhada always-on (sempre ativa) já tem sua canonical source (fonte autorizada única) em `AGENTS.md`, enquanto a política de model routing (roteamento de modelos) está em `MODEL_ROUTING.md`. Uma segunda fonte sempre ativa criaria duplicação e risco de conflito.

As domain rules (regras de domínio), a environment/deployment topology (topologia de ambientes/deployments), as vendor/model preferences (preferências de fornecedor/modelo), o product behavior (comportamento do produto), as business rules (regras de negócio) e os infrastructure paths (caminhos de infraestrutura) permanecem no projeto. Para decidir em qual camada uma nova orientação deve ficar, use a abordagem de safeguard (proteção durável) do skill `continuous-improvement`.

## Habilidades compartilhadas

Skills (habilidades) são task-specific procedures (procedimentos específicos de tarefa), não uma always-on policy (política sempre ativa). Com progressive disclosure (revelação progressiva), normalmente apenas a discovery metadata (metadados de descoberta) fica visível; o corpo completo de `SKILL.md` é carregado apenas quando a tarefa realmente corresponde.

A canonical source (fonte autorizada única) dos Harness-owned skills (habilidades pertencentes ao Harness) é `skills/`. O ownership marker (marcador de propriedade) é:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Um skill (habilidade) com o mesmo nome sem essa chave não é Harness-owned (pertencente ao Harness) e nunca é sobrescrito durante adoption (instalação) ou update (atualização).

O conjunto v2 contém 14 habilidades:

- `backup-and-recovery-review` — prontidão de backup (cópia de segurança), restore (restauração) e recovery (recuperação).
- `interface-qa` — validação de interfaces web, mobile, desktop, CLI e API.
- `calculation-model-validation` — validação de fórmulas e modelos de decisão.
- `change-review` — revisão de mudanças concluídas, regressões e riscos.
- `compatibility-and-rollout` — compatibility (compatibilidade), migration (migração), rollout (liberação gradual) e rollback (reversão).
- `high-risk-change-review` — disciplina extra para mudanças de alto impacto.
- `delegation-strategy` — uso seguro de delegation (delegação) e parallelism (paralelismo) verificados.
- `dependency-change` — revisão de adição, remoção e upgrades (atualizações de versão) de dependencies (dependências).
- `documentation-sync` — manter documentação durável alinhada à realidade.
- `environment-release-safety` — segurança de release (publicação)/deployment (implantação) e de approval (aprovação).
- `continuous-improvement` — transformar falhas recorrentes em safeguards (proteções duráveis).
- `root-cause-debug` — identificar e comprovar a root cause (causa raiz).
- `secret-exposure-response` — resposta à exposure (exposição) de secrets (segredos) e credentials (credenciais).
- `cross-surface-consistency` — consistência de comportamento entre surfaces (superfícies) equivalentes.

O conjunto compartilhado deve permanecer em aproximadamente **20 habilidades ou menos**; cada `description` deve ter **300 caracteres ou menos**.

Precedência: **project-local rules/policy (regras/política locais do projeto) > base compartilhada de `AGENTS.md` > shared skills (habilidades compartilhadas)**. Um skill não pode afrouxar um approval boundary (limite de aprovação), o authorized scope (escopo autorizado), as runtime capabilities (capacidades do ambiente de execução) nem a production/live safety (segurança em produção/ao vivo).

## Instalação e atualização

Os copy/paste prompts (prompts para copiar/colar) operacionais ficam em uma única canonical source (fonte autorizada) e não são traduzidos:

- [Prompt de instalação (em inglês)](../README.md#copypaste-adoption-prompt)
- [Prompt de atualização (em inglês)](../README.md#copypaste-update-prompt)

A adoption (instalação) detecta o uso de runtime (ambientes de execução) a partir de repository evidence (evidência do repositório); ter um CLI instalado não basta. Caminhos project-level (em nível de projeto) verificados para skills: `.agents/skills/` em Cursor/Antigravity/Codex e `.claude/skills/` em Claude Code; Cursor também lê `.claude/skills/`. Se um único root (diretório raiz) verificado cobrir todos os ambientes detectados, usa-se uma só cópia. Se a native activation (ativação nativa) não puder ser verificada, `harness/skills/` é usado como neutral fallback (alternativa neutra) e não se afirma ativação nativa.

Antes de escrever qualquer habilidade, todos os canonical names (nomes da fonte autorizada) são verificados em todos os target roots (diretórios raiz de destino) para collision (colisões de nomes). Qualquer arquivo managed (gerenciado) que será alterado recebe backup byte-for-byte (byte por byte) fora do repository (repositório). As cópias Harness-owned (pertencentes ao Harness) permanecem verbatim (idênticas) à canonical source (fonte autorizada). Um update (atualização) não move a instalação existente; um managed skill (habilidade gerenciada) removido upstream (na fonte superior) não é apagado automaticamente e é reportado como orphaned (ausente da fonte).

## Remoção e testes

Não há uninstaller (desinstalador) automático. Apenas os managed skills (habilidades gerenciadas) que levam o ownership marker (marcador de propriedade) `metadata.ai-engineering-harness` são removidos; project-local skills/rules (habilidades/regras locais do projeto) permanecem intactas. Veja [Remover as habilidades compartilhadas (em inglês)](../README.md#remove-the-shared-skills).

Se a native skill activation (ativação nativa de uma habilidade) não puder ser verificada, o agent (agente) não deve afirmar que a habilidade está active (ativa). Em uma tarefa não relacionada, todos os skill bodies (corpos das habilidades) não devem entrar no context (contexto); somente a discovery metadata (metadados de descoberta) pode ficar visível. Veja [Testar a instalação (em inglês)](../README.md#how-to-test-an-installation).

Os arquivos `SKILL.md` não são traduzidos; mantém-se uma canonical English copy (cópia inglesa autorizada única). Para manutenção detalhada, adoption/update behavior (comportamento de instalação/atualização) e scope boundaries (limites de escopo), consulte o [README em inglês](../README.md).
