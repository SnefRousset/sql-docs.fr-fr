---
title: Exécuter pas à pas du code Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, debugging code
- Transact-SQL debugger, step over
- Transact-SQL debugger, step out
- Transact-SQL debugger, step into
ms.assetid: e09079b8-c4c9-42b4-821b-4ce81a98a086
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b46deb42a6729cbf122aca0fcb4618143bc786a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144409"
---
# <a name="step-through-transact-sql-code"></a>Exécuter pas à pas du code Transact-SQL
  Le débogueur [!INCLUDE[tsql](../../includes/tsql-md.md)] vous permet de contrôler les instructions [!INCLUDE[tsql](../../includes/tsql-md.md)] qui sont exécutées dans une fenêtre de l'éditeur de requête du [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Vous pouvez suspendre le débogueur au niveau d'instructions individuelles, puis afficher l'état des éléments de code à ce stade.  
  
## <a name="breakpoints"></a>Points d’arrêt  
 Un point d'arrêt indique au débogueur de suspendre l'exécution à une instruction [!INCLUDE[tsql](../../includes/tsql-md.md)] spécifique. Pour plus d'informations sur les points d'arrêt, consultez Utilisation de points d'arrêt Transact-SQL.  
  
## <a name="controlling-statement-execution"></a>Contrôle de l'exécution d'instructions  
 Dans le débogueur [!INCLUDE[tsql](../../includes/tsql-md.md)] , vous pouvez spécifier les options suivantes pour exécuter le code [!INCLUDE[tsql](../../includes/tsql-md.md)] à partir de l'instruction actuelle :  
  
-   Exécuter le code jusqu'au point d'arrêt suivant.  
  
-   Effectuer un pas à pas détaillé dans l'instruction suivante.  
  
     Si l'instruction suivante appelle une procédure stockée, une fonction ou un déclencheur [!INCLUDE[tsql](../../includes/tsql-md.md)] , le débogueur affiche une nouvelle fenêtre de l'éditeur de requête contenant le code du module. La fenêtre est en mode débogage, et l'exécution s'arrête à la première instruction dans le module. Vous pouvez ensuite parcourir le code du module, en définissant par exemple des points d'arrêt ou en exécutant le code pas à pas.  
  
-   Effectuer un pas à pas principal dans l'instruction suivante.  
  
     L'instruction suivante est exécutée. Toutefois, si l'instruction appelle une procédure stockée, une fonction ou un déclencheur, le code de module s'exécute jusqu'à ce qu'il se termine, et les résultats sont retournés au code appelant. Si vous êtes certain qu'une procédure stockée ne comporte aucune erreur, vous pouvez faire un pas à pas principal. L'exécution s'arrête à l'instruction qui suit l'appel à la procédure stockée, à la fonction ou au déclencheur.  
  
-   Effectuer un pas à pas sortant dans une procédure stockée, une fonction ou un déclencheur.  
  
     L'exécution s'arrête à l'instruction qui suit l'appel à la procédure stockée, à la fonction ou au déclencheur.  
  
-   Exécuter le code à partir de l'emplacement actuel jusqu'à l'emplacement actuel du pointeur et ignorer tous les points d'arrêt.  
  
 Le tableau suivant répertorie les différentes façons dont vous pouvez contrôler l'exécution des instructions dans le débogueur [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
|Action|Procédure|  
|------------|---------------|  
|Exécuter toutes les instructions à partir de l'instruction actuelle jusqu'au point d'arrêt suivant|Sur le **déboguer** menu, cliquez sur **continuer**.<br /><br /> Sur le **déboguer** barre d’outils, cliquez sur le **continuer** bouton.|  
|Effectuer un pas à pas détaillé dans l'instruction ou le module suivant|Sur le **déboguer** menu, cliquez sur **pas à pas détaillé**.<br /><br /> Sur le **déboguer** barre d’outils, cliquez sur le **pas à pas détaillé** bouton.<br /><br /> Appuyez sur F11.|  
|Effectuer un pas à pas principal dans l'instruction ou le module suivant|Sur le **déboguer** menu, cliquez sur **pas à pas principal**.<br /><br /> Sur le **déboguer** barre d’outils, cliquez sur le **pas à pas principal** bouton.<br /><br /> Appuyez sur F10.|  
|Effectuer un pas à pas sortant dans un module|Sur le **déboguer** menu, cliquez sur **pas à pas sortant**.<br /><br /> Sur le **déboguer** barre d’outils, cliquez sur le **pas à pas sortant** bouton.<br /><br /> Appuyez sur Maj+F11.|  
|Exécuter le code jusqu'à l'emplacement du curseur actuel|Cliquez avec le bouton droit dans la fenêtre de l’éditeur de requête, puis cliquez sur **Exécuter jusqu’au curseur**.<br /><br /> Appuyez sur Ctrl+F10.|  
  
## <a name="see-also"></a>Voir aussi  
 [Informations du débogueur Transact-SQL](transact-sql-debugger-information.md)  
  
  
