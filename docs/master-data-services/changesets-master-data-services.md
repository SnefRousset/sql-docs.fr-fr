---
title: "Ensembles de modifications (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f227c49a-ed46-4e0f-8992-83093456cf94
caps.latest.revision: 13
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 13
---
# Ensembles de modifications (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] prend désormais en charge la possibilité d’enregistrer les modifications en attente dans une entité comme ensembles de modifications. Cette fonctionnalité peut être utilisée dans deux scénarios.  
  
-   **Modifications quand « Approbation requise » est activé par l’administrateur d’entité**  
  
     Si un administrateur d’entité indique que les modifications apportées à une entité donnée doivent être approuvées avant leur validation, les modifications apportées à l’entité doivent être enregistrées dans un ensemble de modifications nouveau ou existant avant d’être soumises pour approbation.  Pour plus d’informations, consultez [Approbation requise &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md).  
  
     Vous devez suivre ce flux de travail.  
  
    1.  Vous créez un ensemble de modifications. L’ensemble de modifications est dans l’état Ouvert. Consultez [Créer un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md).  
  
    2.  Vous appliquez l’ensemble de modifications et ajoutez des modifications à l’ensemble de modifications. Consultez [Appliquer et mettre à jour un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md).  
  
    3.  Vous soumettez l’ensemble de modifications à l’administrateur d’entité pour approbation. L’ensemble de modifications est dans l’état En attente. Consultez [Valider ou envoyer un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md).  
  
    4.  L’administrateur d’entité reçoit une notification par e-mail l’informant qu’un ensemble de modifications est en attente d’approbation. Si l’administrateur d’entité approuve l’ensemble de modifications, celui-ci est dans l’état Approuvé. Consultez [Approuver ou rejeter un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
    5.  L’ensemble de modifications approuvé est validé automatiquement. Si la modification est validée avec succès, l’ensemble de modifications est dans l’état Validé.  
  
-   **Modifications utilisateur locales**  
  
     Si vous souhaitez simplement enregistrer vos modifications locales afin de pouvoir les utiliser ou les récupérer plus tard, vous pouvez pour cela utiliser des ensembles de modifications.  
  
     Vous devez suivre ce flux de travail.  
  
    1.  Vous créez un ensemble de modifications. L’ensemble de modifications est dans l’état Ouvert. Consultez [Créer un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md).  
  
    2.  Vous appliquez l’ensemble de modifications et ajoutez des modifications à l’ensemble de modifications. Consultez [Appliquer et mettre à jour un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md).  
  
    3.  Lorsque vous êtes prêt, vous validez l’ensemble de modifications. Consultez [Valider ou envoyer un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md).  
  
## Voir aussi  
 [Créer un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Appliquer et mettre à jour un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Valider ou envoyer un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [Approuver ou rejeter un ensemble de modifications &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)   
 [Gérer les ensembles de modifications &#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md)  
  
  