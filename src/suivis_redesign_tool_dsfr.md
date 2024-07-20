# Comparaison des fonctionnalités souhaitables et implémentées pour le DSFR-builder

| Fonctionnalité | État actuel |
|----------------|-------------|
| Outils d'aide | ⚠️ Base existante, à améliorer |
| Sélection des enfants possibles en liste blanche | ✅ Implémenté (checkboxes) |
| Sauvegarde locale des composants | ✅ Fonctionnel |
| Édition et suppression des composants sauvegardés | ✅ Opérationnel |
| Confirmation avant suppression | ✅ Fonctionnel |
| Partage des données sauvegardées | ✅ Fonctionnel |
| Visualisation en graphe des composants | ✅ Implémenté |
| Représentation des enfants acceptés | ✅ Intégré au graphe |
| Visualisation des traits (types) | ✅ Dans le graphe |
| Génération de documentation | ✅ Fonctionnel |
| Sélection dynamique des composants | ✅ Fonctionnel |
| Liste exhaustive des composants (atomiques et composés) | ⚠️ Partielle, à compléter |
| Suggestions cohérentes avec le DSFR | ⚠️ Base existante, à affiner |
| Traits avec types JS et input (style GrapesJS) | ⚠️ Base existante, à affiner |
| Représentation des éléments proposables | ⚠️ Base existante, à affiner |
| Documentation interactive | ⚠️ Partiellement implémenté |
| Interface de règles métier pour exports | ⚠️ Base existante, à affiner |
| Mapping des interactions entre composants | ❌ À concevoir |
| Définition d'événements inter-composants | ❌ À développer |
| Visualisation des dépendances | ❌ À concevoir |
| Adaptation contextuelle des composants | ❌ À concevoir |

Légende :
✅ Implémenté
⚠️ Partiellement implémenté
❌ À développer

## Objectifs de l'outil de documentation

- Faciliter la compréhension et la documentation du projet DSFR-builder pour les product managers et owners
- Offrir une plateforme pour repenser et planifier l'évolution du DSFR-builder
- Permettre la définition et la documentation claire des règles métier du DSFR-builder
- Servir d'aide-mémoire pour les considérations techniques et stratégiques importantes du DSFR-builder
- Centraliser les informations sur l'état actuel et les perspectives d'évolution du DSFR-builder
- Améliorer la communication entre les équipes de développement et les parties prenantes du projet
- Fournir une base solide pour la prise de décisions éclairées concernant le développement futur du DSFR-builder
- Permettre une visualisation claire des composants, de leurs relations et de leurs contraintes dans le DSFR-builder
- Faciliter l'identification des opportunités d'amélioration et d'optimisation du DSFR-builder
- Assurer la cohérence entre la documentation et l'implémentation réelle du DSFR-builder

## Considérations pour les évolutions futur du DSFR-builder

### Stratégie d'export
Notre approche pour les exports doit être modulaire et flexible. Points à considérer :
- Développer des moteurs indépendants par format hors effets de bords

### Approche centrée contenu
1. Séparation contenu/présentation :
   - Stocker uniquement les données essentielles (contenu, type de composant)
   - Flexibilité des composants selon le contenu et le contexte
   - Ex : choix automatique entre radio et select selon le nombre d'options
   - Mises à jour des composants sans modification structurelle
2. Rendu dynamique :
   - Génération à la volée basée sur les règles et le contenu
   - Adaptation facile aux évolutions DSFR sans migration massive
3. Optimisation performances :
   - Simplification de la base de données
   - Intégration facilitée des nouvelles versions DSFR

Avantages de cette approche :
- Flexibilité accrue : adaptation facile aux changements DSFR
- Performances améliorées : base de données optimisée
- Respect DSFR : meilleure conformité, expérience utilisateur améliorée
- Évolutivité : facilité d'ajout/modification des composants et règles
