---
title: "Ajout ou suppression de tables ou de vues dans une vue de source de donn&#233;es (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.dsvdesigner.tablespane.f1"
helpviewer_keywords: 
  - "suppression de tables"
  - "tables [Analysis Services]"
  - "effacement de tables"
  - "ajout de tables"
  - "vues de sources de données [Analysis Services], tables"
  - "tables [Analysis Services], vues de sources de données"
ms.assetid: 98307d04-6548-4d7d-9244-2371dd165249
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 34
---
# Ajout ou suppression de tables ou de vues dans une vue de source de donn&#233;es (Analysis Services)
  Après avoir créé une vue de source de données (DSV) dans [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vous pouvez la modifier dans le concepteur de vue de source de données en ajoutant ou en supprimant des tables et des colonnes, y compris les tables et les colonnes d'une autre source de données.  
  
 Pour ouvrir la vue DSV dans le concepteur de vue de source de données, double-cliquez sur la vue DSV dans l'Explorateur de solutions. Une fois que vous avez ouvert la vue DSV, vous pouvez utiliser la commande **Ajouter/supprimer des tables** dans la barre de boutons ou le menu pour modifier ou étendre la vue DSV. Vous pouvez également utiliser les objets du diagramme. Par exemple, vous pouvez sélectionner un objet puis utiliser la touche Suppr de votre clavier pour supprimer un objet.  
  
> [!WARNING]  
>  Soyez prudent lors de la suppression d'une table. La suppression d'une table supprime toutes les colonnes et relations associées de la vue DSV et invalide tous les objets liés à cette table.  
  
## Sélection des tables ou vues à ajouter ou supprimer  
 Dans la boîte de dialogue **Ajouter/supprimer des tables**, vous pouvez déplacer des tables ou des vues entre les listes **Objets disponibles** et **Objets inclus**. La liste **Objets disponibles** inclut à l’origine les tables ou les vues de la source de données principale qui ne se trouvent pas encore dans la vue de source de données. Si la source de données principale prend en charge la fonction **OPENROWSET**, vous pouvez aussi ajouter des tables ou des vues d’autres sources de données dans le projet ou la base de données.  
  
 L'ajout ou la suppression d'une table à la vue DSV ajoute ou supprime également la table au diagramme sélectionné dans cette vue DSV. Pour plus d’informations sur les diagrammes, consultez [Utiliser des diagrammes dans un concepteur de vues de sources de données &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md).  
  
 Une fois que vous avez placé une table dans la liste **Objets inclus** de la boîte de dialogue **Ajouter/supprimer des tables**, vous pouvez ajouter toutes les tables associées. Cette opération ajoute des tables en fonction des contraintes de clé étrangère dans la source de données, si de telles contraintes existent. S’il n’existe aucune contrainte de clé étrangère, vous pouvez utiliser la propriété **NameMatchingCriteria** de la vue de source de données pour déterminer des relations en spécifiant un critère de correspondance des noms de colonnes dans les tables pour générer des relations possibles. Si la propriété **NameMatchingCriteria** est spécifiée pour la vue de source de données, cliquez sur **Ajouter des tables associées** pour ajouter des tables de la source de données dont les noms de colonnes correspondent. Pour plus d’informations sur la définition de la propriété **NameMatchingCriteria**, consultez [Vues de sources de données dans les modèles multidimensionnels](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  L'ajout ou la suppression d'objets dans une vue de source de données n'affecte pas la source de données sous-jacente.  
  
## Voir aussi  
 [Vues de sources de données dans les modèles multidimensionnels](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Utiliser des diagrammes dans un concepteur de vues de sources de données &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  