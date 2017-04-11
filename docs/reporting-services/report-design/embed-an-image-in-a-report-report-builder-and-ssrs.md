---
title: "Incorporer une image dans un rapport (G&#233;n&#233;rateur de rapports et SSRS) | Microsoft Docs"
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
f1_keywords: 
  - "sql13.rtp.rptdesigner.embeddedimages.f1"
  - "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Incorporer une image dans un rapport (G&#233;n&#233;rateur de rapports et SSRS)
  Un rapport peut inclure une image incorporée. L'incorporation garantit que l'image est toujours disponible pour un rapport, mais elle affecte la taille de la définition de rapport, le fichier qui définit le rapport. Les images incorporées dans un rapport sont répertoriées dans le volet des données de rapport.  
  
 Vous pouvez incorporer une image dans la définition de rapport avant d'ajouter l'image à l'aire de conception. Pour plus d’informations, consultez [Ajouter une image d’arrière-plan &#40;Générateur de rapports et SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Pour incorporer une image dans un rapport  
  
1.  En mode Création de rapport, sous l’onglet **Insérer**, cliquez sur **Image**.  
  
2.  Cliquez sur l'aire de conception, puis faites glisser la souris pour créer une zone de la taille voulue pour l'image.  
  
3.  Dans la page **Général** de la boîte de dialogue **Propriétés de l’image**, tapez un nom dans la zone de texte **Nom** ou acceptez le nom par défaut.  
  
4.  (Facultatif) Dans la zone de texte **Info-bulle**, tapez le texte qui doit s’afficher quand l’utilisateur pointe sur l’image dans le rapport rendu.  
  
5.  Dans **Sélectionner la source de l’image**, sélectionnez **Incorporé**.  
  
6.  Cliquez sur le bouton **Importer** en regard de la zone de texte **Utiliser cette image**.  
  
7.  Dans **Fichiers de type**, sélectionnez le type de fichier image, accédez au fichier, puis cliquez sur **Ouvrir**.  
  
8.  Dans la boîte de dialogue **Propriétés de l’image**, cliquez sur **OK**.  
  
     L'image s'affiche dans la zone que vous avez dessinée sur l'aire de conception, et le fichier s'affiche sous le dossier Images dans le volet des données de rapport.  
  
    > [!NOTE]  
    >  Le type MIME (par exemple, bmp) est dérivé automatiquement lorsque l'image est importée. Pour modifier le type MIME, consultez la procédure suivante.  
  
### (Facultatif) Pour modifier le type MIME d'une image importée  
  
1.  Ouvrez le rapport en mode Conception.  
  
2.  Sélectionnez l'image sur l'aire de conception. Le volet **Propriétés** affiche les propriétés de l’image.  
  
    > [!NOTE]  
    >  Si le volet Propriétés n’est pas visible, cliquez sur **Propriétés** sous l’onglet **Affichage**.  
  
3.  Cliquez dans la zone de texte en regard de la propriété **MIMEType** et sélectionnez un nouveau type MIME dans la liste déroulante.  
  
## Voir aussi  
 [Images &#40;Générateur de rapports et SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Ajouter une image liée à des données &#40;Générateur de rapports et SSRS&#41;](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md)   
 [Boîte de dialogue Propriétés de l’image, Général &#40;Générateur de rapports et SSRS&#41;](../Topic/Image%20Properties%20Dialog%20Box,%20General%20\(Report%20Builder%20and%20SSRS\).md)  
  
  