---
title: sys.dm_pdw_nodes_database_encryption_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4d31e3cdd8d4035840f1529a64317d17ba2571d3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036050"
---
# <a name="sysdmpdwnodesdatabaseencryptionkeys-transact-sql"></a>sys.dm_pdw_nodes_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retourne des informations sur l'état de chiffrement d'une base de données et de ses clés de chiffrement de base de données associées. **Sys.dm_pdw_nodes_database_encryption_keys** fournit ces informations pour chaque nœud. Pour plus d’informations sur le chiffrement de base de données, consultez [Transparent Data Encryption (SQL Server PDW)](https://msdn.microsoft.com/b82ad21d-09dd-43dd-8fab-bcf2c8c3ac6d).  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|database_id|**Int**|ID de la base de données physique sur chaque nœud.|  
|encryption_state|**Int**|Indique si la base de données sur ce nœud est chiffré ou non.<br /><br /> 0 = aucune clé de chiffrement de base de données présente, pas de chiffrement<br /><br /> 1 = non chiffré<br /><br /> 2 = chiffrement en cours<br /><br /> 3 = chiffrée.<br /><br /> 4 = modification de clé en cours<br /><br /> 5 = déchiffrement en cours<br /><br /> 6 = modification de la protection en cours (le certificat qui chiffre la clé de chiffrement de base de données est en cours de modification.)|  
|create_date|**datetime**|Affiche la date de création de la clé de chiffrement.|  
|regenerate_date|**datetime**|Affiche la date de régénération de la clé de chiffrement.|  
|modify_date|**datetime**|Affiche la date de modification de la clé de chiffrement.|  
|set_date|**datetime**|Affiche la date à laquelle la clé de chiffrement a été appliquée à la base de données.|  
|opened_date|**datetime**|Indique à quel moment la clé de base de données a été ouverte pour la dernière fois.|  
|key_algorithm|**varchar(?)**|Affiche l'algorithme utilisé pour la clé.|  
|key_length|**Int**|Affiche la longueur de la clé.|  
|encryptor_thumbprint|**varbin**|Affiche l'empreinte numérique du chiffreur.|  
|percent_complete|**real**|Pourcentage accompli de la modification de l'état de chiffrement de la base de données. La valeur 0 indique aucune modification d'état.|  
|node_id|**Int**|Id numérique unique associé au nœud.|  
  
## <a name="permissions"></a>Autorisations  
 Requiert l’autorisation VIEW SERVER STATE sur le serveur.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemples : [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] et [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 L’exemple suivant joint `sys.dm_pdw_nodes_database_encryption_keys` à d’autres tables système pour indiquer l’état de chiffrement pour chaque nœud du TDE de bases de données protégées.  
  
```  
SELECT D.database_id AS DBIDinMaster, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName,   
keys.encryption_state  
FROM sys.dm_pdw_nodes_database_encryption_keys AS keys  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON keys.database_id = PD.database_id AND keys.pdw_node_id = PD.pdw_node_id  
JOIN sys.pdw_database_mappings AS DM  
    ON DM.physical_name = PD.physical_name  
JOIN sys.databases AS D  
    ON D.database_id = DM.database_id  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Vues de gestion dynamique de l’entrepôt SQL Data Warehouse et Parallel Data &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

