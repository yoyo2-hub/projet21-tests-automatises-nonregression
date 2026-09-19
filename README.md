# projet4-pbip-git-alm

## Industrialiser un projet Power BI avec PBIP, Git, collaboration et environnements DEV–TEST–PROD

**Domaine :** DevOps, ALM & CI/CD — **Product Owner :** PO 3

---

## 1. Besoin métier

Aujourd'hui, un rapport Power BI est souvent modifié directement, sans trace claire des changements, sans possibilité simple de revenir en arrière, et sans étape de validation avant que la modification n'atteigne les utilisateurs finaux. Ce projet répond à un besoin réel : **permettre à une équipe de faire évoluer un rapport Power BI de façon maîtrisée**, comme on le ferait pour n'importe quel projet logiciel — avec un historique des modifications, une revue avant validation, et une séparation claire entre développement, test et production.

## 2. Contexte fil rouge

Vous travaillez sur les données de vente de l'entreprise fictive **AdventureWorks** (ventes, clients, produits, magasins, commerciaux) — le même contexte métier que toutes les autres équipes du dispositif.

## 3. Description générale du projet

**Mission :** transformer une solution Power BI existante en projet **PBIP**, la versionner avec **Git** (usage réel de branches et de pull requests), puis organiser un cycle **DEV–TEST–PROD**. Vous devez être capables de montrer, de bout en bout, le parcours d'une modification : depuis son développement jusqu'à sa validation en environnement de test.

## 4. Comment démarrer

1. **Point de départ :** vous n'avez pas à construire un nouveau rapport Power BI de zéro. Réutilisez un rapport `.pbix` déjà construit pendant vos TP/exercices sur la base AdventureWorks (par exemple un rapport simple avec quelques pages : CA par région, top produits, évolution mensuelle). S'il n'en existe pas un tout prêt, construisez-en un **volontairement simple** — l'objectif du projet n'est pas la richesse du rapport, mais la démonstration du processus autour de lui.
2. Convertissez ce rapport au format **PBIP** (Power BI Desktop → options → "Power BI Project (.pbip)").
3. Initialisez ce repo Git et versionnez les fichiers PBIP obtenus.
4. Définissez avec votre équipe une convention de nommage de branches et le rôle de "relecteur" sur les pull requests.
5. Simulez concrètement vos 3 environnements DEV/TEST/PROD (3 workspaces Power BI Service, ou 3 dossiers/branches locales — à documenter dans `docs/architecture.md`).
6. Démontrez le parcours complet d'une modification : développement → pull request → revue → fusion → validation en TEST.

## 5. Structure du repo

```
po3-projet04-pbip-git-alm/
├── README.md
├── docs/
│   ├── architecture.md          → schéma de votre organisation Git/environnements
│   └── note-pedagogique.md      → à remplir au fur et à mesure (voir section 6)
├── pbip/                        → vos fichiers PBIP versionnés
├── scripts/                     → scripts éventuels (vide si non utilisé)
└── tests/                       → non utilisé pour ce projet (laisser vide)
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

- Une démonstration fonctionnelle du cycle complet
- Les fichiers PBIP et l'historique Git (ce repo)
- Un schéma d'architecture (`docs/architecture.md`)
- La note pédagogique complète (`docs/note-pedagogique.md`)

## 8. Critères de réussite

- Le scénario métier est compréhensible
- La solution est reproductible par quelqu'un d'autre
- Les choix techniques sont justifiés simplement
- Le résultat peut être démontré en direct
- Les limites et points de vigilance sont explicités

## 9. Lien avec les autres projets du domaine

- **Projet 5** (`po3-projet05-deployment-pipelines-cicd`) part conceptuellement d'une solution déjà versionnée comme la vôtre pour travailler le déploiement
- **Projet 21** (`po3-projet21-tests-automatises-nonregression`) viendra ajouter des tests avant le déploiement

➡️ Documentez clairement votre structure et vos conventions : les autres équipes s'y réfèrent pour rester cohérentes.
