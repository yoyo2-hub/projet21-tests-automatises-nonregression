# Tests de structure du modèle (US-04)

Suite : `ModelStructure.ANY.Tests` (fichier `DAXQueries/ModelStructure.ANY.Tests.dax`).
Référence : `baseline-v1`.

## Objectif
Vérifier que les objets du modèle existent toujours : tables, mesures, relations.
Une relation supprimée ou une mesure renommée fait échouer un test.

## Catalogue

| Groupe | Tests | Contrôle |
|---|---|---|
| Tables présentes | 8 | Customer, Date, Product, Reseller, Sales, Sales Order, Sales Territory, Table |
| Mesures présentes | 4 | Total Sales, Total Quantity, Order Lines Count, Sales Amount by Due Date |
| Nombre de relations | 3 | 12 au total, 10 actives, 2 inactives |
| Relations métier | 9 | présence et état (active ou inactive) de chaque relation |

Total : 26 tests, tous PASS sur `baseline-v1`.

## Relations protégées
Sales[CustomerKey], [ProductKey], [ResellerKey], [SalesOrderLineKey] (bidirectionnelle),
[SalesTerritoryKey], [OrderDateKey] (actives) ; Product[Category] vers Table[Category] (active) ;
Sales[DueDateKey] et [ShipDateKey] vers Date[DateKey] (inactives).
Les tables techniques `LocalDateTable_*` et `DateTableTemplate_*` sont ignorées (noms variables).

## Exécution
    pql-test run-tests "local/AdventureWorks Sales"

## Note
Les noms `Structure.ANY.Tests` et `Calculations.ANY.Tests` sont refusés par le parseur DAX.
La suite s'appelle donc `ModelStructure.ANY.Tests`.