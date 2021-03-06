---
title: catalog.environment_variables (base de données SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ec7fbb111e1c5cbc8e98117d3cb3be5d2bebab30
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277878"
---
# <a name="catalogenvironmentvariables-ssisdb-database"></a>catalog.environment_variables (base de données SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Affiche les détails de la variable d'environnement pour tous les environnements dans le catalogue [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nom de colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|Identificateur (ID) unique de la variable d'environnement.|  
|environment_id|**bigint**|ID unique de l'environnement auquel la variable est associée.|  
|NAME|**sysname**|Nom de la variable d'environnement.|  
|description|**nvarchar(1024)**|Description de la variable d'environnement.|  
|Type|**nvarchar(128)**|Type de données de la variable d'environnement.|  
| sensible|**bit**|Lorsque la valeur est `1`, la variable est sensible et est chiffrée lorsqu'elle est stockée. Lorsque la valeur est `0`, la variable n'est pas sensible et la valeur est stockée dans en texte en clair.|  
|valeur|**sql_variant**|Valeur de la variable d'environnement. Quand sensitive est `0`, la valeur en texte en clair est indiquée. Quand sensitive est `1`, la valeur **NULL** s’affiche.|  
  
## <a name="remarks"></a>Notes   
 Cette vue affiche une ligne pour chaque variable d'environnement dans le catalogue.  
  
## <a name="permissions"></a>Autorisations  
 Cette vue requiert l'une des autorisations suivantes :  
  
-   Autorisation READ sur l'environnement correspondant  
  
-   Appartenance au rôle de base de données **ssis_admin**  
  
-   Appartenance au rôle serveur **sysadmin**  
  
> [!NOTE]  
>  Lorsque vous avez l'autorisation pour effectuer une opération sur le serveur, vous avez également l'autorisation pour consulter les informations de l'opération. La sécurité au niveau de la ligne est imposée ; uniquement les lignes que vous avez l'autorisation d'afficher s'affichent.  
  
  
