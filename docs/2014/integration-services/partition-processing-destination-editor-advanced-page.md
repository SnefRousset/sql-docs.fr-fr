---
title: Éditeur de Destination de traitement de partition (Page avancé) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.advanced.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 2039ee0f-069d-479d-90b2-2a12481b1162
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3eee8a69013975f7bfe9febcfa85d8143dcef68
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374895"
---
# <a name="partition-processing-destination-editor-advanced-page"></a>Éditeur de destination de traitement de partition (page Avancé)
  Utilisez la page **Avancé** de la boîte de dialogue **Éditeur de destination de traitement de partition** pour configurer la gestion des erreurs.  
  
 Pour en savoir plus sur la destination de traitement de partition, consultez [Partition Processing Destination](data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  Les tâches décrites ici ne s’appliquent pas aux modèles tabulaires Analysis Services.  Vous ne pouvez pas mapper des colonnes d’entrée aux colonnes de partition pour les modèles tabulaires. Vous pouvez en revanche utiliser la tâche DDL d'exécution [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) d'Analysis Services pour traiter la partition.  
  
## <a name="options"></a>Options  
 **Utiliser la configuration d'erreur par défaut**  
 Indiquez si vous voulez utiliser la gestion des erreurs par défaut d' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Par défaut, cette valeur est définie sur `True`.  
  
 **Action pour l'erreur de clé**  
 Indiquez comment traiter les enregistrements dont les valeurs de clé ne sont pas acceptables.  
  
|Value|Description|  
|-----------|-----------------|  
|**ConvertToUnknown**|Convertir la valeur de clé non acceptable en valeur inconnue (Unknown).|  
|**DiscardRecord**|Ignorer l'enregistrement.|  
  
 **Ignorer les erreurs**  
 Spécifiez que les erreurs doivent être ignorées.  
  
 **Arrêter en cas d'erreur**  
 Spécifiez que le traitement doit s'arrêter lorsqu'une erreur se produit.  
  
 **Nombre d'erreurs**  
 Spécifiez le nombre maximal d’erreurs au-delà duquel le traitement doit s’arrêter, si vous avez sélectionné **Arrêter en cas d’erreur**.  
  
 **Action pour l'erreur**  
 Indiquez l’action à appliquer lorsque le nombre maximal d’erreurs est atteint, si vous avez sélectionné **Arrêter en cas d’erreur**.  
  
|Value|Description|  
|-----------|-----------------|  
|**StopProcessing**|Arrêter le traitement.|  
|**StopLogging**|Arrêter d'enregistrer les erreurs.|  
  
 **Clé introuvable**  
 Indiquez l'action à appliquer en cas d'erreur de clé introuvable. Par défaut, cette valeur est définie sur **ReportAndContinue**.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignorer l'erreur et continuer le traitement.|  
|**ReportAndContinue**|Signaler l'erreur et continuer le traitement.|  
|**ReportAndStop**|Signaler l'erreur et arrêter le traitement.|  
  
 **Clé dupliquée**  
 Indiquez l'action à appliquer en cas d'erreur de clé dupliquée. Par défaut, cette valeur est définie sur **IgnoreError**.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignorer l'erreur et continuer le traitement.|  
|**ReportAndContinue**|Signaler l'erreur et continuer le traitement.|  
|**ReportAndStop**|Signaler l'erreur et arrêter le traitement.|  
  
 **Clé NULL convertie en clé inconnue**  
 Indiquez l'action à appliquer lorsqu'une clé NULL a été convertie en clé inconnue (Unknown). Par défaut, cette valeur est définie sur **IgnoreError**.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignorer l'erreur et continuer le traitement.|  
|**ReportAndContinue**|Signaler l'erreur et continuer le traitement.|  
|**ReportAndStop**|Signaler l'erreur et arrêter le traitement.|  
  
 **Clé NULL non autorisée**  
 Indiquez l'action à appliquer si une clé NULL est trouvée alors que les clés NULL ne sont pas autorisées. Par défaut, cette valeur est définie sur **ReportAndContinue**.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreError**|Ignorer l'erreur et continuer le traitement.|  
|**ReportAndContinue**|Signaler l'erreur et continuer le traitement.|  
|**ReportAndStop**|Signaler l'erreur et arrêter le traitement.|  
  
 **Chemin d'accès du journal des erreurs**  
 Tapez le chemin du journal des erreurs ou sélectionnez une destination à l’aide du bouton Parcourir **(...)** .  
  
 **Parcourir (...)**  
 Sélectionnez le chemin d'accès du journal des erreurs.  
  
## <a name="see-also"></a>Voir aussi  
 [Guide de référence des erreurs et des messages propres à Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Éditeur de destination de traitement de partition &#40;page Mappages&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)  
  
  
