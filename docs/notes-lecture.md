# Notes de lecture

## Red Gate Simple Talk : Never ship a broken semantic model again

- DAX et Power Query sont du code : ils doivent être testés comme du code.
- Les tests s'écrivent avec la bibliothèque PQL.Assert (fonctions DAX définies par l'utilisateur).
- Convention de nommage : `[nom].[environnement].Tests`, par exemple `DataQuality.ANY.Tests` (ANY = tous les environnements).
- Exemple : des doublons dans une table de dimension faussent les calculs, d'où un test d'unicité.

## SQLBI : Testing DAX measures by using AI

- Une mesure est correcte seulement si elle donne le bon résultat dans tous les contextes de filtre.
- Il faut des cas positifs et des cas négatifs.
- Le résultat attendu ne doit pas être calculé par la mesure testée (test circulaire).
- L'IA peut aider à trouver les cas, mais l'exigence métier et la validation restent humaines.

## Idées retenues pour le projet

1. Chaque valeur de référence est notée avec son contexte de filtre exact (US-02).
2. Les valeurs attendues sont écrites à la main, issues de baseline-v1.
3. Les fichiers de tests suivront la convention : DataQuality.ANY.Tests, Schema.ANY.Tests.