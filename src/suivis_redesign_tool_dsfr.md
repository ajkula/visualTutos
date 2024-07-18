# Comparaison des fonctionnalités souhaitables et implémentées pour le DSFR-builder

| Fonctionnalité | État actuel |
|----------------|-------------|
| Outils d'aide | ⚠️ Base existante, à améliorer |
| Liste exhaustive des composants (atomiques et composés) | ⚠️ Partielle, à compléter |
| Sélection des enfants possibles en liste blanche | ✅ Implémenté (checkboxes) |
| Suggestions cohérentes avec le DSFR | ❌ À développer |
| Sauvegarde locale des composants | ✅ Fonctionnel |
| Édition et suppression des composants sauvegardés | ✅ Opérationnel |
| Confirmation avant suppression | ❌ À ajouter |
| Partage des données sauvegardées | ✅ Fonctionnel |
| Traits avec types JS et input (style GrapesJS) | ⚠️ Base existante, à affiner |
| Visualisation en graphe des composants | ✅ Implémenté |
| Représentation des enfants acceptés | ✅ Intégré au graphe |
| Visualisation des traits (types) | ✅ Dans le graphe |
| Représentation des éléments proposables | ❌ À concevoir |
| Génération de documentation | ✅ Fonctionnel |
| Documentation interactive | ⚠️ Partiellement implémenté |
| Gestion de variables globales | ❌ À développer |
| Valeurs réutilisables entre traits | ❌ À implémenter |
| Définition de valeurs par défaut et limites | ❌ À ajouter |
| Mapping des interactions entre composants | ❌ À concevoir |
| Définition d'événements inter-composants | ❌ À développer |
| Visualisation des dépendances | ❌ À concevoir |
| Interface de règles métier pour exports | ❌ À concevoir |
| Sélection dynamique des composants | ❌ À implémenter |
| Adaptation contextuelle des composants | ❌ À concevoir |

Légende :
✅ Implémenté
⚠️ Partiellement implémenté
❌ À développer

## Analyse et perspectives d'évolution

### Axes d'amélioration principaux :
- Enrichir la gestion des composants (variables, interactions, versioning)

### Gestionnaire de variables : fonctionnalités clés
1. Affichage du système de variables
2. Gestion de scénarios

### Stratégie d'export
Notre approche pour les exports doit être modulaire et flexible. Points à considérer :

- Moteurs d'export configurables : développer des moteurs indépendants par format hors effets de bords

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
