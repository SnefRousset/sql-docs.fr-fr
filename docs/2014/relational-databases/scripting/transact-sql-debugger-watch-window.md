---
title: Espion, fenêtre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Watch Window [Transact-SQL]
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01caaf26257c06aae8cb7668693fd3ff6b8b5135
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328749"
---
# <a name="watch-window"></a>Espion (fenêtre)
  La fenêtre **Espion** affiche des informations sur les expressions que vous avez sélectionnées. Il peut y avoir jusqu'à quatre fenêtres Espion : **Espion 1**, **espion 2, Espion 3**, et **espion 4**. Les expressions sont évaluées dans l’étendue du frame de pile des appels actuellement sélectionné dans la fenêtre **Pile des appels** . Vous devez être en mode débogage pour surveiller les variables et les expressions.  
  
## <a name="task-list"></a>Liste des tâches  
 **Pour accéder aux fenêtres Espion**  
  
-   Dans le menu **Déboguer** , cliquez sur **Fenêtres**, sur **Espion**puis sur **Espion 1**, **Espion 2, Espion 3**ou **Espion 4**.  
  
 **Pour modifier la valeur d'une expression**  
  
-   Cliquez avec le bouton droit sur l’expression, puis sélectionnez **Modifier la valeur**.  
  
## <a name="columns"></a>Colonnes  
 **Nom**  
 Expressions répertoriées par le débogueur [!INCLUDE[tsql](../../includes/tsql-md.md)] . Les expressions suivantes sont prises en charge :  
  
-   variables ;  
  
-   Paramètres.  
  
-   Fonctions système dont le nom commence par @@.  
  
-   Expressions générées par l’application d’opérateurs à une ou plusieurs variables, un ou plusieurs paramètres ou une ou plusieurs fonctions système, comme @IntegerCounter + 1 ou FirstName + LastName.  
  
-   Instructions Transact-SQL qui retournent une valeur unique, tel que : SELECT CharacterCol FROM MyTable où PrimaryKey = 1.  
  
 **Valeur**  
 Affiche la valeur retournée après que le débogueur [!INCLUDE[tsql](../../includes/tsql-md.md)] a évalué l’expression spécifiée dans **Nom**.  
  
 Si la longueur d'une expression dépasse la largeur de la colonne **Valeur** , une info-bulle affiche la valeur complète lorsque vous placez le pointeur sur la cellule **Valeur** de cette expression.  
  
 La présence d'une icône de loupe dans une cellule **Valeur** indique que le visualiseur du débogueur [!INCLUDE[tsql](../../includes/tsql-md.md)] est disponible. Dans la liste, vous pouvez spécifier **Visualiseur de texte**, **Visualiseur XML**ou **Visualiseur HTML**. Pour démarrer un visualiseur du débogueur, cliquez sur l'icône de loupe. Le débogueur [!INCLUDE[tsql](../../includes/tsql-md.md)] ouvre une boîte de dialogue qui affiche les données dans un format adapté au type de données.  
  
 **Type**  
 Affiche le type de données de l'expression.  
  
## <a name="see-also"></a>Voir aussi  
 [Débogueur Transact-SQL](transact-sql-debugger.md)   
 [Informations du débogueur Transact-SQL](transact-sql-debugger-information.md)   
 [Variables locales (fenêtre)](transact-sql-debugger-locals-window.md)   
 [Fenêtre Pile des appels](transact-sql-debugger-call-stack-window.md)   
 [Boîte de dialogue Espion express](transact-sql-debugger-quickwatch-dialog-box.md)   
 [Expressions &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/expressions-transact-sql)  
