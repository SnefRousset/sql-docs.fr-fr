---
title: MSmerge_conflict_&lt;publication&gt;_&lt;article&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 78036e91dd87b3295c9b8c4e6d0a39311133bbdd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777951"
---
# <a name="msmergeconflictltpublicationgtltarticlegt-transact-sql"></a>MSmerge_conflict_&lt;publication&gt;_&lt;article&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Le **MSmerge_conflict_*publication*_ * article*** table contient des informations sur les lignes qui sont en conflit, ou pour les modifications de lignes qui ont été annulées pour atteindre la convergence des données. Il existe une table de conflits pour chaque table répliquée dans une publication, où le nom de la table de conflits est ajouté au nom de la publication et à celui de l'article. Ces tables de conflits spécifiques aux articles existent dans la base de données utilisée pour la journalisation des conflits ; il s'agit généralement de la base de données de publication, mais il peut s'agir de la base de données d'abonnement si la journalisation des conflits est décentralisée.  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|***article_column_name***|**variable**|Représente une colonne d'une table répliquée. Cette table système contient une colonne pour chaque colonne de l'article de la table.|  
|**ROWGUID**|**uniqueidentifier**|Identificateur de ligne de la ligne en conflit.|  
|**ModifiedDate**|**datetime**|Heure d'occurrence du conflit.|  
|**origin_datasource_id**|**uniqueidentifier**|Abonnement pour lequel la modification de ligne a été annulée ou qui a perdu le conflit.|  
  
## <a name="see-also"></a>Voir aussi  
 [Tables de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vues de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
