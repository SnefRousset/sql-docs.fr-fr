---
title: Importer le module SQLPS | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b6fdc0b8267f1e995812d573ae80f0f24ee11843
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52404115"
---
# <a name="import-the-sqlps-module"></a>Importer le module SQLPS
  La méthode recommandée pour gérer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à partir de PowerShell consiste à importer le module `sqlps` dans un environnement Windows PowerShell 2.0. Le module charge et inscrit les assemblys de facilité de gestion et les composants logiciels enfichables [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
1.  **Avant de commencer :**  [Sécurité](#Security)  
  
2.  **Pour charger le module :**  [Charger le Module sqlps](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Avant de commencer  
 Après avoir importé le module `sqlps` dans Windows PowerShell, vous pouvez :  
  
-   exécuter des commandes Windows PowerShell de façon interactive ;  
  
-   exécuter des fichiers de script Windows PowerShell ;  
  
-   exécuter des applets de commande [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ;  
  
-   utiliser les chemins d'accès du fournisseur [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pour naviguer dans la hiérarchie des objets [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ;  
  
-   utiliser les modèles objets de la facilité de gestion [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (tels que Microsoft.SqlServer.Management.Smo) pour gérer des objets [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Les verbes utilisés dans les noms de deux applets de commande SQL Server (`Encode-Sqlname` et `Decode-Sqlname`) ne correspondent pas aux verbes approuvés pour Windows PowerShell 2.0. Cela n'a aucun effet sur leur opération, mais Windows PowerShell déclenche un avertissement lorsque le module `sqlps` est importé dans une session.  
  
###  <a name="Security"></a> Sécurité  
 Par défaut, Windows PowerShell s’exécute avec le niveau **Restreint**de la stratégie d’exécution de scripts, ce qui empêche l’exécution de tout script Windows PowerShell. Pour charger le module `sqlps`, vous pouvez utiliser l'applet de commande `Set-ExecutionPolicy` pour activer l'exécution de scripts signés uniquement ou de tous les scripts. Exécutez uniquement des scripts provenant de sources fiables et sécurisez tous les fichiers d'entrée et de sortie en utilisant les autorisations NTFS appropriées. Pour plus d'informations sur l'activation de scripts Windows PowerShell, consultez [Exécution de scripts Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/starting-windows-powershell?view=powershell-6#how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows).  
  
##  <a name="LoadSqlps"></a> Charger le module sqlps  
 **Pour charger le module sqlps dans Windows PowerShell**  
  
1.  Utilisez l'applet de commande `Set-ExecutionPolicy` pour définir la stratégie d'exécution de scripts appropriée.  
  
2.  Utilisez l'applet de commande `Import-Module` pour importer le module sqlps. Spécifiez le paramètre `DisableNameChecking` si vous souhaitez supprimer l'avertissement sur `Encode-Sqlname` et `Decode-Sqlname`.  
  
### <a name="example-powershell"></a>Exemple (PowerShell)  
 Cet exemple charge le module `sqlps` avec la fonction de vérification des noms désactivée.  
  
```  
## Import the SQL Server Module.  
  
Import-Module "sqlps" -DisableNameChecking  
  
```  
  

  
## <a name="see-also"></a>Voir aussi  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [fournisseur PowerShell SQL Server](../powershell/sql-server-powershell-provider.md)   
 [Utiliser les applets de commande du moteur de base de données](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
