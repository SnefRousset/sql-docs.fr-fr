---
title: "Utiliser les strat&#233;gies Always On pour afficher l’int&#233;grit&#233; d’un groupe de disponibilit&#233; (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "groupes de disponibilité [SQL Server], stratégies"
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
caps.latest.revision: 17
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 16
---
# Utiliser les strat&#233;gies Always On pour afficher l’int&#233;grit&#233; d’un groupe de disponibilit&#233; (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Cette rubrique explique comment déterminer l’état opérationnel d’un groupe de disponibilité Always On à l’aide d’une stratégie Always On dans [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou PowerShell dans [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Pour plus d’informations sur la gestion basée sur les stratégies Always On, consultez [Stratégies Always On pour les problèmes opérationnels avec des groupes de disponibilité Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always on policies for operational issues - always on availability.md).  
  
> [!IMPORTANT]  
>  Pour les stratégies Always On, les noms de catégorie sont utilisés comme identificateurs. Modifier le nom d’une catégorie Always On compromettrait sa fonctionnalité d’évaluation de l’intégrité. Par conséquent, les noms de catégorie Always On ne doivent jamais être modifiés.  
  
-   **Avant de commencer :** [Sécurité](#Security)  
  
-   **Utiliser les stratégies Always On pour afficher l’intégrité d’un groupe de disponibilité, avec :**  
  
     [Tableau de bord Always On](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Avant de commencer  
  
###  <a name="Security"></a> Sécurité  
  
####  <a name="Permissions"></a> Autorisations  
 Requiert les autorisations CONNECT, VIEW SERVER STATE et VIEW ANY DEFINITION.  
  
##  <a name="SSMSProcedure"></a> Utilisation du tableau de bord Always On  
 **Pour ouvrir le tableau de bord Always On**  
  
1.  Dans l'Explorateur d'objets, connectez-vous à l'instance de serveur qui héberge l'un des réplicas de disponibilité. Pour afficher des informations sur tous les réplicas de disponibilité d'un groupe de disponibilité, utilisez l'instance de serveur qui héberge le réplica principal.  
  
2.  Cliquez sur le nom du serveur pour développer son arborescence.  
  
3.  Développez le nœud **Haute disponibilité Always On**.  
  
     Cliquez avec le bouton droit sur le nœud **Groupes de disponibilité** ou développez ce nœud et cliquez avec le bouton droit sur un groupe de disponibilité spécifique.  
  
4.  Sélectionnez la commande **Afficher le tableau de bord** .  
  
 Pour plus d’informations sur l’utilisation du tableau de bord Always On, consultez [Utiliser le tableau de bord Always On &#40;SQL Server Management Studio&#41;](../Topic/Use%20the%20Always On%20Dashboard%20\(SQL%20Server%20Management%20Studio\).md).  
  
##  <a name="PowerShellProcedure"></a> Utilisation de PowerShell  
 **Utiliser les stratégies Always On pour afficher l’intégrité d’un groupe de disponibilité**  
  
1.  Définissez la valeur par défaut (**cd**) sur une instance de serveur qui héberge l’un des réplicas de disponibilité. Pour afficher des informations sur tous les réplicas de disponibilité d'un groupe de disponibilité, utilisez l'instance de serveur qui héberge le réplica principal.  
  
2.  Utilisez les applets de commande suivantes :  
  
     **Test-SqlAvailabilityGroup**  
     Évalue l'intégrité d'un groupe de disponibilité lors de l'évaluation des stratégies de gestion basées sur des stratégies SQL Server. Vous devez disposer des autorisations CONNECT, VIEW SERVER STATE et VIEW ANY DEFINITION pour exécuter cette applet de commande.  
  
     Par exemple, la commande suivante affiche tous les groupes de disponibilité avec l’état d’intégrité « Erreur » sur l’instance de serveur `Computer\Instance`.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups `   
    | Test-SqlAvailabilityGroup | Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     **Test-SqlAvailabilityReplica**  
     Évalue l'intégrité des réplicas de disponibilité lors de l'évaluation des stratégies de gestion basées sur des stratégies SQL Server. Vous devez disposer des autorisations CONNECT, VIEW SERVER STATE et VIEW ANY DEFINITION pour exécuter cette applet de commande.  
  
     Par exemple, la commande suivante évalue l'intégrité du réplica de disponibilité nommé `MyReplica` dans le groupe de disponibilité `MyAg` et génère un bref résumé.  
  
    ```  
    Test-SqlAvailabilityReplica `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     **Test-SqlDatabaseReplicaState**  
     Évalue l'intégrité d'une base de données de disponibilité sur tous les réplicas de disponibilité joints par l'évaluation des stratégies de gestion basées sur des stratégies SQL Server.  
  
     Par exemple, la commande suivante évalue l'intégrité de toutes les bases de données de disponibilité du groupe de disponibilité `MyAg` et génère un bref résumé pour chaque base de données.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates `   
     | Test-SqlDatabaseReplicaState  
    ```  
  
     Ces applets de commande acceptent les options suivantes :  
  
    |Option|Description|  
    |------------|-----------------|  
    |**AllowUserPolicies**|Exécute des stratégies d’utilisateur présentes dans les catégories de stratégie Always On.|  
    |**InputObject**|Collection d'objets qui représentent des groupes de disponibilité, des réplicas de disponibilité ou des états de base de données de disponibilité (selon les applets de commande que vous utilisez). L'applet de commande calcule l'intégrité des objets spécifiés.|  
    |**NoRefresh**|Quand ce paramètre est défini, l’applet de commande n’actualise pas manuellement les objets spécifiés par le paramètre **-Path** ou **-InputObject**.|  
    |**Chemin d'accès**|Chemin d'accès au groupe de disponibilité, à un ou plusieurs réplicas de disponibilité ou à l'état de cluster de réplica de la base de données de disponibilité (selon les applets de commande que vous utilisez). Il s'agit d'un paramètre facultatif. Si elle n'est pas spécifiée, la valeur de ce paramètre est définie par défaut à l'emplacement de travail actuel.|  
    |**ShowPolicyDetails**|Indique le résultat de chaque évaluation de la stratégie exécutée par cette applet de commande. L'applet de commande génère un objet par évaluation de stratégie, et cet objet comporte des champs décrivant les résultats de l'évaluation (que la stratégie ait réussi ou non, le nom de la stratégie et la catégorie, etc.).|  
  
     Par exemple, la commande **Test-SqlAvailabilityGroup** suivante spécifie le paramètre **ShowPolicyDetails** pour afficher le résultat de chaque évaluation de stratégie exécutée par cette applet de commande pour chaque stratégie de gestion basée sur des stratégies (PBM) exécutée sur le groupe de disponibilité nommé `MyAg`.  
  
    ```  
    Test-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName `  
    -ShowPolicyDetails  
  
    ```  
  
    > [!NOTE]  
    >  Pour voir la syntaxe d’une applet de commande, utilisez l’applet de commande **Get-Help** dans l’environnement [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Pour en savoir plus, voir [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Pour configurer et utiliser le fournisseur SQL Server PowerShell**  
  
-   [fournisseur PowerShell SQL Server](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Obtenir de l'aide sur SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="RelatedContent"></a> Contenu connexe  
 **Blogs de l’équipe de SQL Server Always On - Surveillance de l’intégrité Always On avec PowerShell :**  
  
-   [Partie 1 : Vue d'ensemble de l'applet de commande](http://blogs.msdn.com/b/sqlAlways%20On/archive/2012/02/13/monitoring-Always%20On-health-with-powershell-part-1.aspx)  
  
-   [Partie 2 : Utilisation avancée de l'applet de commande](http://blogs.msdn.com/b/sqlAlways%20On/archive/2012/02/13/monitoring-Always%20On-health-with-powershell-part-2.aspx)  
  
-   [Partie 3 : Application de surveillance simple](http://blogs.msdn.com/b/sqlAlways%20On/archive/2012/02/15/monitoring-Always%20On-health-with-powershell-part-3.aspx)  
  
-   [Partie 4 : Intégration à l'Agent SQL Server](http://blogs.msdn.com/b/sqlAlways%20On/archive/2012/02/15/the-always-on-health-model-part-4.aspx)  
  
## Voir aussi  
 [Vue d’ensemble des groupes de disponibilité Always On &#40;SQL Server&#41;](../Topic/Overview%20of%20Always On%20Availability%20Groups%20\(SQL%20Server\).md)   
 [Administration d’un groupe de disponibilité &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [Surveillance des groupes de disponibilité &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [Stratégies Always On pour les problèmes opérationnels avec des groupes de disponibilité Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always on policies for operational issues - always on availability.md)  
  
  