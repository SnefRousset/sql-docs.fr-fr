---
title: Éditeur de Transformation de tri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort Transformation Editor
ms.assetid: 8ae23970-49a9-4d6d-9f15-c7074783347c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: abc74915adf0f2b3fd3ae96420dea921f28ff8e3
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389037"
---
# <a name="sort-transformation-editor"></a>Éditeur de transformation de tri
  Utilisez la boîte de dialogue **Éditeur de transformation de tri** pour sélectionner les colonnes à trier, définir l'ordre de tri et indiquer si les doublons sont supprimés.  
  
 Pour en savoir plus sur la transformation de tri, consultez [Sort Transformation](data-flow/transformations/sort-transformation.md).  
  
## <a name="options"></a>Options  
 **Colonnes d'entrée disponibles**  
 Définissez les colonnes à trier en utilisant les cases à cocher.  
  
 **Nom**  
 Affiche le nom de chaque colonne d'entrée disponible.  
  
 **Relais**  
 Indique s'il faut inclure la colonne dans la sortie triée.  
  
 **Colonne d'entrée**  
 Sélectionnez dans la liste le nom d'une colonne d'entrée pour chaque ligne. Vos sélections se reflètent dans les sélections des cases à cocher de la table **Colonnes d'entrée disponibles** .  
  
 **Alias de sortie**  
 Permet de saisir un alias pour chaque colonne de sortie. Par défaut, il s'agit du nom de la colonne d'entrée ; vous pouvez néanmoins choisir un nom unique et descriptif.  
  
 **Type de tri**  
 Indiquez si vous voulez effectuer un tri croissant ou décroissant.  
  
 **Ordre de tri**  
 Indiquez l'ordre de tri des colonnes. Vous devez le faire manuellement pour chaque colonne.  
  
 **Indicateurs de comparaison**  
 Pour plus d’informations sur les options de comparaison de chaînes, consultez [Comparaison des données chaînes](data-flow/comparing-string-data.md).  
  
 **Supprimer les lignes avec des valeurs de tri en double**  
 Indiquez si la transformation copie les lignes en double dans la sortie de transformation ou crée une seule entrée pour tous les doublons en fonction des options de comparaison de chaînes définies.  
  
## <a name="see-also"></a>Voir aussi  
 [Guide de référence des erreurs et des messages propres à Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
