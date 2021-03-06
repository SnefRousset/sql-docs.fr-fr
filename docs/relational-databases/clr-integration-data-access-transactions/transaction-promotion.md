---
title: Promotion des transactions | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 893068965ab4566b6f6e4f78e39141de9be2b6ed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855267"
---
# <a name="transaction-promotion"></a>Promotion des transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La *promotion* des transactions décrit une transaction locale légère qui peut être promue automatiquement en une transaction entièrement distribuable si nécessaire. Lorsqu'une procédure stockée managée est appelée au sein d'une transaction de base de données sur le serveur, le CLR s'exécute dans le contexte d'une transaction locale.  Si une connexion à un serveur distant est ouverte dans une transaction de base de données, la connexion au serveur distant est inscrite dans la transaction distribuée et la transaction locale est promue automatiquement en une transaction distribuée. Ainsi, la promotion des transactions réduit les charges mémoire des transactions distribuées en différant la création d'une transaction distribuée tant qu'elle n'est pas nécessaire. La promotion des transactions est automatique, si elle a été activée à l'aide du mot clé **Enlist** , et ne requiert aucune intervention du développeur. Le fournisseur de données .NET Framework pour [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prend en charge la promotion des transactions, gérée via les classes dans le .NET Framework **System.Data.SqlClient** espace de noms.  
  
## <a name="the-enlist-keyword"></a>Mot clé Enlist  
 La propriété **ConnectionString** d'un objet **SqlConnection** prend en charge le mot clé **Enlist** , qui indique si **System.Data.SqlClient** détecte les contextes transactionnels et inscrit automatiquement la connexion dans une transaction distribuée. Si le mot clé est défini avec la valeur true (valeur par défaut), la connexion est automatiquement inscrite dans le contexte de transaction actif du thread d'ouverture. S'il est défini avec la valeur false, la connexion SqlClient n'interagit pas avec une transaction distribuée. Si **Enlist** n'est pas spécifié dans la chaîne de connexion, la connexion est inscrite automatiquement dans une transaction distribuée si celle-ci est détectée au moment où la connexion est ouverte.  
  
## <a name="distributed-transactions"></a>Transactions distribuées  
 Les transactions distribuées consomment en général d'importantes ressources système. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) gère ces transactions et intègre tous les gestionnaires de ressources qui y sont accédés. Promotion des transactions, est en revanche, une forme spéciale d’un **System.Transactions** transaction qui délègue efficacement le travail à une simple [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transaction. **System.Transactions**, **System.Data.SqlClient**, et [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coordonner le travail impliqué dans la gestion de la transaction, la promotion à une transaction entièrement distribuée en fonction des besoins.  
  
 L'avantage de l'utilisation de la promotion des transaction est que lorsqu'une connexion est ouverte avec une transaction **TransactionScope** active et qu'aucune autre connexion n'est ouverte, la transaction est validée comme transaction légère, au lieu d'encourir les charges mémoire supplémentaires d'une transaction distribuée complète. Pour plus d’informations sur **TransactionScope**, consultez [à l’aide de System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Intégration et transactions du CLR](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
