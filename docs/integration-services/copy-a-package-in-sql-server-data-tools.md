---
title: Copier un package dans SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6f267a838322b9e0380828ca926149426f0ce16e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289535"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>Copier un package dans les outils de données SQL Server
  Cette rubrique explique comment créer un package [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en copiant un package existant, et comment mettre à jour les propriétés **Name** et **GUID** du nouveau package.  
  
### <a name="to-copy-a-package"></a>Pour copier un package  
  
1.  Dans [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], ouvrez le projet [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] qui contient le package que vous voulez copier.  
  
2.  Dans l'Explorateur de solutions, double-cliquez sur le package.  
  
3.  Vérifiez soit que le package à copier est sélectionné dans l'Explorateur de solutions, soit que l'onglet du concepteur SSIS qui contient le package est l'onglet actif.  
  
4.  Dans le menu **Fichier**, cliquez sur **Enregistrer \<nom_package> sous**.  
  
    > [!NOTE]  
    >  Le package doit être ouvert dans le concepteur SSIS pour que l’option **Enregistrer sous** apparaisse dans le menu **Fichier** .  
  
5.  Le cas échéant, accédez à un autre dossier.  
  
6.  Mettez à jour le nom du fichier de package. Veillez à conserver l'extension de fichier .dtsx.  
  
7.  Cliquez sur **Enregistrer**.  
  
8.  À l'invite, déterminez si vous voulez mettre à jour le nom de l'objet de package afin qu'il corresponde au nom de fichier. Si vous cliquez sur **Oui**, la propriété **Name** du package est mise à jour. Le nouveau package est ajouté au projet [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] et ouvert dans le concepteur [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
9. Le cas échéant, cliquez sur l’arrière-plan de l’onglet **Flux de contrôle** , puis cliquez sur **Propriétés**.  
  
10. Dans la fenêtre Propriétés, cliquez sur la valeur de la propriété ID, puis cliquez sur **\<Générer un nouvel ID>** dans la liste déroulante.  
  
11. Dans le menu **Fichier** , cliquez sur **Enregistrer les éléments sélectionnés** pour enregistrer le nouveau package.  
  
## <a name="see-also"></a> Voir aussi  
 [Enregistrer une copie d'un package](https://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [Créer des packages dans les outils de données SQL Server](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Packages Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-packages.md)  
  
  
