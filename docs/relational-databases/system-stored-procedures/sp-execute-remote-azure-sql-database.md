---
title: sp_execute_remote (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a475ba50aa8d3ba140ea551306d8b9f17fe66d22
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035900"
---
# <a name="spexecuteremote-azure-sql-database"></a>sp_execute_remote (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Exécute un [!INCLUDE[tsql](../../includes/tsql-md.md)] instruction sur une unique à distance Azure SQL Database ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.  
  
 La procédure stockée fait partie de la fonctionnalité de requête élastique.  Consultez [vue d’ensemble de requête de base de données élastique Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) et [des requêtes de base de données élastique pour le partitionnement (partitionnement horizontal)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>Arguments  
 [ \@data_source_name = ] *datasourcename*  
 Identifie la source de données externe dans laquelle l’instruction est exécutée. Consultez [créer une SOURCE de données externe &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md). La source de données externe peut être de type « SGBDR » ou « SHARD_MAP_MANAGER ».  
  
 [ \@stmt= ] *statement*  
 Est une chaîne Unicode contenant un [!INCLUDE[tsql](../../includes/tsql-md.md)] instruction ou le lot. \@stmt doit être une constante Unicode ou une variable Unicode. L'utilisation d'expressions Unicode plus complexes (comme la concaténation de deux chaînes avec l'opérateur +) n'est pas autorisée. L'utilisation de constantes de caractères n'est pas autorisée. Si une constante Unicode est spécifiée, elle doit porter le préfixe avec un **N**. Par exemple, la constante Unicode **ne sp_who'** est valide, mais la constante caractère **'sp_who'** n’est pas. La taille de la chaîne n'est limitée que par la quantité de mémoire disponible sur le serveur de base de données. Sur les serveurs 64 bits, la taille de la chaîne est limitée à 2 Go, la taille maximale de **nvarchar (max)**.  
  
> [!NOTE]  
>  \@stmt peut contenir des paramètres possédant la même forme qu’un nom de variable, par exemple : `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Chaque paramètre inclus dans \@stmt doit posséder une entrée correspondante à la fois dans le \@liste des définitions de paramètre params et le paramètre de liste de valeurs.  
  
 [ \@params =] N'\@*nom_paramètre ** data_type* [,... *n* ] '  
 Est une chaîne qui contient les définitions de tous les paramètres qui ont été incorporés dans \@stmt. Cette chaîne doit être une constante Unicode ou une variable Unicode. Chaque définition de paramètre se compose d'un nom de paramètre et d'un type de données. *n* est un espace réservé qui indique les définitions de paramètres supplémentaires. Chaque paramètre spécifié dans \@stmtmust être défini dans \@params. Si le [!INCLUDE[tsql](../../includes/tsql-md.md)] instruction ou le lot de \@stmt ne contient-elle pas de paramètres, \@params n’est pas obligatoire. La valeur par défaut de ce paramètre est NULL.  
  
 [ \@param1= ] '*value1*'  
 Valeur du premier paramètre qui est défini dans la chaîne de paramètres. Cette valeur peut être une constante ou une variable Unicode. Il doit y avoir une valeur de paramètre fournie pour chaque paramètre inclus dans \@stmt. Les valeurs ne sont pas requis lorsque la [!INCLUDE[tsql](../../includes/tsql-md.md)] instruction ou le lot de \@stmt n’a aucun paramètre.  
  
 *n*  
 Représente un espace réservé destiné aux valeurs de paramètres supplémentaires. Ces valeurs doivent être des constantes ou des variables. Leur degré de complexité ne doit pas dépasser celui d'expressions telles que les fonctions ou expressions créées à l'aide d'opérateurs.  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 0 (réussite) ou autre que zéro (échec)  
  
## <a name="result-sets"></a>Jeux de résultats  
 Retourne le jeu de résultats de la première instruction SQL.  
  
## <a name="permissions"></a>Autorisations  
 Nécessite l'autorisation `ALTER ANY EXTERNAL DATA SOURCE`.  
  
## <a name="remarks"></a>Notes  
 `sp_execute_remote` paramètres doivent être entrées dans l’ordre spécifique, comme décrit dans la section syntaxe ci-dessus. Si les paramètres sont entrés dans le désordre, un message d'erreur se produira.  
  
 `sp_execute_remote` a le même comportement que [EXECUTE &#40;Transact-SQL&#41; ](../../t-sql/language-elements/execute-transact-sql.md) en ce qui concerne les lots et la portée des noms. L’instruction Transact-SQL ou un lot dans le sp_execute_remote  *\@stmt* paramètre n’est pas compilé jusqu'à ce que l’instruction sp_execute_remote est exécutée.  
  
 `sp_execute_remote` Ajoute une colonne supplémentaire au jeu de résultats nommé « $ShardName » qui contient le nom de la base de données distant qui a généré la ligne.  
  
 `sp_execute_remote` peut être utilisée comme [sp_executesql &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Exemples  
### <a name="simple-example"></a>Exemple simple  
 L’exemple suivant crée et exécute une instruction SELECT simple sur une base de données distante.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Exemple avec plusieurs paramètres  
Créer une information d’identification de niveau base de données dans une base de données utilisateur, en spécifiant les informations d’identification d’administrateur pour la base de données master. Créer une source de données externe qui pointe vers la base de données master et en spécifiant les informations d’identification de niveau base de données. Puis suit, l’exemple dans la base de données utilisateur, exécute le `sp_set_firewall_rule` procédure dans la base de données master. Le `sp_set_firewall_rule` procédure requiert des 3 paramètres et nécessite le `@name` paramètre soit Unicode.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Voir aussi :

[CRÉER LA BASE DE DONNÉES INFORMATIONS D’IDENTIFICATION](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
