---
title: Sys.resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9ed2152873f40fd2f2ded34a11a2cfded2fbe2a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823538"
---
# <a name="sysresourcegovernorexternalresourcepools-transact-sql"></a>Sys.resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**S’applique à** : [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] et [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Retourne la configuration de pool de ressources externes stockées dans [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Chaque ligne de la vue détermine la configuration d'un pool.
  
|Nom de colonne|Type de données|Description|
|-----------------|---------------|-----------------|
|pool_id|**Int**|ID unique du pool de ressources. N'accepte pas la valeur NULL.<br /><br /> **Remarque :** peut être renommée dans le futur.|
|NAME|**sysname**|Nom du pool de ressources. N'accepte pas la valeur NULL.|
|max_cpu_percent|**Int**|Bande passante processeur moyenne maximale pour toutes les demandes dans le pool de ressources en cas de contention du processeur. N'accepte pas la valeur NULL.|
|max_memory_percent|**Int**|Pourcentage de la mémoire totale du serveur qui peut être utilisé par les demandes dans ce pool de ressources. N'accepte pas la valeur NULL. La valeur maximale effective dépend des valeurs minimales du pool. Par exemple, max_memory_percent peut avoir la valeur 100, alors que sa valeur maximale effective est inférieure.|
|max_processes|**Int**|Nombre maximal de processus externes simultanées. La valeur par défaut 0 spécifie qu'il n'y a pas de limite. N'accepte pas la valeur NULL.|
|version|**bigint**|Numéro de version interne.|
  
## <a name="permissions"></a>Permissions

Requiert l'autorisation VIEW SERVER STATE.

## <a name="see-also"></a>Voir aussi

[Gouvernance des ressources de Machine Learning dans SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)

[Affichages catalogue du gouverneur de ressources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

[Sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[external scripts enabled (option de configuration de serveur)](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
