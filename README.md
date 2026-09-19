# projet21-tests-automatises-nonregression

## Mettre en place des tests automatisés pour sécuriser les évolutions d'un modèle sémantique Power BI

**Domaine :** DevOps, ALM & CI/CD — **Product Owner :** PO 3

---

## 1. Besoin métier

Un modèle sémantique Power BI peut être modifié (une formule DAX, une relation, une règle métier) tout en restant **techniquement valide** — il s'ouvre, les mesures ne renvoient pas d'erreur — alors même qu'il produit désormais des **résultats métier faux** (un chiffre d'affaires incorrect, un KPI erroné). Ce projet répond à ce besoin : **détecter automatiquement ce type de régression avant qu'elle n'atteigne la production**, pour passer de "le modèle fonctionne" à "nous pouvons démontrer que le modèle produit toujours les bons résultats".

## 2. Contexte fil rouge

Vous travaillez sur les données de vente de l'entreprise fictive **AdventureWorks** (ventes, clients, produits, magasins, commerciaux) — le même contexte métier que toutes les autres équipes du dispositif.

## 3. Description générale du projet

**Mission :** mettre en place une stratégie de **tests automatisés** vérifiant qu'une évolution d'un modèle sémantique Power BI n'entraîne pas de régression sur les données et les résultats métier. Vous devez définir des valeurs de référence, construire plusieurs catégories de tests, introduire volontairement des régressions pour vérifier qu'elles sont détectées, puis réfléchir à l'intégration de ces tests dans un cycle **PBIP → Git → Tests → PASS/FAIL → Validation → Déploiement**.

## 4. Comment démarrer

1. **Point de départ :** simulez vous-même un modèle sémantique fonctionnel sur AdventureWorks (reprenez un rapport existant de vos TP ou construisez-en un simple), et placez-le dans `pbip/`.
2. Identifiez 3 à 5 mesures/KPI critiques à protéger (ex : chiffre d'affaires total, nombre de commandes, cohérence CA global vs somme des régions).
3. Définissez des **valeurs de référence** précises pour ces mesures, dans des contextes de filtre donnés.
4. Construisez plusieurs catégories de tests dans `tests/` : qualité des données, présence des objets du modèle, stabilité des résultats DAX.
5. Introduisez volontairement 2-3 régressions (formule DAX cassée, relation supprimée, règle métier modifiée) et vérifiez que vos tests les détectent (résultat **FAIL**).
6. Documentez comment ces tests s'intégreraient dans le cycle `PBIP → Git → Tests → PASS/FAIL → Validation → Déploiement`.

## 5. Structure du repo

```
projet21-tests-automatises-nonregression/
├── README.md
├── docs/
│   ├── architecture.md          → schéma d'intégration des tests dans le cycle CI/CD
│   └── note-pedagogique.md      → à remplir au fur et à mesure (voir section 6)
├── pbip/                        → votre modèle sémantique de référence (simulé)
├── scripts/                     → scripts d'exécution des tests
└── tests/                       → catalogue des tests + résultats attendus/obtenus
```

## 6. Note pédagogique — squelette à remplir

Dans `docs/note-pedagogique.md`, structurez votre note selon ce plan (imposé pour tous les mini-projets du dispositif) :

- Contexte et problématique métier
- Objectifs du mini-projet et périmètre retenu
- Architecture ou principe de fonctionnement de la solution
- Prérequis, données et technologies utilisées
- Réalisation pas à pas et démonstration du résultat
- Difficultés rencontrées et erreurs fréquentes
- Bonnes pratiques et points de vigilance
- Limites de la solution et pistes d'amélioration
- Courte synthèse réutilisable comme base pédagogique

## 7. Livrables attendus

- Une démonstration fonctionnelle du dispositif de tests
- Un catalogue des tests avec leurs résultats attendus (`tests/`)
- Les scripts permettant leur exécution (`scripts/`)
- Un rapport synthétique PASS/FAIL par test
- Une démonstration qu'une erreur volontaire est bien détectée
- Un schéma d'intégration dans le cycle PBIP/Git/CI-CD (`docs/architecture.md`)
- La note pédagogique complète (`docs/note-pedagogique.md`)

## 8. Critères de réussite

- Les tests ne se limitent pas à vérifier que le modèle s'ouvre : ils contrôlent les **données, KPI et résultats métier**
- Les valeurs de référence et critères d'acceptation sont clairement définis
- Les tests sont reproductibles
- Une modification incorrecte provoque bien l'échec d'au moins un test
- Les résultats permettent d'identifier rapidement la régression

## 9. Lien avec les autres projets du domaine

- **Projet 4** (`projet4-pbip-git-alm`) fournit le socle de versionning sur lequel repose votre scénario
- **Projet 5** (`projet5-deployment-pipelines-cicd`) automatise le déploiement — vos tests devraient se positionner **juste avant** cette étape, comme un verrou avant mise en production

➡️ Restez cohérents avec les 2 autres équipes sur la structure du modèle sémantique utilisé comme référence commune.
