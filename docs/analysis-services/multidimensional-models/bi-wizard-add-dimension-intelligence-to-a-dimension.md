---
title: "Ajouter l’Intelligence des dimensions à une Dimension | Documents Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Business Intelligence enhancements [Analysis Services], dimension intelligence
- dimensions [Analysis Services], Business Intelligence enhancements
- dimension intelligence [Analysis Services]
- Type property
ms.assetid: b64fa386-eac2-4286-a320-0631a1887aac
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1d167da0ab38819f016dd4a0c18c2e65ef42da1
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="bi-wizard---add-dimension-intelligence-to-a-dimension"></a>Assistant BI - ajouter l’Intelligence des dimensions à une Dimension
  Ajoutez l'intelligence des dimensions à un cube ou à une dimension pour spécifier un type d'entreprise standard pour une dimension. Cette amélioration spécifie également les types correspondants pour les attributs de la dimension. Les applications clientes peuvent utiliser ces spécifications de type lors de l'analyse de données.  
  
 Pour ajouter l’intelligence des dimensions, utilisez l’Assistant Business Intelligence, puis sélectionnez l’option **Définir l’intelligence des dimensions** dans la page **Choisir des améliorations** . Cet Assistant vous guide tout au long des étapes de sélection d'une dimension à laquelle vous souhaitez appliquer l'intelligence des dimensions et d'identification des attributs pour la dimension sélectionnée.  
  
## <a name="selecting-a-dimension"></a>Sélection d'une dimension  
 Dans la première page **Définir les options d’intelligence des dimensions** de l’Assistant, vous spécifiez la dimension à laquelle vous souhaitez appliquer l’intelligence des dimensions. L'amélioration que constitue l'intelligence des dimensions ajoutée à cette dimension se traduit par des modifications de la dimension. Ces modifications seront héritées par tous les cubes contenant la dimension sélectionnée.  
  
> [!NOTE]  
>  Si vous sélectionnez **Compte** comme dimension, vous spécifierez l’intelligence comptable pour la dimension. Pour plus d’informations, consultez [Ajouter de l’intelligence comptable à une dimension](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="specifying-dimension-attributes"></a>Spécification des attributs de dimension  
 Dans la page **Définir l’intelligence des dimensions** , dans la liste **Type de dimension** , la sélection que vous effectuez définit la propriété **Type** de la dimension. La définition de la propriété **Type** fournit des informations aux serveurs et aux applications clientes sur le contenu d’une dimension. Certains paramètres permettent uniquement de guider les applications clientes ; ces paramètres sont facultatifs. D'autres paramètres, tels que Comptes ou Temps, déterminent des comportements spécifiques et peuvent être requis pour implémenter des améliorations de décisionnel particulières. Par exemple, SQL Server Management Studio utilise le type de dimension pour identifier une dimension Devise et définir les règles de conversion monétaire appropriées. La définition par défaut du **Type de dimension** est **Normal**et ne fournit aucune information théorique sur le contenu de la dimension.  
  
 Après avoir sélectionné le type de dimension, dans **Attributs de la dimension**, dans la colonne **Inclure** , cochez la case à côté de chaque type d’attribut standard pour lequel il existe un attribut correspondant dans la dimension. Enfin, dans la colonne **Attribut de dimension** , développez la liste déroulante, puis sélectionnez l’attribut de la dimension qui correspond au type d’attribut sélectionné. La sélection de l’attribut dans la liste définit la propriété **Type** pour les attributs.  
  
 Par exemple, vous souhaitez ajouter l'intelligence des dimensions à une dimension Comptes. Dans **Type de dimension**, vous sélectionnez **Comptes**. Ensuite, si la dimension a les attributs **Type de compte** et **Description du compte** , dans la colonne **Inclure** , cochez les cases pour les types de comptes **Nom du compte** et **Type de compte** . Dans la colonne **Attribut de dimension** , vous associez ensuite ces types de comptes aux attributs **Description du compte** et **Type de compte** , respectivement, dans la dimension.  
  
## <a name="see-also"></a>Voir aussi  
 [Définir des calculs Time Intelligence à l'aide de l'Assistant Business Intelligence](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)  
  
  