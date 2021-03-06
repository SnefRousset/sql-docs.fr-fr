---
title: sys.workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 421f47aee86c2e5bbdffe485ffea0cffef73bafd
ms.sourcegitcommit: 05bb10710489bef16bb2c53b3803e9b8eea1429a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2019
ms.locfileid: "57988775"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (Transact-SQL) (Preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Retourne les détails pour chaque classifieur.  
  
|Nom de la colonne|Type de données|Description|Plage|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**Int**|ID du classifieur. Joignable à [sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md). N'accepte pas la valeur NULL.|
|classifier_type|**sysname**|L’entité sur laquelle la classification est effectuée. N'accepte pas la valeur NULL.|[Classification de charge de travail SQL DATA Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)|
|classifier_value|**sysname**|La valeur du classifieur. N'accepte pas la valeur NULL.||

## <a name="permissions"></a>Autorisations

Requiert l'autorisation VIEW SERVER STATE.

## <a name="next-steps"></a>Étapes suivantes
  
 Pour obtenir la liste de toutes les vues de catalogue pour SQL Data Warehouse et Parallel Data Warehouse, consultez [SQL Data Warehouse et les vues du catalogue Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Pour créer un classifieur de charge de travail, consultez [créer un classifieur de charge de travail](../../t-sql/statements/create-workload-classifier-transact-sql.md). Pour plus d’informations sur la classification de la charge de travail, consultez [SQL la Classification des charges de travail entrepôt de données](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
