---
title: local-nom-from-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name-from-QName function
- local-name-from-QName function
ms.assetid: fafed718-8c3c-403f-93ee-ec51fc157a6e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 544798f1de0b5000cfa6e3b797d72e3af2e6f36c
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256154"
---
# <a name="functions-related-to-qnames---local-name-from-qname"></a>Fonctions relatives aux QName : local-name-from-QName
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retourne un xs : NCName qui représente la partie locale de QName indiquée par *$arg*. Le résultat est une séquence vide si *$arg* correspond à la séquence vide.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
fn:local-name-from-QName($arg as xs:QName?) as xs:NCName?  
```  
  
## <a name="arguments"></a>Arguments  
 *$arg*  
 QName d'où le nom local doit être extrait.  
  
## <a name="examples"></a>Exemples  
 Cette rubrique fournit des exemples de XQuery relatifs à des instances XML stockés dans différentes **xml** colonnes de type le [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de données.  
  
 L’exemple suivant utilise le **local-name-from-QName()** fonction pour récupérer le nom local et l’URI de l’espace de noms des parties d’une valeur de type QName. Cet exemple illustre les opérations suivantes :  
  
-   La requête crée une collection de schémas XML.  
  
-   Elle crée ensuite une table possédant une colonne de type xml. Ce type est typé par le biais de la collection de schémas XML.  
  
-   Elle stocke enfin une instance XML servant d'échantillon dans la table. À l’aide de la **query()** méthode du type de données xml, l’expression de requête est exécutée pour récupérer la partie nom local de la valeur de type QName à partir de l’instance.  
  
```sql
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<root xmlns="QNameXSD" xmlns:a="https://someURI">a:someLocalName</root>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare default element namespace "QNameXSD"; local-name-from-QName(/root[1])')  
FROM T  
-- Result = someLocalName  
-- You can retrieve namespace URI part from the QName using the namespace-uri-from-QName() function  
SELECT xmlCol.query('declare default element namespace "QNameXSD"; namespace-uri-from-QName(/root[1])')  
FROM T  
-- Result = https://someURI  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Fonctions relatives aux QName &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
