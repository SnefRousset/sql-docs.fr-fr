---
title: HasM (type de données geography) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HasM_TSQL
- HasM
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geography
ms.assetid: e752e97f-1619-437d-b962-48c188b4e94c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9ece3c57981f52b1359f40d59487c464b6c5a230
ms.sourcegitcommit: c3b190f8f87a4c80bc9126bb244896197a6dc453
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852854"
---
# <a name="hasm-geography-data-type"></a>HasM (type de données geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retourne 1 (true) si un objet spatial contient au moins une valeur M ; sinon retourne 0 (false).  
  
## <a name="syntax"></a>Syntaxe  
  
```sql  
  
.HasM  
```  
  
## <a name="return-types"></a>Types de retour  
Type de retour [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **bit**  
  
Type de retour CLR : **Booléen**  
  
## <a name="remarks"></a>Notes   
  
## <a name="examples"></a>Exemples  
  
```sql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a> Voir aussi  
 [Méthodes étendues sur des instances Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;type de données geography&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)  
  
  
