---
title: 'Étape 1 : Copie du Package de la leçon 4 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3cf58665c69c744b35c8703f7f00fc07e0b8aafc
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386277"
---
# <a name="step-1-copying-the-lesson-4-package"></a>Étape 1 : Copie du Package de la leçon 4
  Dans cette tâche, vous créez une copie du package Lesson 4.dtsx que vous avez créé à la leçon 4. Vous pouvez également ajouter au projet le package final de la leçon 4 inclus avec le didacticiel, puis le copier. Vous allez utiliser cette nouvelle copie tout au long de la leçon 5.  
  
### <a name="to-copy-the-lesson-4-package"></a>Pour copier le package de la leçon 4  
  
1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools n’est pas déjà ouvert, dans le menu **Démarrer**, pointez sur **Tous les programmes**, puis sur **Microsoft SQL Server 2012**et cliquez sur **SQL Server Data Tools**.  
  
2.  Dans le menu **Fichier** , cliquez sur **Ouvrir**, cliquez sur **Projet/Solution**, sélectionnez **Didacticiel SSIS** , cliquez sur **Ouvrir**, puis double-cliquez sur **SSIS Tutorial.sln**.  
  
3.  Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Lesson 4.dtsx**et choisissez **Copier**.  
  
4.  Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Packages SSIS**et choisissez **Coller**.  
  
     Par défaut, le package copié est nommé Lesson 5.dtsx.  
  
5.  Dans l’Explorateur de solutions, double-cliquez sur **Lesson 5.dtsx** pour ouvrir le package.  
  
6.  Cliquez n’importe où dans l’arrière-plan de l’onglet **Flux de contrôle** , puis cliquez sur **Propriétés**.  
  
7.  Dans la fenêtre Propriétés, mettez à jour le `Name` propriété `Lesson 5`.  
  
8.  Cliquez sur la zone pour le **ID** propriété, puis cliquez sur la flèche déroulante, puis cliquez sur  **\<générer un nouvel ID >**.  
  
### <a name="to-add-the-completed-lesson-4-package"></a>Pour ajouter le package final de la leçon 4  
  
1.  Ouvrez [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools et ouvrez le projet Didacticiel SSIS.  
  
2.  Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Packages SSIS**, puis cliquez sur **Ajouter le package existant**.  
  
3.  Dans la boîte de dialogue **Ajouter une copie des packages existants** , dans **Emplacement du package**, sélectionnez **Système de fichiers**.  
  
4.  Cliquez sur le bouton de navigation **(...)**, accédez à **Lesson 4.dtsx** sur votre ordinateur, puis cliquez sur **Ouvrir**.  
  
     Pour télécharger tous les packages de leçons de ce didacticiel, procédez comme suit.  
  
    1.  Accédez à [Exemples de produits Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Cliquez sur l'onglet **DOWNLOADS** (Téléchargements).  
  
    3.  Cliquez sur le fichier SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copiez et collez le package de la leçon 4 comme décrit dans les étapes 3 à 8 de la procédure précédente.  
  
## <a name="next-task-in-lesson"></a>Tâche suivante de la leçon  
 [Étape 2 : Activation et configuration des Configurations de Package](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
  
