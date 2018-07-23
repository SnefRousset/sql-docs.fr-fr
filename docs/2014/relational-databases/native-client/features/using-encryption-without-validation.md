---
title: Utilisation du chiffrement sans Validation | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3349bd91f4e0e4e3db252b6406dc58cdbe6179b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430318"
---
# <a name="using-encryption-without-validation"></a>Utilisation du chiffrement sans validation
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] chiffre toujours les paquets réseau associés à l’ouverture de session. Si aucun certificat n'a été fourni sur le serveur à son démarrage, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] génère un certificat auto-signé qui est utilisé pour chiffrer les paquets d’ouverture de session.  
  
 Les applications peuvent également demander le chiffrement de tout le trafic réseau en utilisant des mots clés de chaîne de connexion ou des propriétés de connexion. Les mots clés sont « Encrypt » pour ODBC et OLE DB lors de l’utilisation d’une chaîne de fournisseur avec **IDbInitialize::Initialize**, ou « Use Encryption for Data » pour ADO et OLE DB lors de l’utilisation d’une chaîne d’initialisation avec **IDataInitialize** . Cela peut également être configuré par [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à l’aide du Gestionnaire de Configuration le **forcer le chiffrement du protocole** option. Par défaut, le chiffrement de tout le trafic réseau pour une connexion requiert la fourniture d'un certificat sur le serveur.  
  
 Pour plus d’informations sur les mots clés de chaîne de connexion, consultez [Using Connection String Keywords with SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Pour activer le chiffrement à utiliser lorsqu’aucun certificat n’a pas été fourni sur le serveur, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager peut être utilisé pour définir les deux le **forcer le chiffrement du protocole** et **faire confiance au certificat serveur**  options. Dans ce cas, le chiffrement utilise un certificat de serveur auto-signé sans validation si aucun certificat vérifiable n'a été fourni sur le serveur.  
  
 Les applications peuvent également utiliser le mot clé « TrustServerCertificat » ou son attribut de connexion associé pour garantir que le chiffrement est réalisé. Les paramètres de l'application ne réduisent jamais le niveau de sécurité défini par le Gestionnaire de configuration du client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], mais peuvent le renforcer. Par exemple, si **forcer le chiffrement du protocole** n’est pas définie pour le client, une application peut demander elle-même le chiffrement. Pour garantir le chiffrement même si aucun certificat de serveur n'a été fourni, une application peut demander le chiffrement et « TrustServerCertificate ». Toutefois, si« TrustServerCertificate » n'est pas activé dans la configuration client, un certificat de serveur fourni est toujours requis. Le tableau ci-dessous décrit l'ensembles des scénarios :  
  
|Paramètre client Forcer le chiffrement du protocole|Paramètre client Faire confiance au certificat de serveur|Chaîne de connexion/attribut de connexion Encrypt/Use Encryption for Data|Chaîne de connexion/attribut de connexion Trust Server Certificate|Résultats|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|non|Néant|Non (par défaut)|Ignoré|Aucun chiffrement ne se produit.|  
|non|Néant|Oui|Non (par défaut)|Le chiffrement se produit uniquement s'il existe un certificat de serveur vérifiable ; sinon, la tentative de connexion échoue.|  
|non|Néant|Oui|Oui|Le chiffrement se produit toujours, mais peut utiliser un certificat de serveur auto-signé.|  
|Oui|non|Ignoré|Ignoré|Le chiffrement se produit uniquement s'il existe un certificat de serveur vérifiable ; sinon, la tentative de connexion échoue.|  
|Oui|Oui|Non (par défaut)|Ignoré|Le chiffrement se produit toujours, mais peut utiliser un certificat de serveur auto-signé.|  
|Oui|Oui|Oui|Non (par défaut)|Le chiffrement se produit uniquement s'il existe un certificat de serveur vérifiable ; sinon, la tentative de connexion échoue.|  
|Oui|Oui|Oui|Oui|Le chiffrement se produit toujours, mais peut utiliser un certificat de serveur auto-signé.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Fournisseur OLE DB SQL Server Native Client  
 Le [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client fournisseur OLE DB natif prend en charge le chiffrement sans validation via l’ajout de la propriété de l’initialisation SSPROP_INIT_TRUST_SERVER_CERTIFICATE données source qui est implémentée dans le jeu de propriétés DBPROPSET_SQLSERVERDBINIT ensemble. De plus, un nouveau mot clé de chaîne de connexion, « TrustServerCertificate» , a été ajouté. Il accepte les valeurs Oui ou non ; non est la valeur par défaut. Lors de l'utilisation de composants du service, il accepte les valeurs true ou false ; false étant la valeur par défaut.  
  
 Pour plus d’informations sur les améliorations apportées au jeu de propriétés DBPROPSET_SQLSERVERDBINIT, consultez [propriétés d’initialisation et d’autorisation](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Pilote ODBC SQL Server Native Client  
 Le [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pilote ODBC Native Client prend en charge le chiffrement sans validation grâce à des ajouts à la [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) et [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md) fonctions. SQL_COPT_SS_TRUST_SERVER_CERTIFICATE a été ajouté pour accepter SQL_TRUST_SERVER_CERTIFICATE_YES ou SQL_TRUST_SERVER_CERTIFICATE_NO ; SQL_TRUST_SERVER_CERTIFICATE_NO étant la valeur par défaut. De plus, un nouveau mot clé de chaîne de connexion, « TrustServerCertificate », a été ajouté. Il accepte les valeurs « yes » ou « no » ; «no » étant la valeur par défaut.  
  
## <a name="see-also"></a>Voir aussi  
 [Fonctionnalités de SQL Server Native Client](sql-server-native-client-features.md)  
  
  