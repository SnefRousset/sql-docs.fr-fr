---
title: Implémentation de la fonctionnalité de fusion | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: faf6112fa3f8ec588d00480d09ff072a71051a02
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52508160"
---
# <a name="implementing-merge-functionality"></a>Implémentation de la fonctionnalité MERGE
  Une base de données devra peut-être effectuer l'insertion d'une mise à jour, selon qu'une ligne particulière existe déjà ou non dans la base de données.  
  
 Sans utiliser l'instruction `MERGE`, voici une approche que vous pouvez utiliser dans [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
```tsql  
UPDATE mytable SET col=@somevalue WHERE myPK = @parm  
IF @@ROWCOUNT = 0  
    INSERT mytable (columns) VALUES (@parm, @other values)  
```  
  
 Autre méthode [!INCLUDE[tsql](../../includes/tsql-md.md)] pour implémenter une fusion :  
  
```tsql  
IF EXISTS (SELECT 1 FROM mytable WHERE myPK = @parm)  
    UPDATE....  
ELSE  
    INSERT  
```  
  
 Pour une procédure stockée compilée en mode natif  
  
```tsql  
DECLARE @i  int  = 0  -- or whatever your PK data type is  
UPDATE mytable SET @i=myPK, othercolums = other values WHERE myPK = @parm  
IF @i = 0  
   INSERT....  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Problèmes de migration pour les procédures stockées compilées en mode natif](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Les constructions Transact-SQL ne sont pas prises en charge par l’OLTP en mémoire](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
