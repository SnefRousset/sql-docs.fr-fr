---
title: sp_delete_backuphistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_backuphistory
- sp_delete_backuphistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_backuphistory
ms.assetid: bdb56834-616e-47e4-b942-e895d2325e97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2252fe0339a13a6d75c43a09351b95b17b7abd7b
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49168759"
---
# <a name="spdeletebackuphistory-transact-sql"></a>sp_delete_backuphistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Réduit la taille des tables d'historique de sauvegarde et de restauration en supprimant les entrées correspondant aux jeux de sauvegarde antérieurs à la date spécifiée. Des lignes supplémentaires sont ajoutées à la sauvegarde et restauration des tables d’historique après chaque sauvegarde ou opération de restauration est effectuée ; Par conséquent, nous vous recommandons d’exécuter régulièrement **sp_delete_backuphistory**.  
  
> [!NOTE]  
>  Les tables d’historique de sauvegarde et de restauration résident dans le **msdb** base de données.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_delete_backuphistory [ @oldest_date = ] 'oldest_date'   
```  
  
## <a name="arguments"></a>Arguments  
 [  **@oldest_date=** ] **'**_plus ancien\_date_**'**  
 Date la plus ancienne conservée dans les tables d'historique de sauvegarde et de restauration. *oldest_date* est **datetime**, sans valeur par défaut.  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 0 (réussite) ou 1 (échec)  
  
## <a name="result-sets"></a>Jeux de résultats  
 None  
  
## <a name="remarks"></a>Notes  
 **sp_delete_backuphistory** doit être exécuté à partir de la **msdb** de base de données et affecte les tables suivantes :  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
  
-   [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
  
-   [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
  
-   [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
  
-   [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
  
 Les fichiers de sauvegarde physiques sont conservés, même si tout l'historique est supprimé.  
  
## <a name="permissions"></a>Permissions  
 Nécessite l’appartenance dans le **sysadmin** rôle serveur fixe, mais les autorisations peuvent être accordées à d’autres utilisateurs.  
  
## <a name="examples"></a>Exemples  
 L'exemple suivant supprime toutes les entrées créées avant le 14 janvier 2010, 12h00, dans les tables d'historique de sauvegarde et de restauration.  
  
```  
USE msdb;  
GO  
EXEC sp_delete_backuphistory @oldest_date = '01/14/2010';  
```  
  
## <a name="see-also"></a>Voir aussi  
 [sp_delete_database_backuphistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-backuphistory-transact-sql.md)   
 [Historique de sauvegarde et informations d’en-tête &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
