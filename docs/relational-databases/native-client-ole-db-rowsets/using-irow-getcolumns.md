---
title: "À l’aide d’IRow::GetColumns | Documents Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f4f66d36796de8c4dbb0c39b169314be9bdc473
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2017
---
# <a name="using-irowgetcolumns"></a>Utilisation d'IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Le **IRow** implémentation autorise un accès séquentiel avant uniquement aux colonnes. Vous pouvez soit accéder à toutes les colonnes de la ligne avec un seul appel à **IRow::GetColumns** ou appelez **IRow::GetColumns** chaque fois que vous y accéder à plusieurs colonnes dans la ligne.  
  
 Les appels multiples à **IRow::GetColumns** ne doivent pas se chevaucher. Par exemple, si le premier appel à **IRow::GetColumns** récupère les colonnes 1, 2 et 3, le deuxième appel à **IRow::GetColumns** doit appeler les colonnes 4, 5 et 6. Si appels ultérieurs à **IRow::GetColumns** se chevauchent, l’indicateur d’état (champ dwstatus dans DBCOLUMNACCESS) a la valeur DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Voir aussi  
 [Récupération d’une ligne unique avec IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  