---
title: '@@REMSERVER (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@REMSERVER'
- '@@REMSERVER_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], remote servers
- remote servers [SQL Server], logins
- '@@REMSERVER function'
ms.assetid: 0bb451a9-3866-4064-963d-b74a2f864049
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edc51e80ac7e0753ff110f690566489225b7c1b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688547"
---
# <a name="x40x40remserver-transact-sql"></a>&#x40;&#x40;REMSERVER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Utilisez des serveurs liés et des procédures stockées de serveur lié à la place.  
  
 Retourne le nom du serveur de base de données distant [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tel qu'il apparaît dans l'enregistrement de connexion.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
@@REMSERVER  
```  
  
## <a name="return-types"></a>Types de retour  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Notes   
 @@REMSERVER permet à une procédure stockée de vérifier le nom du serveur de base de données sur lequel la procédure s’exécute.  
  
## <a name="examples"></a>Exemples  
 Cet exemple crée la procédure `usp_CheckServer` qui retourne le nom du serveur distant.  
  
```  
CREATE PROCEDURE usp_CheckServer  
AS  
SELECT @@REMSERVER;  
```  
  
 La procédure stockée suivante est créée sur `SEATTLE1`, le serveur local. L'utilisateur se connecte à un serveur distant, `LONDON2`, et exécute `usp_CheckServer`.  
  
```  
EXEC SEATTLE1...usp_CheckServer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------  
LONDON2  
```  
  
## <a name="see-also"></a> Voir aussi  
 [Fonctions de configuration &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Serveurs distants](../../database-engine/configure-windows/remote-servers.md)  
  
  
