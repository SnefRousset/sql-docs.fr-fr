---
title: Éditeur de tâche de système de fichiers (Page Général) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System Task Editor
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5b010d4c532db61d65fb312cdf9b02a1684332c3
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377277"
---
# <a name="file-system-task-editor-general-page"></a>Éditeur de tâche de système de fichiers (page Général)
  Utilisez la page **Général** de l' **Éditeur de tâche de système de fichiers** pour configurer l'opération de système de fichiers qu'exécute la tâche.  
  
 Pour en savoir plus sur cette tâche, consultez [File System Task](control-flow/file-system-task.md).  
  
 Vous devez spécifier un gestionnaire de connexions source et de destination en définissant les propriétés SourceConnection et DestinationConnection. Vous pouvez fournir les noms de gestionnaires de connexions de fichiers qui pointent sur les fichiers utilisés par la tâche comme source ou destination. Si les chemins de fichiers sont stockés dans des variables, vous pouvez également fournir le nom des variables. Pour utiliser des variables afin de stocker les chemins des fichiers, vous devez d’abord définir l’option IsSourcePathVariable de la connexion source et l’option IsDestinationPatheVariable de la connexion de destination sur **True**. Ensuite, vous pouvez créer de nouvelles variables ou choisir les variables existantes, système ou définies par l'utilisateur, à utiliser. Dans la boîte de dialogue **Ajouter une variable** , vous pouvez configurer et spécifier l'étendue des variables. L'étendue doit être la tâche de système de fichiers ou un conteneur parent. Pour plus d’informations, consultez [Variables Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) et [Utiliser des variables dans des packages](../../2014/integration-services/use-variables-in-packages.md).  
  
> [!NOTE]  
>  Pour remplacer les variables que vous avez sélectionné pour le `SourceConnection` et `DestinationConnection` propriétés, entrez une expression pour la **Source** et **Destination** propriétés. Vous entrez les expressions sur la page **Expressions** de l' **Éditeur de tâche de système de fichiers**. Par exemple, pour définir le chemin d'accès des fichiers utilisés comme destination par la tâche, vous pouvez utiliser la variable A dans certaines conditions et la variables B dans d'autres conditions.  
  
> [!NOTE]  
>  La tâche de système de fichiers s'exécute sur un seul fichier ou répertoire. Cette tâche ne prend donc pas en charge l'utilisation de caractères génériques pour effectuer la même opération sur plusieurs fichiers ou répertoires. Pour que la tâche de système de fichiers répète une même opération sur plusieurs fichiers ou répertoires, placez-la dans un conteneur de boucles Foreach. Pour plus d’informations, consultez [File System Task](control-flow/file-system-task.md).  
  
 Vous pouvez utiliser des expressions pour recourir à différentes variables.  
  
## <a name="options"></a>Options  
 **IsDestinationPathVariable**  
 Indique si le chemin d'accès de destination est stocké dans une variable. Cette propriété dispose des options répertoriées dans le tableau suivant.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|Le chemin d'accès de destination est stocké dans une variable. Cette valeur affiche l'option dynamique **DestinationVariable**.|  
|**False**|Le chemin d'accès de destination est défini dans un gestionnaire de connexions de fichiers. Cette valeur affiche l’option dynamique `DestinationConnection`.|  
  
 **OverwriteDestination**  
 Indiquez si l'opération peut remplacer les fichiers dans le répertoire de destination.  
  
 **Nom**  
 Fournissez un nom unique pour la tâche de système de fichiers. Ce nom sert d'étiquette à l'icône de la tâche.  
  
> [!NOTE]  
>  Les noms de tâche doivent être uniques dans un package.  
  
 **Description**  
 Tapez la description de la tâche de système de fichiers.  
  
 **Opération**  
 Sélectionnez l'opération de système de fichiers à exécuter. Cette propriété dispose des options répertoriées dans le tableau suivant.  
  
|Value|Description|  
|-----------|-----------------|  
|**Copier le répertoire**|Copier un répertoire. Cette valeur affiche les options dynamiques d'une source et d'une destination.|  
|**Copier le fichier**|Copier un fichier. Cette valeur affiche les options dynamiques d'une source et d'une destination.|  
|**Créer un répertoire**|Créer un répertoire. Cette valeur affiche les options dynamiques d'un répertoire source et de destination.|  
|**Supprimer le répertoire**|Supprimer un répertoire. Cette valeur affiche les options dynamiques d'une source.|  
|**Supprimer le contenu du répertoire**|Supprimer le contenu d'un répertoire. Cette valeur affiche les options dynamiques d'une source.|  
|**Supprimer le fichier**|Supprimer un fichier. Cette valeur affiche les options dynamiques d'une source.|  
|**Déplacer le répertoire**|Déplacer un répertoire. Cette valeur affiche les options dynamiques d'une source et d'une destination.|  
|**Déplacer le fichier**|Déplacer un fichier. Cette valeur affiche les options dynamiques d'une source et d'une destination.<br /><br /> Remarque : Lorsque vous déplacez un fichier, n'incluez pas de nom de fichier dans le chemin d'accès au répertoire que vous fournissez comme destination.|  
|**Renommer le fichier**|Renommer un fichier. Cette valeur affiche les options dynamiques d'une source et d'une destination.<br /><br /> Remarque : Lorsque vous renommez un fichier, incluez le nouveau nom de fichier dans le chemin d'accès au répertoire que vous fournissez comme destination.|  
|**Définir les attributs**|Définir les attributs d'un fichier ou d'un répertoire. Cette valeur affiche les options dynamiques d'une source et d'une opération.|  
  
 `IsSourcePathVariable`  
 Indique si le chemin d'accès de destination est stocké dans une variable. Cette propriété dispose des options répertoriées dans le tableau suivant.  
  
|Value||  
|-----------|-|  
|**True**|Le chemin d'accès de destination est stocké dans une variable. Sélectionnez cette valeur pour afficher l'option dynamique **SourceVariable**.|  
|**False**|Le chemin d'accès de destination est défini dans un gestionnaire de connexions de fichiers. Cette valeur affiche l'option dynamique **DestinationVariable**.|  
  
## <a name="isdestinationpathvariable-dynamic-options"></a>Options dynamiques IsDestinationPathVariable  
  
### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 Sélectionnez le nom de la variable dans la liste ou cliquez sur \<**Nouvelle variable...**> pour en créer une.  
  
 **Rubriques connexes :** [Integration Services &#40;SSIS&#41; Variables](integration-services-ssis-variables.md), [ajouter une Variable](../../2014/integration-services/add-variable.md)  
  
### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 `DestinationConnection`  
 Sélectionnez un gestionnaire de connexions de fichiers dans la liste ou cliquez sur \<**Nouvelle connexion...**> pour en créer un.  
  
 **Rubriques connexes :** [Gestionnaire de connexions file](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="issourcepathvariable-dynamic-options"></a>Options dynamiques IsSourcePathVariable  
  
### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 Sélectionnez le nom de la variable dans la liste ou cliquez sur \<**Nouvelle variable...**> pour en créer une.  
  
 **Rubriques connexes :** [Integration Services &#40;SSIS&#41; Variables](integration-services-ssis-variables.md), [ajouter une Variable](../../2014/integration-services/add-variable.md)  
  
### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 `SourceConnection`  
 Sélectionnez un gestionnaire de connexions de fichiers dans la liste ou cliquez sur \<**Nouvelle connexion...**> pour en créer un.  
  
 **Rubriques connexes :** [Gestionnaire de connexions file](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="operation-dynamic-options"></a>Options dynamiques d'opération  
  
### <a name="operation--set-attributes"></a>Opération = Définir les attributs  
 **Hidden**  
 Indique si le fichier ou le répertoire est visible.  
  
 **En lecture seule**  
 Indique si le fichier est en lecture seule.  
  
 **Archive**  
 Indique si le fichier ou le répertoire est prêt pour l'archivage.  
  
 **Système**  
 Indique si le fichier est un fichier de système d'exploitation.  
  
### <a name="operation--create-directory"></a>Opération = Créer un répertoire  
 `UseDirectoryIfExists`  
 Indique si l’option **Créer un répertoire** utilise un répertoire existant portant le nom spécifié au lieu de créer un nouveau répertoire.  
  
## <a name="see-also"></a>Voir aussi  
 [Guide de référence des erreurs et des messages propres à Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Page Expressions](expressions/expressions-page.md)  
  
  
