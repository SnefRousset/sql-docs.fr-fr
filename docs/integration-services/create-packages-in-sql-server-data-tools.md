---
title: "Cr&#233;er des packages dans les outils de donn&#233;es SQL Server | Microsoft Docs"
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
  - "packages SSIS, création"
  - "packages Integration Services, création"
  - "packages [Integration Services], création"
  - "packages SQL Server Integration Services, création"
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
caps.latest.revision: 51
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 51
---
# Cr&#233;er des packages dans les outils de donn&#233;es SQL Server
  Dans [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], vous pouvez créer un nouveau package à l'aide de l'une des méthodes suivantes :  
  
-   Utiliser le modèle de package inclus dans [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Utiliser un modèle personnalisé  
  
     Pour utiliser des packages personnalisés comme modèles pour la création de nouveaux packages, il vous suffit de les copier dans le dossier DataTransformationItems. Par défaut, ce dossier se trouve dans C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
-   Copier un package existant.  
  
     Si des packages existants incluent des fonctionnalités que vous souhaitez réutiliser, vous pouvez construire le flux de contrôle et les flux de données dans le package plus rapidement en copiant et en collant des objets à partir de nouveaux packages. Pour plus d’informations sur le copier et coller dans des projets [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], consultez [Réutiliser des objets de packages](../integration-services/reuse-of-package-objects.md).  
  
     Si vous créez un nouveau package en copiant un package existant ou en utilisant un package personnalisé comme modèle, le nom et le GUID du package existant sont copiés également. Vous devez mettre à jour le nom et le GUID du nouveau package pour le différencier plus facilement du package à partir duquel il a été copié. Par exemple, si des packages ont le même GUID, il est plus difficile d'identifier le package auquel appartiennent les données de journal. Vous pouvez régénérer le GUID dans la propriété **ID** et mettre à jour la valeur de la propriété **Name** à l’aide de la fenêtre Propriétés dans [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Pour plus d’informations, consultez [Définir les propriétés d’un package](../integration-services/set-package-properties.md) et [Utilitaire dtutil](../integration-services/dtutil-utility.md).  
  
-   Utiliser un package personnalisé que vous avez désigné comme modèle.  
  
-   Exécuter l'Assistant Importation et Exportation [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
     L'Assistant Importation et Exportation [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] crée un package complet pour une opération simple d'importation ou d'exportation. Cet Assistant configure les connexions, la source et la destination, et ajoute toutes les transformations de données requises pour vous permettre d'exécuter l'opération d'importation ou d'exportation immédiatement. Vous pouvez enregistrer, le cas échéant, le package pour l'exécuter de nouveau ultérieurement ou pour l'affiner et l'améliorer dans [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Toutefois, si vous enregistrez le package, vous devez l'ajouter à un projet [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] existant avant de pouvoir le modifier ou l'exécuter dans [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 Les packages que vous créez dans [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] à l'aide du concepteur [!INCLUDE[ssIS](../includes/ssis-md.md)] sont enregistrés dans le système de fichiers. Pour enregistrer un package dans [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou dans le magasin de packages, vous devez enregistrer une copie du package. Pour plus d’informations, consultez [Enregistrer une copie d’un package](../Topic/Save%20a%20Copy%20of%20a%20Package.md).  

 Pour obtenir une vidéo qui montre comment créer un package de base à l’aide du modèle de package par défaut, consultez[Création d’un package de base (Vidéo liée à SQL Server)](http://go.microsoft.com/fwlink/?LinkId=131023).  

## Obtenir SQL Server Data Tools
Pour installer SQL Server Data Tools (SSDT), consultez [Télécharger SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## Créer un package dans SQL Server Data Tools à l’aide du modèle de package  
  
1.  Dans [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], ouvrez le projet [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dans lequel vous souhaitez créer un package.  
  
2.  Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le dossier **Packages SSIS**, puis cliquez sur **Nouveau package SSIS**.  
  
3.  Si vous le souhaitez, ajoutez des tâches de flux de contrôle, des tâches de flux de données et des gestionnaires d'événements au package. Pour plus d’informations, consultez [Flux de contrôle](../integration-services/control-flow/control-flow.md), [Flux de données](../integration-services/data-flow/data-flow.md) et [Gestionnaires d’événements Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-event-handlers.md).  
  
4.  Dans le menu **Fichier** , cliquez sur **Enregistrer les éléments sélectionnés** pour enregistrer le nouveau package.  
  
    > [!NOTE]  
    >  Vous pouvez enregistrer un package vide.  
  
## Choisir la version cible d’un projet et de ses packages  
  
1.  Dans l’Explorateur de solutions, cliquez avec le bouton droit sur un projet Integration Services, puis sélectionnez **Propriétés** pour ouvrir les pages de propriétés du projet.  
  
2.  Sous l’onglet **Général** de **Propriétés de configuration**, sélectionnez la propriété **TargetServerVersion** , puis choisissez SQL Server 2016, SQL Server 2014 ou SQL Server 2012.  
  
     ![TargetServerVersion property in project properties dialog box](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
  
 Vous pouvez créer, gérer et exécuter des packages qui ciblent SQL Server 2016, SQL Server 2014 ou SQL Server 2012.  
  
  