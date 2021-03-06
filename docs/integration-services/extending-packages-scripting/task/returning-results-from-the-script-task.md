---
title: Retour de résultats de la tâche de script | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5db80c310c7810123d5702b729a227ebe891527
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290835"
---
# <a name="returning-results-from-the-script-task"></a>Retour de résultats de la tâche de script
  La tâche de script utilise la propriété <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> et la propriété facultative <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> pour renvoyer des informations d'état à l'exécution [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], lesquelles peuvent être utilisées pour déterminer le chemin d'accès du flux de travail une fois que la tâche de script est terminée.  
  
## <a name="taskresult"></a>TaskResult  
 La propriété <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> indique si la tâche a réussi ou a échoué. Exemple :  
  
 `Dts.TaskResult = ScriptResults.Success`  
  
## <a name="executionvalue"></a>ExecutionValue  
 La propriété <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> renvoie facultativement un objet défini par l'utilisateur qui quantifie ou fournit des informations supplémentaires sur le succès ou l'échec de la tâche de script. Par exemple, la tâche FTP utilise la propriété <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> pour renvoyer le nombre de fichiers transférés. La tâche d'exécution SQL renvoie le nombre de lignes affectées par la tâche. La propriété <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> peut également servir à déterminer le chemin d'accès du flux de travail. Exemple :  
  
 `Dim rowsAffected as Integer`  
  
 `...`  
  
 `rowsAffected = 1000`  
  
 `Dts.ExecutionValue = rowsAffected`  
