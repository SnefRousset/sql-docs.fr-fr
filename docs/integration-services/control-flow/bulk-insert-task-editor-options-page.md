---
title: "&#201;diteur de t&#226;che d&#39;insertion en bloc (page Options) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.bulkinserttask.options.f1"
helpviewer_keywords: 
  - "Éditeur de tâche d'insertion en bloc"
ms.assetid: b3702811-3eb8-4b28-9190-5ae7a1a7bb6f
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# &#201;diteur de t&#226;che d&#39;insertion en bloc (page Options)
  Utilisez la page **Options** de la boîte de dialogue **Éditeur de tâche d'insertion en bloc** afin de définir les propriétés de l'opération d'insertion en bloc. La tâche d'insertion en bloc copie des volumes importants de données dans une table ou une vue [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Pour en savoir plus sur l’utilisation des insertions en bloc, consultez [Tâche d’insertion en bloc](../../integration-services/control-flow/bulk-insert-task.md) et [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## Options  
 **CodePage**  
 Permet d'indiquer la page de codes des données dans le fichier de données.  
  
 **DataFileType**  
 Permet d'indiquer la valeur correspondant au type de données à utiliser lors d'une opération de chargement.  
  
 **BatchSize**  
 Permet d'indiquer le nombre de lignes contenues dans un traitement. La valeur par défaut correspond à la totalité du fichier de données. Si vous attribuez à **BatchSize** la valeur zéro, les données sont chargées dans un traitement unique.  
  
 **LastRow**  
 Permet de spécifier la dernière ligne à copier.  
  
 **FirstRow**  
 Permet de spécifier la première ligne à partir de laquelle la copie doit commencer.  
  
 **Options**  
 |Terme|Définition|  
|----------|----------------|  
|**Contraintes de validation**|Permet de vérifier les contraintes s'appliquant à la table et aux colonnes.|  
|**Conserver les valeurs NULL**|Permet de conserver les valeurs Null pendant l'opération d'insertion en bloc au lieu d'insérer des valeurs par défaut dans les colonnes vides.|  
|**Activer l'insertion d'identité**|Permet d'insérer des valeurs existantes dans une colonne d'identité.|  
|**Verrou de table**|Permet de verrouiller la table lors de l'opération d'insertion en bloc.|  
|**Exécuter les déclencheurs**|Lance tout déclencheur d'insertion, de mise à jour ou de suppression sur la table.|  
  
 **SortedData**  
 Implique l'ajout de la clause ORDER BY dans l'instruction d'insertion en bloc. Le nom de colonne que vous fournissez doit être celui d'une colonne valide pour la table de destination. La valeur par défaut est **false**. En d'autres termes, les données ne sont pas triées par une clause ORDER BY.  
  
 **MaxErrors**  
 Permet de spécifier le nombre maximal d'erreurs tolérées avant l'annulation de l'opération d'insertion en bloc. La valeur 0 indique qu'un nombre illimité d'erreurs est autorisé.  
  
> [!NOTE]  
>  Chaque ligne ne pouvant pas être importée par l'opération de chargement en masse est comptée comme une erreur.  
  
## Voir aussi  
 [Guide de référence des erreurs et des messages propres à Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Éditeur de tâche d’insertion en bloc &#40;page Général&#41;](../../integration-services/control-flow/bulk-insert-task-editor-general-page.md)   
 [Éditeur de tâche d’insertion en bloc &#40;page Connexion&#41;](../../integration-services/control-flow/bulk-insert-task-editor-connection-page.md)   
 [Page Expressions](../../integration-services/expressions/expressions-page.md)   
 [Flux de contrôle](../../integration-services/control-flow/control-flow.md)  
  
  