---
title: Créer automatiquement des jointures réflexives (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f1d7bdeca1202eb46bf2926d2ddc86855bd5f71
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652508"
---
# <a name="create-self-joins-automatically-visual-database-tools"></a>Créer automatiquement des jointures réflexives (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Si une table possède une relation réflexive dans la base de données, vous pouvez la joindre à elle-même de façon automatique.  
  
### <a name="to-create-a-self-join-automatically"></a>Pour créer automatiquement une jointure réflexive  
  
1.  Ajoutez la table que vous souhaitez utiliser au [volet Schéma](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) .  
  
2.  Ajoutez de nouveau la même table, afin que le volet Schéma affiche deux fois la même table.  
  
    Le [Concepteur de requêtes et de vues](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) assigne un alias à la seconde instance en ajoutant un numéro séquentiel au nom de la table. Par ailleurs, il crée une ligne de jointure entre les deux rectangles qui représentent les deux façons différentes dont la table intervient dans la requête.  
  
## <a name="see-also"></a> Voir aussi  
[Interroger avec des jointures &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
