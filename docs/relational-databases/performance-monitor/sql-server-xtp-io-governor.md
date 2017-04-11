---
title: "Administrateur d’E/S SQL Server XTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
caps.latest.revision: 2
author: "dagiro"
ms.author: "v-dagir"
manager: "jhubbard"
caps.handback.revision: 2
---
# Administrateur d’E/S SQL Server XTP
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

L’objet de performances Administrateur d’E/S SQL Server XTP contient des compteurs liés à l’Administrateur de taux d’E/S OLTP en mémoire.

Ce tableau décrit les compteurs **Administrateur d’E/S SQL Server XTP**.

|Compteur|Description|  
|-------------|-----------------|  
|**Attentes de crédits insuffisants/s**|Nombre d’attentes en raison de crédits insuffisants dans les objets de taux (par seconde).|
|**E/S émises/s**|Nombre d’E/S émises par seconde par les threads de vidage.|
|**Blocs de journal/s**|Nombre de blocs de journal traités par le contrôleur par seconde.|
|**Emplacements de crédit manqués**|Nombre d’emplacements de crédit manqués en raison de l’attente de crédits à partir de l’objet de taux.|
|**Taux des attentes d’objets périmés/s**|Nombre d’attentes en raison d’objets périmés (par seconde).|
|**Proportion totale d’objets publiés**|Nombre total de proportions d’objets publiés.|
 

## Voir aussi  
[Compteurs de performances SQL Server XTP &#40;OLTP en mémoire&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)