---
title: Élément de table pour le schéma (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Table element [DTA]
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b3a72f800643afa5e7edf6bdfa9928196f5da2d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781811"
---
# <a name="table-element-for-schema-dta"></a>Table, élément pour les schémas (Assistant Paramétrage de base de données)
  Spécifie la table pour le paramétrage.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
<Schema>  
...code removed here...  
    <Table>...</Table>  
```  
  
## <a name="element-attributes"></a>Attributs des éléments  
  
|Attribute|Description|  
|---------------|-----------------|  
|`NumberOfRows`|Facultatif. Entier qui vous permet de simuler des tables de différentes tailles.|  
  
## <a name="element-characteristics"></a>Caractéristiques de l'élément  
  
|Caractéristique|Description|  
|--------------------|-----------------|  
|**Type de données et longueur**|**string**, entre 1 et 255 caractères.|  
|**Valeur par défaut**|Aucun.|  
|**Occurrence**|Facultatif. Répertoriez autant de tables que nécessaire pour votre charge de travail.|  
  
## <a name="element-relationships"></a>Relations entre les éléments  
  
|Relation|Éléments|  
|------------------|--------------|  
|**Élément parent**|[Schema, élément pour les bases de données &#40;Assistant Paramétrage de base de données&#41;](schema-element-for-database-dta.md)|  
|**Éléments enfants**|[Name, élément pour les tables &#40;Assistant Paramétrage de base de données&#41;](name-element-for-table-dta.md)|  
  
## <a name="remarks"></a>Notes  
 Si vous ne spécifiez pas d'élément `Table`, l'Assistant Paramétrage du moteur de base de données suppose que toutes les tables sur la base de données spécifiée peuvent être paramétrées.  
  
## <a name="example"></a>Exemple  
 Pour obtenir un exemple d’utilisation, consultez [Server, élément &#40;Assistant Paramétrage de base de données&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Référence des fichiers d’entrée XML &#40;Assistant Paramétrage du moteur de base de données&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
