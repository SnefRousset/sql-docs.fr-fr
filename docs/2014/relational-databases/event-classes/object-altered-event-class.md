---
title: Object:Altered, classe d’événements | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Object:Altered event class
ms.assetid: f94e3b59-ff2f-4d8d-8479-e85ce5b3483e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd38e8d1685b23cfeeb1793d02b0fff1d7de0640
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770691"
---
# <a name="objectaltered-event-class"></a>Object:Altered (classe d'événements)
  La classe d'événements Object:Altered indique qu'un objet a été modifié ; par exemple, à l'aide d'une instruction ALTER INDEX, ALTER TABLE, ou d'une instruction ALTER DATABASE. Cette classe d'événements peut être utilisée pour déterminer si des objets sont modifiés ; par exemple, par les applications ODBC, qui créent souvent des procédures stockées temporaires.  
  
 La classe d'événements Object:Altered se produit toujours sous forme de deux événements. Le premier événement indique la phase Begin. Le second événement indique la phase Rollback ou Commit.  
  
 En surveillant les colonnes de données LoginName et NTUserName, vous pouvez déterminer le nom de l'utilisateur qui est en train de créer, supprimer ou modifier des objets.  
  
## <a name="objectaltered-event-class-data-columns"></a>Colonnes de données de la classe d'événements Object:Altered  
  
|Nom de la colonne de données|Type de données|Description|ID de la colonne|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nom de l'application cliente qui a créé la connexion à une instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cette colonne est remplie avec les valeurs passées par l'application plutôt que par le nom affiché du programme.|10|Oui|  
|ClientProcessID|`int`|ID affecté par l'ordinateur hôte au processus dans lequel s'exécute l'application cliente. La colonne de données est remplie si le client fournit l'ID du processus client.|9|Oui|  
|DatabaseID|`int`|ID de la base de données spécifiée par l'instruction USE *database* ou celui de la base de données par défaut si aucune instruction USE *database* n'a été spécifiée pour une instance donnée. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] affiche le nom de la base de données si la colonne de données ServerName est capturée dans la trace et que le serveur est disponible. Déterminez la valeur pour une base de données à l'aide de la fonction DB_ID.|3|Oui|  
|DatabaseName|`nvarchar`|Nom de la base de données dans laquelle l'instruction de l'utilisateur est exécutée.|35|Oui|  
|EventClass|`int`|Type d’événement = 164.|27|Non|  
|EventSequence|`int`|Séquence d'un événement donné au sein de la demande.|51|Non|  
|EventSubClass|`int`|Type de sous-classe d'événements.<br /><br /> 0=Début<br /><br /> 1=Validation<br /><br /> 2=Annulation|21|Oui|  
|GroupID|`int`|ID du groupe de charges de travail où l'événement Trace SQL se déclenche.|66|Oui|  
|HostName|`nvarchar`|Nom de l'ordinateur sur lequel le client est exécuté. La colonne de données est remplie si le client fournit le nom de l'hôte. Pour déterminer le nom de l'hôte, utilisez la fonction HOST_NAME.|8|Oui|  
|IndexID|`int`|ID de l'index de l'objet affecté par l'événement. Pour déterminer l'ID d'index d'un objet, utilisez la colonne index_id de l'affichage catalogue sys.indexes.|24|Oui|  
|IntegerData|`int`|Numéro d'ordre d'événement par rapport à l'événement Begin correspondant. Cette colonne n'est disponible que pour le type Commit ou Rollback de sous-classe d'événements.|25|Oui|  
|IsSystem|`int`|Indique si l'événement s'est produit sur un processus système ou sur un processus utilisateur. 1 = système, NULL = utilisateur.|60|Oui|  
|LoginName|`nvarchar`|Nom de la connexion de l'utilisateur (soit la connexion de sécurité [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , soit les informations d'identification de connexion [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows au format DOMAINE\nom_utilisateur).|11|Oui|  
|LoginSid|`image`|Numéro d'identification de sécurité (SID) de l'utilisateur connecté. Vous pouvez trouver ces informations dans l'affichage catalogue sys.server_principals. Chaque connexion possède un SID unique au niveau du serveur.|41|Oui|  
|NTDomainName|`nvarchar`|Domaine Windows auquel appartient l'utilisateur.|7|Oui|  
|NTUserName|`nvarchar`|Nom d'utilisateur Windows.|6|Oui|  
|ObjectID|`int`|ID affecté à l'objet par le système.|22|Oui|  
|ObjectID2|`bigint`|ID de la fonction de partition lorsque le schéma de la partition est modifié, ID de la file d'attente lorsque le service est modifié ou ID du schéma de la collection lorsque le schéma XML est modifié.|56|Oui|  
|ObjectName|`nvarchar`|Nom de l'objet référencé.|34|Oui|  
|ObjectType|`int`|Valeur représentant le type de l'objet qui intervient dans l'événement. Cette valeur correspond à la colonne type de l'affichage catalogue sys.objects. Pour connaître les valeurs, consultez [Colonne d’événements de trace ObjectType](objecttype-trace-event-column.md).|28|Oui|  
|RequestID|`int`|ID de la demande de traitement contenant l'instruction.|49|Oui|  
|ServerName|`nvarchar`|Nom de l'instance [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracée.|26|Non|  
|SessionLoginName|`nvarchar`|Nom de connexion de l'utilisateur à l'origine de la session. Par exemple, si vous vous connectez à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en utilisant le nom Connexion1 et que vous exécutez une instruction en tant que Connexion2, SessionLoginName affiche Connexion1 et LoginName, Connexion2. Cette colonne affiche à la fois les connexions [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] et Windows.|64|Oui|  
|SPID|`int`|ID de la session au cours de laquelle l'événement s'est produit.|12|Oui|  
|StartTime|`datetime`|Heure à laquelle a débuté l'événement, si elle est connue.|14|Oui|  
|TransactionID|`bigint`|ID affecté par le système à la transaction.|4|Oui|  
|XactSequence|`bigint`|Jeton qui décrit la transaction en cours.|50|Oui|  
  
## <a name="see-also"></a>Voir aussi  
 [Événements étendus](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
