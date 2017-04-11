---
title: "Initialiser manuellement un abonnement | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "initialisation manuelle des abonnements [réplication SQL Server]"
  - "abonnements [réplication SQL Server], initialisation"
  - "initialisation d’abonnements [réplication SQL Server], sans instantanés"
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Initialiser manuellement un abonnement
  Cette rubrique explique comment initialiser manuellement un abonnement dans [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] à l'aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou de [!INCLUDE[tsql](../../includes/tsql-md.md)]. L'instantané initial est normalement utilisé pour initialiser un abonnement, mais les abonnements aux publications peuvent être initialisés sans utiliser d'instantané, à condition que le schéma et les données initiales soient déjà présents sur l'Abonné.  
  

##  <a name="BeforeYouBegin"></a> Avant de commencer  
  
###  <a name="Restrictions"></a> Limitations et restrictions  
  
-   S'il existe une activité sur une base de données publiée à l'aide de la réplication transactionnelle entre le moment où les données et le schéma sont copiés vers l'Abonné et le moment auquel l'abonnement est initialisé manuellement, les modifications résultant de cette activité peuvent ne pas être répliquées vers l'Abonné.  
  
##  <a name="SSMSProcedure"></a> Utilisation de SQL Server Management Studio  
 Initialisez manuellement un abonnement à une publication en copiant le schéma (et généralement les données) dans la base de données d'abonnement. Le schéma et les données doivent correspondre à la base de données de publication. Précisez ensuite que l'abonnement ne nécessite pas de schéma et de données dans la page **Initialiser les abonnements** de l'Assistant Nouvel abonnement. Pour plus d’informations sur l’accès à cet Assistant, consultez la page [initialiser un abonnement transactionnel sans instantané](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) et [créer un abonnement extrait](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Lors de la première synchronisation de l'abonnement, les objets et les métadonnées dont la réplication a besoin sont copiés dans la base de données d'abonnement.  
  
#### Pour initialiser manuellement un abonnement à une publication  
  
1.  Vérifiez que le schéma et les données sont copiés dans la base de données d'abonnement.  
  
2.  Désactivez la case à cocher **Initialiser** dans la page **Initialiser les abonnements** de l'Assistant Nouvel abonnement. Procédez de même pour chaque abonnement nécessitant uniquement la copie des objets et des métadonnées de réplication.  
  
##  <a name="TsqlProcedure"></a> Utilisation de Transact-SQL  
 Les abonnements peuvent être initialisés manuellement à l'aide des procédures stockées de réplication.  
  
#### Pour initialiser manuellement un abonnement par extraction à une publication transactionnelle  
  
1.  Assurez-vous que le schéma et les données existent dans la base de données d'abonnement. Pour plus d’informations, consultez [initialiser un abonnement transactionnel sans instantané](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  Sur le serveur de publication sur la base de données de publication, exécutez [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Spécifiez **@publication**, **@subscriber**, le nom de la base de données sur l’abonné contenant les données publiées pour **@destination_db**, une valeur de **extraction** pour **@subscription_type**, et la valeur **prise en charge de la réplication uniquement** pour **@sync_type**. Pour plus d'informations, voir [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  Sur l’Abonné, exécutez [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Pour les abonnements mis à jour, consultez [créer un abonnement à une Publication transactionnelle actualisable](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
4.  Sur l’Abonné, exécutez [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Pour plus d'informations, voir [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Démarrez l'Agent de distribution pour transférer des objets de réplication et télécharger les modifications les plus récentes à partir du serveur de publication. Pour plus d'informations, voir [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Pour initialiser manuellement un abonnement par émission de données à une publication transactionnelle  
  
1.  Assurez-vous que le schéma et les données existent dans la base de données d'abonnement. Pour plus d’informations, consultez [initialiser un abonnement transactionnel sans instantané](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  Sur le serveur de publication sur la base de données de publication, exécutez [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Spécifiez le nom de la base de données sur l’abonné contenant les données publiées pour **@destination_db**, une valeur de **push** pour **@subscription_type**, et la valeur **prise en charge de la réplication uniquement** pour **@sync_type**. Pour les abonnements mis à jour, consultez [créer un abonnement à une Publication transactionnelle actualisable](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
3.  Sur le serveur de publication sur la base de données de publication, exécutez [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Pour plus d'informations, voir [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Démarrez l'Agent de distribution pour transférer des objets de réplication et télécharger les modifications les plus récentes à partir du serveur de publication. Pour plus d'informations, voir [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### Pour initialiser manuellement un abonnement par extraction à une publication de fusion  
  
1.  Assurez-vous que le schéma et les données existent dans la base de données d'abonnement. Pour cela, vous pouvez restaurer une sauvegarde de la base de données de publication sur l'Abonné.  
  
2.  Sur le serveur de publication, exécutez [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Spécifiez **@publication**, **@subscriber**, **@subscriber_db**, et la valeur **extraction** pour **@subscription_type**. L'abonnement par extraction est inscrit.  
  
3.  Sur la base de données contenant les données publiées de l’abonné, exécutez [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Spécifiez la valeur **aucun** pour **@sync_type**.  
  
4.  Sur l’abonné, exécutez [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Pour plus d'informations, voir [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Démarrez l'Agent de fusion pour transférer des objets de réplication et télécharger les modifications les plus récentes à partir du serveur de publication. Pour plus d'informations, voir [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Pour initialiser manuellement un abonnement par émission de données à une publication de fusion  
  
1.  Assurez-vous que le schéma et les données existent dans la base de données d'abonnement. Pour cela, vous pouvez restaurer une sauvegarde de la base de données de publication sur l'Abonné.  
  
2.  Sur le serveur de publication sur la base de données de publication, exécutez [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Spécifiez le nom de la base de données sur l’abonné contenant les données publiées pour **@subscriber_db**, une valeur de **push** pour **@subscription_type**, et la valeur **aucun** pour **@sync_type**.  
  
3.  Sur le serveur de publication sur la base de données de publication, exécutez [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Pour plus d'informations, voir [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Démarrez l'Agent de fusion pour transférer des objets de réplication et télécharger les modifications les plus récentes à partir du serveur de publication. Pour plus d'informations, voir [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## Voir aussi  
 [Initialiser un abonnement transactionnel sans instantané](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [Sauvegarder et restaurer des bases de données répliquées](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Méthodes préconisées en matière de sécurité de réplication](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  