# Tests sur les résultats des mesures DAX (US-05)

Suite : `Measures.ANY.Tests` (fichier `DAXQueries/Measures.ANY.Tests.dax`).
Référence : `baseline-v1`. Valeurs : `tests/valeurs-de-reference.md`.

## Critères d'acceptation

- Comptages : égalité exacte (`PQL.Assert.ShouldEqual`).
- Montants : arrondi à 2 décimales, comme les valeurs de référence (`ShouldEqual` sur `ROUND(..., 2)`).
- Règles de cohérence : écart absolu <= 0.01 (`PQL.Assert.ShouldBeTrue`).
- En cas d'échec, les colonnes Expected et Actual affichent la valeur attendue et la valeur obtenue.

## Catalogue

| Groupe | Tests | Mesures | Contexte de filtre | Référence |
|---|---|---|---|---|
| Sans filtre | 4 | Total Sales, Total Quantity, Order Lines Count, Sales Amount by Due Date | aucun | 3.1 |
| Par année fiscale | 12 | les 4 mesures | `'Date'[Fiscal Year]` FY2018 à FY2020 | 3.2 |
| Par catégorie | 12 | Total Sales, Total Quantity, Order Lines Count | `Product[Category]` (4 valeurs) | 3.3 |
| Par groupe de territoire | 9 | Total Sales, Total Quantity, Order Lines Count | `'Sales Territory'[Group]` (3 valeurs) | 3.4 |
| Année x catégorie | 12 | Total Sales | `'Date'[Fiscal Year]` et `Product[Category]` | 3.5 |
| Cohérence | 5 | C1, C2, C3, C4a, C4b | aucun | 4 |

Total : 54 tests, tous PASS sur `baseline-v1`.

## Exécution

    pql-test run-tests "local/AdventureWorks Sales"

Résultat attendu : `Measures.ANY.Tests` 54 PASS, `DataQuality.ANY.Tests` 2 PASS.

## Note

Le nom `Calculations.ANY.Tests` prévu au départ est refusé par le parseur DAX
(erreur de syntaxe sur `Calculations`). La suite s'appelle donc `Measures.ANY.Tests`.