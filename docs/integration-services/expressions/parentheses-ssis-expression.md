---
title: () (Parenthèses) (expression SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 99ab67a88006579d61ba4d084d37b60d5b80bd45
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276918"
---
# <a name="-parentheses-ssis-expression"></a>() (Parenthèses) (expression SSIS)
  Identifie l'ordre d'évaluation des expressions. Les expressions entre parenthèses ont la priorité d'évaluation la plus élevée. L'évaluation des expressions imbriquées placées entre parenthèses commence par celle située le plus à l'intérieur, puis se poursuit jusqu'à celle située le plus à l'extérieur.  
  
 Les parenthèses permettent également de faciliter la compréhension des expressions complexes.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>Arguments  
 *expression*  
 Toute expression valide.  
  
## <a name="result-types"></a>Types des résultats  
 Le type de données *expression*. Pour plus d’informations, consultez [Types de données Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Exemples d'expressions  
 Cet exemple illustre la façon dont l'utilisation des parenthèses modifie la priorité des opérateurs. La première expression totalise 100 tandis que la seconde cumule à 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a> Voir aussi  
 [Priorités et associativité des opérateurs](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Opérateurs &#40;expression SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
