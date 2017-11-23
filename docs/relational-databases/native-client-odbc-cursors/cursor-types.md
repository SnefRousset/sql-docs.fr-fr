---
title: Types de curseurs | Documents Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c280132b77dabe4ad88a9734f8ee8de84db1441d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2017
---
# <a name="cursor-types"></a>Types de curseurs
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC définit quatre types de curseurs pris en charge par Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] et [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pilote ODBC Native Client. Ces curseurs diffèrent dans leur capacité à détecter les modifications apportées au jeu de résultats et dans les ressources qu’ils consomment, telles que la mémoire et de l’espace dans **tempdb**. Un curseur peut détecter des modifications apportées à des lignes uniquement lorsqu'il tente d'extraire à nouveau ces lignes ; il n'existe aucun moyen pour la source de données d'informer le curseur des modifications apportées aux lignes en cours d'extraction. La capacité d'un curseur à détecter des modifications qui n'ont pas été apportées par le biais du curseur est également influencée par le niveau d'isolation de la transaction.  
  
 Les quatre types de curseurs ODBC pris en charge par [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sont les suivants :  
  
-   Les curseurs avant uniquement ne prennent pas en charge le défilement, mais seulement l'extraction de lignes en séquence à partir du début jusqu'à la fin du curseur.  
  
-   Les curseurs statiques sont générés **tempdb** lorsque le curseur est ouvert. Ils affichent toujours l'ensemble de résultats tel qu'il était au moment où le curseur a été ouvert. Ils ne reflètent jamais les modifications apportées aux données. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Les curseurs statiques sont toujours en lecture seule. Comme un curseur côté serveur statique est créé comme une table de travail **tempdb**, la taille du jeu de résultats de curseur ne peut pas dépasser la taille de ligne maximale autorisée par [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   L'appartenance et l'ordre des lignes dans le jeu de résultats des curseurs de jeux de clés sont fixés au moment de l'ouverture du curseur. Les modifications aux colonnes non-clés sont visibles à travers le curseur.  
  
-   Les curseurs dynamiques sont le contraire des curseurs statiques. Les curseurs dynamiques reflètent toutes les modifications apportées aux lignes de leur jeu de résultats. Les valeurs des données, l'ordre et l'appartenance des lignes du jeu de résultats peuvent changer à chaque extraction.  
  
## <a name="see-also"></a>Voir aussi  
 [À l’aide de curseurs &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  