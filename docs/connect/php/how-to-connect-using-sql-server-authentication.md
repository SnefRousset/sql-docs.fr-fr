---
title: Guide pratique pour se connecter avec l’authentification SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, SQL Server Authentication
ms.assetid: 8d298830-3186-47e7-aef6-586b457901c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d2188b99a43dbf26d97871535204f3da69c23af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731797"
---
# <a name="how-to-connect-using-sql-server-authentication"></a>Procédure : se connecter à l’aide de l’authentification SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Le [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] prend en charge l’authentification SQL Server quand vous vous connectez à SQL Server.  
  
Vous devez utiliser l’authentification SQL Server uniquement quand l’authentification Windows n’est pas possible. Pour plus d’informations sur la connexion avec l’authentification Windows, consultez [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Prenez en considération les points suivants quand vous utilisez l’authentification SQL Server pour la connexion à SQL Server :  
  
-   L’authentification en mode mixte SQL Server doit être activée sur le serveur.  
  
-   L’identifiant utilisateur et le mot de passe (attributs de connexion *UID* et *PWD* dans le pilote SQLSRV) doivent être définis au moment de la tentative de connexion. L’ID utilisateur et le mot de passe doivent être mappés à un utilisateur et un mot de passe SQL Server valides.  
  
> [!NOTE]  
> Les mots de passe qui contiennent une accolade fermante (}) doivent être précédés d’une deuxième accolade fermante. Par exemple, si le mot de passe SQL Server est “mot}depasse”, la valeur de l’attribut de connexion *PWD* doit être “mot}}depasse”.  
  
Appliquez les précautions suivantes quand vous utilisez l’authentification SQL Server pour vous connecter à SQL Server :  
  
-   Protégez (chiffrez) les informations d’identification transmises sur le réseau à partir du serveur web vers la base de données. Les informations d’identification sont chiffrées par défaut à compter de SQL Server 2005. Pour renforcer la sécurité, affectez la valeur “on” à l’attribut de connexion Encrypt pour chiffrer toutes les données envoyées au serveur.  
  
> [!NOTE]  
> L’affectation de la valeur “on” à l’attribut de connexion Encrypt peut diminuer les performances, car le chiffrement des données peut nécessiter beaucoup de ressources de calcul.  
  
-   N’incluez pas de valeurs pour les attributs de connexion *UID* et *PWD* en texte brut dans des scripts PHP. Vous devez stocker ces valeurs dans un répertoire propre à l’application avec des autorisations d’accès appropriées.  
  
-   Évitez d’utiliser le compte *sa* . Mappez l’application à un utilisateur de base de données qui possède les privilèges souhaités et utilisez un mot de passe fort.  
  
> [!NOTE]  
> Vous pouvez définir des attributs de connexion autres que l’ID utilisateur et le mot de passe quand vous établissez une connexion. Pour obtenir la liste complète des attributs de connexion pris en charge, consultez [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="example"></a> Exemple  
L’exemple suivant utilise le pilote SQLSRV avec l’authentification SQL Server pour établir une connexion à une instance locale de SQL Server. Les valeurs des attributs de connexion obligatoires *UID* et *PWD* sont extraites à partir de fichiers texte propres à l’application, *uid.txt* et *pwd.txt*, dans le répertoire *C:\AppData*. Une fois la connexion établie, le serveur est interrogé pour vérifier la connexion de l’utilisateur.  
  
L’exemple part du principe que SQL Server et la base de données [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) sont installés sur l’ordinateur local. Toute la sortie est écrite dans le navigateur quand l’exemple est exécuté à partir du navigateur.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
  
/* Get UID and PWD from application-specific files.  */  
$uid = file_get_contents("C:\AppData\uid.txt");  
$pwd = file_get_contents("C:\AppData\pwd.txt");  
$connectionInfo = array( "UID"=>$uid,  
                         "PWD"=>$pwd,  
                         "Database"=>"AdventureWorks");  
  
/* Connect using SQL Server Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a> Exemple  
Cet exemple utilise le pilote PDO_SQLSRV pour illustrer comment se connecter avec l’authentification SQL Server.  
  
```  
<?php  
   $serverName = "(local)";   
   $database = "AdventureWorks";  
  
   // Get UID and PWD from application-specific files.   
   $uid = file_get_contents("C:\AppData\uid.txt");  
   $pwd = file_get_contents("C:\AppData\pwd.txt");  
  
   try {  
      $conn = new PDO( "sqlsrv:server=$serverName;Database = $database", $uid, $pwd);   
      $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
   }  
  
   catch( PDOException $e ) {  
      die( "Error connecting to SQL Server" );   
   }  
  
   echo "Connected to SQL Server\n";  
  
   $query = 'select * from Person.ContactType';   
   $stmt = $conn->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
      print_r( $row );   
   }  
  
   // Free statement and connection resources.   
   $stmt = null;   
   $conn = null;   
?>  
```  
  
## <a name="see-also"></a> Voir aussi  
[Guide pratique pour se connecter à l’aide de l’authentification SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[Guide de programmation pour les pilotes Microsoft pour PHP pour SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[À propos des exemples de code dans la documentation](../../connect/php/about-code-examples-in-the-documentation.md)

[SUSER_SNAME (Transact-SQL)](../../t-sql/functions/suser-sname-transact-sql.md)

[Guide pratique pour créer un compte de connexion SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)

[Guide pratique pour créer un utilisateur de base de données](../../relational-databases/security/authentication-access/create-a-database-user.md)

[Gestion des utilisateurs, rôles et connexions](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Séparation du schéma et de l’utilisateur](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Accorder des autorisations d’objet (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
