---
title: "Décrivant les paramètres | Documents Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d78b3b7ac10fae37bb35f88cefaf5983e0df09a4
ms.contentlocale: fr-fr
ms.lasthandoff: 09/09/2017

---
# <a name="describing-parameters"></a>Décrivant les paramètres
**SQLBindParameter** a des arguments qui décrivent le paramètre : son type SQL, la précision et l’échelle. Le pilote utilise ces informations, ou *métadonnées,* pour convertir la valeur du paramètre du type requis par la source de données. À première vue, il peut sembler que le pilote est en mesure de mieux connaître les métadonnées de paramètre que l’application ; Après tout, le pilote peut découvrir facilement les métadonnées de colonne du jeu de résultats. En fait, cela n’est pas le cas. Tout d’abord, la plupart des sources de données ne fournissent pas un moyen pour le pilote découvrir les métadonnées de paramètre. Ensuite, la plupart des applications connaissez déjà les métadonnées.  
  
 Si une instruction SQL est codée en dur dans l’application, le writer d’application connaît déjà le type de chaque paramètre. Si une instruction SQL est générée par l’application au moment de l’exécution, l’application peut déterminer les métadonnées, car elle génère l’instruction. Par exemple, lorsque l’application construit la clause  
  
```  
WHERE OrderID = ?  
```  
  
 elle peut appeler **SQLColumns** pour la colonne OrderID.  
  
 Le seul cas dans lequel l’application ne peut pas déterminer facilement les métadonnées de paramètre est lorsque l’utilisateur entre une instruction paramétrable. Dans ce cas, l’application appelle **SQLPrepare** pour préparer l’instruction, **SQLNumParams** pour déterminer le nombre de paramètres, et **SQLDescribeParam** pour décrire chaque paramètre. Toutefois, comme indiqué précédemment, la plupart des sources de données ne fournissent pas un moyen pour le pilote découvrir les métadonnées de paramètre, donc **SQLDescribeParam** n’est pas largement pris en charge.