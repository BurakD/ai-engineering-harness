<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Langues :** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · **Français** · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Une base minimale et indépendante des fournisseurs pour le développement logiciel assisté par IA : une couche portable de politiques/contexte, complétée par un petit ensemble de procédures réutilisables. Ce n'est ni un agent runtime (environnement d'exécution d'agents), ni un orchestrateur, ni un installateur, ni un framework.

## Fichiers

- `AGENTS.md` — base d'ingénierie partagée always-on (toujours active).
- `MODEL_ROUTING.md` — politique stable qualité/coût et capability-tier (niveau de capacité).
- `MODEL_CATALOG.md` — catalogue de runtime (environnement d'exécution)/modèles sensible au temps.
- `CLAUDE.md` — pont minimal de Claude Code vers `AGENTS.md`.
- `skills/` — procédures Harness-owned (appartenant au Harness), canonical (source de référence), on-demand (à la demande).
- `i18n/` — résumés README localisés.

## Règles et skills (compétences) : quatre couches

| | Always-on | On-demand |
| --- | --- | --- |
| **Partagée** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Spécifique au projet** | Mécanisme de règles/politiques propre au projet | Skills propres au projet |

Le Harness ne fournit volontairement pas de répertoire `rules/` séparé : la source canonical de la couche partagée always-on existe déjà dans `AGENTS.md`, avec la politique de routing dans `MODEL_ROUTING.md`. Une seconde source always-on de référence créerait duplication et risques de contradiction.

Les règles métier/domaine, la topologie des environnements et déploiements, les préférences fournisseur/modèle, le comportement produit, les règles business et les chemins d'infrastructure restent propres au projet. Pour décider où placer une nouvelle guidance, utilisez le skill `continuous-improvement` et son principe du plus petit safeguard (garde-fou) durable adapté.

## Skills partagés

Les skills sont des procédures liées à une tâche, pas une politique always-on. Avec progressive disclosure (affichage progressif), seule leur metadata doit normalement être disponible pour discovery ; le corps complet de `SKILL.md` est chargé uniquement quand la tâche correspond réellement.

La source canonical des skills Harness-owned est `skills/`. L'ownership marker (marqueur de propriété) est :

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Un skill de même nom sans cette clé n'appartient pas au Harness et ne doit jamais être écrasé pendant adoption (adoption) ou update.

Le jeu v2 contient 14 skills :

- `backup-and-recovery-review` — préparation backup, restore et recovery.
- `interface-qa` — validation d'interfaces web, mobile, desktop, CLI et API.
- `calculation-model-validation` — validation de formules et modèles de décision.
- `change-review` — revue des changements terminés, régressions et risques.
- `compatibility-and-rollout` — compatibilité, migration, déploiement progressif et retour arrière.
- `high-risk-change-review` — discipline renforcée pour les changements à fort impact.
- `delegation-strategy` — usage sûr de la délégation et de la parallélisation vérifiées.
- `dependency-change` — évaluation des ajouts, suppressions et mises à niveau de dépendances.
- `documentation-sync` — alignement de la documentation durable avec la réalité.
- `environment-release-safety` — sécurité release/deployment et limites d'approbation.
- `continuous-improvement` — transformer les échecs récurrents en garde-fous durables.
- `root-cause-debug` — identifier et démontrer la cause racine.
- `secret-exposure-response` — réponse à l'exposition de secrets/credentials.
- `cross-surface-consistency` — cohérence comportementale entre plusieurs surfaces.

Le jeu partagé doit rester autour de **20 skills ou moins** ; chaque `description` doit rester à **300 caractères maximum**.

Priorité : **règles/politique du projet > baseline partagée `AGENTS.md` > skills partagés**. Un skill ne peut jamais assouplir une limite d'approbation, le scope autorisé, les capacités du runtime ou la sécurité production/live.

## Adoption et mise à jour

Les prompts opérationnels copy/paste restent dans une source canonical unique et ne sont pas traduits :

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

L'adoption détecte les runtimes à partir de preuves dans le repository ; la simple présence d'un CLI installé ne suffit pas. Chemins de projet vérifiés : `.agents/skills/` pour Cursor, Antigravity et Codex ; `.claude/skills/` pour Claude Code. Cursor sait aussi lire `.claude/skills/`. Si une seule racine vérifiée couvre tous les runtimes détectés, une seule copie est utilisée. Si la native activation (activation native) ne peut pas être vérifiée, `harness/skills/` sert de neutral fallback (solution de repli neutre) et aucune activation native n'est revendiquée.

Avant toute écriture de skill, tous les noms canonical sont vérifiés contre les collisions dans toutes les racines cibles. Tout fichier managed (géré) modifié est sauvegardé byte-for-byte hors du repository. Les copies Harness-owned restent verbatim (identiques) à la source canonical. Une mise à jour ne déplace jamais l'installation existante ; un skill managed supprimé upstream n'est pas effacé automatiquement, il est signalé comme orphaned (sans équivalent upstream).

## Suppression et tests

Il n'existe pas d'uninstaller automatique. Seuls les skills portant `metadata.ai-engineering-harness` sont considérés comme Harness-owned pour la suppression ; les règles et skills du projet restent intacts. Voir [Remove the shared skills](../README.md#remove-the-shared-skills).

Si l'activation native ne peut pas être vérifiée, l'agent ne doit pas prétendre qu'un skill est actif. Pour une tâche sans rapport, les corps de tous les skills ne doivent pas entrer dans le contexte ; seule la metadata de discovery peut rester visible. Voir [How to test an installation](../README.md#how-to-test-an-installation).

Les fichiers `SKILL.md` ne sont pas traduits ; une seule copie canonical anglaise est conservée. Pour les détails de maintenance, adoption/update et limites de scope, consultez le [README anglais](../README.md).
