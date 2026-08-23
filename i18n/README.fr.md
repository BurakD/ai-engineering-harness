<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Langues :** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · **Français** · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Une base minimale pour le développement logiciel assisté par AI, avec une approche vendor-neutral (indépendante du fournisseur) : une couche portable de politiques/contexte et un petit ensemble de procédures réutilisables. Ce n’est ni un agent runtime (environnement d’exécution d’agents), ni un orchestrator (orchestrateur), ni un installer (outil d’installation), ni un framework (cadre logiciel).

## Fichiers

- `AGENTS.md` — base d’ingénierie partagée et always-on (toujours active).
- `MODEL_ROUTING.md` — politique stable qualité/coût et capability tier (niveau de capacité).
- `MODEL_CATALOG.md` — catalogue de runtime (environnements d’exécution)/modèles sensible au temps.
- `CLAUDE.md` — passerelle légère de Claude Code vers `AGENTS.md`.
- `skills/` — procédures Harness-owned (appartenant au Harness), canonical (issues de la source de référence) et on-demand (chargées à la demande).
- `i18n/` — résumés localisés du README.

## Règles et compétences : quatre couches

Ici, rules (règles) désigne les consignes applicables en permanence et skills (compétences) les procédures utilisées pour des tâches précises.

| | Toujours active | À la demande |
| --- | --- | --- |
| **Partagée** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Spécifique au projet** | Mécanisme de règles/politiques propre au projet | Compétences propres au projet |

AI Engineering Harness ne fournit volontairement pas de répertoire `rules/` séparé : la couche partagée always-on (toujours active) a déjà sa canonical source (source de référence unique) dans `AGENTS.md`, tandis que la politique de model routing (routage des modèles) est dans `MODEL_ROUTING.md`. Une seconde source toujours active créerait duplication et risques de contradiction.

Les domain rules (règles de domaine), l’environment/deployment topology (topologie des environnements/déploiements), les vendor/model preferences (préférences fournisseur/modèle), le product behavior (comportement produit), les business rules (règles métier) et les infrastructure paths (chemins d’infrastructure) restent propres au projet. Pour décider où placer une nouvelle consigne, utilisez l’approche de safeguard (protection durable) du skill `continuous-improvement`.

## Compétences partagées

Les skills (compétences) sont des task-specific procedures (procédures propres à une tâche), pas une always-on policy (politique toujours active). Avec progressive disclosure (révélation progressive), seule la discovery metadata (métadonnée de découverte) est normalement visible ; le contenu complet de `SKILL.md` n’est chargé que lorsque la tâche correspond réellement.

La canonical source (source de référence unique) des Harness-owned skills (compétences appartenant au Harness) est `skills/`. L’ownership marker (marqueur de propriété) est :

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Un skill (compétence) du même nom qui ne porte pas cette clé n’est pas Harness-owned (appartenant au Harness) et ne doit jamais être écrasé pendant adoption (installation) ou update (mise à jour).

Le jeu v2 contient 14 compétences :

- `backup-and-recovery-review` — préparation de backup (sauvegarde), restore (restauration) et recovery (récupération).
- `interface-qa` — validation des interfaces web, mobile, bureau, CLI et API.
- `calculation-model-validation` — validation de formules et modèles de décision.
- `change-review` — revue des changements terminés, régressions et risques.
- `compatibility-and-rollout` — compatibility (compatibilité), migration (migration), rollout (déploiement progressif) et rollback (retour arrière).
- `high-risk-change-review` — discipline renforcée pour les changements à fort impact.
- `delegation-strategy` — usage sûr de delegation (délégation) et parallelism (parallélisme) vérifiés.
- `dependency-change` — évaluation des ajouts, suppressions et upgrades (mises à niveau) de dependencies (dépendances).
- `documentation-sync` — maintenir la documentation durable alignée sur la réalité.
- `environment-release-safety` — sécurité de release (publication)/deployment (déploiement) et de approval (approbation).
- `continuous-improvement` — transformer les échecs récurrents en safeguards (protections durables).
- `root-cause-debug` — identifier et démontrer la root cause (cause racine).
- `secret-exposure-response` — réponse à l’exposure (exposition) de secrets (secrets) et credentials (identifiants).
- `cross-surface-consistency` — cohérence du comportement entre surfaces (surfaces) équivalentes.

Le jeu partagé doit rester autour de **20 compétences ou moins** ; chaque `description` doit rester à **300 caractères maximum**.

Priorité : **project-local rules/policy (règles/politique propres au projet) > base partagée `AGENTS.md` > shared skills (compétences partagées)**. Un skill ne peut jamais assouplir un approval boundary (seuil d’approbation), le authorized scope (périmètre autorisé), les runtime capabilities (capacités de l’environnement d’exécution) ni la production/live safety (sécurité en production/en direct).

## Installation et mise à jour

Les copy/paste prompts (prompts de copier/coller) opérationnels restent dans une seule canonical source (source de référence) et ne sont pas traduits :

- [Prompt d’installation (en anglais)](../README.md#copypaste-adoption-prompt)
- [Prompt de mise à jour (en anglais)](../README.md#copypaste-update-prompt)

L’adoption (installation) détecte l’usage des runtimes (environnements d’exécution) à partir de repository evidence (preuves du dépôt) ; la simple présence d’un CLI installé ne suffit pas. Chemins project-level (au niveau du projet) vérifiés pour les skills : `.agents/skills/` pour Cursor/Antigravity/Codex et `.claude/skills/` pour Claude Code ; Cursor sait aussi lire `.claude/skills/`. Si un seul root (répertoire racine) vérifié couvre tous les environnements détectés, une seule copie est utilisée. Si la native activation (activation native) ne peut pas être vérifiée, `harness/skills/` sert de neutral fallback (solution de repli neutre) et aucune activation native n’est revendiquée.

Avant toute écriture, tous les canonical names (noms de la source de référence) sont vérifiés dans tous les target roots (répertoires racine cibles) pour détecter les collisions (collisions de noms). Tout fichier managed (géré) modifié est sauvegardé byte-for-byte (octet par octet) hors du repository (dépôt). Les copies Harness-owned (appartenant au Harness) restent verbatim (strictement identiques) à la canonical source (source de référence). Un update (mise à jour) ne déplace pas l’installation existante ; un managed skill (skill géré) supprimé upstream (dans la source amont) n’est pas effacé automatiquement et est signalé comme orphaned (absent de la source).

## Suppression et tests

Il n’existe pas d’uninstaller (outil de désinstallation) automatique. Seuls les managed skills (compétences gérées) portant l’ownership marker (marqueur de propriété) `metadata.ai-engineering-harness` sont supprimés ; les project-local skills/rules (compétences/règles propres au projet) restent intacts. Voir [Supprimer les compétences partagées (en anglais)](../README.md#remove-the-shared-skills).

Si la native skill activation (activation native d’une compétence) ne peut pas être vérifiée, l’agent (agent) ne doit pas prétendre que la compétence est active (active). Pour une tâche sans rapport, tous les skill bodies (corps des compétences) ne doivent pas être chargés dans le context (contexte) ; seule la discovery metadata (métadonnée de découverte) peut rester visible. Voir [Tester l’installation (en anglais)](../README.md#how-to-test-an-installation).

Les fichiers `SKILL.md` ne sont pas traduits ; une canonical English copy (copie anglaise de référence unique) est conservée. Pour la maintenance détaillée, l’adoption/update behavior (comportement d’installation/mise à jour) et les scope boundaries (limites de périmètre), consultez le [README en anglais](../README.md).
