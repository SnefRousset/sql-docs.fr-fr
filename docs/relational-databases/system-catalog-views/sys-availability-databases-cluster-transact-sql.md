---
title: Sys.availability_databases_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_databases_cluster_TSQL
- sys.availability_databases_cluster
- availability_databases_cluster_TSQL
- availability_databases_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.availability_databases_cluster catalog view
- Availability Groups [SQL Server], databases
ms.assetid: 8d9c57e5-7f39-4315-b466-92748231140a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7d312a5ecb60e1ab046b0108e01ef1834adaa900
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47842307"
---
# <a name="sysavailabilitydatabasescluster-transact-sql"></a>sys.availability_databases_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contient une ligne pour chaque base de données de disponibilité sur l’instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qui héberge un réplica de disponibilité pour n’importe quel groupe de disponibilité Always On dans le cluster de Clustering de basculement Windows Server (WSFC), indépendamment de si la copie locale de base de données a été joint au groupe de disponibilité encore.  
  
> [!NOTE]  
>  Lorsqu'une base de données est ajoutée à un groupe de disponibilité, la base de données primaire est automatiquement jointe au groupe. Les bases de données secondaires doivent être préparées sur chaque réplica secondaire avant de pouvoir être jointes au groupe de disponibilité.   
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificateur unique du groupe de disponibilité, le cas échéant, auquel la base de données participe.<br /><br /> NULL = base de données ne fait pas partie d’un réplica de disponibilité du groupe de disponibilité.|  
|**group_database_id**|**uniqueidentifier**|Identificateur unique de la base de données dans le groupe de disponibilité, le cas échéant, auquel la base de données participe. **group_database_id** est identique pour cette base de données sur le réplica principal et sur chaque réplica secondaire sur lequel la base de données a été jointe au groupe de disponibilité.<br /><br /> NULL = La base de données ne fait pas partie d'un réplica de disponibilité dans un groupe de disponibilité.|  
|**database_name**|**sysname**|Nom de la base de données qui a été ajoutée au groupe de disponibilité.|  
  
## <a name="permissions"></a>Permissions  
 Si l’appelant de **sys.availability_databases_cluster** n’est pas le propriétaire de la base de données, les autorisations minimales requises pour consulter la ligne correspondante sont ALTER ANY DATABASE ou autorisation de VIEW ANY DATABASE au niveau du serveur ou créer Autorisation de base de données dans le **master** base de données.  
  
## <a name="see-also"></a>Voir aussi  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [Sys.dm_hadr_database_replica_cluster_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [Vue d’ensemble des groupes de disponibilité Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
