---
title: Se connecter à un référentiel MDS (Complément MDS pour Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 28afdb4a07177f9ba34b946c4c9c4e1e12e672c0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52797931"
---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>Se connecter à un référentiel MDS (Complément MDS pour Excel)
  Dans le [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], vous devez vous connecter à un référentiel MDS avant de pouvoir charger ou publier des données.  
  
## <a name="prerequisites"></a>Prérequis  
 Pour effectuer cette procédure :  
  
-   Vous devez avoir l'autorisation d'accéder à la zone fonctionnelle **Explorateur** .  
  
### <a name="to-connect-to-an-mds-repository"></a>Pour vous connecter à un référentiel MDS  
  
1.  Dans le Complément MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], sous l’onglet **Données de référence** , dans le groupe **Se connecter et charger** , cliquez sur la flèche du bas sous le bouton **Se connecter** et cliquez sur **Gérer les connexions**.  
  
2.  Dans la boîte de dialogue **Gérer les connexions** , dans la section **Nouvelle connexion** , cliquez sur **Créer une connexion**.  
  
3.  Cliquez sur **Nouveau**.  
  
4.  Dans la boîte de dialogue **Ajouter une nouvelle connexion** , dans le champ **Description** , tapez une description pour votre connexion. Cette connexion s’affiche lorsque vous cliquez sur la flèche sous le bouton **Se connecter** dans la barre d’outils.  
  
5.  Dans la zone **Adresse du serveur MDS**, tapez l’URL de l’application web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], par exemple http://contoso/mds.  
  
    > [!NOTE]  
    >  Vérifiez que vous utilisez le nom d’ordinateur ; n’utilisez pas « localhost ».  
  
6.  Cliquez sur **OK**. Le nom est affiché dans la section **Connexions existantes** .  
  
7.  Vous pouvez également cliquer sur **Tester** pour tester la connexion. Une boîte de dialogue de confirmation ou d'erreur s'affiche. Cliquez sur **OK** pour la fermer.  
  
8.  Cliquer sur **Se connecter**. Le volet **Master Data Services** est affiché.  
  
## <a name="next-steps"></a>Étapes suivantes  
  
-   [Charger des données MDS dans Excel](export-data-to-excel-from-master-data-services.md)  
  
-   [Filtrer les données avant le chargement &#40;complément MDS pour Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Connexions &#40;Complément MDS pour Excel#41;](connections-mds-add-in-for-excel.md)  
  
  
