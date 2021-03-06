---
title: Supprimer des index XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- dropping indexes
- XML indexes [SQL Server], dropping
ms.assetid: 7591ebea-34af-4925-8553-b2adb5b487c2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 82fd8836bb4fda85a7fdadd6345826cf432485cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194149"
---
# <a name="drop-xml-indexes"></a>Supprimer des index XML
  L’instruction [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] permet de supprimer des index XML et non XML, qu’ils soient primaires ou secondaires. Les options DROP INDEX ne s'appliquent cependant pas aux index XML. Si vous supprimez l'index XML primaire, tous les index secondaires présents sont alors également supprimés.  
  
 La syntaxe DROP avec *TableName.IndexName* est cependant en cours de retrait des fonctionnalités et n’est pas prise en charge pour les index XML.  
  
## <a name="example-creating-and-dropping-a-primary-xml-index"></a>Exemple : création puis suppression d'un index XML primaire  
 Dans l’exemple suivant, un index XML est créé sur un `xml` colonne de type.  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create Primary XML index   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Verify the index creation.   
-- Note index type is 3 for xml indexes.  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'   
-- Drop the index.  
DROP INDEX PIdx_T_XmlCol ON T  
```  
  
 Lorsqu'une table est supprimée, tous les index XML qui lui sont associés sont également automatiquement supprimés. Ceci dit, une colonne XML ne peut pas être supprimée d'une table si un index XML existe sur cette colonne.  
  
 Dans l’exemple suivant, un index XML est créé sur un `xml` colonne de type. Pour plus d’informations, consultez [Comparer du XML typé et du XML non typé](../xml/compare-typed-xml-to-untyped-xml.md).  
  
```  
CREATE TABLE TestTable(  
 Col1 int primary key,   
 Col2 xml (Production.ProductDescriptionSchemaCollection))   
GO  
```  
  
 Vous pouvez à présent créer un index XML primaire relatif à `Co12`.  
  
```  
CREATE PRIMARY XML INDEX PIdx_TestTable_Col2   
ON TestTable(Col2)  
GO  
```  
  
## <a name="example-creating-an-xml-index-by-using-the-dropexisting-index-option"></a>Exemple : création d'un index XML par le biais de l'option d'index DROP_EXISTING  
 Dans cet exemple, un index XML est créé sur une colonne nommée`XmlColx`. Ensuite, un autre index XML portant le même nom est créé sur une autre colonne nommée`XmlColy`. L'option `DROP_EXISTING` étant spécifiée, l'index XML existant sur (`XmlColx)` est supprimé et un nouvel index sur (`XmlColy`) est créé.  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T(Col1 int primary key, XmlColx xml, XmlColy xml)  
GO  
-- Create XML index on XmlColx.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColx)  
GO  
-- Create same name XML index on XmlColy.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColy)   
WITH (DROP_EXISTING = ON)  
-- Verify the index is created on XmlColy.d.  
SELECT sc.name   
FROM   sys.xml_indexes si inner join sys.index_columns sic   
ON     sic.object_id=si.object_id and sic.index_id=si.index_id  
INNER  join sys.columns sc on sc.object_id=sic.object_id   
AND    sc.column_id=sic.column_id  
WHERE  si.name='PIdx_T_XmlCol'   
AND    si.object_id=object_id('T')  
```  
  
 La requête renvoie le nom de la colonne sur laquelle l'index XML spécifié est créé.  
  
## <a name="see-also"></a>Voir aussi  
 [Index XML &#40;SQL Server&#41;](xml-indexes-sql-server.md)  
  
  
