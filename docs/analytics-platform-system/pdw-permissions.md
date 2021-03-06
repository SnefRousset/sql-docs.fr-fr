---
title: Autorisations dans Parallel Data Warehouse | Microsoft Docs
description: Cet article décrit la configuration requise et les options de gestion des autorisations de base de données pour Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1ac058e42b8bad4f499210835a1f85c3cc7a08a5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523592"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>La gestion des autorisations dans Parallel Data Warehouse
Cet article décrit la configuration requise et les options de gestion des autorisations de base de données pour SQL Server PDW.  
  
## <a name="BackupRestoreBasics"></a>Autorisation principes de base du moteur de base de données  
Autorisations de moteur de base de données sur SQL Server PDW sont gérées au niveau du serveur via des connexions et au niveau de la base de données par le biais des utilisateurs de base de données et les rôles de base de données défini par l’utilisateur.  
  
**Connexions**  
Les connexions sont des comptes d’utilisateur individuels pour vous connecter à l’ordinateur SQL Server PDW. SQL Server PDW prend en charge les connexions à l’aide de l’authentification de l’authentification Windows et SQL Server.  Connexions d’authentification de Windows peuvent être des utilisateurs de Windows ou des groupes Windows à partir de n’importe quel domaine approuvé par SQL Server PDW. Connexions d’authentification de SQL Server sont définies et authentifiées par SQL Server PDW et doit être créé en spécifiant un mot de passe.  
  
Membres de la **sysadmin** rôle serveur fixe (tel que le **sa** connexion) peut se connecter à une base de données sans avoir à qui est mappé à un utilisateur de base de données. Elles sont mappées à la **dbo** utilisateur. Le propriétaire de la base de données est également mappé comme le **dbo** utilisateur.  
  
**Rôles de serveur**  
Il existe quatre rôles de serveur spéciaux avec un ensemble de rôles préconfigurés qui fournissent un groupe pratique d’autorisations de niveau serveur. Le **sysadmin**, **MediumRC**, **LargeRC**, et **XLargeRCfixed** les rôles de serveur sont les rôles de serveur uniquement actuellement implémentés dans SQL Server PDW. Le **sa** connexion est le seul membre de la **sysadmin** rôle serveur fixe et des connexions supplémentaires ne peuvent pas être ajouté à la **sysadmin** rôle. Connexions peuvent être accordées le **CONTROL SERVER** autorisation, qui est similaire, mais pas identiques, à la **sysadmin** rôle serveur fixe. Utilisez [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) pour ajouter des membres à d’autres rôles de serveur. SQL Server PDW ne prend pas en charge les rôles serveur définis par l’utilisateur.  
  
**Utilisateurs de base de données**  
Connexions autorisées à accéder à une base de données par la création d’un utilisateur de base de données dans une base de données et le mappage de cet utilisateur de base de données à une connexion. En général, le nom d’utilisateur de base de données est le même que le nom de connexion, mais ce n’est pas obligatoire. Chaque utilisateur de base de données est mappé à une seule connexion. Une connexion ne peut être mappée qu’à un seul utilisateur dans une base de données, mais peut être mappée comme utilisateur de base de données dans plusieurs bases de données.  
  
**Rôles de base de données fixe**  
Rôles de base de données fixes sont un ensemble de rôles préconfigurés qui fournissent un groupe pratique d’autorisations de niveau de base de données. Les utilisateurs de base de données et les rôles de base de données défini par l’utilisateur peuvent être ajoutés aux rôles de base de données fixe à l’aide de la [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) procédure. Pour plus d’informations sur les rôles de base de données fixe, consultez [rôles de base de données fixes](#fixed-database-roles).  
  
**Rôles de base de données défini par l’utilisateur**  
Les utilisateurs avec le **CREATE ROLE** autorisation permettre créer de nouveaux rôles de base de données défini par l’utilisateur pour représenter des groupes d’utilisateurs disposant d’autorisations courantes. En général, les autorisations sont accordées ou refusées à l’ensemble du rôle, ce qui simplifie la gestion et la surveillance des autorisations.  
  
Des autorisations aux principaux de sécurité (connexions, utilisateurs et rôles) à l’aide de la **GRANT** instruction. Les autorisations sont refusées explicitement à l’aide de la **DENY** commande. A précédemment autorisation accordée ou refusée est supprimée à l’aide de la **RÉVOQUER** instruction. Les autorisations sont cumulatives : l’utilisateur bénéficie de toutes les autorisations accordées à lui-même, à la connexion et à toute appartenance à un groupe. Toutefois, tout refus d’autorisation remplace toutes les attributions. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
L’exemple suivant illustre une méthode courante et recommandée pour configurer des autorisations.  
  
1.  Si vous utilisez l’authentification Windows, créez une connexion pour chaque utilisateur de Windows ou un groupe Windows qui se connecte à SQL Server PDW. Si vous utilisez l’authentification SQL Server, créez une connexion pour chaque personne qui se connecte à SQL Server PDW.  
  
2.  Créer un utilisateur de base de données pour chaque connexion dans toutes les bases de données nécessaires.  
  
3.  Créer un ou plusieurs rôles de base de données défini par l’utilisateur, chacun représentant une fonction similaire. Par exemple, analyste financier et analyste des ventes.  
  
4.  Ajouter des utilisateurs de base de données à un ou plusieurs rôles de base de données défini par l’utilisateur.  
  
5.  Accordez des autorisations aux rôles de base de données définis par l’utilisateur.  
  
Connexions sont des objets au niveau du serveur et peut être répertoriées en consultant [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Uniquement les autorisations de niveau serveur peuvent être accordées aux principaux de serveur.  
  
Les utilisateurs et rôles de base de données sont des objets de niveau de base de données et peut être répertoriés en consultant [sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Uniquement les autorisations de niveau de base de données peuvent être accordées aux principaux de base de données.  
  
## <a name="BackupTypes"></a>Autorisations par défaut  
La liste suivante décrit les autorisations par défaut :  
  
-   Création d’un compte de connexion par les instructions using **CREATE LOGIN** instruction, la connexion reçoit le **CONNECT SQL** autorisation permettant la connexion pour se connecter à l’ordinateur SQL Server PDW.  
  
-   Lorsqu’un utilisateur de base de données est créé à l’aide de la **CREATE USER** instruction, l’utilisateur reçoit le **connecter ON DATABASE ::**_< nom_base_de_données >_ autorisation, ce qui permet le connexion pour se connecter à cette base de données en tant qu’utilisateur.  
  
-   Tous les principaux, y compris le rôle PUBLIC, aucune autorisation explicite ou implicite par défaut ont l’héritage des autorisations implicites des autorisations explicites. Par conséquent, lorsque aucune autorisation explicite n’est présente, il ne peut également être aucune autorisation implicite.  
  
-   Lorsqu’une connexion devient le propriétaire d’un objet ou d’une base de données, la connexion a toujours toutes les autorisations sur l’objet ou de la base de données. Les autorisations de propriété ne sont pas visibles comme des autorisations explicites. Le **GRANT**, **RÉVOQUER**, et **DENY** instructions n’ont aucun effet sur les autorisations de la propriété. La propriété peut être modifiée à l’aide de la [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) instruction.  
  
-   La connexion sa a toutes les autorisations sur l’appliance. Autorisations de propriété, les autorisations d’administrateur système ne peut pas être modifiées et similaires ne sont pas visibles comme des autorisations explicites. Le **GRANT**, **RÉVOQUER**, et **DENY** instructions n’ont aucun effet sur les autorisations d’administrateur système.  
  
-   Le rôle serveur PUBLIC ne reçoit aucune autorisation par défaut et n’hérite pas des autorisations d’autres rôles de serveur. Le rôle serveur PUBLIC peut recevoir des autorisations explicites avec le **GRANT**, **RÉVOQUER**, et **DENY** instructions.  
  
-   Les transactions ne nécessitent pas d’autorisations. Tous les principaux peuvent exécuter la **BEGIN TRANSACTION**, **valider**, et **ROLLBACK** les commandes de transaction. Toutefois, un principal doit avoir les autorisations appropriées pour exécuter chaque instruction dans la transaction.  
  
-   L’instruction **USE** n’a pas besoin d’autorisation. Tous les principaux peuvent exécuter la **utilisez** instruction sur une base de données, mais pour accéder à une base de données, elles doivent avoir un principal d’utilisateur dans la base de données ou de l’utilisateur invité doit être activé.  
  
### <a name="the-public-role"></a>Le rôle PUBLIC  
Toutes les nouvelles connexions d’appliance appartiennent automatiquement au rôle PUBLIC. Le rôle de serveur PUBLIC possède les caractéristiques suivantes :  
  
-   Le rôle serveur PUBLIC dispose d’aucune autorisation par défaut.  
  
-   Tous les principaux sont membres du rôle serveur PUBLIC et le rôle serveur PUBLIC n’est pas un membre d’un autre rôle de serveur.  
  
-   Le rôle serveur PUBLIC ne peut pas hériter des autorisations implicites. Les autorisations accordées au rôle PUBLIC doivent être accordées explicitement.  
  
## <a name="BackupProc"></a>Détermination des autorisations  
Une connexion ait ou non autorisé à effectuer une action spécifique varie selon les autorisations accordées ou refusées à la connexion, utilisateur et l’utilisateur est membre des rôles. Autorisations de niveau serveur (tel que **CREATE LOGIN** et **VIEW SERVER STATE**) sont disponibles pour les entités de sécurité au niveau du serveur (connexions). Autorisations de niveau de base de données (tel que **sélectionnez** à partir d’une table ou **EXECUTE** sur une procédure) sont disponibles au niveau de la base de données principaux (utilisateurs et rôles de base de données).  
  
### <a name="implicit-and-explicit-permissions"></a>Autorisations implicites et explicites  
Une *autorisation explicite* est une autorisation **GRANT** ou **DENY** donnée à un principal par une instruction **GRANT** ou **DENY**. Autorisations de niveau de base de données sont répertoriées dans le [sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) vue. Les autorisations au niveau du serveur sont répertoriées dans le [sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vue.  
  
Un *autorisation implicite* est un **GRANT** ou **DENY** autorisation une entité de sécurité (rôle de serveur ou la connexion) a hérité. Une autorisation peut être héritée de plusieurs manières.  
  
-   Un principal peut hériter une autorisation à partir d’un rôle si l’entité est membre du rôle, même si l’entité de sécurité n’a pas explicite **GRANT** ou **DENY** autorisation.  
  
-   Un principal peut hériter une autorisation sur un objet subordonné (par exemple, une table) si le principal possède une autorisation sur l’une des portées parent objets (par exemple, le schéma de la table ou l’autorisation sur la base de données entière).  
  
-   Un principal peut hériter d’une autorisation en demandant une autorisation qui inclut une autorisation subordonnée. Par exemple le **ALTER ANY USER** autorisation inclut les deux valeurs le **CREATE USER** et le **modifier un utilisateur ON ::** _<name>_ autorisations.  
  
### <a name="determining-permissions-when-performing-actions"></a>Détermination des autorisations lors de l’exécution des Actions  
Le processus permettant de déterminer quelle autorisation d’affecter à une entité de sécurité est complexe. La complexité se produit lors de la détermination des autorisations implicites, car ces principaux peuvent être membres de plusieurs rôles et autorisations peuvent être passées à travers plusieurs niveaux dans la hiérarchie des rôles.  
  
La liste suivante décrit les règles générales pour la détermination des autorisations :  
  
-   La propriété implique l’autorisation.  
  
    Un propriétaire d’objets a toutes les autorisations sur l’objet. De même, un propriétaire de base de données a toutes les autorisations sur la base de données et toutes les autorisations sur les objets dans la base de données. Ces autorisations ne peuvent pas être modifiées.  
  
-   Les autorisations peuvent être héritées sur plusieurs niveaux dans la hiérarchie des appartenances au rôle de serveur.  
  
    Par exemple, supposons que vous avez la situation suivante :  
  
    -   David de connexion est membre du rôle de base de données PerfAnalysts.  
  
    -   PerfAnalysts est un membre du rôle de base de données Production.  
  
    -   David et PerfAnalysts n’ont pas **sélectionnez** autorisation sur la table Customer. L’autorisation a été révoquée ou jamais explicitement accordée.  
  
    -   Production a **sélectionnez** autorisation sur la table Customer.  
  
    Dans ce cas, PerfAnalysts héritera **GRANT** hériteront des autorisations sur la table Customer de Production et David **GRANT** autorisation sur la table Customer de la Production.  
  
-   **DENY** substitue **GRANT** lorsque les autorisations sont en conflit.  
  
    Par exemple, supposons que la connexion David dispose d’aucune autorisation sur la table Customer et est membre des deux rôles de base de données-dbgroup1, ce qui a **DENY** autorisation sur la table Customer et dbgroup2, qui a **GRANT** autorisation sur la table Customer. Dans ce cas, David hériteront le **DENY** autorisation sur la table Customer. C’est le cas si les rôles acquise leurs autorisations explicitement ou implicitement.  
  
### <a name="auditing-permissions"></a>L’audit des autorisations  
Pour effectuer des recherches sur les autorisations d’un utilisateur de vérifier les points suivants.  
  
-   Exécutez la requête suivante pour déterminer quelles connexions sont des administrateurs système.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   Exécutez la requête suivante pour déterminer les connexions qui disposent d’autorisations explicites.  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   Exécutez la requête suivante dans une base de données utilisateur pour déterminer quels utilisateurs de base de données sont membres d’un rôle de base de données.  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   Exécutez la requête suivante dans une base de données utilisateur pour déterminer les utilisateurs de base de données et les rôles ont été accordés ou refusés des autorisations spécifiques. Vous devrez les affichages des requêtes supplémentaires tels que sys.objects et sys.schemas pour identifier les éléments décrits avec la major_id.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Meilleures pratiques de base de données autorisations  
  
-   Accorder des autorisations au niveau granulaire au plus pratique. L’octroi d’autorisations à la table ou des autorisations au niveau d’affichage peut devenir ingérables. Mais accorder des autorisations au niveau de la base de données peut être trop permissives. Si la base de données est conçue avec des schémas pour définir les limites de travail, par exemple l’octroi de l’autorisation au schéma est un compromis approprié entre le niveau de la table et le niveau de base de données.  
  
-   Accorder des autorisations aux rôles plutôt qu’à des utilisateurs ou des connexions. Gestion des droits à l’aide de rôles au lieu d’utilisateurs facilite la rapidement accorder ou révoquer un jeu d’autorisations pour un utilisateur ou d’une connexion en les déplaçant vers ou à partir du rôle. Quand une fonction passe à partir d’une personne à l’autre, les autorisations peuvent rester intactes au niveau du rôle pendant les modifications de l’appartenance au rôle.  
  
-   Accorder des autorisations aux rôles basés sur la fonction et sur les rôles de groupes de niveau supérieurs qui combinent les rôles de fonction de travail basés sur le groupe d’entreprise en effectuant les actions.  
  
-   Tous les utilisateurs finaux doivent avoir une connexion unique. Ne permettent pas aux utilisateurs de partager des connexions. En fournissant une connexion pour chaque utilisateur garantit une piste d’audit et simplifie la gestion des autorisations.  
  
## <a name="fixed-database-roles"></a>Rôles de base de données fixes
SQL Server fournit des rôles de niveau de base de données (fixes) préconfigurés pour vous aider à gérer les autorisations sur un serveur. Les rôles préconfigurés ont été résolus dans la mesure où vous ne pouvez pas modifier les autorisations affectées. Rôles de base de données défini par l’utilisateur peuvent également être créés. Vous pouvez modifier les autorisations affectées aux rôles de base de données défini par l’utilisateur.  
  
Les rôles sont des entités de sécurité qui regroupent d’autres principaux. Rôles de base de données sont à l’échelle de la base de données dans leur étendue des autorisations. Les utilisateurs de base de données et d’autres rôles de base de données peuvent être ajoutés en tant que membres des rôles de base de données. Les rôles de base de données fixe ne peut pas être ajoutés entre eux. (Les*rôles* sont semblables aux *groupes* du système d’exploitation Microsoft Windows.)  
  
Il existe des rôles de base de données fixe 9.  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>Autorisations des rôles de base de données fixe  
Le système de rôles serveur fixes et rôles de base de données fixe est un système hérité provient dans les années 80. Rôles fixes sont toujours pris en charge et sont utiles dans les environnements où il existe peu d’utilisateurs et les besoins de sécurité sont simples. À compter de SQL Server 2005, un système plus détaillé de l’octroi d’autorisation a été créé. Ce nouveau système est plus granulaire, en fournissant de nombreuses autres options pour l’octroi et refus d’autorisations. La complexité supplémentaire du système plus précis, il est plus difficile à apprendre, mais la plupart des systèmes d’entreprise doivent accorder des autorisations au lieu d’utiliser les rôles fixes. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->Le graphique suivant montre les autorisations qui sont associées à chaque rôle de base de données fixe. Toutes les autorisations dans ce graphique de SQL Server ne sont pas disponibles (ou nécessaire) dans les points d’accès.  
  
![Rôles de base de données fixé de sécurité APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>Contenu associé  
  
-   Pour créer des rôles définis par l’utilisateur, consultez [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Rôles serveur fixes
Rôles serveur fixes sont créés automatiquement par SQL Server. SQL Server PDW a une implémentation limitée de rôles serveur fixes de SQL Server. Uniquement les **sysadmin** et **public** compte de connexion utilisateur en tant que membres. Le **setupadmin** et **dbcreator** sont utilisés en interne par SQL Server PDW. Membres supplémentaires ne peuvent pas être ajoutés ou supprimés à partir de n’importe quel rôle.  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin rôle serveur fixe  
Les membres du rôle serveur fixe **sysadmin** peuvent effectuer n’importe quelle activité sur le serveur. Le **sa** connexion est le seul membre de la **sysadmin** rôle serveur fixe. Impossible d’ajouter des connexions supplémentaires à la **sysadmin** rôle serveur fixe. L’accord de l’autorisation**CONTROL SERVER** s’apparente à une appartenance au rôle serveur fixe **sysadmin**. L’exemple suivant accorde la **CONTROL SERVER** autorisation à une connexion nommée Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> Le **CONTROL SERVER** autorisation fournit un contrôle presque complète de SQL Server PDW. Autant que possible, fournissez les autorisations plus précises pour les connexions à la place. Par exemple, envisagez d’accorder le **VIEW SERVER STATE**, **ALTER ANY LOGIN**, **VIEW ANY DATABASE**, ou **CREATE ANY DATABASE** autorisations.  
  
### <a name="public-server-role"></a>Rôle serveur public  
Chaque nom de connexion peut se connecter à SQL Server PDW est un membre de la **public** rôle de serveur. Toutes les connexions héritent des autorisations accordées à **public** sur n’importe quel objet. Affecter uniquement **public** autorisations sur un objet lorsque vous souhaitez que l’objet soit disponible pour tous les utilisateurs. Vous ne pouvez pas modifier l’appartenance à la **public** rôle.  
  
> [!NOTE]  
> **public** est implémenté différemment des autres rôles. Étant donné que tous les principaux de serveur sont membres du public, l’appartenance de le **public** rôle n’est pas répertorié dans le **sys.server_role_members** DMV.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Visual Studio de rôles de serveur fixe. Octroi d’autorisations  
Le système de rôles serveur fixes et rôles de base de données fixe est un système hérité provient dans les années 80. Rôles fixes sont toujours pris en charge et sont utiles dans les environnements où il existe peu d’utilisateurs et les besoins de sécurité sont simples. À compter de SQL Server 2005, un système plus détaillé de l’octroi d’autorisation a été créé. Ce nouveau système est plus granulaire, en fournissant de nombreuses autres options pour l’octroi et refus d’autorisations. La complexité supplémentaire du système plus précis, il est plus difficile à apprendre, mais la plupart des systèmes d’entreprise doivent accorder des autorisations au lieu d’utiliser les rôles fixes. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>Rubriques connexes  
  
- [Accorder des autorisations](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

