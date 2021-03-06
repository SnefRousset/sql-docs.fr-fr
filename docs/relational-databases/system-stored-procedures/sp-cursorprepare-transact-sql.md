---
title: sp_cursorprepare (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1f26ada2f116d684091f7e5e928d04e3530567f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535505"
---
# <a name="spcursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Compile le lot ou l'instruction de curseur dans un plan d'exécution, mais ne crée pas le curseur. L'instruction compilée peut être utilisée ultérieurement par sp_cursorexecute. Cette procédure, couplée avec sp_cursorexecute, a la même fonction que sp_cursoropen, mais est fractionnée en deux phases. sp_cursorprepare est appelée en spécifiant ID = 3 dans un paquet data stream (TDS).  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>Arguments  
 *prepared_handle*  
 Un généré par SQL Server préparée *gérer* identificateur qui retourne une valeur entière.  
  
> [!NOTE]  
>  *prepared_handle* est fournie par la suite à une procédure sp_cursorexecute pour ouvrir un curseur. Une fois un handle créé, il existe jusqu'à ce que vous vous déconnectiez ou que vous le supprimiez de façon explicite par le biais d'une procédure sp_cursorunprepare.  
  
 *params*  
 Identifie des instructions paramétrables. Le *params* définition de variables est substituée aux marqueurs de paramètre dans l’instruction. *params* est un paramètre obligatoire qui demande un **ntext**, **nchar**, ou **nvarchar** valeur d’entrée. Entrez une valeur NULL si l'instruction n'est pas paramétrable.  
  
> [!NOTE]  
>  Utilisez un **ntext** chaîne comme entrée valeur lorsque *stmt* est paramétré et le *scrollopt* parameterized_stmt est ON.  
  
 *stmt*  
 Définit le jeu de résultats de curseur. Le *stmt* paramètre est obligatoire et demande pour un **ntext**, **nchar** ou **nvarchar** valeur d’entrée.  
  
> [!NOTE]  
>  Les règles de spécification le *stmt* valeur sont les mêmes que celles pour sp_cursoropen, sauf que le *stmt* type de données de chaîne doit être **ntext**.  
  
 *options*  
 Paramètre optionnel qui retourne une description des colonnes du jeu de résultats du curseur. *options* requiert ce qui suit **int** valeur d’entrée.  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Option de défilement. *scrollopt* est un paramètre optionnel qui requiert l’une des opérations suivantes **int** valeurs d’entrée.  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 Étant donné que la valeur demandée ne peut pas être appropriée pour le curseur défini par *stmt*, ce paramètre sert à la fois d’entrée et de sortie. Dans de tels cas, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] affecte une valeur appropriée.  
  
 *ccopt*  
 Option de contrôle en matière d'accès concurrentiel. *ccopt* est un paramètre optionnel qui requiert l’une des opérations suivantes **int** valeurs d’entrée.  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (précédemment appelé LOCKCC)|  
|0x0004|**OPTIMISTE** (anciennement optcc)|  
|0x0008|OPTIMISTIC (précédemment appelé OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Comme avec *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] peut affecter une valeur différente de celle demandée.  
  
## <a name="remarks"></a>Notes  
 Le paramètre d'état RPC prend l'une des valeurs suivantes :  
  
|Value|Description|  
|-----------|-----------------|  
|0|Opération réussie|  
|0x0001|Failure|  
|1FF6|Impossible de retourner des métadonnées.<br /><br /> Remarque : Cela se produit lorsque l'instruction ne produit pas de jeu de résultats ; par exemple, il s'agit d'une instruction INSERT ou DDL.|  
  
## <a name="examples"></a>Exemples  
 Lorsque *stmt* est paramétré et le *scrollopt* parameterized_stmt est ON, le format de la chaîne est comme suit :  
  
 {  *\<nom de variable locale > **\<type de données >* } [,... *n* ]  
  
## <a name="see-also"></a>Voir aussi  
 [sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [Procédures stockées système &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
