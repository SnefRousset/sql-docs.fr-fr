---
title: Programme d’administration | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 740a09d9a6bceb9d3f290faa71444df0d1e7c6c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792317"
---
# <a name="administration-program"></a>Programme d’administration
> [!NOTE]  
>  ODBC à partir de Windows XP et Windows Server 2003, est inclus dans le système d’exploitation Windows. Vous devez explicitement uniquement installer ODBC dans les versions antérieures de Windows.  
  
 Un programme d’administration, l’administrateur ODBC, est inclus dans le Kit de développement Windows SDK/MDAC. Ce programme et peut être redistribué par les utilisateurs du SDK. En outre, les développeurs peuvent écrire leurs propres programmes d’administration. En règle générale, les développeurs écrivent leurs propres programmes d’administration uniquement s’ils veulent garder un contrôle total sur la configuration de source de données, ou si elles sont configuration des sources de données directement à partir d’une application qui agit comme un programme d’administration. Par exemple, un programme de feuille de calcul peut autoriser les utilisateurs à ajouter, puis utiliser les sources de données en cours d’exécution.  
  
 Le programme d’administration du premier charge de la DLL d’installation. Il appelle ensuite les fonctions dans le programme d’installation DLL pour effectuer les tâches suivantes :  
  
-   **Ajouter, modifier ou supprimer des sources de données de manière interactive.** Le programme d’administration peut appeler **SQLManageDataSources**, **SQLCreateDataSource**, ou **SQLConfigDataSource**.  
  
     **SQLManageDataSources** affiche une boîte de dialogue avec laquelle l’utilisateur peut ajouter, modifier, ou supprimer des sources de données et spécifiez les options de suivi ; cette fonction est appelée lorsque le programme d’installation DLL est appelée directement à partir du panneau. **SQLCreateDataSource** affiche une boîte de dialogue avec laquelle l’utilisateur peut uniquement ajouter des sources de données. **SQLConfigDataSource** passe l’appel directement à la DLL d’installation du pilote.  
  
     Dans tous les cas, le programme d’installation DLL appelle **ConfigDSN** dans la configuration du pilote DLL pour ajouter, modifier ou supprimer la source de données. La DLL d’installation du pilote peut inviter l’utilisateur pour des informations supplémentaires.  
  
-   **Ajouter, modifier ou supprimer des sources de données en mode silencieux.** Le programme d’administration appelle **SQLConfigDataSource** dans la DLL d’installation et la passe il une fenêtre nulle gère, le nom de source de données à ajouter, modifier ou supprimer et une liste de valeurs pour le Registre. Les appels DLL du programme d’installation **ConfigDSN** dans la configuration du pilote DLL pour ajouter, modifier ou supprimer la source de données.  
  
-   **Ajouter, modifier ou supprimer une source de données par défaut.** La source de données par défaut est le même que toute autre source de données, à ceci près que son nom est la valeur par défaut. Il est ajouté, modifié ou supprimé de la même manière que toute autre source de données.
