---
title: Afficher les informations sur l’espace occupé par les données et par le journal d’une base de données | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], space
- status information [SQL Server], space
- displaying space information
- disk space [SQL Server], displaying
- databases [SQL Server], space used
- viewing space information
- space allocation [SQL Server], displaying
- data space [SQL Server]
ms.assetid: c7b99463-4bab-4e9b-9217-fcb0898dc757
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04777f6f03ed5e97249eaf50b04f44e8e9aac763
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149060"
---
# <a name="display-data-and-log-space-information-for-a-database"></a>Afficher les informations sur l'espace occupé par les données et par le journal d'une base de données
  Cette rubrique explique comment afficher des informations sur l'espace occupé par les données et par le journal d'une base de données dans [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] à l'aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Dans cette rubrique**  
  
-   **Avant de commencer :**  
  
     [Sécurité](#Security)  
  
-   **Pour afficher les données et enregistrer des informations d’espace pour une base de données, à l’aide de :**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Avant de commencer  
  
###  <a name="Security"></a> Sécurité  
  
####  <a name="Permissions"></a> Permissions  
 L’autorisation d’exécuter **sp_spaceused** est accordée au rôle **public** . Seuls les membres du rôle de base de données fixe **db_owner** peuvent spécifier le paramètre **@updateusage** .  
  
##  <a name="SSMSProcedure"></a> Utilisation de SQL Server Management Studio  
  
#### <a name="to-display-data-and-log-space-information-for-a-database"></a>Pour afficher les informations sur l'espace occupé par les données et par le journal d'une base de données  
  
1.  Dans l'Explorateur d'objets, connectez-vous à une instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] et développez-la.  
  
2.  Développez **Bases de données**.  
  
3.  Cliquez avec le bouton droit sur une base de données, pointez sur **Rapports**, sur **Rapports standard**, puis cliquez sur **Utilisation du disque**.  
  
##  <a name="TsqlProcedure"></a> Utilisation de Transact-SQL  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-using-spspaceused"></a>Pour afficher les informations sur l'espace occupé par les données et par le journal d'une base de données à l'aide de sp_spaceused  
  
1.  Connectez-vous au [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dans la barre d'outils standard, cliquez sur **Nouvelle requête**.  
  
3.  Copiez et collez l'exemple suivant dans la fenêtre de requête, puis cliquez sur **Exécuter**. Cet exemple utilise la procédure stockée système [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) pour communiquer des informations sur l’espace disque pour la table `Vendor` et ses index.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-querying-sysdatabasefiles"></a>Pour afficher les informations sur l'espace occupé par les données et par le journal d'une base de données en interrogeant sys.database_files  
  
1.  Connectez-vous au [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dans la barre d'outils standard, cliquez sur **Nouvelle requête**.  
  
3.  Copiez et collez l'exemple suivant dans la fenêtre de requête, puis cliquez sur **Exécuter**. L’exemple suivant interroge l’affichage catalogue [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) pour retourner des informations spécifiques sur les fichiers de données et les fichiers journaux de la base de données [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name, type_desc, physical_name, size, max_size  
FROM sys.database_files ;  
GO  
  
```  
  
## <a name="see-also"></a>Voir aussi  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sp_spaceused &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)   
 [Ajouter des fichiers de données ou journaux à une base de données](add-data-or-log-files-to-a-database.md)   
 [Supprimer des fichiers de données ou des fichiers journaux d'une base de données](delete-data-or-log-files-from-a-database.md)  
  
  