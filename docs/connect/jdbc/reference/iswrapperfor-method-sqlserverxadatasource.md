---
title: iswrapperfor, méthode (SQLServerXADataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d612461d-4c3f-46db-b968-ff4c80b2aa7c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb5c7e7d4b95b66cfb1524d9c9729f9b9132fc5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722134"
---
# <a name="iswrapperfor-method-sqlserverxadatasource"></a>Méthode isWrapperFor (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indique si cet objet est un wrapper pour l'interface spécifiée.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Paramètres  
 *iface*  
  
 Un **classe** définissant une interface.  
  
## <a name="return-value"></a>Valeur retournée  
 **true** si cet objet implémente l’interface ou encapsule un objet qui implémente l’interface. Dans le cas contraire, la valeur est **false**.  
  
## <a name="exceptions"></a>Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notes   
 La méthode [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) et la méthode [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) sont définies par l’interface java.sql.Wrapper, introduite dans les spécifications de JDBC 4.0.  
  
 Si cette méthode retourne la valeur True, l’appel de [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) avec le même argument réussit.  
  
 Pour plus d’informations, consultez [Wrappers et Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a> Voir aussi  
 [Méthode Unwrap &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource, méthodes](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource, membres](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource, classe](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
