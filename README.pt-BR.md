# AI Engineering Harness

**Idiomas:** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · **Português (Brasil)** · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

Uma base mínima e neutra em relação a fornecedores para desenvolvimento de software assistido por IA.

Trocar entre ferramentas ou modelos de programação com IA normalmente significa perder o contexto de engenharia do projeto e ter de explicá-lo novamente. O AI Engineering Harness é uma pequena camada portátil de políticas e contexto para evitar isso. Ele não é um runtime de agentes nem um orquestrador; Cursor, Claude Code, Codex e Antigravity fornecem suas próprias capacidades de execução.

## O que resolve

1. Mantém o contexto do projeto e a disciplina de engenharia ao trocar de ferramenta ou modelo.
2. Equilibra qualidade e custo usando raciocínio mais forte apenas quando a complexidade ou o risco justificam.
3. Mantém escolhas de modelo/runtime atualizadas sem fixar nomes de modelos de curta duração na política estável.

## Arquivos

- `AGENTS.md` — baseline compartilhada de engenharia para agentes compatíveis.
- `MODEL_ROUTING.md` — política estável FAST / STANDARD / REASONING / FRONTIER.
- `MODEL_CATALOG.md` — catálogo temporal de modelos/runtimes e recomendações atuais.
- `CLAUDE.md` — adaptador mínimo para Claude Code importar `AGENTS.md`.
- `README.md` — guia principal de adoção, atualização, testes e manutenção.

## O que é — e o que não é

O valor principal está nas políticas: contexto orientado pelo repositório, tiers de routing, verificação fail-closed das capacidades do runtime, aprovação humana baseada no efeito, disciplina de escopo, handoff durável e atualização segura.

Não é um workflow engine, framework multiagente, runtime, gerador de regras sincronizadas ou substituto para regras/skills nativos de cada ferramenta.

## Compatibilidade

`AGENTS.md` é uma convenção externa e cross-tool. Runtimes que o leem diretamente não precisam de adaptador. Claude Code usa `CLAUDE.md`, por isso este repositório inclui apenas a ponte mínima `@AGENTS.md`. Mecanismos específicos do Antigravity, como `.agents/skills/` e `.agents/workflows/`, continuam locais ao projeto.

## Adoção em um projeto existente

1. Trabalhe no repositório e branch atuais.
2. Faça um agente capaz inspecionar regras, docs, estado do Git, topologia de deploy e comandos de validação antes de editar.
3. Antes de modificar qualquer arquivo existente, crie um backup byte-for-byte fora do repositório.
4. Preserve todo o conteúdo específico do projeto e adicione somente o conteúdo compartilhado do Harness.
5. Não crie branch, worktree, installer, manifest, adaptador ou sincronizador apenas para adotar o Harness.
6. Não faça commit, push, deploy ou publish sem aprovação explícita.

**Prompt completo de adoção:** [README em inglês](README.md#copypaste-adoption-prompt)

## Atualização

Uma atualização renova apenas o conteúdo compartilhado pertencente ao Harness. `AGENTS.md`, `MODEL_ROUTING.md`, `MODEL_CATALOG.md` e a parte compartilhada de `CLAUDE.md` são atualizados a partir do upstream, preservando regras, modelos, skills, docs, código e trabalho não commitado do projeto.

**Prompt completo de atualização:** [README em inglês](README.md#copypaste-update-prompt)

## Princípios principais

- A verdade do repositório deve sobreviver à troca de modelo ou agente.
- Adicionar, não substituir: regras nativas de ferramentas permanecem onde já estão.
- `MODEL_ROUTING.md` é estável; `MODEL_CATALOG.md` é intencionalmente temporal.
- O runtime ativo é a autoridade sobre quais modelos/agentes podem realmente ser invocados.
- Descobrir um problema não autoriza corrigi-lo fora do escopo solicitado.
- Ações de alto impacto exigem aprovação humana pelo seu efeito, não pelo nome da ferramenta ou ambiente.
- Testes, linters, tipos, CI e outros controles determinísticos são preferíveis ao julgamento repetido do modelo quando conseguem impor a mesma regra.

## Testes de instalação

Teste em sessões novas: structural smoke test, real-task behavior test, approval-boundary test e cross-tool runtime-capability test. O agente deve descobrir corretamente o contexto e nunca alegar capacidades que o runtime ativo não consiga verificar.

Prompts exatos: [How to test an installation](README.md#how-to-test-an-installation)

## Licença

Código aberto sob **Apache License 2.0**.