---
title: sysdatatypemappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31f90836b26d9551cc3e5a1200208cc51e3ef30a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756941"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Le **sysdatatypemappings** vue permet d’afficher le mappage entre les types de données SQL Server et les types de données d’un système de gestion de base de données (SGBD) non-SQL Server. Cette vue est stockée dans le **msdb** base de données.  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**Int**|ID du mappage du type de données.|  
|**source_dbms**|**sysname**|Indique le nom du SGBD à partir duquel les types de données sont mappés. Peut prendre l'une des valeurs suivantes :<br /><br /> **MSSQLSERVER** = la source est une base de données SQL Server.<br /><br /> **ORACLE** = la source est une base de données Oracle.|  
|**source_version**|**sysname**|Indique la version de produit de la source SGBD.|  
|**source_type**|**sysname**|Indique le type de données répertorié dans la source SGBD.|  
|**source_length_min**|**bigint**|Longueur minimale du type de données dans la source DBMS, où une valeur NULL indique que la longueur n'est pas utilisée.|  
|**source_length_max**|**bigint**|Longueur maximale du type de données dans la source DBMS, où une valeur NULL indique que la longueur n'est pas utilisée.|  
|**source_precision_min**|**bigint**|Précision minimale du type de données dans la source DBMS, où une valeur NULL indique que la précision n'est pas utilisée.|  
|**source_precision_max**|**bigint**|Précision maximale du type de données dans la source DBMS, où une valeur NULL indique que la précision n'est pas utilisée.|  
|**source_scale_min**|**Int**|Échelle minimale du type de données dans la source DBMS, où une valeur NULL indique que l'échelle n'est pas utilisée.|  
|**source_scale_max**|**Int**|Échelle maximale du type de données dans la source DBMS, où une valeur NULL indique que l'échelle n'est pas utilisée.|  
|**source_nullable**|**bit**|Mentionné si le type de données de destination prend en charge les valeurs NULL.|  
|**source_createparams**|**Int**|À usage interne uniquement|  
|**destination_dbms**|**sysname**|Indique le nom du SGBD de destination. Peut prendre l'une des valeurs suivantes :<br /><br /> **MSSQLSERVER** = la destination est une base de données SQL Server.<br /><br /> **ORACLE** = la destination est une base de données Oracle.<br /><br /> **DB2** = la destination est une base de données IBM DB2.<br /><br /> **SYBASE** = la destination est une base de données Sybase.|  
|**destination_version**|**sysname**|Version de produit du SGBD de destination.|  
|**destination_type**|**sysname**|Type de données du SGBD de destination.|  
|**destination_length**|**bigint**|Longueur du type de données du SGBD de destination.|  
|**destination_precision**|**bigint**|Précision du type de données du SGBD de destination.|  
|**destination_scale**|**Int**|Échelle du type de données du SGBD de destination.|  
|**destination_nullable**|**bit**|Indique si le type de données du SGBD de destination prend en charge une valeur NULL.|  
|**destination_createparams**|**Int**|À usage interne uniquement|  
|**perte de données**|**bit**|Indique si des données ont été perdues lors du mappage entre le type de données du SGBD source et de destination.|  
|**is_default**|**bit**|Indique si le mappage du type de données est utilisé par défaut.|  
  
## <a name="see-also"></a>Voir aussi  
 [Réplication de base de données hétérogène](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tables de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vues de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
