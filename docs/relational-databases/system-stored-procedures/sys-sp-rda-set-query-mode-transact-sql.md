---
title: Sys.sp_rda_set_query_mode (Transact-SQL) | Documents Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a98d67b6d6cec581cdfcff31f7f9c0fd692b2520
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2017
---
# <a name="syssprdasetquerymode-transact-sql"></a>Sys.sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Spécifie si les requêtes sur la base de données prenant en charge Stretch en cours et ses tables de retournent les données locales et distantes (par défaut), ou uniquement les données locales.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>Arguments  
 [ @mode = ] *@mode*  
 Est une des valeurs suivantes.  
  
-   **DÉSACTIVÉ** toutes les requêtes sur les tables compatibles Stretch échouent.  
  
-   **LOCAL_ONLY** requêtes destinées aux tables compatibles Stretch retournent uniquement les données locales.  
  
-   **LOCAL_AND_REMOTE** requêtes destinées aux tables compatibles Stretch retournent des données locales et distantes. Il s'agit du comportement par défaut.  
  
 [ @force = ]  *@force*  
 Est une valeur de bit facultatif que vous pouvez définir sur 1, si vous souhaitez modifier le mode de requête sans validation.  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 0 (réussite) ou >0 (échec)  
  
## <a name="permissions"></a>Permissions  
 Nécessite les autorisations db_owner.  
  
## <a name="remarks"></a>Notes  
 Les procédures stockées étendues suivantes également définissent le mode de requête pour une base de données Stretch.  
  
-   **sp_rda_deauthorize_db**  
  
     Après avoir exécuté **sp_rda_deauthorize_db** , toutes les requêtes sur les tables et les bases de données Stretch échouent. Autrement dit, le mode de requête est défini sur désactivé. Pour quitter ce mode, effectuez l’une des opérations suivantes.  
  
    -   Exécutez [sys.sp_rda_reauthorize_db &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) se reconnecter à la base de données Azure distante. Cette opération réinitialise automatiquement le mode de requête LOCAL_AND_REMOTE, qui est le comportement par défaut pour la base de données Stretch. Autrement dit, les requêtes retournent des résultats à partir des données locales et distantes.  
  
    -   Exécutez [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) avec l’argument LOCAL_ONLY pour vous permettre de requêtes continuent de s’exécuter avec les données locales uniquement.  
  
-   **sp_rda_reauthorize_db**  
  
     Lorsque vous exécutez [sys.sp_rda_reauthorize_db &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) pour vous reconnecter à la base de données Azure distante, cette opération réinitialise automatiquement le mode de requête LOCAL_AND_REMOTE, qui est le comportement par défaut pour la base de données Stretch. Autrement dit, les requêtes retournent des résultats à partir des données locales et distantes.  
  
## <a name="see-also"></a>Voir aussi  
 [Sys.sp_rda_deauthorize_db &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  