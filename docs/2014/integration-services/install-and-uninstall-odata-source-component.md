---
title: Installer et désinstaller le composant Source OData | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 34a71ed768c49436a4dba4ecf225bdd009132866
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385257"
---
# <a name="install-and-uninstall-odata-source-component"></a>Installer et désinstaller le composant source OData
  Cette rubrique fournit des instructions pour installer ou supprimer le composant source OData sur votre ordinateur.  
  
## <a name="installation"></a>Installation  
 Le composant source OData requiert les composants suivants et sera installé sur votre ordinateur.  
  
-   SQL Server Data Tools (pour concevoir des packages)  
  
-   SQL Server Integration Services (pour exécuter des packages hors de Visual Studio)  
  
 Pour installer le composant source OData, téléchargez [SQL Server 2014 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkId=391999) et exécutez l'un des fichiers MSI suivants.  
  
-   ODataSourceForSQLServer2014-amd64.msi pour les plateformes 64 bits  
  
-   ODataSourceForSQLServer2014-x86.msi pour les plateformes 32 bits  
  
> [!IMPORTANT]  
>  Le programme d'installation 64 bits installera les versions 32 bits et 64 bits du composant source OData. Exécutez uniquement le programme d'installation 32 bits si vous utilisez un système d'exploitation 32 bits.  
  
## <a name="uninstallation"></a>Désinstallation  
 Le composant source OData peut être désinstallé à partir du menu **Programmes et fonctionnalités** . Recherchez l'entrée **Composant source OData Microsoft SQL Server SSIS (x64)** et cliquez sur **Désinstaller**.  
  
  
