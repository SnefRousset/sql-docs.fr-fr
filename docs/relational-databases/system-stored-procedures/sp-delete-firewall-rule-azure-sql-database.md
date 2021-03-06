---
title: sp_delete_firewall_rule (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 406f94ab0ab2d0ebaddf9635448e364bf90ceb8c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031750"
---
# <a name="spdeletefirewallrule-azure-sql-database"></a>sp_delete_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Supprime des paramètres de pare-feu de niveau serveur de votre serveur [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Cette procédure stockée est uniquement disponible dans la base de données master à la connexion du principal au niveau du serveur.  

  
## <a name="syntax"></a>Syntaxe  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>Arguments  
 L'argument de la procédure stockée est le suivant :  
  
 [@name =] '*name*'  
 Nom du paramètre de pare-feu de niveau serveur qui sera supprimé. *nom* est **nvarchar (128)** sans valeur par défaut.  
  
## <a name="remarks"></a>Notes  
 Dans [!INCLUDE[ssSDS](../../includes/sssds-md.md)], les données de connexion exigées pour authentifier une connexion et les règles de pare-feu de niveau serveur sont temporairement mises en cache dans chaque base de données. Ce cache est régulièrement actualisé. Pour forcer une actualisation du cache d’authentification et garantir qu’une base de données a la version la plus récente de la table de connexions, exécutez [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Autorisations  
 Seul le nom de connexion du principal au niveau du serveur créé par le processus de déploiement peut supprimer les règles de pare-feu côté serveur. L’utilisateur doit être connecté à la base de données master pour exécuter sp_delete_firewall_rule.  
  
## <a name="example"></a>Exemple  
 L'exemple suivant supprime le paramètre de pare-feu de niveau serveur nommé « Example setting 1 ». Exécutez l’instruction dans la base de données master virtuelle.  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>Voir aussi  
 [Pare-feu de base de données SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Procédure : Configurer les paramètres de pare-feu (base de données SQL Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;base de données SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Sys.firewall_rules &#40;base de données SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


