---
title: Méthode getQueryTimeout (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8dff954f-b458-4fa6-abe6-be62ff75e2b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b19809f549fa252f18964f2c3b9e63de1c8cf5e3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841467"
---
# <a name="getquerytimeout-method-sqlserverstatement"></a>Méthode getQueryTimeout (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Récupère le nombre de secondes pendant lesquelles [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] attend que cet objet [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) s’exécute.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
public final int getQueryTimeout()  
```  
  
## <a name="return-value"></a>Valeur retournée  
 Un **int** qui indique le nombre de secondes que le pilote JDBC doit attendre, ou 0 s’il n’existe aucune limite.  
  
## <a name="exceptions"></a>Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notes   
 Cette méthode getQueryTimeout est spécifiée par la méthode getQueryTimeout dans l’interface java.sql.Statement.  
  
## <a name="see-also"></a> Voir aussi  
 [SQLServerStatement, membres](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement, classe](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
