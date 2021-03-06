---
title: sp_browsereplcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5356ebc173e435595315badf9a3c2abe224d186b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802381"
---
# <a name="spbrowsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retourne un jeu de résultats, dans une version lisible, des commandes répliquées et stockées dans la base de données de distribution. Également utilisé en tant qu'outil de diagnostic. Cette procédure stockée est exécutée au niveau du serveur de distribution sur la base de données de distribution.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>Arguments  
 [  **@xact_seqno_start =**] **'**_xact_seqno_start_**'**  
 Spécifie le plus petit numéro de séquence exact à retourner. *xact_seqno_start* est **nchar (22)**, avec 0 x 00000000000000000000 comme valeur par défaut.  
  
 [  **@xact_seqno_end =**] **'**_xact_seqno_end_**'**  
 Spécifie le plus grand numéro de séquence exact à retourner. *xact_seqno_end* est **nchar (22)**, avec 0xFFFFFFFFFFFFFFFFFFFF comme valeur par défaut.  
  
 [  **@originator_id =**] **'**_originator_id_**'**  
 Spécifie si les commandes avec la valeur *originator_id* sont retournés. *originator_id* est **int**, avec NULL comme valeur par défaut.  
  
 [  **@publisher_database_id =**] **'**_publisher_database_id_**'**  
 Spécifie si les commandes avec la valeur *publisher_database_id* sont retournés. *publisher_database_id* est **int**, avec NULL comme valeur par défaut.  
  
 [  **@article_id =**] **'**_article_id_**'**  
 Spécifie si les commandes avec la valeur *article_id* sont retournés. *article_id* est **int**, avec NULL comme valeur par défaut.  
  
 [  **@command_id =**] *command_id*  
 Est l’emplacement de la commande dans [MSrepl_commands &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md) à décoder. *command_id* est **int**, avec NULL comme valeur par défaut. Si spécifié, tous les autres paramètres doivent être spécifiés en outre, et *xact_seqno_start*doit être identique à *xact_seqno_end*.  
  
 [  **@agent_id =**] *agent_id*  
 Spécifie que seules les commandes correspondant à un Agent de réplication donné sont retournées. *éléments agent_id* est **int**, avec NULL comme valeur par défaut.  
  
 [  **@compatibility_level =**] *compatibility_level*  
 Est la version de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sur lequel le *compatibility_level* est **int**, avec 9000000 comme valeur par défaut.  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 **0** (réussite) ou **1** (échec)  
  
## <a name="result-sets"></a>Jeux de résultats  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|Numéro de séquence de la commande.|  
|**originator_srvname**|**sysname**|Serveur d'origine de la transaction.|  
|**originator_db**|**sysname**|Base de données d'origine de la transaction.|  
|**article_id**|**Int**|ID de l’article.|  
|**type**|**Int**|Type de commande.|  
|**commande_partielle**|**bit**|Indique s'il s'agit d'une commande partielle.|  
|**hashkey**|**Int**|À usage interne uniquement|  
|**originator_publication_id**|**Int**|ID de la publication d'origine de la transaction.|  
|**originator_db_version**|**Int**|Version de la base de données d'origine de la transaction.|  
|**originator_lsn**|**varbinary(16)**|Identifie le numéro séquentiel dans le journal (LSN) de la commande dans la publication d'origine. Utilisé dans la réplication transactionnelle peer-to-peer.|  
|**commande**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] commande.|  
|**command_id**|**Int**|ID de la commande dans [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
  
 Les commandes longues peuvent être réparties entre plusieurs lignes dans l'ensemble de résultats.  
  
## <a name="remarks"></a>Notes  
 **sp_browsereplcmds** est utilisé dans la réplication transactionnelle.  
  
## <a name="permissions"></a>Autorisations  
 Seuls les membres de la **sysadmin** rôle serveur fixe ou membres de la **db_owner** ou **replmonitor** des rôles de base de données fixe sur la base de données de distribution peuvent exécuter **sp_browsereplcmds**.  
  
## <a name="see-also"></a>Voir aussi  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [Procédures stockées système &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
