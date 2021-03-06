---
title: la procédure sp_dropmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 722a8092a799695be0ab5e4f6925cd7416b7c1b9
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134719"
---
# <a name="spdropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Supprime un serveur de publication de substitution d'une publication de fusion. Cette procédure stockée est exécutée sur la base de données d'abonnement de l'Abonné.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>Arguments  
 [  **@publisher=**] **'**_publisher_**'**  
 Nom du serveur de publication actuel. *serveur de publication*est **sysname**, sans valeur par défaut.  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 Nom de la base de données de publication active. *publisher_db*est **sysname**, sans valeur par défaut.  
  
 [  **@publication =**] **'**_publication_**'**  
 Nom de la publication actuelle. *publication* est **sysname**, sans valeur par défaut.  
  
 [  **@alternate_publisher=**] **'**_alternate_publisher_**'**  
 Nom du serveur de publication de remplacement à supprimer en tant que partenaire de synchronisation de substitution. *alternate_publisher*est **sysname**, sans valeur par défaut.  
  
 [  **@alternate_publisher_db=**] **'**_alternate_publisher_db_**'**  
 Nom de la base de données de publication à supprimer en tant que base de données de publication du partenaire de synchronisation de substitution. *alternate_publisher_db*est **sysname**, sans valeur par défaut.  
  
 [  **@alternate_publication=**] **'**_alternate_publication_**'**  
 Nom de la publication à supprimer en tant que publication du partenaire de synchronisation de substitution. *alternate_publication*est **sysname**, sans valeur par défaut.  
  
## <a name="return-code-values"></a>Valeurs des codes de retour  
 **0** (réussite) ou **1** (échec)  
  
## <a name="remarks"></a>Notes  
 **la procédure sp_dropmergealternatepublisher** est utilisé dans la réplication de fusion.  
  
## <a name="permissions"></a>Autorisations  
 Seuls les membres de la **sysadmin** rôle serveur fixe ou le **db_owner** rôle de base de données fixe peuvent exécuter **sp_dropmergelternatepublisher**.  
  
## <a name="see-also"></a>Voir aussi  
 [sp_addmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
