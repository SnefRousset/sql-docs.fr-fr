---
title: "Deploy Model Solutions Using the Deployment Wizard | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services Deployment Wizard"
  - "deploying [Analysis Services], Analysis Services Deployment Wizard"
  - "Analysis Services deployments, Analysis Services Deployment Wizard"
  - "Assistant Déploiement d’Analysis Services, à propos de l’Assistant Déploiement d’Analysis Services"
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
caps.latest.revision: 39
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 37
---
# Deploy Model Solutions Using the Deployment Wizard
  L'Assistant Déploiement de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilise les fichiers de sortie XML générés à partir d'un projet [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] comme fichiers d'entrée. Il est facile de modifier ces fichiers d'entrée pour personnaliser le déploiement d'un projet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Le script de déploiement généré peut alors être immédiatement exécuté ou enregistré en vue d'un déploiement ultérieur.  
  
 Vous pouvez déployer un projet à l'aide de l'Assistant comme l'explique la présente rubrique. Vous pouvez aussi automatiser le déploiement ou utiliser la fonctionnalité de Synchronisation. Si la base de données déployée est de grande taille, envisagez d'utiliser des partitions sur les systèmes cibles. Vous pouvez aussi automatiser la création et le remplissage des partitions à l’aide d’objets \(AMO\) (Analysis Management Objects).  
  
> [!IMPORTANT]  
>  Ni les fichiers de sortie XML, ni le script de déploiement ne contiennent l'ID utilisateur ou le mot de passe si ces derniers sont spécifiés dans la chaîne de connexion d'une source de données ou à des fins d'emprunt d'identité. Dans la mesure où ces informations sont nécessaires pour le traitement dans ce scénario, vous devez les ajouter manuellement. Si le déploiement n'inclut pas de traitement, vous pouvez ajouter ces informations de connexion et d'emprunt d'identité en fonction de vos besoins après le déploiement. Si le déploiement inclut un traitement, vous pouvez ajouter ces informations dans l'Assistant ou dans le script de déploiement une fois qu'il a été enregistré.  
  
## Dans cette section  
 Les rubriques suivantes expliquent comment utiliser l'Assistant Déploiement de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , les fichiers d'entrée et le script de déploiement :  
  
|Rubrique|Description|  
|-----------|-----------------|  
|[Exécution de l'Assistant Déploiement d'Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|Décrit les différentes façons d'exécuter l'Assistant Déploiement de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Précisions sur les fichiers d'entrée utilisés pour créer le script de déploiement](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)|Décrit les fichiers que l'Assistant Déploiement de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilise comme valeurs d'entrée et leur contenu, en fournissant des liens à des rubriques qui expliquent comment modifier les valeurs stockées dans chacun des fichiers d'entrée.|  
|[Description du script de déploiement Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|Décrit le contenu du script de déploiement et explique comment il s'exécute.|  
  
## Voir aussi  
 [Déployer des solutions de modèle à l'aide de XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Synchroniser des base de données Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Précisions sur les fichiers d'entrée utilisés pour créer le script de déploiement](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)   
 [Déployer des solutions de modèle avec l'utilitaire de déploiement](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  