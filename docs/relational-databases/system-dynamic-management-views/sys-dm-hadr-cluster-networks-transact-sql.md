---
title: Sys.dm_hadr_cluster_networks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7b48507e59fa77cc0e6e47b4874cd1c010cd36cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746207"
---
# <a name="sysdmhadrclusternetworks-transact-sql"></a>sys.dm_hadr_cluster_networks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retourne une ligne pour chaque membre de cluster WSFC qui participe à la configuration du sous-réseau d'un groupe de disponibilité. Vous pouvez utiliser cette vue de gestion dynamique pour valider l'adresse IP virtuelle de réseau qui est configurée pour chaque réplica de disponibilité.  
  
 Clé primaire : **member_name** + **network_subnet_IP** + **network_subnet_prefix_length**  
  
 > [!TIP]
 > À compter de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], cette vue de gestion dynamique prend en charge le basculement Instances de Cluster AlwaysOn en plus des groupes de disponibilité AlwaysOn.  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**MEMBER_NAME**|**nvarchar(128)**|Nom d'ordinateur d'un nœud dans le cluster WSFC.|  
|**network_subnet_ip**|**nvarchar(48)**|Adresse IP réseau du sous-réseau auquel l'ordinateur appartient. Cela peut être une adresse IPv4 ou IPv6.|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|Masque de sous-réseau de réseau qui spécifie le sous-réseau auquel l'adresse IP appartient. **network_subnet_ipv4_mask** pour spécifier les options DHCP < network_subnet_option > dans une clause WITH DHCP de la [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instruction.<br /><br /> NULL = Sous-réseau IPv6.|  
||||  
|**network_subnet_prefix_length**|**Int**|Longueur de préfixe IP de réseau qui spécifie le sous-réseau auquel l'ordinateur appartient.|  
|**is_public**|**bit**|Si le réseau est privé ou public sur le cluster WSFC, une des valeurs suivantes :<br /><br /> 0 = Privé<br /><br /> 1 = Public|  
|**is_ipv4**|**bit**|Type de sous-réseau, un des suivants :<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>Sécurité  
  
### <a name="permissions"></a>Permissions  
 requièrent l'autorisation VIEW SERVER STATE sur le serveur.  
  
## <a name="see-also"></a>Voir aussi  
 [Clustering de basculement et groupes de disponibilité Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Surveiller des groupes de disponibilité &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Sys.dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [Interrogation des catalogues système SQL Server FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Affichages catalogue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
