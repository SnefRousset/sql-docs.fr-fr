---
title: "&#201;diteur de t&#226;che de profilage de donn&#233;es (page G&#233;n&#233;ral) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataprofilingtask.general.f1"
helpviewer_keywords: 
  - "Éditeur de tâche de profilage de données"
ms.assetid: eec15906-d757-4079-b2f6-aca4e52b3b4c
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# &#201;diteur de t&#226;che de profilage de donn&#233;es (page G&#233;n&#233;ral)
  Utilisez la page **Général** de l' **Éditeur de tâche de profilage de données** pour configurer les options suivantes :  
  
-   Spécifiez la destination de la sortie du profil.  
  
-   Utilisez les paramètres par défaut pour simplifier la tâche de profilage d'une table ou vue unique.  
  
 Pour plus d’informations sur l’utilisation de la tâche de profilage des données, consultez [Configuration de la tâche de profilage des données](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Pour plus d’informations sur l’utilisation de la visionneuse du profil des données pour analyser le résultat de la tâche de profilage des données, consultez [Visionneuse du profil des données](../../integration-services/control-flow/data-profile-viewer.md).  
  
 **Pour ouvrir la page Général de l'Éditeur de tâche de profilage de données**  
  
1.  Dans [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], ouvrez le package [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] doté de la tâche de profilage de données.  
  
2.  Sous l’onglet **Flux de contrôle**, double-cliquez sur la tâche de profilage des données.  
  
3.  Dans l' **Éditeur de tâche de profilage de données**, cliquez sur **Général**.  
  
## Options de profilage des données  
 **Délai d'expiration**  
 Spécifiez le nombre de secondes après lesquelles la tâche de profilage des données doit expirer et ne plus s'exécuter. La valeur par défaut est 0, ce qui indique l'absence de délai d'expiration.  
  
## Options de destination  
  
> [!IMPORTANT]  
>  Le fichier de sortie peut contenir des données sensibles qui concernent votre base de données et les données qu'elle contient. Pour obtenir des suggestions sur la manière de sécuriser davantage ce fichier, consultez [Accéder aux fichiers utilisés par des packages](../../integration-services/security/access-to-files-used-by-packages.md).  
  
 **DestinationType**  
 Spécifiez si la sortie du profil des données doit être enregistrée dans un fichier ou une variable :  
  
|Valeur|Description|  
|-----------|-----------------|  
|**FileConnection**|Enregistrez la sortie du profil dans un fichier à l'emplacement spécifié dans un gestionnaire de connexions de fichiers.<br /><br /> Remarque : vous devez spécifier le gestionnaire de connexions de fichiers à utiliser dans l’option **Destination** .|  
|**Variable**|Enregistrez la sortie du profil dans une variable de package.<br /><br /> Remarque : vous devez spécifier la variable de package à utiliser dans l’option **Destination** .|  
  
 **Destination**  
 Spécifiez le gestionnaire de connexions de fichiers ou la variable de package qui contient la sortie du profil des données :  
  
-   Si l'option **DestinationType** est définie sur **FileConnection**, l'option **Destination** affiche les gestionnaires de connexions de fichiers disponibles. Choisissez l’un de ces gestionnaires de connexions ou sélectionnez l’option \<Nouvelle connexion de fichier> pour créer un nouveau gestionnaire de connexions de fichiers.  
  
-   Si l'option **DestinationType** est définie sur **Variable**, l'option **Destination** affiche les variables de package disponibles dans la liste **Destination** . Choisissez l’une de ces variables ou sélectionnez l’option \<Nouvelle variable> pour créer une variable.  
  
 **OverwriteDestination**  
 Spécifiez si le fichier de sortie est à remplacer s'il existe déjà. La valeur par défaut est **False**. La valeur de cette propriété est utilisée uniquement lorsque l'option DestinationType est définie sur FileConnection. Lorsque l'option DestinationType est définie sur Variable, la tâche remplace toujours la valeur précédente de la variable.  
  
> [!IMPORTANT]  
>  Si vous tentez d’exécuter la tâche de profilage des données plus d’une fois sans modifier le nom du fichier de sortie ou redéfinir la valeur de la propriété **OverwriteDestination** sur **True**, la tâche échoue et affiche un message indiquant que le fichier de sortie existe déjà.  
  
## Autres options  
 **Profil rapide**  
 Affichez le **Formulaire de profil rapide de table simple**. Ce formulaire simplifie la tâche de profilage d'une table ou d'une vue unique à l'aide des paramètres par défaut. Pour plus d’informations, consultez [Formulaire de profil rapide de table simple &#40;tâche de profilage des données&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md).  
  
 **Ouvrir la visionneuse de profil**  
 Ouvre la visionneuse du profil des données. La visionneuse de profil des données autonome affiche la sortie du profil des données de la tâche de profilage des données. Pour afficher la sortie du profil des données, vous devez avoir exécuté la tâche de profilage des données dans le package [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] et avoir calculé les profils des données.  
  
> [!NOTE]  
>  Pour ouvrir la Visionneuse du profil des données, vous pouvez aussi exécuter DataProfileViewer.exe dans le dossier, *\<lecteur>*:\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn.  
  
## Voir aussi  
 [Formulaire de profil rapide de table simple &#40;tâche de profilage des données&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)   
 [Éditeur de tâche de profilage de données &#40;page Demandes de profil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  