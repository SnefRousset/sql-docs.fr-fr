---
title: PredictAdjustedProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9fd11ec1fcdf9a3c6ce5dc6476e877d808710b54
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989638"
---
# <a name="predictadjustedprobability-dmx"></a>PredictAdjustedProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retourne la probabilité ajustée d'un état spécifié.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
PredictAdjustedProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>S'applique à  
 Colonne scalaire  
  
## <a name="return-type"></a>Type de retour  
 Une valeur scalaire.  
  
## <a name="remarks"></a>Notes  
 Si l'état prévisible est omis, c'est l'état doté de la probabilité de prévision la plus élevée qui est utilisé, à l'exception du compartiment des états manquants. Pour inclure le compartiment des États manquants, définissez le \<état prédit > à **INCLUDE_NULL**.  
  
 Pour retourner la probabilité ajustée des États manquants, définissez la \<état prédit > sur la valeur NULL.  
  
 Le **PredictAdjustedProbability** fonction est un [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] extension pour le [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB pour la spécification d’exploration de données.  
  
## <a name="examples"></a>Exemples  
 L'exemple suivant utilise une prédiction de jointure naturelle pour déterminer si un individu peut se révéler un acheteur potentiel de bicyclette selon le modèle d'exploration de données Arbre de décision TM et pour définir la probabilité ajustée de cette prévision.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictAdjustedProbability([Bike Buyer]) AS [Adjusted Probability]  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Data Mining Extensions &#40;DMX&#41; référence de fonction](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Fonctions &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Fonctions de prédiction générales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
