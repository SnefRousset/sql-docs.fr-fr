---
title: Connexion et l’extraction de données | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a711ab2e1f8f8f454e69b3b81b878d024d81eeba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742007"
---
# <a name="connecting-and-retrieving-data"></a>Connexion et extraction de données

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Lorsque vous travaillez avec le [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], il existe deux méthodes principales pour établir une connexion à une base de données [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La première méthode consiste à définir les propriétés de connexion de l'URL de connexion, puis à appeler la méthode getConnection de la classe DriverManager pour retourner un objet [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
> [!NOTE]  
> Pour obtenir la liste des propriétés de connexion pris en charge par le pilote JDBC, consultez [définissant les propriétés de connexion](../../../connect/jdbc/setting-the-connection-properties.md).  
  
La seconde méthode implique de définir les propriétés de connexion grâce aux méthodes setter de la classe [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md), puis d'appeler la méthode [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) pour retourner un objet SQLServerConnection.  
  
Les rubriques de cette section décrivent les différentes façons de se connecter à une base de données [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ; elles présentent également différentes techniques d'extraction de données.  
  
## <a name="in-this-section"></a>Dans cette section  
  
|Rubrique|Description|  
|-----------|-----------------|  
|[Exemple d’URL de connexion](../../../connect/jdbc/code-samples/connection-url-sample.md)|Décrit l'utilisation d'une URL de connexion pour se connecter à [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] et l'utilisation d'une instruction SQL pour extraire des données.|  
|[Exemple de source de données](../../../connect/jdbc/code-samples/data-source-sample.md)|Décrit l'utilisation d'une source de données pour se connecter à SQL Server et l'utilisation d'une procédure stockée pour extraire des données.|  
  
## <a name="see-also"></a> Voir aussi

[Exemples d’applications JDBC Driver](../../jdbc/code-samples/sample-jdbc-driver-applications.md)
  
