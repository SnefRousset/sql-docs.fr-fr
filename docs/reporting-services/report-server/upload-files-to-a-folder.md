---
title: "T&#233;l&#233;charger des fichiers dans un dossier | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publication de rapports [Reporting Services], chargement de fichiers"
  - "rapports [Reporting Services], publication"
  - "téléchargement de rapports (upload) [Reporting Services]"
  - "téléchargement de fichiers (upload) [Reporting Services]"
  - "fichiers [Reporting Services], chargement"
  - "fichiers [Reporting Services]"
  - "dossiers [Reporting Services], chargement de fichiers"
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# T&#233;l&#233;charger des fichiers dans un dossier
  Vous pouvez télécharger des fichiers à partir du système de fichiers, puis les stocker comme éléments gérés dans une base de données de serveur de rapports. Ce qui se produit lorsque vous téléchargez un fichier dépend du type du fichier.  
  
-   Le téléchargement d'un fichier .rdl équivaut à la publication d'un rapport.  
  
-   Le téléchargement de n'importe quel autre fichier l'ajoute à la base de données du serveur de rapports en tant qu'objet binaire unique. Ces fichiers sont publiés sur un serveur de rapports en tant que ressource. Les ressources peuvent être n'importe quel type de fichier. Si l'extension de fichier correspond à un type MIME connu, une icône associée à ce type MIME est utilisée pour identifier le type de la ressource. Sinon, une icône de fichier générique indique la présence d'une ressource.  
  
> [!NOTE]  
>  Vous pouvez télécharger un fichier de source de données de rapports (.rds) pour créer une source de données partagée. Les fichiers .rds sont utilisables uniquement dans le Générateur de rapports. Ils ne peuvent en aucun cas fournir le contenu d'un élément de source de données partagée que vous définissez et gérez via le Gestionnaire de rapports. Outre le téléchargement, vous pouvez écrire un script qui crée une source de données partagée en se basant sur un fichier .rds.  
  
 La taille de fichier maximale des éléments téléchargés est déterminée par [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Par défaut, la taille maximale est de 4 mégaoctets (Mo).  
  
 Sur un plan visuel, les fichiers que vous téléchargez dans une base de données de serveur de rapports s'affichent dans l'arborescence des dossiers avec les icônes suivantes.  
  
 ![Icône de rapport](../../reporting-services/report-server/media/hlp-16doc.png "Icône de rapport")  
icône de rapport  
  
 ![Icône Modèle](../../reporting-services/report-server/media/model-icon.png "Icône Modèle")  
icône de modèle de rapport  
  
 ![icône de ressource générique](../../reporting-services/report-server/media/hlp-16file.png "icône de ressource générique")  
icône de ressource générique  
  
 Lorsque vous téléchargez un fichier, il est toujours placé dans le dossier en cours de sélection. Vous pouvez soit naviguer d'abord vers le dossier où l'élément sera stocké, soit télécharger un fichier puis le déplacer ultérieurement vers son emplacement définitif.  
  
 Pour télécharger un fichier, utilisez le Gestionnaire de rapports. Votre possibilité de télécharger des fichiers sur un serveur de rapports dépend des tâches incluses dans votre attribution de rôle. Si vous utilisez la sécurité par défaut, les administrateurs locaux peuvent ajouter des éléments à un serveur de rapports. Si la fonctionnalité Mes rapports est activée, tout utilisateur disposant d'un dossier Mes rapports est autorisé à télécharger des éléments dans ce dossier. Si vous utilisez des attributions de rôle personnalisées, l'attribution de rôle doit inclure les tâches prenant en charge la gestion de dossiers.  
  
|Pour effectuer cette opération|Incluez ces tâches|  
|----------------|-------------------------|  
|Télécharger un fichier .rdl dans un dossier|Gérer les rapports|  
|Télécharger un fichier en tant qu'objet binaire|Gérer les ressources|  
|Afficher le contenu d'un dossier|Afficher les ressources, afficher les rapports|  
  
## Voir aussi  
 [Gestionnaire de rapports &#40;SSRS en mode natif&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)   
 [Octroi d'autorisations sur un serveur de rapports en mode natif](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Tâches et autorisations](../../reporting-services/security/tasks-and-permissions.md)   
 [Télécharger un fichier ou un rapport &#40;Gestionnaire de rapports&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)  
  
  