---
title: Objet SQL Server, ExecStatistics | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 054ff1d108a958e40a17a2316377559295746e7b
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380025"
---
# <a name="sql-server-execstatistics-object"></a>Objet SQL Server, ExecStatistics
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'objet **SQLServer:ExecStatistics** de Microsoft SQL Server intègre des compteurs chargés de surveiller les diverses exécutions.  
  
 Ce tableau décrit les compteurs **Exec Statistics** de SQL Server.  
  
|Compteurs ExecStatistics de SQL Server|Description|  
|-----------------------------------------|-----------------|  
|**Requête distribuée**|Statistiques relatives à l'exécution de requêtes distribuées|  
|**Appels DTC**|Statistiques relatives à l'exécution d'appels DTC|  
|**Procédures étendues**|Statistiques relatives à l'exécution de procédures étendues|  
|**Appels OLEDB**|Statistiques relatives à l''exécution d'appels OLEDB|  
  
 Chaque compteur de l'objet contient les instances suivantes :  
  
|Élément|Description|  
|----------|-----------------|  
|**Temps d'exécution moyen (ms)**|Temps d'exécution moyen pour le type d'exécution sélectionné|  
|**Temps d'exécution cumulé (ms) par seconde**|Temps d'exécution global par seconde pour le type d'exécution sélectionné|  
|**Exécutions en cours**|Nombre d'exécutions en cours pour le type d'exécution sélectionné|  
|**Exécutions démarrées par seconde**|Nombre d'exécutions démarrées par seconde pour le type d'exécution sélectionné|  
  
## <a name="see-also"></a> Voir aussi  
 [Analyser l’utilisation des ressources &#40;Moniteur système&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
