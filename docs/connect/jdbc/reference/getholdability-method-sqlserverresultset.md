---
title: getholdability, méthode (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cf27049e45c8e52c8a63a419327f377dd1f558f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841397"
---
# <a name="getholdability-method-sqlserverresultset"></a>Méthode getHoldability (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Récupère la fonctionnalité de mise en attente de cet objet [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>Valeur retournée  
 Valeur **int** contenant l’un des niveaux de mise en attente suivants :  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notes   
 Cette méthode getHoldability est spécifiée par la méthode getHoldability dans l’interface java.sql.ResultSet.  
  
 Pour définir la capacité de mise en attente du jeu de résultats, les applications peuvent utiliser la méthode [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) de la classe [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md). Une fois la méthode [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) appelée, l’objet d’instruction et son objet de jeu de résultats créés, et l’instruction exécutée, l’application doit dans certains cas modifier à nouveau la capacité de mise en attente.  
  
 Pour les curseurs côté serveur, lors d'une connexion à SQL Server 2005 ou version ultérieure, la définition de la fonctionnalité de mise en attente affecte uniquement la fonctionnalité des nouveaux jeux de résultats qui doivent être créés sur cette connexion. Toutefois, avec SQL Server 2000, la définition de la fonctionnalité de mise en attente affecte la fonctionnalité de mise en attente des jeux de résultats existants et des nouveaux jeux de résultats qui doivent être créés sur cette connexion.  
  
 Lorsque la fonctionnalité est réinitialisée et la méthode getHoldability est appelée sur objet de jeu de résultats créé précédemment, la valeur retournée par cette méthode peut être différente de celui de la valeur de la mise en attente retournée par les méthodes suivantes : Statement.getResultSetHoldability , Connection.getHoldability ou DatabaseMetaData.getResultSetHoldability.  
  
## <a name="see-also"></a> Voir aussi  
 [SQLServerResultSet, membres](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet, classe](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
