---
title: MSdistributiondbs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistributiondbs_TSQL
- MSdistributiondbs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistributiondbs system table
ms.assetid: d7ffa9df-bf1d-41b8-837e-b762c17c2764
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 173e1a32b986e750ee924c1950fd12cc5ded0ab2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817242"
---
# <a name="msdistributiondbs-transact-sql"></a>MSdistributiondbs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Le **MSdistributiondbs** table contient une ligne pour chaque base de données de distribution définie sur le serveur de distribution local. Cette table est stockée dans le **msdb** base de données.  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**nom**|**sysname**|Le nom de la base de données de distribution.|  
|**rétention_de_distribution_minimale**|**Int**|Délai de rétention minimal en heures, avant la suppression des transactions.|  
|**max_distretention**|**Int**|Délai de rétention maximal en heures, avant la suppression des transactions.|  
|**history_retention**|**Int**|Le nombre d’heures de rétention de l’historique.|  
  
## <a name="see-also"></a>Voir aussi  
 [Tables de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vues de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
