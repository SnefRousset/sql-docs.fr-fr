---
title: DROP TYPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP TYPE
- DROP_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [SQL Server], deleting
- UDTs [SQL Server], deleting
- alias data types [SQL Server], removing
- DROP TYPE statement
ms.assetid: 11bf83f9-0718-4238-a835-83d2eb14ae7b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b6416febd415ef75f2455a55c14c2e220c4b5b0a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215678"
---
# <a name="drop-type-transact-sql"></a>DROP TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Supprime de la base de données active un type de données alias ou un type de données CLR (Common Language Runtime) défini par l'utilisateur.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>Arguments  
 *IF EXISTS*  
 **S’applique à** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] jusqu’à la [version actuelle](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Supprime, de manière conditionnelle, le type uniquement s’il existe déjà.  
  
 *schema_name*  
 Nom du schéma auquel appartient le type de données alias ou défini par l'utilisateur  
  
 *TYPE_NAME*  
 Nom du type de données alias ou défini par l'utilisateur à supprimer  
  
## <a name="remarks"></a>Notes   
 L'instruction DROP TYPE ne s'exécutera pas si l'une des informations suivantes est vraie :  
  
-   Des tables de la base de données contiennent des colonnes du type de données alias ou du type défini par l'utilisateur. Il est possible d’obtenir des informations sur les colonnes de type alias ou défini par l’utilisateur en interrogeant la vue de catalogue [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) ou [sys.column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md).  
  
-   Il existe des colonnes calculées, des contraintes CHECK, des vues liées au schéma et des fonctions liées au schéma dont les définitions font référence au type alias ou au type défini par l'utilisateur. Il est possible d’obtenir des informations sur ces références en interrogeant la vue de catalogue [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md).  
  
-   Il existe des fonctions, des procédures stockées ou des déclencheurs créés dans la base de données, et ces routines utilisent des variables et des paramètres de type alias ou de type défini par l'utilisateur. Il est possible d’obtenir des informations sur les paramètres de type alias ou défini par l’utilisateur en interrogeant la vue de catalogue [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) ou [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Nécessite soit une autorisation CONTROL sur *type_name*, soit une autorisation ALTER sur *schema_name*.  
  
## <a name="examples"></a>Exemples  
 Cet exemple suppose qu'un type nommé `ssn` est déjà créé dans la base de données actuelle.  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a> Voir aussi  
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
