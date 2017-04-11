---
title: "Mise en miroir et instantan&#233;s de bases de donn&#233;es (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mise en miroir de bases de données [SQL Server], interopérabilité"
  - "instantanés [instantanés de base de données SQL Server], mise en miroir de bases de données"
  - "instantanés [SQL Server], mise en miroir de bases de données"
ms.assetid: 0bf1be90-7ce4-484c-aaa7-f8a782f57c5f
caps.latest.revision: 41
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 40
---
# Mise en miroir et instantan&#233;s de bases de donn&#233;es (SQL Server)
  Une base de données miroir maintenue à des fins de disponibilité peut être utilisée dans le but de décharger la création de rapports. Pour utiliser une base de données miroir à des fins de création de rapports, créez un instantané de base de données sur la base de données miroir et redirigez les requêtes de connexions clientes vers l'instantané le plus récent. Un instantané de base de données est une image – statique, en lecture seule et cohérente par rapport aux transactions – de sa base de données source telle qu'elle existait au moment de la création de l'instantané. Pour créer un instantané de base de données dans une base de données miroir, la base de données doit être dans un état de mise en miroir synchronisée.  
  
 Contrairement à la base de données miroir, un instantané de base de données est accessible à tous les clients. Tant que le serveur miroir communique avec le serveur principal, vous pouvez demander aux clients sources des rapports de se connecter à un instantané. Notez qu'un instantané de base de données étant statique, les nouvelles données ne sont pas disponibles. Pour que les utilisateurs puissent accéder aux données relativement récentes, un instantané de base de données doit être créé régulièrement et les applications doivent diriger les connexions clientes entrantes vers ce nouvel instantané.  
  
 Un nouvel instantané de base de données est pratiquement vide mais, au fil du temps, il grossit à mesure qu'un nombre croissant de pages de base de données sont mises à jour pour la première fois. Du fait de ce mode de croissance incrémentielle des instantanés dans une base de données, chaque instantané consomme autant de ressources qu'une base de données classique. Selon les configurations du serveur miroir et du serveur principal, la présence d'un nombre excessif d'instantanés dans une base de données miroir peut réduire les performances dans la base de données principale. Nous vous recommandons donc de conserver uniquement quelques instantanés relativement récents dans vos bases de données miroir. Normalement, une fois que vous avez créé un instantané de remplacement, vous devez rediriger les requêtes entrantes vers le nouvel instantané et supprimer l'instantané antérieur après avoir exécuté toutes les requêtes en cours.  
  
> [!NOTE]  
>  Pour plus d’informations sur les instantanés de base de données, consultez [Instantanés de base de données &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
 S'il se produit un basculement de rôle, la base de données et ses instantanés sont redémarrés, ce qui entraîne une déconnexion temporaire des utilisateurs. Ensuite, les instantanés de base de données demeurent sur l'instance de serveur où ils ont été créés et qui est devenue la nouvelle base de données principale. Les utilisateurs peuvent continuer à utiliser ces instantanés après le basculement. Cependant, il s'ensuit une charge supplémentaire sur le nouveau serveur principal. Si les performances constituent l'une de vos préoccupations majeures, nous vous recommandons de créer un instantané sur la nouvelle base de données miroir dès qu'elle est disponible, de rediriger les clients vers le nouvel instantané et de supprimer de la base de données miroir précédente l'ensemble des instantanés de base de données.  
  
> [!NOTE]  
>  Pour une solution de création de rapports dotée d'une bonne capacité de déploiement horizontal, envisagez la réplication. Pour plus d’informations, consultez [Réplication SQL Server](../../relational-databases/replication/sql-server-replication.md).  
  
## Exemple  
 Cet exemple créé des instantanés de bases de données sur une base de données miroir.  
  
 Imaginons que la base de données d'une session de mise en miroir de base de données soit la base de données [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Cet exemple crée trois instantanés de base de données sur la copie miroir de la base de données `AdventureWorks` qui réside sur le lecteur `F`. Les noms des instantanés sont `AdventureWorks_0600`, `AdventureWorks_1200` et `AdventureWorks_1800` ; ils identifient les heures de création approximatives des captures.  
  
1.  Créez le premier instantané de base de données sur le miroir de la base de données [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
    ```  
    CREATE DATABASE AdventureWorks_0600  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_0600.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
2.  Créez le deuxième instantané de base de données sur le miroir de la base de données [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Les utilisateurs qui se servent encore de `AdventureWorks_0600` peuvent continuer à le faire.  
  
    ```  
    CREATE DATABASE AdventureWorks_1200  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1200.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     À ce stade, les nouvelles connexions clientes peuvent être orientées, par programme, vers l'instantané le plus récent.  
  
3.  Créez le troisième instantané de base de données sur le miroir de la base de données [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Les utilisateurs qui se servent encore de `AdventureWorks_0600` ou de `AdventureWorks_1200` peuvent continuer à le faire.  
  
    ```  
    CREATE DATABASE AdventureWorks_1800  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1800.SNP')  
        AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     À ce stade, les nouvelles connexions clientes peuvent être orientées, par programme, vers l'instantané le plus récent.  
  
##  <a name="RelatedTasks"></a> Tâches associées  
  
-   [Créer un instantané de base de données &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Afficher un instantané de base de données &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Supprimer un instantané de base de données &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
 ![Icône de flèche utilisée avec le lien Retour en haut](../../analysis-services/instances/media/uparrow16x16.png "Icône de flèche utilisée avec le lien Retour en haut") [&#91;Haut&#93;](#Top)  
  
## Voir aussi  
 [Instantanés de base de données &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [Connecter des clients à une session de mise en miroir de bases de données &#40;SQL Server&#41;](../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  