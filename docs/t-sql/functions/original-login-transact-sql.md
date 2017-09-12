---
title: ORIGINAL_LOGIN (Transact-SQL) | Documents Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1f97da47505e5c812e43f4481d9f36027bf14c9
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Renvoie le nom de la connexion qui s'est connectée à l'instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vous pouvez utiliser cette fonction pour renvoyer l'identité de la connexion d'origine dans les sessions où il y a un grand nombre de changements de contexte implicites ou explicites.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>Types de retour  
 **sysname**  
  
## <a name="remarks"></a>Notes  
 Cette fonction peut s'avérer utile pour auditer l'identité du contexte de connexion d'origine. Alors que les fonctions telles que [SESSION_USER](../../t-sql/functions/session-user-transact-sql.md) et [CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md) retour le contexte d’exécution actuel ORIGINAL_LOGIN renvoie l’identité de la connexion tout d’abord être connecté à l’instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dans cette session.  
  
 Retourne la valeur NULL sur [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
## <a name="examples"></a>Exemples  
 L'exemple suivant change le contexte d'exécution de la session actuelle de l'appelant des instructions vers `login1`. Les fonctions `SUSER_SNAME` et `ORIGINAL_LOGIN` sont utilisées pour renvoyer l'utilisateur de la session actuelle (l'utilisateur vers lequel le contexte a été basculé) et le compte de connexion d'origine.  
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>Voir aussi  
 [EXECUTE AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [Rétablir &#40; Transact-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  