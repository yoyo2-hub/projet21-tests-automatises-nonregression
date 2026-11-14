# Mesures du modèle AdventureWorks Sales

Relevé effectué le 14/11/2026 dans Power BI Desktop, vue Requête DAX,
avec `EVALUATE INFO.MEASURES()`. Les valeurs sont calculées **sans filtre**.

| Mesure | Origine | Formule | Valeur (sans filtre) |
|---|---|---|---|
| Sales Amount by Due Date | Existante (Microsoft) | `CALCULATE(SUM(Sales[Sales Amount]), USERELATIONSHIP(Sales[DueDateKey], 'Date'[DateKey]))` | 109 809 274,20 |
| Total Sales | Ajoutée par l'équipe | `SUM(Sales[Sales Amount])` | 109 809 274,20 |
| Total Quantity | Ajoutée par l'équipe | `SUM(Sales[Order Quantity])` | 274 776 |
| Order Lines Count | Ajoutée par l'équipe | `COUNTROWS(Sales)` | 121 253 |

## Exemple avec contexte de filtre

| Mesure | Contexte de filtre | Valeur |
|---|---|---|
| Total Sales | `'Date'[Fiscal Year] = "FY2019"` | 34 070 108,50 |

## Remarques

- Le modèle d'origine ne contient qu'une seule mesure explicite. Les 3 autres ont été ajoutées pour atteindre les 3 mesures métier demandées par US-00.
- Les 3 mesures ajoutées seront incluses dans `baseline-v1` (US-01).
- Les valeurs d'un visuel du rapport peuvent différer à cause des segments et filtres du rapport.