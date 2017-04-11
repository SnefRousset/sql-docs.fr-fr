---
title: "D&#233;sactiver Stretch Database et r&#233;cup&#233;rer les donn&#233;es distantes | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "08/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch Database, désactivation"
  - "désactivation de Stretch Database"
ms.assetid: c1bbb24e-47e3-46aa-b786-fcadf9fb65ce
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# D&#233;sactiver Stretch Database et r&#233;cup&#233;rer les donn&#233;es distantes
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Afin de désactiver Stretch Database pour une table, sélectionnez **Stretch** pour une table dans SQL Server Management Studio. Puis sélectionnez l'une des options suivantes.  
  
-   **Désactiver | Récupérer les données à partir d’Azure**. Copiez les données distantes pour la table d'Azure vers SQL Server, puis désactivez Stretch Database pour la table. Cette opération entraîne des coûts de transfert de données et ne peut pas être annulée.  
  
-   **Désactiver | Laisser les données dans Azure**. Désactivez Stretch Database pour la table.  Abandonnez les données distantes pour la table dans Azure.  
  
 Vous pouvez également utiliser Transact-SQL pour désactiver Stretch Database pour une table ou une base de données.  
  
 Après avoir désactivé Stretch Database pour une table, la migration des données s’arrête et les résultats de la requête n'incluent plus les résultats de la table distante.  
  
 Si vous voulez simplement interrompre la migration des données, consultez [Suspension et reprise de la migration des données &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
> [!NOTE] La désactivation de Stretch Database pour une table ou une base de données ne supprime pas l'objet distant. Si vous souhaitez supprimer la table distante ou la base de données distante, vous devez la supprimer à l'aide du portail de gestion Azure. Les objets distants continuent d’entraîner des coûts Azure tant qu’ils n’ont pas été supprimés. Pour plus d'informations, consultez la rubrique [Tarification de SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## Désactiver Stretch Database pour une table  
  
### Utiliser SQL Server Management Studio afin de désactiver Stretch Database pour une table  
  
1.  Dans SQL Server Management Studio, dans l'Explorateur d'objets, sélectionnez la table pour laquelle vous souhaitez désactiver Stretch Database.  
  
2.  Cliquez avec le bouton droit, sélectionnez **Stretch**, puis choisissez l’une des options suivantes.  
  
    -   **Désactiver | Récupérer les données à partir d’Azure**. Copiez les données distantes pour la table d'Azure vers SQL Server, puis désactivez Stretch Database pour la table. Cette commande ne peut pas être annulée.  
  
        > [!NOTE] La copie des données distantes pour la table d'Azure vers SQL Server entraîne des coûts de transfert de données. Pour plus d'informations, consultez la rubrique [Détails de la tarification des transferts de données](https://azure.microsoft.com/pricing/details/data-transfers/).  
  
         Une fois que toutes les données distantes ont été copiées d'Azure vers SQL Server, Stretch est désactivée pour la table.  
  
    -   **Désactiver | Laisser les données dans Azure**. Désactivez Stretch Database pour la table.  Abandonnez les données distantes pour la table dans Azure.  
  
    > [!NOTE] La désactivation de Stretch Database pour une table ne supprime pas l'objet distant ou la table distante. Si vous souhaitez supprimer la table distante, vous devez la supprimer à l'aide du portail de gestion Azure. La table distante continue d’entraîner des coûts Azure tant qu’elle n’a pas été supprimée. Pour plus d'informations, consultez la rubrique [Tarification de SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### Utilisation de Transact-SQL pour désactiver Stretch Database sur une table  
  
-   Pour désactiver Stretch pour une table et copier les données distantes pour la table d’Azure vers SQL Server, exécutez la commande suivante. Une fois que toutes les données distantes ont été copiées d’Azure vers SQL Server, Stretch est désactivé pour la table.

    Cette commande ne peut pas être annulée.  
  
    ```tsql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ; 
    GO 
    ```  
  
    > [!NOTE] La copie des données distantes pour la table d'Azure vers SQL Server entraîne des coûts de transfert de données. Pour plus d'informations, consultez la rubrique [Détails de la tarification des transferts de données](https://azure.microsoft.com/pricing/details/data-transfers/).    
  
-   Pour désactiver Stretch pour une table et abandonner les données distantes, exécutez la commande suivante.  
  
    ```tsql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ; 
    GO
    ```  
  
> [!NOTE] La désactivation de Stretch Database pour une table ne supprime pas l'objet distant ou la table distante. Si vous souhaitez supprimer la table distante, vous devez la supprimer à l'aide du portail de gestion Azure. La table distante continue d’entraîner des coûts Azure tant qu’elle n’a pas été supprimée. Pour plus d'informations, consultez la rubrique [Tarification de SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## Désactiver Stretch Database pour une base de données  
 Avant de pouvoir désactiver Stretch Database pour une base de données, vous devez désactiver Stretch Database sur les tables Stretch individuelles dans la base de données.  
  
### Utiliser SQL Server Management Studio afin de désactiver Stretch Database pour une base de données  
  
1.  Dans SQL Server Management Studio, dans l'Explorateur d'objets, sélectionnez la base de données pour laquelle vous souhaitez désactiver Stretch Database.  
  
2.  Cliquez avec le bouton droit, puis sélectionnez **Tâches**, **Stretch** et **Désactiver**.  
  
> [!NOTE] La désactivation de Stretch Database pour une base de données ne supprime pas la base de données distante. Si vous souhaitez supprimer la base de données distante, vous devez la supprimer à l'aide du portail de gestion Azure. La base de données distante continue d’entraîner des coûts Azure tant qu’elle n’a pas été supprimée. Pour plus d'informations, consultez la rubrique [Tarification de SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### Utilisation de Transact-SQL pour désactiver Stretch Database sur une base de données  
 Exécutez la commande suivante :  
  
```tsql  
ALTER DATABASE <Stretch-enabled database name>  
    SET REMOTE_DATA_ARCHIVE = OFF ;  
GO 
```  
  
> [!NOTE] La désactivation de Stretch Database pour une base de données ne supprime pas la base de données distante. Si vous souhaitez supprimer la base de données distante, vous devez la supprimer à l'aide du portail de gestion Azure. La base de données distante continue d’entraîner des coûts Azure tant qu’elle n’a pas été supprimée. Pour plus d'informations, consultez la rubrique [Tarification de SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## Voir aussi  
 [Options ALTER DATABASE SET &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)   
 [Suspension et reprise de la migration de données &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
  