---
title: Configurer l’option de configuration de serveur network packet size | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default packet size
- size [SQL Server], packets
- packets [SQL Server], size
- network packet size option
ms.assetid: 236985bf-fc4a-4a57-98f7-a71ef977fd7b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 22f78cc38a71f518d5223e9f310588c4d55bdf88
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640020"
---
# <a name="configure-the-network-packet-size-server-configuration-option"></a>Configurer l'option de configuration de serveur network packet size
  Cette rubrique explique comment configurer le `network packet size` option de configuration de serveur dans [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] à l’aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Le `network packet size` option définit la taille de paquet (en octets) utilisée sur tout le réseau. Les paquets constituent les morceaux de taille définie de données qui transfèrent les requêtes et les résultats entre les clients et les serveurs. La taille des paquets par défaut est 4 096 octets.  
  
> [!NOTE]  
>  Ne modifiez pas la taille des paquets, sauf si vous êtes certain que cela permettra d'accroître les performances. Pour la plupart des applications, la taille de paquet par défaut représente la meilleure solution.  
  
 **Dans cette rubrique**  
  
-   **Avant de commencer :**  
  
     [Limitations et restrictions](#Restrictions)  
  
     [Recommandations](#Recommendations)  
  
     [Sécurité](#Security)  
  
-   **Pour configurer l'option network packet size, utilisez :**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Suivi :**  [Après avoir configuré l’option network packet size](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Avant de commencer  
  
###  <a name="Restrictions"></a> Limitations et restrictions  
  
-   La taille de paquet réseau maximale pour les connexions chiffrées est 16 383 octets.  
  
###  <a name="Recommendations"></a> Recommandations  
  
-   Cette option avancée ne doit être modifiée que par un administrateur de base de données qualifié ou un technicien agréé [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Si une application effectue des opérations de copie en bloc, ou envoie ou reçoit de grandes quantités de données de type texte ou image, l'utilisation d'une taille de paquet supérieure à la taille par défaut peut améliorer les performances car elle permet de réduire les opérations de lecture et d'écriture sur le réseau. Si une application envoie et reçoit de petites quantités d'informations, la taille de paquets peut être définie à 512 octets, ce qui est suffisant pour la plupart des transferts de données.  
  
-   Pour des systèmes utilisant différents protocoles réseau, attribuez à l’option network packet size la taille adaptée au protocole le plus utilisé. L'option network packet size permet d'accroître les performances lorsque les protocoles réseau prennent en charge les paquets de grande taille. Les applications clientes peuvent remplacer cette valeur.  
  
-   Vous pouvez également appeler les fonctions OLE DB, ODBC (Open Database Connectivity ) et DB-Library pour demander une modification de la taille des paquets. Si le serveur ne peut pas prendre en charge la taille des paquets demandée, le [!INCLUDE[ssDE](../../includes/ssde-md.md)] envoie un message d’avertissement au client. Dans certains cas, la modification de la taille des paquets peut entraîner un échec de la liaison de communication, tel que :  
  
     `Native Error: 233, no process is on the other end of the pipe.`  
  
###  <a name="Security"></a> Sécurité  
  
####  <a name="Permissions"></a> Permissions  
 Les autorisations d’exécution de **sp_configure** , sans paramètre ou avec le premier paramètre uniquement, sont accordées par défaut à tous les utilisateurs. Pour exécuter **sp_configure** avec les deux paramètres afin de modifier une option de configuration ou d’exécuter l’instruction RECONFIGURE, un utilisateur doit disposer de l’autorisation de niveau serveur ALTER SETTINGS. L'autorisation ALTER SETTINGS est implicitement détenue par les rôles serveur fixes **sysadmin** et **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilisation de SQL Server Management Studio  
  
#### <a name="to-configure-the-network-packet-size-option"></a>Pour configurer l'option network packet size  
  
1.  Dans l’Explorateur d’objets, cliquez avec le bouton droit sur un serveur et sélectionnez **Propriétés**.  
  
2.  Cliquez sur le nœud **Avancé** .  
  
3.  Sous **Réseau**, sélectionnez une valeur pour la zone **Taille du paquet réseau** .  
  
##  <a name="TsqlProcedure"></a> Utilisation de Transact-SQL  
  
#### <a name="to-configure-the-network-packet-size-option"></a>Pour configurer l'option network packet size  
  
1.  Connectez-vous au [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dans la barre d'outils standard, cliquez sur **Nouvelle requête**.  
  
3.  Copiez et collez l'exemple suivant dans la fenêtre de requête, puis cliquez sur **Exécuter**. Cet exemple montre comment utiliser [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) pour attribuer à l’option `network packet size` la valeur `6500` octets.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'network packet size', 6500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Pour plus d’informations, consultez [Options de configuration de serveur &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Suivi : Après avoir configuré l’option network packet size  
 Le paramètre prend effet immédiatement sans redémarrage du serveur.  
  
## <a name="see-also"></a>Voir aussi  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Options de configuration de serveur &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
