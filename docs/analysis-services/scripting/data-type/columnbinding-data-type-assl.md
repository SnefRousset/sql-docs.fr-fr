---
title: "Type de données ColumnBinding (ASSL) | Documents Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ColumnBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ColumnBinding
helpviewer_keywords:
- ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e93d9587957409df5678eac7f0d31df71d201532
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="columnbinding-data-type-assl"></a>Type de données ColumnBinding (ASSL)
  Définit un type de données dérivé qui représente la liaison d’une colonne dans une vue de source de données à un [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) élément.  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>Caractéristiques du type de données  
  
|Caractéristique|Description|  
|--------------------|-----------------|  
|Types de données de base|[Liaison](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Types de données dérivés|Aucune|  
  
## <a name="data-type-relationships"></a>Relations du type de données  
  
|Relation|Élément|  
|------------------|-------------|  
|Éléments parents|Aucune|  
|Éléments enfants|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md), [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|Éléments dérivés|Consultez [de liaison](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Notes  
 Pour créer des noms d’élément XML valides, [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] **DataSet** objets encoder les noms de table pendant la sérialisation vers XML XSD (Schema Definition) ; par exemple, le nom « Order Details » devient « Order_x0020_Details ». De même, la **ColumnID** et **TableID** éléments contenus par le **ColumnBinding** élément et les objets de référence dans la vue de source de données (DSV) doivent aussi encoder les noms pendant la sérialisation, pour vous assurer que les noms correspondent directement le texte dans la vue DSV. L’instance Analysis Services décodera ces noms, tout comme le **DataSet** fait le modèle objet.  
  
 A **TableDefinitions** élément contenu dans un élément à l’aide de la **TableBinding** type de données et qui fait référence aux tables dans la vue DSV doivent aussi encoder les noms lors de leur sérialisation en XSD. Toutefois, les noms de la table dans le **Partition** liaisons ne doivent pas être codés, car ces noms sont simplement des noms de tables qui existent dans la base de données et n’ont pas à être dans la vue DSV. Codage ne pas de la table de noms dans le **Partition** liaisons ailleurs les conséquences suivantes :  
  
-   Ceci permet de simplifier la bibliothèque de définition de données (DDL) des partitions.  
  
-   Il en résulte une cohérence accrue dans la mesure où les partitions peuvent avoir soit un nom de table, soit une instruction SELECT, et l'instruction SELECT ne doit pas être encodée.  
  
 Les noms de table et de colonne n'incluent pas de séparateurs (par exemple « [ » pour [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
 Pour plus d’informations sur la **liaison** type, y compris les tableaux des objets Analysis Services Scripting Language (ASSL) de la **liaison** type et la hiérarchie d’héritage de **liaison** types, consultez [Type de liaison de données &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Pour une vue d’ensemble des liaisons de données dans ASSL, consultez [des Sources de données et liaisons &#40; SSAS multidimensionnel &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 L'élément correspondant dans le modèle objet AMO est <xref:Microsoft.AnalysisServices.ColumnBinding>.  
  
## <a name="see-also"></a>Voir aussi  
 [Analysis Services script des Types de données XML Language &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  