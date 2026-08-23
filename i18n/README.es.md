<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Idiomas:** [English](../README.md) · [Türkçe](README.tr.md) · **Español** · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Una base mínima para desarrollo de software asistido por AI, con enfoque vendor-neutral (independiente del proveedor): una capa portátil de políticas/contexto y un pequeño conjunto de procedimientos reutilizables. No es un agent runtime (entorno de ejecución de agentes), un orchestrator (orquestador), un installer (instalador) ni un framework (marco de trabajo).

## Archivos

- `AGENTS.md` — base de ingeniería compartida y always-on (siempre activa).
- `MODEL_ROUTING.md` — política estable de calidad/coste y capability tier (nivel de capacidad).
- `MODEL_CATALOG.md` — catálogo de runtime (entornos de ejecución)/modelos sensible al tiempo.
- `CLAUDE.md` — puente ligero de Claude Code hacia `AGENTS.md`.
- `skills/` — procedimientos Harness-owned (propiedad del Harness), canonical (procedentes de la fuente autorizada) y on-demand (cargados bajo demanda).
- `i18n/` — resúmenes localizados del README.

## Reglas y habilidades: cuatro capas

Aquí, rules (reglas) significa orientación de aplicación continua y skills (habilidades) significa procedimientos que se usan para tareas concretas.

| | Siempre activa | Bajo demanda |
| --- | --- | --- |
| **Compartida** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Específica del proyecto** | Mecanismo propio de reglas/políticas | Habilidades propias del proyecto |

AI Engineering Harness no distribuye un directorio `rules/` separado: la capa compartida always-on (siempre activa) ya tiene su canonical source (fuente autorizada única) en `AGENTS.md`, mientras que la política de model routing (enrutamiento de modelos) está en `MODEL_ROUTING.md`. Una segunda fuente siempre activa generaría duplicación y riesgo de contradicciones.

Las domain rules (reglas de dominio), la environment/deployment topology (topología de entornos/despliegues), las vendor/model preferences (preferencias de proveedor/modelo), el product behavior (comportamiento del producto), las business rules (reglas de negocio) y las infrastructure paths (rutas de infraestructura) permanecen en el proyecto. Para decidir en qué capa debe vivir una nueva guía, use el enfoque de safeguard (protección duradera) del skill `continuous-improvement`.

## Habilidades compartidas

Los skills (habilidades) son task-specific procedures (procedimientos específicos de una tarea), no una always-on policy (política siempre activa). Con progressive disclosure (revelación progresiva), normalmente solo queda visible la discovery metadata (metadatos de descubrimiento); el cuerpo completo de `SKILL.md` se carga únicamente cuando la tarea realmente coincide.

La canonical source (fuente autorizada única) de los Harness-owned skills (habilidades propiedad del Harness) es `skills/`. El ownership marker (marcador de propiedad) es:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Un skill (habilidad) con el mismo nombre que no lleve esa clave no es Harness-owned (propiedad del Harness) y nunca se sobrescribe durante adoption (instalación) o update (actualización).

El conjunto v2 contiene 14 habilidades:

- `backup-and-recovery-review` — preparación de backup (copia de seguridad), restore (restauración) y recovery (recuperación).
- `interface-qa` — validación de interfaces web, móvil, de escritorio, CLI y API.
- `calculation-model-validation` — validación de fórmulas y modelos de decisión.
- `change-review` — revisión de cambios terminados, regresiones y riesgos.
- `compatibility-and-rollout` — compatibility (compatibilidad), migration (migración), rollout (despliegue gradual) y rollback (reversión).
- `high-risk-change-review` — disciplina adicional para cambios de alto impacto.
- `delegation-strategy` — uso seguro de delegation (delegación) y parallelism (paralelismo) verificados.
- `dependency-change` — revisión de altas, bajas y upgrades (actualizaciones de versión) de dependencies (dependencias).
- `documentation-sync` — mantener la documentación duradera alineada con la realidad.
- `environment-release-safety` — seguridad de release (publicación)/deployment (despliegue) y de approval (aprobación).
- `continuous-improvement` — convertir fallos repetidos en safeguards (protecciones duraderas).
- `root-cause-debug` — identificar y demostrar la root cause (causa raíz).
- `secret-exposure-response` — respuesta a la exposure (exposición) de secrets (secretos) y credentials (credenciales).
- `cross-surface-consistency` — consistencia de comportamiento entre surfaces (superficies) equivalentes.

El conjunto compartido debe mantenerse aproximadamente en **20 habilidades o menos**; cada `description` debe tener **300 caracteres o menos**.

Precedencia: **project-local rules/policy (reglas/política locales del proyecto) > base compartida de `AGENTS.md` > shared skills (habilidades compartidas)**. Un skill no puede relajar un approval boundary (límite de aprobación), el authorized scope (alcance autorizado), las runtime capabilities (capacidades del entorno de ejecución) ni la production/live safety (seguridad en producción/en vivo).

## Instalación y actualización

Los copy/paste prompts (prompts para copiar/pegar) operativos se mantienen en una única canonical source (fuente autorizada) y no se traducen:

- [Prompt de instalación (en inglés)](../README.md#copypaste-adoption-prompt)
- [Prompt de actualización (en inglés)](../README.md#copypaste-update-prompt)

La adoption (instalación) detecta el uso de runtime (entornos de ejecución) a partir de repository evidence (evidencia del repositorio); tener un CLI instalado no basta. Rutas project-level (a nivel de proyecto) verificadas para skills: `.agents/skills/` en Cursor/Antigravity/Codex y `.claude/skills/` en Claude Code; Cursor también puede leer `.claude/skills/`. Si un único root (directorio raíz) verificado cubre todos los entornos detectados, se usa una sola copia. Si no puede verificarse la native activation (activación nativa), `harness/skills/` se usa como neutral fallback (alternativa neutral) y no se afirma que haya activación nativa.

Antes de escribir cualquier habilidad, todos los canonical names (nombres de la fuente autorizada) se revisan en todos los target roots (directorios raíz de destino) para detectar collision (colisiones de nombres). Cualquier archivo managed (gestionado) que vaya a cambiar se respalda byte-for-byte (byte por byte) fuera del repository (repositorio). Las copias Harness-owned (propiedad del Harness) se mantienen verbatim (idénticas) a la canonical source (fuente autorizada). Un update (actualización) no mueve la ubicación existente; un managed skill (habilidad gestionada) eliminado upstream (en la fuente superior) no se borra automáticamente y se reporta como orphaned (ausente de la fuente).

## Eliminación y pruebas

No hay un uninstaller (desinstalador) automático. Solo se eliminan los managed skills (habilidades gestionadas) que llevan el ownership marker (marcador de propiedad) `metadata.ai-engineering-harness`; las project-local skills/rules (habilidades/reglas locales del proyecto) permanecen intactas. Véase [Eliminar las habilidades compartidas (en inglés)](../README.md#remove-the-shared-skills).

Si no puede verificarse la native skill activation (activación nativa de una habilidad), el agent (agente) no debe afirmar que la habilidad está active (activa). En una tarea no relacionada no deben cargarse todos los skill bodies (cuerpos de habilidades) en el context (contexto); solo puede quedar visible la discovery metadata (metadatos de descubrimiento). Véase [Probar la instalación (en inglés)](../README.md#how-to-test-an-installation).

Los archivos `SKILL.md` no se traducen; se conserva una canonical English copy (copia inglesa autorizada única). Para mantenimiento detallado, adoption/update behavior (comportamiento de instalación/actualización) y scope boundaries (límites de alcance), consulte el [README en inglés](../README.md).
