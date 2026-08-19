# AI Engineering Harness

**Idiomas:** [English](README.md) · [Türkçe](README.tr.md) · **Español** · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

Una base mínima y neutral respecto al proveedor para el desarrollo de software asistido por IA.

Cambiar entre herramientas o modelos de programación con IA suele implicar perder el contexto de ingeniería del proyecto y tener que explicarlo de nuevo. AI Engineering Harness es una pequeña capa portátil de políticas y contexto que evita ese problema. No es un runtime de agentes ni un orquestador; Cursor, Claude Code, Codex y Antigravity aportan sus propias capacidades de ejecución.

## Qué resuelve

1. Mantener el contexto del proyecto y la disciplina de ingeniería al cambiar de herramienta o modelo.
2. Equilibrar calidad y coste usando razonamiento más potente solo cuando la complejidad o el riesgo lo justifican.
3. Mantener actualizadas las decisiones de modelo/runtime sin fijar nombres de modelos efímeros en la política estable.

## Archivos

- `AGENTS.md` — base compartida de ingeniería para agentes compatibles.
- `MODEL_ROUTING.md` — política estable FAST / STANDARD / REASONING / FRONTIER.
- `MODEL_CATALOG.md` — catálogo temporal de modelos/runtimes y recomendaciones actuales.
- `CLAUDE.md` — adaptador mínimo para que Claude Code importe `AGENTS.md`.
- `README.md` — guía canónica de adopción, actualización, pruebas y mantenimiento.

## Qué es y qué no es

El valor principal está en las políticas: contexto basado en el repositorio, tiers de routing, verificación fail-closed de capacidades del runtime, aprobación humana según el efecto, disciplina de alcance, handoff durable y actualización segura.

No es un motor de workflow, un framework multiagente, un runtime, un generador de reglas sincronizadas ni un reemplazo de reglas/skills nativos de cada herramienta.

## Compatibilidad

`AGENTS.md` es una convención externa y multiplataforma. Los runtimes que la leen directamente no necesitan adaptador. Claude Code usa `CLAUDE.md`, por eso este repositorio incluye únicamente el puente mínimo `@AGENTS.md`. Los mecanismos específicos de Antigravity como `.agents/skills/` y `.agents/workflows/` permanecen locales al proyecto.

## Adopción en un proyecto existente

1. Trabaja en el repositorio y branch actuales.
2. Haz que un agente capaz inspeccione primero reglas, docs, estado Git, topología de despliegue y comandos de validación.
3. Antes de modificar un archivo existente, crea una copia byte-for-byte fuera del repositorio.
4. Conserva todo el contenido específico del proyecto y añade solo el contenido compartido del Harness.
5. No crees branches, worktrees, installers, manifests, adaptadores o sincronizadores solo por instalar el Harness.
6. No hagas commit, push, deploy o publish sin aprobación explícita.

**Prompt completo de adopción:** [README en inglés](README.md#copypaste-adoption-prompt)

## Actualización

Una actualización refresca solo el contenido compartido propiedad del Harness. `AGENTS.md`, `MODEL_ROUTING.md`, `MODEL_CATALOG.md` y la parte compartida de `CLAUDE.md` se actualizan desde upstream conservando reglas, modelos, skills, docs, código y trabajo sin commit del proyecto.

**Prompt completo de actualización:** [README en inglés](README.md#copypaste-update-prompt)

## Principios clave

- La verdad del repositorio debe sobrevivir a cambios de modelo o agente.
- Añadir, no reemplazar: las reglas nativas de cada herramienta permanecen donde están.
- `MODEL_ROUTING.md` es estable; `MODEL_CATALOG.md` es deliberadamente temporal.
- El runtime activo es la autoridad sobre qué modelos/agentes puede invocar realmente.
- Descubrir un problema no autoriza a corregirlo fuera del alcance solicitado.
- Las acciones de alto impacto requieren aprobación humana por su efecto, no por el nombre de la herramienta o entorno.
- Tests, linters, tipos, CI y otros controles deterministas son preferibles al juicio repetido de un modelo cuando pueden imponer la misma regla.

## Pruebas de instalación

Prueba desde sesiones nuevas: structural smoke test, real-task behavior test, approval-boundary test y cross-tool runtime-capability test. El agente debe descubrir correctamente el contexto y nunca afirmar capacidades que el runtime activo no pueda verificar.

Prompts exactos: [How to test an installation](README.md#how-to-test-an-installation)

## Licencia

Código abierto bajo **Apache License 2.0**.