---
title: Afficher et enregistrer les résultats d’une requête de prédiction | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- viewing prediction query results
- displaying prediction query results
- Mining Model Prediction [Analysis Services], viewing results
ms.assetid: abba4d24-3619-44c1-8279-88f27ad627d3
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff501825009b9ebdfeb8708419b8dbfb4690be62
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253191"
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>Afficher et enregistrer les résultats d'une requête de prédiction
  Après avoir défini une requête dans [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en utilisant le Générateur de requêtes de prédiction, vous pouvez exécuter la requête et afficher les résultats en basculant vers l’affichage des résultats de la requête.  
  
 Vous pouvez enregistrer les résultats d’une requête de prédiction dans une table d’une source de données définie dans un projet [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Vous pouvez créer une table ou enregistrer les résultats de la requête dans une table existante. Si vous enregistrez les résultats dans une table existante, vous pouvez remplacer les données actuellement stockées dans la table. Sinon, les résultats de la requête sont ajoutés aux données existantes dans la table.  
  
### <a name="run-a-query-and-view-the-results"></a>Exécuter une requête et afficher les résultats  
  
1.  Dans la barre d’outils de l’onglet **Prédiction de modèle d’exploration de données** du Concepteur d’exploration de données dans [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], cliquez sur **Résultat** .  
  
     L'affichage des résultats de la requête s'ouvre et exécute la requête. Les résultats s'affichent dans une grille de la visionneuse.  
  
### <a name="save-the-results-of-a-prediction-query-to-a-table"></a>Enregistrer les résultats d'une requête de prédiction dans une table  
  
1.  Dans la barre d’outils de l’onglet **Prédiction de modèle d’exploration de données** du Concepteur d’exploration de données, cliquez sur **Enregistrer le résultat de la requête**.  
  
     La boîte de dialogue **Enregistrer le résultat de la requête d’exploration de données** s’ouvre.  
  
2.  Sélectionnez une source de données dans la liste **Source de données** ou cliquez sur **Nouvelle** pour créer une source de données.  
  
3.  Dans la zone **Nom de la table** , tapez le nom de la table. Si la table existe, sélectionnez **Remplacer en cas d’existence** pour remplacer le contenu de la table par les résultats de la requête. Si vous ne voulez pas remplacer le contenu de la table, n'activez pas cette case à cocher. Les résultats de la nouvelle requête seront ajoutés aux données existantes dans la table.  
  
4.  Sélectionnez une vue de source de données dans **Ajouter à la vue de source de données** si vous voulez ajouter la table à une vue de source de données.  
  
5.  Cliquez sur **Enregistrer**.  
  
    > [!WARNING]  
    >  Si la destination ne prend pas en charge les ensembles de lignes hiérarchiques, vous pouvez ajouter le mot clé FALTTENED aux résultats pour les enregistrer sous forme de table plate.  
  
  