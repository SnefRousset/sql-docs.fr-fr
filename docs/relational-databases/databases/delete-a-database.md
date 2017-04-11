---
title: "Supprimer une base de donn&#233;es | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "suppression de bases de données [SQL Server], SQL Server Management Studio"
  - "suppression de bases de données"
  - "suppression de bases de données"
  - "élimination de bases de données"
  - "bases de données [SQL Server], élimination"
  - "suppression de bases de données [SQL Server]"
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Supprimer une base de donn&#233;es
  Cette rubrique explique comment supprimer une base de données définie par l'utilisateur dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dans [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] à l'aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Dans cette rubrique**  
  
-   **Avant de commencer :**  
  
     [Limitations et restrictions](#Restrictions)  
  
     [Conditions préalables](#Prerequisites)  
  
     [Recommandations](#Recommendations)  
  
     [Sécurité](#Security)  
  
-   **Pour supprimer une base de données, utilisez :**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Suivi :**  [Après la suppression d'une base de données](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Avant de commencer  
  
###  <a name="Restrictions"></a> Limitations et restrictions  
  
-   Les bases de données système ne peuvent pas être supprimées.  
  
###  <a name="Prerequisites"></a> Configuration requise  
  
-   Supprimez les instantanés de la base de données qui existent. Pour plus d’informations, consultez [Supprimer un instantané de base de données &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
-   Si la base de données intervient dans l'envoi de journaux, supprimez l'envoi de journaux.  
  
-   Si la base de données est publiée pour une réplication transactionnelle, ou encore publiée ou souscrite pour une réplication de fusion, supprimez la réplication.  
  
###  <a name="Recommendations"></a> Recommandations  
  
-   Effectuez une sauvegarde complète de la base de données. Vous ne pouvez recréer une base de données supprimée qu'en restaurant une copie de sauvegarde.  
  
###  <a name="Security"></a> Sécurité  
  
####  <a name="Permissions"></a> Autorisations  
 Pour exécuter DROP DATABASE, un utilisateur doit au moins disposer de l'autorisation CONTROL sur la base de données.  
  
##  <a name="SSMSProcedure"></a> Utilisation de SQL Server Management Studio  
  
#### Pour supprimer une base de données  
  
1.  Dans l' **Explorateur d'objets**, connectez-vous à une instance du [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], puis développez-la.  
  
2.  Développez le dossier **Bases de données**, cliquez avec le bouton droit sur la base de données à supprimer, puis cliquez sur **Supprimer**.  
  
3.  Vérifiez que la base de données correcte est sélectionnée, puis cliquez sur **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilisation de Transact-SQL  
  
#### Pour supprimer une base de données  
  
1.  Connectez-vous au [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dans la barre d'outils standard, cliquez sur **Nouvelle requête**.  
  
3.  Copiez et collez l'exemple suivant dans la fenêtre de requête, puis cliquez sur **Exécuter**. L'exemple suivant supprime les bases de données `Sales` et `NewSales` .  
  
```tsql  
USE master ;  
GO  
DROP DATABASE Sales, NewSales ;  
GO  
```  
  
##  <a name="FollowUp"></a> Suivi : Après la suppression d'une base de données  
 Sauvegardez la base de données **master** . Si vous devez restaurer la base de données **master** , toutes les bases de données supprimées depuis la dernière sauvegarde de **master** seront encore référencées dans les vues du catalogue système, ce qui risque de générer des messages d'erreur.  
  
## Voir aussi  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  