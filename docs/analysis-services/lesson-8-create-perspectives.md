---
title: Leçon 8 créer des Perspectives | Microsoft Docs
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90120c5dd439e4518086b261d507bf49f62450f1
ms.sourcegitcommit: e8e013b4d4fbd3b25f85fd6318d3ca8ddf73f31e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42795538"
---
# <a name="lesson-8-create-perspectives"></a>Leçon 8 : Créer des Perspectives
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Dans cette leçon, vous allez créer une perspective Internet Sales. Une perspective définit un sous-ensemble visualisable d'un modèle et des points de vue du modèle focalisés sur un domaine d'activité ou sur une application. Lorsqu’un utilisateur se connecte à un modèle à l’aide d’un point de vue, ils voient uniquement les objets de modèle (tables, colonnes, les mesures, hiérarchies et KPI) en tant que champs définis dans cette perspective.  
  
La perspective Internet Sales que vous créez dans cette leçon exclura l’objet de la table DimCustomer. Lorsque vous créez une perspective qui exclut certains objets de la vue, cet objet existe toujours dans le modèle ; toutefois, il n'est pas visible dans une liste de champs de client de création de rapports. Les colonnes calculées et les mesures incluses ou non dans une perspective peuvent toujours être calculées à partir de données d'objet exclues.  
  
L'objectif de cette leçon est plutôt de décrire comment créer des points de vue et de vous familiariser avec les outils de création de modèles tabulaires. Si vous décidez plus tard ce modèle pour inclure des tables supplémentaires, vous pouvez créer des perspectives supplémentaires pour définir les différents points de vue du modèle, par exemple, les ventes et les stocks. Pour plus d’informations, consultez [Perspectives](../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
Durée estimée pour effectuer cette leçon : **5 minutes**  
  
## <a name="prerequisites"></a>Prérequis  
Cette rubrique fait partie d'un didacticiel de modélisation tabulaire, qui doit être suivi dans l'ordre. Avant d’effectuer les tâches de cette leçon, vous devez avoir terminé la leçon précédente : [leçon 7 : créer des indicateurs de Performance clés](../analysis-services/lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Créer des perspectives  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Pour créer une perspective Internet Sales  
  
1.  Cliquez sur le **modèle** menu > **Perspectives** > **créer et gérer**.  
  
2.  Dans la boîte de dialogue **Perspectives** , cliquez sur **Nouvelle perspective**.  
  
3.  Double-cliquez sur le **nouvelle Perspective** en-tête de colonne et puis renommerez **Internet Sales**.  
  
4.  Sélectionnez toutes les tables *sauf* **DimCustomer**.  
  
    ![en tant que-tabulaire-lesson8-perspectives](../analysis-services/media/as-tabular-lesson8-perspectives.png)
  
    Dans une leçon ultérieure, vous utiliserez l’analyser dans la fonctionnalité Excel pour tester cette perspective. La liste de champs de tableau croisé dynamique Excel inclut chaque table à l’exception de la table DimCustomer.  

## <a name="whats-next"></a>Quelle est l’étape suivante ?
Accédez à la leçon suivante : [leçon 9 : créer des hiérarchies](../analysis-services/lesson-9-create-hierarchies.md).
  
  
  
  
