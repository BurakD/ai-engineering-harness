<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Idiomas:** [English](../README.md) · [Türkçe](README.tr.md) · **Español** · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Una base mínima y neutral respecto al proveedor para desarrollo de software asistido por IA: una capa portátil de políticas/contexto más un pequeño conjunto de procedimientos reutilizables. No es un agent runtime (entorno de ejecución de agentes), un orquestador, un instalador ni un framework.

## Archivos

- `AGENTS.md` — base de ingeniería compartida always-on (siempre activa).
- `MODEL_ROUTING.md` — política estable de calidad/coste y capability-tier (nivel de capacidad).
- `MODEL_CATALOG.md` — catálogo de runtime (entorno de ejecución)/modelos sensible al tiempo.
- `CLAUDE.md` — puente mínimo de Claude Code hacia `AGENTS.md`.
- `skills/` — procedimientos Harness-owned (propiedad del Harness), canonical (fuente autoritativa) y on-demand (bajo demanda).
- `i18n/` — resúmenes localizados del README.

## Reglas y skills (habilidades): cuatro capas

| | Always-on | On-demand |
| --- | --- | --- |
| **Compartida** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Específica del proyecto** | Mecanismo propio de reglas/políticas | Skills propios del proyecto |

El Harness no distribuye un directorio `rules/` separado: la fuente canonical de la capa compartida always-on ya es `AGENTS.md`, con la política de routing en `MODEL_ROUTING.md`. Una segunda fuente always-on autoritativa produciría duplicación y riesgo de contradicciones.

Las reglas de dominio, topología de entornos y despliegues, preferencias de proveedor/modelo, comportamiento del producto, reglas de negocio y rutas de infraestructura permanecen en el proyecto. Para decidir dónde debe vivir una nueva guía, use el skill `continuous-improvement` y su enfoque de elegir el safeguard (protección) duradero más pequeño.

## Skills compartidos

Los skills son procedimientos específicos de una tarea, no política always-on. Con progressive disclosure (divulgación gradual), normalmente solo su metadata queda disponible para discovery; el cuerpo completo de `SKILL.md` se carga cuando la tarea realmente coincide.

La fuente canonical de los skills Harness-owned es `skills/`. El ownership marker (marcador de propiedad) es:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Un skill con el mismo nombre que no lleve esa clave no pertenece al Harness y nunca debe sobrescribirse durante adoption (adopción) o update.

El conjunto v2 contiene 14 skills:

- `backup-and-recovery-review` — preparación de backup, restore y recovery.
- `interface-qa` — validación de interfaces web, móvil, desktop, CLI y API.
- `calculation-model-validation` — validación de fórmulas y modelos de decisión.
- `change-review` — revisión de cambios terminados, regresiones y riesgos.
- `compatibility-and-rollout` — compatibilidad, migraciones, despliegue gradual y reversión.
- `high-risk-change-review` — disciplina adicional para cambios de alto impacto.
- `delegation-strategy` — uso seguro de delegación y paralelismo verificados.
- `dependency-change` — revisión de altas, bajas y actualizaciones de dependencias.
- `documentation-sync` — mantener documentación duradera alineada con la realidad.
- `environment-release-safety` — seguridad de release/deployment y límites de aprobación.
- `continuous-improvement` — convertir fallos repetidos en protecciones duraderas.
- `root-cause-debug` — identificar y demostrar la causa raíz.
- `secret-exposure-response` — respuesta a exposición de secretos/credenciales.
- `cross-surface-consistency` — consistencia de comportamiento entre superficies.

El conjunto debe mantenerse aproximadamente en **20 skills o menos**; cada `description` debe tener **300 caracteres o menos**.

Precedencia: **reglas/política locales del proyecto > base compartida de `AGENTS.md` > skills compartidos**. Un skill nunca puede relajar límites de aprobación, alcance autorizado, capacidades del runtime o seguridad production/live.

## Adoption y update

Los prompts operativos copy/paste se mantienen en una única fuente canonical y no se traducen:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

La adoption detecta runtimes a partir de evidencia del repositorio; tener un CLI instalado no basta. Rutas de proyecto verificadas: `.agents/skills/` para Cursor, Antigravity y Codex; `.claude/skills/` para Claude Code. Cursor también puede leer `.claude/skills/`. Si una sola raíz verificada cubre todos los runtimes detectados, se usa una sola copia. Si la native activation (activación nativa) no puede verificarse, se usa `harness/skills/` como neutral fallback (alternativa neutral) y no se afirma activación nativa.

Antes de escribir cualquier skill se buscan collisions (colisiones) para todos los nombres canonical en todas las raíces destino. Cualquier archivo managed (gestionado) que vaya a cambiar se respalda byte por byte fuera del repositorio. Las copias Harness-owned se mantienen verbatim (idénticas) a la fuente canonical. Un update no mueve la ubicación existente de los skills; un skill gestionado eliminado upstream no se borra automáticamente, se reporta como orphaned (sin equivalente upstream).

## Eliminación y pruebas

No hay uninstaller automático. Solo se eliminan skills que lleven `metadata.ai-engineering-harness`; los skills y reglas del proyecto permanecen intactos. Véase [Remove the shared skills](../README.md#remove-the-shared-skills).

Si el runtime no permite verificar la activación nativa, el agente no debe afirmar que el skill está activo. En una tarea no relacionada no deben cargarse los cuerpos de todos los skills; solo puede estar visible la metadata de discovery. Véase [How to test an installation](../README.md#how-to-test-an-installation).

Los archivos `SKILL.md` no se traducen; se conserva una única copia canonical en inglés. Para mantenimiento detallado, adoption/update y límites de alcance, consulte el [README en inglés](../README.md).
