---
title: Éditeur de Destination de traitement de dimension (Page Gestionnaire de connexions) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.connection.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e48018f3bbc3f266a4e537f067b3fa9466dea275
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381954"
---
# <a name="dimension-processing-destination-editor-connection-manager-page"></a>Éditeur de destination de traitement de dimension (page Gestionnaire de connexions)
  La page **Gestionnaire de connexions** de la boîte de dialogue **Éditeur de destination de traitement de dimension** vous permet de spécifier une connexion à un projet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou à une instance de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Pour en savoir plus sur la destination de traitement de dimension, consultez [Dimension Processing Destination](data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Options  
 **Connection manager**  
 Sélectionnez un gestionnaire de connexions existant dans la liste ou cliquez sur **Nouveau** pour créer un gestionnaire de connexions.  
  
 **Nouveau**  
 Créez une connexion à l’aide de la boîte de dialogue **Ajout d’un gestionnaire de connexions Analysis Services** .  
  
 **Liste des dimensions disponibles**  
 Sélectionnez la dimension à traiter.  
  
 **Méthode de traitement**  
 Sélectionnez la méthode de traitement à appliquer à la dimension sélectionnée dans la liste. La valeur par défaut de cette option est **Complète**.  
  
|Value|Description|  
|-----------|-----------------|  
|**Ajouter (incrémentiel)**|Permet d'effectuer un traitement incrémentiel de la dimension.|  
|**Complète**|Permet d'effectuer un traitement complet de la dimension.|  
|**Update**|Permet d'effectuer un traitement de mise à jour de la dimension.|  
  
## <a name="see-also"></a>Voir aussi  
 [Guide de référence des erreurs et des messages propres à Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Éditeur de destination de traitement de dimension &#40;page Mappages&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)   
 [Éditeur de destination de traitement de dimension &#40;page Avancé&#41;](../../2014/integration-services/dimension-processing-destination-editor-advanced-page.md)  
  
  
