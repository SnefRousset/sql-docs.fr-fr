---
title: sp_helpsubscriptionerrors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriptionerrors_TSQL
- sp_helpsubscriptionerrors
helpviewer_keywords:
- sp_helpsubscriptionerrors
ms.assetid: 01c8bc21-939e-490d-8cc8-219c068be31e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f98790bbf68309eef561662a6eb0be9f1da34971
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818801"
---
# <a name="sphelpsubscriptionerrors-transact-sql"></a>sp_helpsubscriptionerrors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retourne toutes les erreurs de réplication transactionnelle pour un abonnement donné. Cette procédure stockée est exécutée au niveau du serveur de distribution sur la base de données de distribution.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_helpsubscriptionerrors [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'  
```  
  
## <a name="arguments"></a>Arguments  
 [  **@publisher=** ] **'***publisher***'**  
 Nom du serveur de publication. *serveur de publication* est **sysname**, sans valeur par défaut.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Nom de la base de données de publication. *publisher_db* est **sysname**, sans valeur par défaut.  
  
 [  **@publication=** ] **'***publication***'**  
 Nom de la publication. *publication* est **sysname**, sans valeur par défaut.  
  
 [  **@subscriber=** ] **'***abonné***'**  
 Nom de l'Abonné. *abonné* est **sysname**, sans valeur par défaut.  
  
 [  **@subscriber_db=** ] **'***bd_abonné***'**  
 Est le nom de la base de données d’abonnement. *bd_abonné* est **sysname**, sans valeur par défaut.  
  
## <a name="result-set"></a>Jeu de résultats  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**id**|**Int**|Identification de l'erreur|  
|**time**|**datetime**|Heure à laquelle l'erreur s'est produite.|  
|**error_type_id**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**Int**|Identification du type de source de l'erreur|  
|**source_name**|**nvarchar(100)**|Nom de la source de l'erreur|  
|**error_code**|**sysname**|Code d'erreur|  
|**texte_erreur**|**ntext**|message d’erreur.|  
|**xact_seqno**|**varbinary(16)**|Numéro séquentiel dans le journal de la première transaction du traitement dont l'exécution a échoué. Uniquement utilisé par les Agents de distribution, c'est le numéro séquentiel dans le journal de la première transaction dans le lot dont l'exécution a échoué.|  
|**command_id**|**Int**|ID de commande du traitement dont l'exécution a échoué. Utilisé uniquement par les Agents de distribution, il s'agit de l'ID de commande de la première commande du lot en échec.|  
|**session_id**|**Int**|ID de la session de l'agent dans laquelle l'erreur s'est produite.|  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 **0** (réussite) ou **1** (échec)  
  
## <a name="remarks"></a>Notes  
 **sp_helpsubscriptionerrors** est utilisé avec la réplication transactionnelle et de capture instantanée.  
  
## <a name="permissions"></a>Autorisations  
 Seuls les membres de la **sysadmin** rôle serveur fixe ou **db_owner** rôle de base de données fixe peuvent exécuter **sp_helpsubscriptionerrors**.  
  
## <a name="see-also"></a>Voir aussi  
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
