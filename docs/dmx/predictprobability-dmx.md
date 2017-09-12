---
title: PredictProbability (DMX) | Documents Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictProbability
dev_langs:
- DMX
helpviewer_keywords:
- PredictProbability function
ms.assetid: 7bb7e74f-e33b-4f7b-ade8-be21ace0dbd0
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e0cdcf4b193cf1b05967fdbc5b266ebd0ca9700
ms.contentlocale: fr-fr
ms.lasthandoff: 08/02/2017

---
# <a name="predictprobability-dmx"></a>PredictProbability (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retourne la probabilité pour un état spécifié.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
PredictProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>S'applique à  
 Colonne scalaire  
  
## <a name="return-type"></a>Type de retour  
 Une valeur scalaire.  
  
## <a name="remarks"></a>Notes  
 Si l'état prédit est omis, l'état ayant la probabilité la plus élevée est utilisé, à l'exception du compartiment des états manquants. Pour inclure le compartiment des États manquants, définissez la \<état prédit > à **INCLUDE_NULL**. Pour retourner la probabilité des États manquants, définissez la \<état prédit > sur la valeur NULL.  
  
> [!NOTE]  
>  Certains modèles d'exploration de données ne fournissent pas de valeurs de probabilité et ne peuvent donc pas utiliser cette fonction. De plus, les valeurs de probabilité des valeurs cibles spécifiques sont calculées différemment ou peuvent avoir une interprétation différente selon le type de modèle que vous interrogez. Pour plus d’informations sur la façon dont la probabilité est calculée pour un type de modèle particulier, consultez la rubrique de l’algorithme individuel dans [contenu du modèle d’exploration de données &#40; Analysis Services - Exploration de données &#41; ](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Exemples  
 L'exemple suivant utilise une prédiction de jointure naturelle pour déterminer si un individu peut se révéler un acheteur potentiel de bicyclette selon le modèle d'exploration de données Arbre de décision TM et pour définir la probabilité de cette prévision. Cet exemple inclut deux fonctions PredictProbability, à raison d'une pour chaque valeur possible. Si vous omettez cet argument, la fonction retourne la probabilité pour la valeur la plus probable.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictProbability([Bike Buyer], 1) AS [Bike Buyer = Yes],  
  PredictProbability([Bike Buyer], 0) AS [Bike Buyer = No]  
FROM [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Résultats de l'exemple :  
  
|Bike Buyer|Bike Buyer = Yes|Bike Buyer = No|  
|----------------|-----------------------|----------------------|  
|1|0.867074195848097|0.132755556974282|  
  
## <a name="see-also"></a>Voir aussi  
 [Les Extensions d’exploration de données &#40; DMX &#41; Référence de fonction](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Fonctions &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Fonctions de prédiction générales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
