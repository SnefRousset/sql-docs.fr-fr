---
title: ALTER CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER CREDENTIAL
- ALTER_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], credentials
- credentials [SQL Server], ALTER CREDENTIAL statement
- modifying credentials
- authentication [SQL Server], credentials
- ALTER CREDENTIAL statement
ms.assetid: b08899a6-c09e-4af4-91aa-a978ada79264
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 32df63456e46fd8f522d897cd6068967bbb785b0
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411846"
---
# <a name="alter-credential-transact-sql"></a>ALTER CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Modifie les propriétés d'une information d'identification.  

> [!IMPORTANT]
> Les bonnes pratiques sont des pratiques recommandées ; d’autres sont obligatoires pour effectuer la tâche. ![Icône du lien de la rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône du lien de la rubrique")[Conventions syntaxiques de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
ALTER CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>Arguments  
 *credential_name*  
 Spécifie le nom d'une information d'identification à modifier.  
  
 IDENTITY **='***identity_name***'**  
 Spécifie le nom du compte à utiliser lors d'une connexion en dehors du serveur.  
  
 SECRET **='***secret***'**  
 Spécifie le secret requis pour l'authentification sortante. *secret* est facultatif.
  
> [!IMPORTANT]
> Azure SQL Database ne prend en charge que les identités de type signature d’accès partagé et Azure Key Vault. Les identités d’utilisateur Windows ne sont pas prises en charge.
  
## <a name="remarks"></a>Notes   
 Quand des informations d’identification sont modifiées, les valeurs d’*identity_name* et de *secret* sont réinitialisées. Si l'argument facultatif SECRET n'est pas spécifié, sa valeur stockée est NULL.  
  
 Le secret est chiffré au moyen de la clé principale du service. Si cette clé est regénérée, le secret est à nouveau chiffré à l'aide de la nouvelle clé principale du service.  
  
 Des informations sur les informations d’identification sont consultables dans la vue de catalogue **sys.credentials**.  
  
## <a name="permissions"></a>Permissions  
 Requiert l'autorisation ALTER ANY CREDENTIAL. Si l'information d'identification est une information d'identification système, l'autorisation CONTROL SERVER est requise.  
  
## <a name="examples"></a>Exemples  
  
### <a name="a-changing-the-password-of-a-credential"></a>A. Modification du mot de passe d'une information d'identification  
 Le code exemple suivant modifie le secret stocké dans l'information d'identification nommée `Saddles`. L'information d'identification contient la connexion Windows `RettigB` et son mot de passe. Le nouveau mot de passe est ajouté à l'information d'identification à l'aide de la clause SECRET.  
  
```  
ALTER CREDENTIAL Saddles WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. Suppression du mot de passe d'une information d'identification  
 Le code exemple suivant supprime le mot de passe de l'information d'identification nommée `Frames`. L'information d'identification contient la connexion Windows `Aboulrus8` et un mot de passe. Après l'exécution de l'instruction, le mot de passe de l'information d'identification a la valeur NULL car l'option SECRET n'est pas spécifiée.  
  
```  
ALTER CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a> Voir aussi  
 [Informations d’identification &#40;moteur de base de données&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
