---
title: AVG (Transact-SQL) | Documents Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVG_TSQL
- AVG
dev_langs:
- TSQL
helpviewer_keywords:
- AVG function [Transact-SQL]
- GROUP BY clause, AVG function
- DISTINCT keyword
- values [SQL Server], average
- average values
ms.assetid: 4534b705-d946-441b-9b5d-5fbe561c9131
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 710e588843de71aadbb6675baba8f29a7686f3e1
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="avg-transact-sql"></a>AVG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retourne la moyenne des valeurs d'un groupe. Les valeurs NULL sont ignorées.
  
![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntaxe  
  
```sql
AVG ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
## <a name="arguments"></a>Arguments  
ALL  
Applique la fonction d'agrégation à toutes les valeurs. ALL est l'argument par défaut.
  
DISTINCT  
Spécifie que la fonction AVG doit uniquement être appliquée à chaque instance unique d'une valeur, quel que soit le nombre d'occurrences de la valeur.
  
*expression*  
Est un [expression](../../t-sql/language-elements/expressions-transact-sql.md) de la catégorie, de type de données numérique approximatives ou à l’exception de la **bits** type de données. Les fonctions d'agrégation et les sous-requêtes ne sont pas autorisées.
  
SUR **(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause* divise le jeu de résultats généré par la clause FROM en partitions auxquelles la fonction est appliquée. S'il n'est pas spécifié, la fonction gère toutes les lignes du jeu de résultats de la requête en un seul groupe. *order_by_clause* détermine l’ordre logique dans lequel l’opération est effectuée. *order_by_clause* est requis. Pour plus d’informations, consultez [la Clause OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Types de retour
Le type de retour est déterminé par le type de résultat de le *expression*.
  
|Résultat de l'expression|Type de retour|  
|---|---|
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|**décimal** catégorie (p, s)|**Decimal (38, s)** divisé par **décimale (10, 0)**|  
|**Money** et **smallmoney** catégorie|**money**|  
|**float** et **réel** catégorie|**float**|  
  
## <a name="remarks"></a>Notes  
Si le type de données de *expression* est un alias de données type, le type de retour est également du type de données alias. Toutefois, si le type de données de base de type de données alias est promu, par exemple à partir de **tinyint** à **int**, la valeur de retour de données promues n’est pas le type de données d’alias et de type.
  
AVG() calcule la moyenne d'un jeu de valeurs en divisant la somme de ces valeurs par le nombre de valeurs non nulles. Si la somme dépasse la valeur maximale pour le type de données de la valeur de retour, une erreur est renvoyée.
  
AVG est une fonction déterministe lorsqu'elle est utilisée sans les clauses OVER et ORDER BY. Elle n'est pas déterministe avec les clauses OVER et ORDER BY. Pour plus d’informations, consultez [Fonctions déterministes et non déterministes](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Exemples  
  
### <a name="a-using-the-sum-and-avg-functions-for-calculations"></a>A. Utilisation des fonctions SUM et AVG pour des calculs  
L'exemple suivant calcule la moyenne des heures de congés ainsi que la somme des heures de congés maladie utilisées par les vice-présidents d'[!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]. Chacune de ces fonctions d'agrégation produit une valeur de résumé unique pour toutes les lignes récupérées. L'exemple utilise la base de données [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
SELECT AVG(VacationHours)AS 'Average vacation hours',   
    SUM(SickLeaveHours) AS 'Total sick leave hours'  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Vice President%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`Average vacation hours       Total sick leave hours`
  
`----------------------       ----------------------`
  
`25                           97`
  
`(1 row(s) affected)`
  
### <a name="b-using-the-sum-and-avg-functions-with-a-group-by-clause"></a>B. Utilisation des fonctions SUM et AVG avec une clause GROUP BY  
Lorsqu'elle est utilisée avec une clause `GROUP BY`, chaque fonction d'agrégation produit une valeur unique pour chaque groupe, plutôt que pour la totalité de la table. L'exemple suivant produit des valeurs de synthèse pour chaque secteur géographique de ventes dans la base de données [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Le résumé répertorie la moyenne des bonus reçus par les vendeurs dans chaque secteur, ainsi que la somme des ventes annuelles à ce jour pour chaque secteur.
  
```sql
SELECT TerritoryID, AVG(Bonus)as 'Average bonus', SUM(SalesYTD) as 'YTD sales'  
FROM Sales.SalesPerson  
GROUP BY TerritoryID;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
TerritoryID Average Bonus         YTD Sales  
----------- --------------------- ---------------------  
NULL        0.00                  1252127.9471  
1           4133.3333             4502152.2674  
2           4100.00               3763178.1787  
3           2500.00               3189418.3662  
4           2775.00               6709904.1666  
5           6700.00               2315185.611  
6           2750.00               4058260.1825  
7           985.00                3121616.3202  
8           75.00                 1827066.7118  
9           5650.00               1421810.9242  
10          5150.00               4116871.2277  
  
(11 row(s) affected)  
```  
  
### <a name="c-using-avg-with-distinct"></a>C. Utilisation de la fonction AVG avec DISTINCT  
L'instruction suivante retourne les tarifs moyens des produits dans la base de données [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. En spécifiant DISTINCT, seules les valeurs uniques sont prises en compte dans le calcul.
  
```sql
SELECT AVG(DISTINCT ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`------------------------------`
  
`437.4042`
  
`(1 row(s) affected)`
  
### <a name="d-using-avg-without-distinct"></a>D. Utilisation de la fonction AVG sans DISTINCT  
Sans l'option DISTINCT, la fonction `AVG` recherche le tarif moyen de tous les produits dans la table `Product` de la base de données [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], y compris les valeurs dupliquées.
  
```sql
SELECT AVG(ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`------------------------------`
  
`438.6662`
  
`(1 row(s) affected)`
  
### <a name="e-using-the-over-clause"></a>E. Utilisation de la clause OVER  
L'exemple suivant utilise la fonction AVG avec la clause OVER pour fournir une moyenne mobile des ventes annuelles pour chaque secteur dans la table `Sales.SalesPerson` de la base de données [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Les données sont partitionnées par `TerritoryID` et classées logiquement par `SalesYTD`. Cela signifie que la fonction AVG est calculée pour chaque secteur selon l'année de vente. Notez que pour `TerritoryID` 1, il y a deux lignes pour l'année 2005 représentant les deux vendeurs avec leurs ventes de l'année. Les ventes moyennes pour ces deux lignes sont calculées et la troisième ligne représentant les ventes de l'année 2006 est incluse dans le calcul.
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
Dans cet exemple, la clause OVER n'inclut pas PARTITION BY. Cela signifie que la fonction sera appliquée à toutes les lignes retournées par la requête. La clause ORDER BY spécifiée dans la clause OVER détermine l'ordre logique selon lequel la fonction AVG est appliquée. La requête retourne une moyenne mobile des ventes par année pour tous les secteurs de vente spécifiés dans la clause WHERE. La clause ORDER BY spécifiée dans l'instruction SELECT détermine l'ordre dans lequel les lignes de la requête sont affichées.
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="see-also"></a>Voir aussi
[Fonctions d’agrégation &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[SUR la clause for &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
