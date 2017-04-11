---
title: "G&#233;rer des bases de donn&#233;es&#160;DQS | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 655a67aa-d662-42f2-b982-c6217125ada8
caps.latest.revision: 14
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 14
---
# G&#233;rer des bases de donn&#233;es&#160;DQS
  Cette section fournit des informations sur les activités de gestion de bases de données qui peuvent être effectuées sur des bases de données DQS, telles que la sauvegarde/restauration ou le détachement et l'attachement.  
  
##  <a name="BackupRestore"></a> Sauvegarder et restaurer les bases de données DQS  
 La sauvegarde et la restauration de bases de données SQL Server sont des opérations courantes que les administrateurs de bases de données exécutent pour empêcher la perte de données en cas d'incident lors de la récupération de données à partir des bases de données de sauvegarde. [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] est implémentée principalement par deux bases de données SQL Server : DQS_MAIN et DQS_PROJECTS. Les procédures de sauvegarde et de restauration des bases de données [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) sont similaires à celles de toute autre base de données SQL Server. Il existe trois défis inhérents à la sauvegarde et à la restauration des bases de données DQS :  
  
-   Les opérations de sauvegarde et de restauration des bases de données de DQS doivent être synchronisées. Sinon la base de données [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] restaurée ne sera pas fonctionnelle.  
  
-   Les deux bases de données DQS, DQS_MAIN et DQS_PROJECTS, contiennent des assemblys et autres objets complexes, indépendamment des seuls objets simples de base de données (tels que tables et procédures stockées).  
  
-   Il existe certaines entités extérieures aux bases de données DQS nécessaires pour que les bases de données DQS soient fonctionnelles, comme [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], en particulier les deux connexions SQL Server (##MS_dqs_db_owner_login## et ##MS_dqs_service_login##), et une procédure stockée d'initialisation (DQInitDQS_MAIN) dans la base de données MASTER.  
  
 Pour obtenir des informations détaillées sur la sauvegarde et la restauration dans SQL Server, consultez [Back Up and Restore of SQL Server Databases](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
### Taille de croissance automatique et mode de récupération par défaut des bases de données DQS  
 Pour éviter que les bases de données DQS et les journaux des transactions se développent à l'infini et saturent potentiellement le disque dur :  
  
-   La taille de **Croissance automatique** par défaut des bases de données DQS est définie à 10 %.  
  
-   Le mode de récupération par défaut des bases de données DQS est défini sur **Simple**. En mode de récupération simple, les transactions sont journalisées de façon minimale et la troncation du journal se produit automatiquement une fois que la transaction est terminée pour libérer de l'espace dans le journal des transactions (fichier .ldf). Pour plus d’informations sur le modèle de récupération simple, consultez [sauvegardes complètes de base de données & #40 ; SQL Server & #41 ;](../relational-databases/backup-restore/full-database-backups-sql-server.md).  
  
> [!IMPORTANT]  
>  -   En mode de récupération simple, lorsque les enregistrements du journal restent actifs longtemps (par exemple, lors d'une longue transaction), la troncation peut être différée et peut donc entraîner la saturation du journal des transactions. Par ailleurs, la troncation du journal ne réduit pas la taille du fichier journal physique (fichier .ldf). Pour réduire la taille d'un fichier journal physique, vous devez réduire le fichier journal. Pour plus d’informations sur la résolution des problèmes liés au journal des transactions, consultez la page [du journal des transactions & #40 ; SQL Server & #41 ;](../relational-databases/logs/the-transaction-log-sql-server.md) ou l’article de Support Microsoft à [http://go.microsoft.com/fwlink/?LinkId=237446](http://go.microsoft.com/fwlink/?LinkId=237446).  
> -   Vous devez effectuer régulièrement une sauvegarde complète ou différentielle des bases de données DQS et sauvegarder le journal des transactions pour récupérer les données jusqu'à une date et une heure spécifiques. Pour plus d’informations, consultez [sauvegardes complètes de base de données & #40 ; SQL Server & #41 ;](../relational-databases/backup-restore/full-database-backups-sql-server.md) et [sauvegarder un journal des transactions & #40 ; SQL Server & #41 ;](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  
  
##  <a name="DetachAttach"></a> Attacher et détacher les bases de données DQS  
 Vous pouvez détacher les données et les fichiers journaux des transactions des bases de données DQS, puis rattachez les bases de données à la même instance ou à une autre instance de SQL Server si vous souhaitez remplacer les bases de données DQS par une autre instance de SQL Server sur le même ordinateur ou les déplacer.  
  
 Pour plus d’informations sur les éléments à prendre en compte avant et pendant le détachement et attachement de bases de données SQL Server, consultez [détachement de la base de données et attacher & #40 ; SQL Server & #41 ;](../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
## Tâches associées  
  
|Description de la tâche|Rubrique|  
|----------------------|-----------|  
|Explique comment sauvegarder et restaurer les bases de données DQS.|[Sauvegarde et restauration de bases de données DQS](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|Décrit comment détacher et attacher les bases de données DQS.|[Detaching and Attaching DQS Databases](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## Voir aussi  
 [Administration de DQS](../data-quality-services/dqs-administration.md)  
  
  