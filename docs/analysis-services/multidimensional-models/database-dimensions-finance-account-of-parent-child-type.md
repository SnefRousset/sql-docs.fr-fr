---
title: Créer un compte Finance de la Dimension de type parent-enfant | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a9db268d931d46f6254501e95d68739c3e71db3b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52517230"
---
# <a name="database-dimensions---finance-account-of-parent-child-type"></a>Dimensions de base de données - compte Finance de type parent-enfant
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Dans [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], une dimension de type compte est une dimension dont les attributs représentent un graphique de comptes utilisé à des fins de génération de rapports financiers.  
  
 Une dimension de comptes permet de gérer dans le temps et de manière sélective le comportement de l'agrégation dans les comptes. Un compte de dimensions permet également d'utiliser un mécanisme standard pour résoudre la plupart des problèmes d'agrégation non standard associés généralement aux solutions décisionnelles qui gèrent des données financières. Si vous ne disposiez pas d'un tel mécanisme standard, la résolution des problèmes d'agrégation non standard nécessiterait des formules de cumul personnalisées, des membres calculés ou des scripts d'expression multidimensionnelle (MDX, Multidimensional Expressions).  
  
 Pour définir une dimension sous la forme d’une dimension de comptes, affectez à la propriété **Type** de la dimension la valeur **Accounts**.  
  
## <a name="dimension-structure"></a>Structure de la dimension  
 Une dimension de comptes contient au moins deux attributs :  
  
-   Un attribut un attribut de clé qui identifie les comptes individuels dans la table de dimension pour la dimension de compte.  
  
-   Un attribut d’un attribut parent de compte qui décrit la façon dont les comptes sont organisés hiérarchiquement dans la dimension account.  
  
     Pour définir un attribut comme attribut de compte, affectez à la propriété **Type** de l’attribut la valeur **Account** et à la propriété **Usage** , la valeur **Parent**.  
  
 Les dimensions de comptes peuvent éventuellement contenir les attributs suivants :  
  
-   Un attribut un attribut de type compte qui définit le type de compte pour chaque compte de la dimension. Les noms des membres de l’attribut de type de compte sont associés aux types de comptes définis pour la base de données ou le projet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , et indiquent la fonction d’agrégation utilisée par [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pour ces comptes. Vous pouvez également utiliser des opérateurs unaires ou des formules de cumul personnalisées pour déterminer le comportement d'agrégation des attributs de comptes, mais les types de comptes permettent d'appliquer aisément un comportement cohérent à un graphique de comptes sans avoir à modifier la base de données relationnelle sous-jacente.  
  
     Pour identifier un attribut de type de compte, affectez à la propriété **Type** de l’attribut la valeur **AccountType**.  
  
-   Un nom attribut un attribut de compte qui est utilisé pour générer des rapports. Pour identifier un attribut de nom de compte, affectez à la propriété **Type** de l’attribut la valeur **AccountName**.  
  
-   Un compte numéro attribut un attribut qui est utilisé pour générer des rapports. Pour identifier un attribut de numéro de compte, affectez à la propriété **Type** de l’attribut la valeur **AccountNumber**.  
  
 Pour plus d’informations sur les types d’attributs, consultez [Configurer des types d’attributs](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md).  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>Ajout de l'intelligence comptable avec l'Assistant Business Intelligence  
 Après avoir défini une dimension de comptes et ajouté la dimension à un cube, vous pouvez utiliser l’Assistant Business Intelligence pour ajouter des fonctions d’intelligence comptable, telles que l’identification et le mappage de types de comptes, à la dimension. Pour plus d’informations, consultez [Ajouter de l’intelligence comptable à une dimension](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Attributs et hiérarchies d'attributs](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Aide (F1) de l'Assistant Business Intelligence](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [Types de dimensions](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
