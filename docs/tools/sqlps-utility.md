---
title: "Utilitaire sqlps | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sqlps (utilitaire)"
  - "PowerShell [SQL Server], utilitaire sqlps"
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# Utilitaire sqlps
  L’utilitaire **sqlps** démarre une session Windows PowerShell avec le fournisseur PowerShell [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] et les applets de commande chargés et inscrits. Vous pouvez entrer des scripts ou des commandes PowerShell qui utilisent les composants [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell pour travailler avec des instances de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] et leurs objets.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] Utilisez plutôt le module **sqlps** PowerShell. Pour plus d’informations sur le module **sqlps** , consultez [Import the SQLPS Module](../relational-databases/scripting/import-the-sqlps-module.md).  
  
## Syntaxe  
  
```  
  
sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -args argument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## Arguments  
 **-NoLogo**  
 Spécifie que l’utilitaire **sqlps** doit masquer la bannière de copyright quand il démarre.  
  
 **-NoExit**  
 Spécifie que l’utilitaire **sqlps** doit poursuivre son exécution après le lancement des commandes de démarrage.  
  
 **-NoProfile**  
 Spécifie que l’utilitaire **sqlps** ne doit pas charger de profil utilisateur. Les profils utilisateur enregistrent des alias, fonctions et variables fréquemment utilisés en vue de leur utilisation au cours de différentes sessions PowerShell.  
  
 **-OutPutFormat** { **Text** | **XML** }  
 Spécifie que la sortie de l’utilitaire **sqlps** doit être mise en forme en tant que chaînes de texte (**Text**) ou format CLIXML sérialisé (**XML**).  
  
 **-InPutFormat** { **Text** | **XML** }  
 Spécifie que l’entrée de l’utilitaire **sqlps** est mise en forme en tant que chaînes de texte (**Text**) ou format CLIXML sérialisé (**XML**).  
  
 **-Command**  
 Spécifie la commande que l’utilitaire **sqlps** doit exécuter. L’utilitaire **sqlps** exécute la commande, puis se ferme, sauf si **-NoExit** est également spécifié. Ne spécifiez pas d’autres commutateurs après **-Command**, car ils seront lus comme des paramètres de commande.  
  
 **-**  
 **-Command-** spécifie que l’utilitaire **sqlps** doit lire l’entrée à partir de l’entrée standard.  
  
 *script_block* [ **-args***argument_array* ]  
 Spécifie un bloc de commandes PowerShell à exécuter ; le bloc doit être placé entre accolades : {}. *Script_block* peut uniquement être spécifié quand l’utilitaire **sqlps** est appelé depuis **PowerShell** ou une autre session de l’utilitaire **sqlps**. *argument_array* est un tableau de variables PowerShell contenant les arguments pour les commandes PowerShell de *script_block*.  
  
 *string* [ *command_parameters* ]  
 Spécifie une chaîne qui contient les commandes PowerShell à exécuter. Utilisez le format **"&{***command***}"**. Les guillemets indiquent une chaîne et l’opérateur d’appel (&) entraîne l’exécution de la commande par l’utilitaire **sqlps**.  
  
 [ **-?** | **-Help** ]  
 Affiche le résumé de la syntaxe des options de l’utilitaire **sqlps**.  
  
## Notes  
 L’utilitaire **sqlps** démarre l’environnement PowerShell (PowerShell.exe) et charge le module [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell. Le module, également nommé **sqlps**, charge et inscrit ces composants logiciels enfichables [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell :  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     Implémente le fournisseur PowerShell pour [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] et les applets de commande associées, comme **Encode-SqlName** et **Decode-SqlName**.  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     Implémente les applets de commande **Invoke-Sqlcmd** et **Invoke-PolicyEvaluation**.  
  
 Vous pouvez recourir à l’utilitaire **sqlps** pour effectuer les opérations suivantes :  
  
-   exécuter des commandes PowerShell de façon interactive ;  
  
-   exécuter des fichiers script PowerShell ;  
  
-   exécuter des applets de commande [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ;  
  
-   utiliser les chemins d'accès du fournisseur [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pour naviguer dans la hiérarchie des objets [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ;  
  
 Par défaut, l’utilitaire **sqlps** s’exécute avec le niveau de stratégie d’exécution de scripts défini sur **Restreint**. Cela empêche l'exécution de scripts PowerShell. Vous pouvez utiliser l’applet de commande **Set-ExecutionPolicy** pour activer l’exécution de scripts signés ou de tout type de script. Exécutez uniquement des scripts provenant de sources fiables et sécurisez tous les fichiers d'entrée et de sortie en utilisant les autorisations NTFS appropriées. Pour plus d'informations sur l'activation de scripts PowerShell, consultez [Exécution de scripts Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=103166).  
  
 La version de l’utilitaire **sqlps** dans [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] et [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] a été implémentée en tant que mini-shell Windows PowerShell 1.0. Les mini-shells comportent certaines restrictions, comme le fait de ne pas autoriser les utilisateurs à charger des composants logiciels enfichables autres que ceux chargés par le mini-shell. Ces restrictions ne s'appliquent pas à la version [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] et aux versions ultérieures de l'utilitaire, qui ont été modifiées pour utiliser le module **sqlps** .  
  
## Exemples  
 **A. Exécution de l’utilitaire sqlps en mode interactif par défaut, sans bannière de copyright**  
  
```  
sqlps -NoLogo  
```  
  
 **B. Exécution d'un script SQL Server PowerShell à partir de l'invite de commandes**  
  
```  
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
 **C. Exécution d'un script SQL Server PowerShell à partir de l'invite de commandes et poursuite de l'exécution une fois le script terminé**  
  
```  
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## Voir aussi  
 [Activer ou désactiver un protocole réseau de serveur](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)  
  
  