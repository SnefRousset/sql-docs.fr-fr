---
title: STPointFromText (type de données geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointFromText (geography Data Type)
- STPointFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromText method
ms.assetid: e5fe54dc-0007-4631-8dde-7ae4d4c41f6e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 78ea6106d85a6295a6b9cc2088febe5d1498fff5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698453"
---
# <a name="stpointfromtext-geography-data-type"></a>STPointFromText (type de données geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retourne une instance **geography** à partir d’une représentation OGC (Open Geospatial Consortium) WKT (Well-Known Text), à laquelle s’ajoutent les valeurs Z (élévation) et M (mesure) apportées par l’instance.
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
STPointFromText ( 'point_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Arguments  
 *point_tagged_text*  
 Représentation WKT de l’instance **geographyPoint** à retourner. *point_tagged_text* est une expression **nvarchar(max)**.  
  
 *SRID*  
 Expression **int** qui représente le SRID (ID de référence spatiale) de l’instance **geographyPoint** à retourner.  
  
## <a name="return-types"></a>Types de retour  
 Type de retour [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **geography**  
  
 Type de retour CLR : **SqlGeography**  
  
 Type OGC : **Point**  
  
## <a name="remarks"></a>Notes   
 Cette méthode lève **FormatException** si l’entrée n’est pas au format approprié.  
  
## <a name="examples"></a>Exemples  
 L'exemple suivant utilise la méthode `STPointFromText()` pour créer une instance `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STPointFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a> Voir aussi  
 [Méthodes geography statiques de l’OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
