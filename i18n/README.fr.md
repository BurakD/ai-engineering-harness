# AI Engineering Harness

**Langues :** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · **Français** · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

Une base minimale et indépendante des fournisseurs pour le développement logiciel assisté par IA.

Changer d’outil ou de modèle de programmation IA fait souvent perdre le contexte d’ingénierie du projet et oblige à tout réexpliquer. AI Engineering Harness est une petite couche portable de politiques et de contexte conçue pour éviter cela. Ce n’est ni un runtime d’agents ni un orchestrateur ; Cursor, Claude Code, Codex et Antigravity fournissent leurs propres capacités d’exécution.

## Problèmes résolus

1. Conserver le contexte du projet et la discipline d’ingénierie lors des changements d’outil ou de modèle.
2. Équilibrer qualité et coût en réservant le raisonnement le plus puissant aux tâches dont la complexité ou le risque le justifient.
3. Garder les choix de modèle/runtime à jour sans figer des noms de modèles éphémères dans la politique stable.

## Fichiers

- `AGENTS.md` — base d’ingénierie partagée pour les agents compatibles.
- `MODEL_ROUTING.md` — politique stable FAST / STANDARD / REASONING / FRONTIER.
- `MODEL_CATALOG.md` — catalogue temporel des modèles/runtimes et recommandations actuelles.
- `CLAUDE.md` — adaptateur minimal permettant à Claude Code d’importer `AGENTS.md`.
- `README.md` — guide principal d’adoption, de mise à jour, de test et de maintenance.

## Ce que c’est — et ce que ce n’est pas

La valeur principale réside dans les politiques : contexte centré sur le repository, tiers de routing, vérification fail-closed des capacités du runtime, approbation humaine selon l’impact, discipline de scope, handoff durable et mises à jour sûres.

Ce projet n’est ni un moteur de workflow, ni un framework multi-agents, ni un runtime, ni un générateur de synchronisation de règles, ni un remplacement des rules/skills natifs des outils.

## Compatibilité

`AGENTS.md` est une convention externe et cross-tool. Les runtimes qui la lisent directement n’ont pas besoin d’adaptateur propre au Harness. Claude Code utilise `CLAUDE.md`, d’où la présence du seul pont minimal `@AGENTS.md`. Les mécanismes propres à Antigravity comme `.agents/skills/` et `.agents/workflows/` restent locaux au projet.

## Adoption dans un projet existant

1. Rester dans le repository et la branche actuels.
2. Faire inspecter avant toute modification les règles, docs, l’état Git, la topologie de déploiement et les commandes de validation.
3. Avant de modifier un fichier existant, créer une sauvegarde byte-for-byte hors du repository.
4. Préserver tout le contenu spécifique au projet et n’ajouter que le contenu partagé du Harness.
5. Ne pas créer de branche, worktree, installer, manifeste, adaptateur ou synchroniseur uniquement pour adopter le Harness.
6. Ne pas commit, push, deploy ou publish sans approbation explicite.

**Prompt complet d’adoption :** [README anglais](README.md#copypaste-adoption-prompt)

## Mise à jour

Une mise à jour ne renouvelle que le contenu partagé appartenant au Harness. `AGENTS.md`, `MODEL_ROUTING.md`, `MODEL_CATALOG.md` et la partie partagée de `CLAUDE.md` sont rafraîchis depuis l’upstream tout en préservant les règles, modèles, skills, docs, code et travaux non commités du projet.

**Prompt complet de mise à jour :** [README anglais](README.md#copypaste-update-prompt)

## Principes clés

- La vérité du repository doit survivre aux changements de modèle ou d’agent.
- Ajouter plutôt que remplacer : les règles natives des outils restent à leur place.
- `MODEL_ROUTING.md` est stable ; `MODEL_CATALOG.md` est volontairement temporel.
- Le runtime actif fait autorité sur les modèles/agents réellement invocables.
- Découvrir un problème n’autorise pas à le corriger hors du scope demandé.
- Les actions à fort impact exigent une approbation humaine selon leur effet, pas selon le nom de l’outil ou de l’environnement.
- Tests, linters, types, CI et autres garde-fous déterministes sont préférables au jugement répété d’un modèle lorsqu’ils peuvent imposer la même règle de façon fiable.

## Tester l’installation

Tester dans des sessions neuves : structural smoke test, real-task behavior test, approval-boundary test et cross-tool runtime-capability test. L’agent doit découvrir correctement le contexte et ne jamais prétendre disposer de capacités que le runtime actif ne peut pas vérifier.

Prompts exacts : [How to test an installation](README.md#how-to-test-an-installation)

## Licence

Open source sous **Apache License 2.0**.