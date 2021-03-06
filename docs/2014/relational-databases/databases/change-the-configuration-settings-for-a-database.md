---
title: Modifier les paramètres de configuration d’une base de données | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- database configuration [SQL Server]
- configuration options [SQL Server], databases
- modifying database configuration settings
ms.assetid: c29c3385-5043-400f-bb4e-044a4c9a9a4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 05dc6188a46e0e2d43b7a4bc3275fae7d4cd8da6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822823"
---
# <a name="change-the-configuration-settings-for-a-database"></a>Modifier les paramètres de configuration d'une base de données
  Cette rubrique explique comment modifier les options de base de données dans [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] à l'aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Ces options sont spécifiques à chaque base de données et n'affectent pas les autres.  
  
 **Dans cette rubrique**  
  
-   **Avant de commencer :**  
  
     [Limitations et restrictions](#Restrictions)  
  
     [Sécurité](#Security)  
  
-   **Pour modifier les paramètres d'option d'une base de données, utilisez :**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Avant de commencer  
  
###  <a name="Restrictions"></a> Limitations et restrictions  
  
-   Seuls l’administrateur système, le propriétaire de la base de données, les membres des rôles serveur fixes **sysadmin** et **dbcreator** et des rôles de base de données fixes **db_owner** peuvent modifier ces options.  
  
###  <a name="Security"></a> Sécurité  
  
####  <a name="Permissions"></a> Permissions  
 Nécessite l'autorisation ALTER sur la base de données.  
  
##  <a name="SSMSProcedure"></a> Utilisation de SQL Server Management Studio  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>Pour modifier les paramètres d'option d'une base de données  
  
1.  Dans l’Explorateur d’objets, connectez-vous à une instance du [!INCLUDE[ssDE](../../includes/ssde-md.md)] , développez le serveur, puis **Bases de données**, cliquez avec le bouton droit sur une base de données, puis cliquez sur **Propriétés**.  
  
2.  Dans la boîte de dialogue **Propriétés de la base de données** , cliquez sur **Options** pour accéder à la plupart des paramètres de configuration. Les configurations de fichiers et de groupes de fichiers, la mise en miroir et la copie des journaux de transactions sont sur leurs pages respectives.  
  
##  <a name="TsqlProcedure"></a> Utilisation de Transact-SQL  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>Pour modifier les paramètres d'option d'une base de données  
  
1.  Connectez-vous au [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dans la barre d'outils standard, cliquez sur **Nouvelle requête**.  
  
3.  Copiez et collez l'exemple suivant dans la fenêtre de requête, puis cliquez sur **Exécuter**. Cet exemple définit les options de mode de récupération et de vérification de pages de données pour l'exemple de base de données [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
 [!code-sql[DatabaseDDL#AlterDatabase7](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase7)]  
  
 Pour plus d’exemples, consultez [Options ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
## <a name="see-also"></a>Voir aussi  
 [Niveau de compatibilité ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)   
 [Mise en miroir de bases de données ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)   
 [Modifier le nom d'une base de données](rename-a-database.md)   
 [Réduire une base de données](shrink-a-database.md)  
  
  
