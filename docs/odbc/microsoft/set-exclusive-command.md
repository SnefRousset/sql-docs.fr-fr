---
title: SET EXCLUSIVE, commande | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fccbc9b258cbff1e14ccc76e10af9d26efc4b70b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618817"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE, commande
Spécifie si les fichiers de la table sont ouverts pour une utilisation exclusive ou partagée sur un réseau.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Arguments  
 ON  
 Limite d’accessibilité d’une table ouverte sur un réseau à l’utilisateur qui l’avez ouverte. La table n’est pas accessible à d’autres utilisateurs sur le réseau. SET de ON exclusif empêche également tous les autres utilisateurs ayant un accès en lecture seule.  
  
 OFF  
 (Valeur par défaut pour le pilote ; les valeurs par défaut pour Visual FoxPro sont ON pour la session de données globales et désactivée (OFF) pour une session de données privées). Permet à une table est ouverte sur un réseau partagé et modifiés par n’importe quel utilisateur sur le réseau.  
  
## <a name="remarks"></a>Notes  
 Modification du paramètre de valeur exclusif ne change pas l’état des tables précédemment ouverts. Par exemple, si une table est ouvert avec définir exclusif la valeur ON et définissez exclusif est modifié ultérieurement à OFF, la table conserve son état de l’usage exclusif.  
  
## <a name="see-also"></a>Voir aussi  
 [Configuration d’ODBC pour Visual FoxPro, boîte de dialogue](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
