---
title: Les attributs personnalisés pour les Routines CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c59df39f3d4d0df423f48df092e49e53dba1861c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664963"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Attributs personnalisés de l’intégration du CLR pour les routines CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Les attributs répertoriés peuvent être appliqués au common language runtime (CLR) routines, types définis par l’utilisateur et les agrégats définis par l’utilisateur qui sont inscrits dans [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si l'attribut n'est pas appliqué, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilise la valeur par défaut. Les attributs répertoriés sont définis dans le **Microsoft.SqlServer.Server** espace de noms.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Attribut SqlUserDefinedAggregate  
 Le **SqlUserDefinedAggregate** attribut indique que la méthode doit être inscrit en tant qu’un agrégat défini par l’utilisateur. Chaque agrégat défini par l'utilisateur doit être annoté avec cet attribut.  
  
 Pour plus d’informations, consultez [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Attribut SqlFunction  
 Le **SqlFunction** attribut indique la méthode doit être inscrit en tant que fonction, avec l’ensemble d’attributs de fonction appropriée.  
  
 Pour plus d’informations, consultez [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Attribut SqlFacet  
 Le **SqlFacet** attribut est utilisé pour retourner des informations sur le type de retour d’une expression de type défini par l’utilisateur (UDT).  
  
 Pour plus d’informations, consultez [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Attribut SqlProcedure  
 Le **SqlProcedure** attribut indique que la méthode doit être enregistrée comme une procédure stockée. Cet attribut est utilisé uniquement par Visual Studio pour inscrire automatiquement la méthode spécifiée en tant que procédure stockée ; il n'est pas utilisé par [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Pour plus d’informations, consultez [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Attribut SqlTrigger  
 Le **SqlTrigger** attribut indique la méthode doit être inscrit en tant que déclencheur.  
  
 Pour plus d’informations, consultez [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022) et [SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 Vous pouvez appliquer SqlUserDefinedTypeAttribute à une définition de classe dans l'assembly. Cela oblige [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à créer un type défini par l'utilisateur et lié à la définition de classe qui possède cet attribut personnalisé.  
  
 Pour plus d’informations, consultez [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Attribut SqlMethod  
 Le **SqlMethod** attribut est utilisé pour indiquer les propriétés d’accès de données et de déterminisme d’une méthode ou une propriété sur un type UDT.  
  
 Pour plus d’informations, consultez [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Voir aussi  
 [Agrégats CLR définis par l’utilisateur](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Fonctions CLR définies par l’utilisateur](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Types CLR définis par l’utilisateur](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Procédures stockées CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Déclencheurs CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
