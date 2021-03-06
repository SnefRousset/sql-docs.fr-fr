---
title: sp_validate_redirected_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47bf5c0ada106a11bdef72debf401de0640ff11f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818921"
---
# <a name="spvalidateredirectedpublisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Vérifie que l'hôte actuel de la base de données de publication peut prendre en charge la réplication. Doit être exécutée à partir d'une base de données de distribution. Cette procédure est appelée par **sp_get_redirected_publisher**.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Arguments  
 [ **@original_publisher** =] **'***original_publisher***'**  
 Nom de l'instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qui a publié la base de données à l'origine. *original_publisher* est **sysname**, sans valeur par défaut.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Nom de la base de données publiée. *publisher_db* est **sysname**, sans valeur par défaut.  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***'**  
 La cible de redirection spécifiée lorsque **sp_redirect_publisher** a été appelée pour la paire serveur de publication/base de données. *redirected_publisher* est **sysname**, sans valeur par défaut.  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 **0** (réussite) ou **1** (échec)  
  
## <a name="result-sets"></a>Jeux de résultats  
 Aucun.  
  
## <a name="remarks"></a>Notes  
 Si aucune entrée n’existe pour le serveur de publication et de la base de données de publication, **sp_validate_redirected_publisher** retourne la valeur null dans le paramètre de sortie *@redirected_publisher*. Si une entrée existe, elle est retournée dans le paramètre de sortie dans les deux cas (réussite et échec).  
  
 Si la validation réussit, **sp_validate_redirected_publisher** retourne une indication de réussite.  
  
 Si la validation échoue, des erreurs sont générées, qui décrivent l'échec.  
  
## <a name="permissions"></a>Autorisations  
 L’appelant doit être un membre de la **sysadmin** rôle serveur fixe le **db_owner** rôle de base de données fixe pour la base de données de distribution ou un membre d’une liste d’accès à une publication définie associé à la base de données du serveur de publication.  
  
## <a name="see-also"></a>Voir aussi  
 [Procédures stockées de réplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
