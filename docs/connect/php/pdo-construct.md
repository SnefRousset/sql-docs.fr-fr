---
title: PDO::__construct | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91b4edcd65f972adb98cf1a4f6c62a81ebb184f8
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600140"
---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Crée une connexion à une base de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>Paramètres  
*$dsn* : chaîne qui contient le nom du préfixe (toujours `sqlsrv`), un signe deux-points et le mot clé Server. Par exemple, `"sqlsrv:server=(local)"`. Vous pouvez éventuellement spécifier d’autres mots clés de connexion. Consultez [Connection Options](../../connect/php/connection-options.md) pour obtenir la description du mot clé Server et des autres mots clés de connexion. La totalité de *$dsn* est entre guillemets, si bien que chaque mot clé de connexion ne doit pas être individuellement mis entre guillemets.  
  
*$username*: facultatif. Chaîne qui contient le nom de l’utilisateur. Pour vous connecter en utilisant l’authentification [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , spécifiez l’ID de connexion. Pour vous  connecter avec l’authentification Windows, spécifiez `""`.  
  
*$password*: facultatif. Chaîne qui contient le mot de passe de l’utilisateur. Pour vous connecter en utilisant l’authentification [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , spécifiez le mot de passe. Pour vous  connecter avec l’authentification Windows, spécifiez `""`.  
  
*$driver_options*: facultatif. Vous pouvez spécifier les attributs du Gestionnaire de pilotes PDO et des attributs de pilotes spécifiques [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] : PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ATTR_DIRECT_QUERY. Un attribut non valide ne lève pas d’exception. Les attributs non valides lèvent des exceptions quand ils sont spécifiés avec [PDO::setAttribute](../../connect/php/pdo-setattribute.md).  
  
## <a name="return-value"></a>Valeur retournée  
Retourne un objet PDO. En cas d’échec, retourne un objet PDOException.  
  
## <a name="exceptions"></a>Exceptions  
PDOException  
  
## <a name="remarks"></a>Notes   
Vous pouvez fermer un objet de connexion en affectant à l’instance la valeur Null.  
  
Une fois la connexion, PDO::errorCode affiche 01000 au lieu de 00000.  
  
Si PDO::__construct échoue pour une raison quelconque, une exception est levée, même si PDO::ATTR_ERRMODE a la valeur PDO::ERRMODE_SILENT.  
  
La prise en charge de PDO a été ajoutée dans la version 2.0 de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a> Exemple  
Cet exemple montre comment se connecter à un serveur en utilisant l’authentification Windows et spécifier une base de données.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example"></a> Exemple  
Cet exemple montre comment se connecter à un serveur en spécifiant la base de données plus tard.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a> Voir aussi  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
