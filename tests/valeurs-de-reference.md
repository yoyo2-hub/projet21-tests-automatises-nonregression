# Valeurs de référence (US-02)

Source : version `baseline-v1` du projet PBIP (commit b3e6829).
Relevées le 15/11/2026 dans Power BI Desktop, vue Requête DAX, sans rien enregistrer.
Les nombres sont écrits comme la vue Requête DAX les affiche (séparateur décimal : point).

## 1. KPI protégés

| KPI | Définition | Pourquoi le protéger |
|---|---|---|
| Total Sales | `SUM(Sales[Sales Amount])` | Chiffre d'affaires, le KPI le plus visible |
| Total Quantity | `SUM(Sales[Order Quantity])` | Volume vendu |
| Order Lines Count | `COUNTROWS(Sales)` | Nombre de lignes de vente |
| Sales Amount by Due Date | `CALCULATE(SUM(Sales[Sales Amount]), USERELATIONSHIP(Sales[DueDateKey], 'Date'[DateKey]))` | Dépend d'une relation inactive, très sensible à une régression |

## 2. Critères d'acceptation

- Comptages (Total Quantity, Order Lines Count) : égalité exacte avec la valeur de référence.
- Montants (Total Sales, Sales Amount by Due Date) : écart absolu inférieur ou égal à 0.01.
- Règles de cohérence : écart absolu inférieur ou égal à 0.01 (0 attendu).
- Un test est PASS si toutes ses valeurs respectent ces critères, FAIL sinon.

## 3. Valeurs de référence

### 3.1 Sans filtre

| Mesure | Contexte de filtre | Valeur attendue |
|---|---|---|
| Total Sales | aucun | 109809274.2 |
| Total Quantity | aucun | 274776 |
| Order Lines Count | aucun | 121253 |
| Sales Amount by Due Date | aucun | 109809274.2 |

### 3.2 Par année fiscale (`'Date'[Fiscal Year]`)

| Année | Total Sales | Total Quantity | Order Lines Count | Sales Amount by Due Date |
|---|---|---|---|---|
| FY2018 | 23860891.17 | 24349 | 10918 | 23348493.12 |
| FY2019 | 34070108.5 | 83339 | 26050 | 33636168.52 |
| FY2020 | 51878274.54 | 167088 | 84285 | 52824612.56 |

### 3.3 Par catégorie (`Product[Category]`)

| Catégorie | Total Sales | Total Quantity | Order Lines Count |
|---|---|---|---|
| Accessories | 1272057.89 | 61931 | 41193 |
| Bikes | 94620526.21 | 90220 | 40005 |
| Clothing | 2117613.45 | 73598 | 21368 |
| Components | 11799076.66 | 49027 | 18687 |

### 3.4 Par groupe de territoire (`'Sales Territory'[Group]`)

| Groupe | Total Sales | Total Quantity | Order Lines Count |
|---|---|---|---|
| Europe | 19800577.06 | 53010 | 26978 |
| North America | 79353361.18 | 203473 | 79217 |
| Pacific | 10655335.96 | 18293 | 15058 |

### 3.5 Deux filtres : année fiscale et catégorie (Total Sales)

| Année | Accessories | Bikes | Clothing | Components |
|---|---|---|---|---|
| FY2018 | 36814.85 | 22590983.47 | 66327.53 | 1166765.32 |
| FY2019 | 138901.55 | 28544881.62 | 757224.19 | 4629101.14 |
| FY2020 | 1096341.49 | 43484661.12 | 1294061.73 | 6003210.2 |

## 4. Règles de cohérence

| ID | Règle | Résultat sur baseline-v1 |
|---|---|---|
| C1 | Total Sales = Sales Amount by Due Date, sans filtre | écart 0 |
| C2 | La somme de Total Sales par catégorie est égale au total | écart 0 |
| C3 | La somme de Total Sales par groupe de territoire est égale au total | écart 0 |
| C4 | La somme de Total Quantity et de Order Lines Count par année, par catégorie et par groupe est égale au total | vérifiée par addition |

## 5. Reproduire les valeurs

Ouvrir `pbip/AdventureWorks Sales.pbip` (version baseline-v1), vue Requête DAX, sans enregistrer.

    EVALUATE
    SUMMARIZECOLUMNS('Date'[Fiscal Year],
        "Total Sales", [Total Sales], "Total Quantity", [Total Quantity],
        "Order Lines Count", [Order Lines Count],
        "Sales Amount by Due Date", [Sales Amount by Due Date])
    ORDER BY 'Date'[Fiscal Year]

    EVALUATE
    SUMMARIZECOLUMNS(Product[Category],
        "Total Sales", [Total Sales], "Total Quantity", [Total Quantity],
        "Order Lines Count", [Order Lines Count])
    ORDER BY Product[Category]

    EVALUATE
    SUMMARIZECOLUMNS('Sales Territory'[Group],
        "Total Sales", [Total Sales], "Total Quantity", [Total Quantity],
        "Order Lines Count", [Order Lines Count])
    ORDER BY 'Sales Territory'[Group]

    EVALUATE
    SUMMARIZECOLUMNS('Date'[Fiscal Year], Product[Category], "Total Sales", [Total Sales])
    ORDER BY 'Date'[Fiscal Year], Product[Category]

    EVALUATE
    ROW("Total Sales", [Total Sales],
        "Ecart C1", [Total Sales] - [Sales Amount by Due Date],
        "Ecart C2", [Total Sales] - SUMX(VALUES(Product[Category]), [Total Sales]),
        "Ecart C3", [Total Sales] - SUMX(VALUES('Sales Territory'[Group]), [Total Sales]))

## 6. Remarque

Les montants sont affichés avec 2 décimales. Une somme de valeurs arrondies peut différer de 0.01 du total exact, d'où la tolérance de 0.01 sur les montants.