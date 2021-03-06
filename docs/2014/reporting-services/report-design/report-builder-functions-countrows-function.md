---
title: Fonction CountRows (Générateur de rapports et SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1dc4b25309228eb0b5a65ab1ec54fc6b59a82c9d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297317"
---
# <a name="countrows-function-report-builder-and-ssrs"></a>Fonction CountRows (Générateur de rapports et SSRS)
  Retourne le nombre de lignes dans l'étendue spécifiée, y compris celles contenant des valeurs Null.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>Paramètres  
 *portée*  
 (`String`) Nom d'un dataset, d'un groupe ou d'une région de données qui contient les éléments de rapport à compter.  
  
 *récursifs*  
 (**Type énuméré**) Facultatif. `Simple` (par défaut) ou `RdlRecursive`. Indique s'il faut effectuer l'agrégation de manière récursive.  
  
## <a name="return-type"></a>Type de retour  
 Retourne un `Integer`.  
  
## <a name="remarks"></a>Notes  
 `CountRows` compte toutes les lignes dans l'étendue spécifiée, y compris celles contenant des valeurs Null.  
  
 La valeur du paramètre *scope* ne peut pas être une expression et doit faire référence à l'étendue actuelle ou à une étendue contenante.  
  
 Pour plus d’informations, consultez [Référence aux fonctions d’agrégation &#40;Générateur de rapports et SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) et [Étendue des expressions pour les totaux, les agrégats et les collections intégrées &#40;Générateur de rapports et SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Pour plus d’informations sur les agrégats récursifs, consultez [Création de groupes de hiérarchies récursives &#40;Générateur de rapports et SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemple  
 L'exemple de code suivant affiche une expression qui calcule le nombre de lignes dans un groupe de lignes nommé `GroupbyCategory` (basé sur l'expression `[Category]`).  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Utilisation d’expressions dans les rapports &#40;Générateur de rapport et SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemples d’expressions &#40;Générateur de rapports et SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Types de données dans les expressions &#40;Générateur de rapports et SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Étendue des expressions pour les totaux, les agrégats et les collections intégrées &#40;Générateur de rapports et SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
