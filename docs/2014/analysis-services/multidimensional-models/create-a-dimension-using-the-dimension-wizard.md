---
title: Créer une Dimension à l’aide de l’Assistant Dimension | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], creating
ms.assetid: d84f66ae-7551-49bf-99d0-88368ca2dd0e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad05272b38a2f3dec72c4be160f48981e4fd43a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118065"
---
# <a name="create-a-dimension-using-the-dimension-wizard"></a>Créer une dimension à l'aide de l'Assistant Dimension
  Vous pouvez créer une dimension en utilisant l'Assistant Dimension dans [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-create-a-new-dimension"></a>Pour créer une dimension  
  
1.  Dans l’ **Explorateur de solutions**, cliquez avec le bouton droit sur **Dimensions**, puis cliquez sur **Nouvelle dimension**.  
  
2.  Dans la page **Sélectionner la méthode de création** de l’Assistant Dimension, sélectionnez **Utiliser une table existante**, puis cliquez sur **Suivant**.  
  
    > [!NOTE]  
    >  Parfois, vous devrez peut-être créer une dimension sans utiliser de table existante. Pour plus d’informations, consultez [Créer une dimension en générant une table non temporelle dans la source de données](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md) et [Créer une dimension de temps en générant une table de temps](create-a-time-dimension-by-generating-a-time-table.md).  
  
3.  Dans la page **Spécifier des informations sur la source** , exécutez les procédures suivantes :  
  
    1.  Dans la liste **Vue de source de données** , sélectionnez une vue de source de données.  
  
    2.  Dans la liste **Table principale** , sélectionnez la table de dimension principale.  
  
    3.  Dans la liste **Colonnes clés** , examinez les colonnes clés que l’Assistant a sélectionnées automatiquement selon la clé primaire qui est définie dans la table de dimension principale. Pour modifier ce paramètre par défaut, spécifiez les colonnes clés qui lient la table de dimension à la table de faits.  
  
    4.  Dans la liste déroulante **Colonne de nom** , examinez la colonne de nom que l’Assistant a sélectionnée automatiquement.  
  
         Ce nom par défaut est approprié lorsque la colonne contient des informations descriptives. Toutefois, vous pouvez souhaiter spécifier un nom qui contient des valeurs qui sont plus explicites pour l'utilisateur final. Par exemple, si un attribut de catégorie de produit d’une dimension Products utilise la colonne **ProductCategoryKey** en tant que colonne clé, vous pouvez spécifier la colonne **ProductCategoryName** en tant que colonne de nom.  
  
         Si la liste **Colonnes clés** contient plusieurs colonnes clés, vous devez spécifier une colonne de nom qui fournit les valeurs d’un membre pour l’attribut de clé. Pour cela, vous pouvez créer un calcul nommé dans la vue de source de données et l'utiliser comme colonne de nom.  
  
    5.  Cliquez sur **Suivant**.  
  
4.  Dans la page **Sélectionner les tables associées** , sélectionnez les tables associées à inclure dans votre dimension, puis cliquez sur **Suivant**.  
  
    > [!NOTE]  
    >  La page **Sélectionner les tables associées** apparaît si la table de dimension principale que vous avez spécifiée a des relations avec d’autres tables de dimension.  
  
5.  Dans la page **Sélectionner les attributs de la dimension** , sélectionnez les attributs associés à inclure dans la dimension, puis cliquez sur **Suivant**.  
  
     Vous pouvez éventuellement modifier les noms d'attribut, activer ou désactiver l'exploration et spécifier le type d'attribut.  
  
    > [!NOTE]  
    >  Pour activer les champs **Permettre la navigation** et **Type d’attribut** d’un attribut, l’attribut doit être sélectionné pour être inclus dans la dimension.  
  
6.  Dans la page **Définir l’intelligence comptable** , dans la colonne **Types de comptes intégrés** , sélectionnez le type de compte, puis cliquez sur **Suivant**.  
  
     Le type de compte doit correspondre au type de compte de la table source qui est répertorié dans la colonne **Types de comptes de la table source** .  
  
    > [!NOTE]  
    >  La page **Définir l’intelligence comptable** apparaît si vous avez défini un attribut de dimension **Type de compte** dans la page **Sélectionner les attributs de la dimension** de l’Assistant.  
  
7.  Dans la page **Fin de l’Assistant** , entrez le nom de la nouvelle dimension et examinez sa structure. Si vous souhaitez apporter des modifications, cliquez sur **Précédent**; sinon, cliquez sur **Terminer**.  
  
    > [!NOTE]  
    >  Vous pouvez utiliser le Concepteur de dimensions après avoir terminé l'Assistant Dimension pour ajouter, supprimer et configurer des attributs et des hiérarchies dans la dimension.  
  
## <a name="see-also"></a>Voir aussi  
 [Créer une dimension à l’aide d’une table existante](create-a-dimension-by-using-an-existing-table.md)  
  
  
