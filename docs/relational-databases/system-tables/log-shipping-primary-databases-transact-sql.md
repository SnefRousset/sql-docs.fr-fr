---
title: log_shipping_primary_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3904f6188ad1087c58a6044c1abd9fc2493c8129
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826537"
---
# <a name="logshippingprimarydatabases-transact-sql"></a>log_shipping_primary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stocke un enregistrement pour la base de données primaire dans une configuration de la copie des journaux de transaction. Cette table est stockée dans le **msdb** base de données.  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|ID de la base de données primaire pour la configuration de la copie des journaux de transaction.|  
|**primary_database**|**sysname**|Nom de la base de données primaire dans la configuration d'envoi de journaux.|  
|**backup_directory**|**nvarchar(500)**|Répertoire où les fichiers de sauvegarde des journaux de transactions du serveur principal sont stockés.|  
|**backup_share**|**nvarchar(500)**|Réseau ou chemin d'accès UNC au répertoire de sauvegarde.|  
|**backup_retention_period**|**Int**|Durée de conservation (en minutes) avant la suppression d'un fichier de sauvegarde de journal dans le répertoire de sauvegarde.|  
|**backup_job_id**|**uniqueidentifier**|Le [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID de tâche de l’Agent associé à la tâche de sauvegarde sur le serveur principal.|  
|**monitor_server**|**sysname**|Le nom de l’instance de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilisé en tant que serveur moniteur dans la configuration d’envoi de journaux.|  
|**monitor_server_security_mode**|**bit**|Mode de sécurité utilisé pour la connexion au serveur moniteur.<br /><br /> 1 = Authentification Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l’authentification.|  
|**last_backup_file**|**nvarchar(500)**|Chemin d'accès absolu de la sauvegarde la plus récente des journaux de transactions.|  
|**last_backup_date**|**datetime**|Date et heure de la dernière opération de sauvegarde des journaux.|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database** et **sp_help_log_shipping_secondary_primary** utiliser cette colonne pour contrôler l’affichage des paramètres du moniteur dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].<br /><br /> 0 = lors de l’appel de l’une de ces deux procédures stockées, l’utilisateur ne spécifiait pas une valeur explicite pour le **@monitor_server** paramètre.<br /><br /> 1 = Une valeur explicite a été spécifiée par l'utilisateur.|  
|**backup_compression**|**tinyint**|Indique si la configuration de la copie des journaux de transaction substitue le comportement de compression de la sauvegarde au niveau du serveur.<br /><br /> 0 = Désactivées. Les sauvegardes de fichiers journaux ne sont jamais compressés, quels que soient les paramètres de compression de sauvegarde configurés par serveur.<br /><br /> 1 = Activé. Les sauvegardes de fichiers journaux sont toujours compressés, quels que soient les paramètres de compression de sauvegarde configurés par serveur.<br /><br /> 2 = utilise la configuration du serveur pour le [afficher ou configurer l’Option de Configuration de serveur par défaut de compression de la sauvegarde](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) option de configuration de serveur. Il s'agit de la valeur par défaut.<br /><br /> La compression de la sauvegarde est prise en charge uniquement dans l'édition Enterprise de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="see-also"></a>Voir aussi  
 [À propos de la copie des journaux des transactions &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [Tables système &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
