---
title: "Outils de gestion et le d&#233;veloppement Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "environnements Studio [Integration Services]"
  - "outils [Integration Services], Business Intelligence Development Studio"
  - "Business Intelligence Development Studio, Integration Services"
  - "SQL Server Management Studio [Integration Services]"
  - "SSIS, environnements de studio"
  - "SQL Server Integration Services, environnements de studio"
  - "outils [Integration Services], SQL Server Management Studio"
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
caps.latest.revision: 52
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 52
---
# Outils de gestion et le d&#233;veloppement Integration Services (SSIS)
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclut deux studios de travail pour travailler avec [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] pour le développement des packages [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] requis par une solution métier. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fournit le projet [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dans lequel vous créez des packages.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] pour la gestion de packages dans un environnement de production.  
  
## Outils de données SQL Server  
 Vous pouvez réaliser les tâches suivantes dans [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]:  
  
-   exécuter l'Assistant Importation et Exportation [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pour créer des packages de base qui copient des données entre une source et une destination ;  
  
-   créer des packages qui incluent un flux de contrôle complexe, un flux de données, une logique piloté par les événements et la journalisation ;  
  
-   tester et déboguer les packages à l'aide des fonctionnalités de résolution des problèmes et de surveillance du concepteur [!INCLUDE[ssIS](../includes/ssis-md.md)] et des fonctionnalités de débogage de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)];  
  
-   créer des configurations qui mettent à jour les propriétés des packages et les objets de package au moment de l'exécution ;  
  
-   créer un utilitaire de déploiement qui peut installer les packages et leurs dépendances sur d'autres ordinateurs ;  
  
-   Enregistrer des copies des packages dans le [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb de base de données, le magasin de packages de [!INCLUDE[ssIS](../includes/ssis-md.md)] et le système de fichiers.  
  
 Pour plus d'informations sur [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], consultez [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686.aspx).  
  
## SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fournit le service [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que vous utilisez pour gérer des packages, surveiller les packages en cours d'exécution, et déterminer l'impact et le lignage des données pour les objets [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] et [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Vous pouvez réaliser les tâches suivantes dans [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]:  
  
-   créer des dossiers pour organiser les packages de manière significative pour votre organisation ;  
  
-   exécuter les packages stockés sur l'ordinateur local à l'aide de l'utilitaire d'exécution de package ;  
  
-   Exécutez l’utilitaire d’exécution de Package pour générer une ligne de commande à utiliser lorsque vous exécutez le **dtexec** utilitaire de ligne de commande (dtexec.exe).  
  
-   importer et exporter des packages dans la base de données msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la banque de packages [!INCLUDE[ssIS](../includes/ssis-md.md)] et le système de fichiers.  