# Sources et licences

| Ressource | Usage dans le projet | Licence | Lien |
|---|---|---|---|
| microsoft/powerbi-desktop-samples (AdventureWorks Sales Sample) | Modèle sémantique de référence et données Excel | MIT | https://github.com/microsoft/powerbi-desktop-samples |
| pql-test (PyPI) | Outil d'exécution des tests DAX | AGPL-3.0-only | https://pypi.org/project/pql-test/ |
| PQL.Assert (DAXLib) | Fonctions d'assertion DAX utilisées par les tests | à vérifier | voir l'article Red Gate |
| Red Gate Simple Talk : « Never ship a broken semantic model again » | Article de référence sur les tests de modèles sémantiques | contenu protégé, lien uniquement | https://www.red-gate.com/simple-talk/data-analytics/powerbi/never-ship-a-broken-semantic-model-again-how-to-build-automated-tests-in-power-bi-with-user-defined-functions/ |
| SQLBI : tester les mesures DAX avec l'IA | Article de référence | contenu protégé, lien uniquement | https://www.sqlbi.com/articles/testing-dax-measures-by-using-ai/ |
| Power BI Desktop | Ouverture du modèle et connexion de pql-test | gratuit, licence Microsoft | https://www.microsoft.com/power-platform/products/power-bi/desktop |

## Remarques

- Le fichier `.pbix` n'est pas versionné dans Git.
- L'exemple `SampleModel` de pql-test a servi uniquement à vérifier le fonctionnement de l'outil.
- Résultat de cet essai : 62 tests, 32 réussis, 30 en échec (capture : `pql-test-exemple.png`). Les échecs concernent le modèle de démonstration, pas l'installation.