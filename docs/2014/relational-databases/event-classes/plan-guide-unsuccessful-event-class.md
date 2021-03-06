---
title: Plan Guide Unsuccessful, classe d’événements | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Plan Guide Unsuccessful event class
ms.assetid: ef9759f8-5613-4884-9257-86b609313f69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6ce753ceaa0cc0ee16b395918390a4402cf5f39
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788767"
---
# <a name="plan-guide-unsuccessful-event-class"></a>Plan Guide Unsuccessful (classe d'événements)
  La classe d'événements Plan Guide Unsuccessful indique que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] n'a pas pu produire de plan d'exécution pour une requête ou un lot qui contenait un repère de plan. En remplacement, le plan a été compilé sans utiliser le repère de plan. L'événement est déclenché lorsque les conditions suivantes sont remplies :  
  
-   Le lot/module dans la définition de repère de plan correspond au lot exécuté.  
  
-   La requête dans la définition de repère de plan correspond à celle en cours d'exécution.  
  
-   Les indicateurs dans la définition de repère de plan, y compris l'indicateur USE PLAN, n'ont pas été appliqués correctement à la requête ou au lot. Autrement dit, le plan de requête compilé n'a pas pu honorer les indicateurs spécifiés et le plan a été compilé sans utiliser le repère de plan.  
  
 Un repère de plan non valide peut provoquer le déclenchement de cet événement. Validez le repère de plan utilisé par la requête ou le lot à l’aide de la fonction [sys.fn_validate_plan_guide](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql) et corrigez l’erreur signalée par cette fonction.  
  
 Cet événement est inclus dans le modèle Tuning de [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] .  
  
## <a name="plan-guide-unsuccessful-event-class-data-columns"></a>Colonnes de données de la classe d'événements Plan Guide Unsuccessful  
  
|Nom de la colonne de données|Type de données|Description|ID de la colonne|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nom de l'application cliente qui a créé la connexion à une instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cette colonne est remplie par des valeurs transmises par l'application et non pas du nom affiché du programme.|10|Oui|  
|ClientProcessID|`int`|ID affecté par l'ordinateur hôte au processus dans lequel s'exécute l'application cliente. La colonne de données est remplie si le client fournit l'ID du processus client.|9|Oui|  
|DatabaseID|`int`|ID de la base de données spécifiée par l'instruction USE *database* ou celui de la base de données par défaut si aucune instruction USE *database* n'a été spécifiée pour une instance indiquée. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] affiche le nom de la base de données si la colonne de données ServerName du serveur est capturée dans la trace et que le serveur est disponible. Déterminez la valeur pour une base de données à l'aide de la fonction DB_ID.|3|Oui|  
|DatabaseName|`nvarchar`|Nom de la base de données dans laquelle l'instruction de l'utilisateur est exécutée.|35|Oui|  
|EventClass|`int`|Type d’événement = 218.|27|Non|  
|EventSequence|`int`|Séquence d'un événement spécifique dans la demande.|51|Non|  
|HostName|`nvarchar`|Nom de l'ordinateur sur lequel le client est exécuté. La colonne de données est remplie si le client fournit le nom de l'hôte. Pour déterminer le nom de l'hôte, utilisez la fonction HOST_NAME.|8|Oui|  
|IsSystem|`int`|Indique si l'événement s'est produit sur un processus système ou sur un processus utilisateur : 1 = système, 0 = utilisateur.|60|Oui|  
|LoginName|`nvarchar`|Nom de la connexion de l’utilisateur (soit la connexion de sécurité [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , soit les informations d’identification de connexion [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows au format DOMAINE\\*nom_utilisateur*).|11|Oui|  
|LoginSid|`image`|Numéro d'identification de sécurité (SID) de l'utilisateur connecté. Ces informations se trouvent dans les vues de catalogue [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql) ou [sys.sql_logins](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql) . Chaque connexion possède un SID unique au niveau du serveur.|41|Oui|  
|NTDomainName|`nvarchar`|Domaine Windows auquel appartient l'utilisateur.|7|Oui|  
|NTUserName|`nvarchar`|Nom d'utilisateur Windows.|6|Oui|  
|ObjectID|`int`|ID d'objet du module compilé lorsque le repère de plan a été appliqué. Si le repère de plan n'a pas été appliqué à un module, cette colonne a la valeur NULL.|22|Oui|  
|RequestID|`int`|ID de la demande contenant l'instruction.|49|Oui|  
|ServerName|`nvarchar`|Nom de l'instance [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracée.|26|Non|  
|SessionLoginName|`nvarchar`|Nom de connexion de l'utilisateur à l'origine de la session. Par exemple, si vous vous connectez à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en utilisant le nom Connexion1 et que vous exécutez une instruction en tant que Connexion2, SessionLoginName affiche Connexion1 et LoginName, Connexion2. Cette colonne affiche à la fois les connexions [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] et Windows.|64|Oui|  
|SPID|`int`|ID de la session au cours de laquelle l'événement s'est produit.|12|Oui|  
|StartTime|`datetime`|Heure à laquelle a débuté l'événement, si elle est connue.|14|Oui|  
|TextData|`ntext`|Nom du repère de plan.|1|Oui|  
|TransactionID|`bigint`|ID affecté par le système à la transaction.|4|Oui|  
|XactSequence|`bigint`|Jeton qui décrit la transaction en cours.|50|Oui|  
  
## <a name="see-also"></a>Voir aussi  
 [Classe d'événements Plan Guide Successful](plan-guide-successful-event-class.md)   
 [Événements étendus](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
