---
title: Concepts CSDLBI | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 2fbdf621-a94d-4a55-a088-3d56d65016ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57ab374fb8ba0e5a75fc9a97300dace76452174b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377001"
---
# <a name="csdlbi-concepts"></a>Concepts CSDLBI
  Le langage CSDL (Conceptual Schema Definition Language) avec annotations Business Intelligence (CSDLBI) est basé sur l'infrastructure de données d'entités (Entity Data Framework), qui est une abstraction pour représenter différents types de données de façon à activer les jeux de données disparates pour qu'ils soient accessibles, interrogés ou exportés par programme. CSDLBI est utilisé pour représenter les modèles de données créés à l'aide d'[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], car il prend en charge les applications et la création de rapports complets pilotée par les données.  
  
 Cette section explique comment la représentation CSDLBI mappe aux modèles de données [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (tabulaires ou multidimensionnels), et fournit des exemples de chaque type de modèle.  
  
 Les exemples utilisés pour illustrer ces concepts proviennent de l'exemple de base de données AdventureWorks, disponible sur Codeplex. Pour plus d’informations sur les exemples, consultez [exemples Adventure Works pour SQL Server](https://go.microsoft.com/fwlink/?linkID=220093).  
  
## <a name="structure-of-a-tabular-model-in-csdlbi"></a>Structure d'un modèle tabulaire en CSDLBI  
 Document CSDLBI qui décrit un modèle de rapport. Ses données commencent par l'instruction XSD, suivie de la définition d'un modèle.  
  
 Le modèle est un espace de noms qui contient les entités, les associations et les propriétés principales suivantes :  
  
-   `EntityContainer` répertorie les tables contenues dans le modèle.  
  
-   Chaque table apparaît avec `EntityContainer` comme `EntitySet`.  
  
-   Chaque relation entre deux tables est décrite comme un `AssociationSet` définissant les points de terminaison de relation et les rôles de relation.  
  
-   L'élément `EntityType` est étendu pour que BISM fournisse des détails supplémentaires sur les tables et les colonnes qu'il contient, y compris les propriétés de tri et d'affichage.  
  
-   L'élément `Measure` définit les calculs qui peuvent être utilisés dans le modèle. Une mesure peut être transformée en indicateur de performance clé en ajoutant un jeu d'attributs d'affichage spécial, à l'aide du nouvel élément `KPI`.  
  
-   Il n'y a pas de représentation distincte des perspectives. Les colonnes et les tables qui ne sont pas incluses dans une perspective sont présentes dans le langage CSDL mais marquées avec l'attribut `Hidden`.  
  
### <a name="entities-entitysets-and-entitytypes"></a>Entités, EntitySets et EntityTypes  
 La notion d'entité dans l'infrastructure de données d'entité Entity Data Framework est étendue pour représenter des colonnes et des tables de données. L'extrait suivant affiche la liste des éléments `EntitySet` dans un modèle simple contenant uniquement trois tables.  
  
```  
<EntityContainer Name="SimpleModel">  
<EntitySet Name="DimCustomer"EntityType="SimpleModel.DimCustomer">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimDate" EntityType="SimpleModel.DimDate">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimGeography" EntityType="SimpleModel.DimGeography">  
     <bi:EntitySet />  
   </EntitySet> />  
  
```  
  
 L'`EntitySet` ne contient pas d'informations sur les colonnes ou les données de la table. La description détaillée des colonnes et leurs propriétés est fournie dans l'élément EntityType.  
  
 L'élément `EntitySet` pour chaque entité (table) inclut une collection de propriétés qui définissent la colonne clé, le type de données et la longueur de la colonne, la possibilité de valeur NULL, le comportement de tri, etc. Par exemple, l'extrait CSDL suivant décrit trois colonnes dans la table Customer. La première colonne est une colonne masquée spéciale utilisée en interne par le modèle.  
  
```  
<EntityType Name="Customer">  
  <Key>  
     <PropertyRef Name="RowNumber" />  
  </Key>  
    <Property Name="RowNumber" Type="Int64" Nullable="false">  
     <bi:Property Hidden="true" Contents="RowNumber"  
       Stability="RowNumber" />  
    </Property>  
    <Property Name="CustomerKey" Type="Int64" Nullable="false">  
      <bi:Property />  
    </Property>  
     <Property Name="FirstName" Type="String" MaxLength="Max" FixedLength="false">  
       <bi:Property />  
      </Property>  
  
```  
  
 Pour limiter la taille du document CSDLBI généré, les propriétés qui apparaissent plus d'une fois dans une entité sont spécifiées par une référence à une propriété existante, afin que la propriété soit répertoriée une seule fois pour l'`EntityType`. L'application cliente peut obtenir la valeur de la propriété en recherchant l'`EntityType` qui représente l'`OriginEntityType`.  
  
### <a name="relationships"></a>Relations  
 Dans l’Entity Data Framework, les relations sont définies comme *associations* entre des entités.  
  
 Les associations ont toujours exactement deux terminaisons, chacune pointant sur un champ ou colonne dans une table. Par conséquent, plusieurs relations sont possibles entre deux tables, si les relations ont des points de terminaison différents. Un rôle de nom est affecté aux points de terminaison de l'association, et indique comment l'association est utilisée dans le contexte du modèle de données. Un exemple de nom de rôle peut être **ShipTo**, lorsqu’il est appliqué à un ID de client qui est lié à l’ID de client dans une table de commandes.  
  
 La représentation CSDLBI du modèle contient également les attributs de l’association qui déterminent la façon dont les entités sont mappées entre eux en termes de la *multiplicité* de l’association. La pluralité indique si l'attribut ou la colonne au point de terminaison d'une relation entre des tables se trouve du côté « un » d'une relation ou du côté « plusieurs ». Il n'y a aucune valeur distincte pour les relations un-à-un. Les annotations CSDLBI prennent en charge la pluralité 0 (ce qui signifie que l'entité n'est associée à aucun élément) ou bien 0..1, ce qui indique soit une relation un-à-un, soit une relation un-à-plusieurs.  
  
 L'exemple suivant représente la sortie CSDLBI d'une relation entre les tables, Date et ProductInventory, où les deux tables sont jointes sur la colonne DateAlternateKey. Notez que, par défaut, le nom de l'`AssociationSet` est le nom complet des colonnes impliquées dans la relation. Toutefois, vous pouvez modifier ce comportement lorsque vous concevez le modèle et utiliser un format de nom différent.  
  
```  
<AssociationSet Name="ProductInventory_Date_DateKey" Association="Model.ProductInventory_Date_DateKey">  
              <End EntitySet="ProductInventory" />  
              <End EntitySet="Date" />  
              <bi:AssociationSet />  
            </AssociationSet>  
  
```  
  
### <a name="visualization-and-navigation-properties"></a>Propriétés de visualisation et de navigation  
 Une partie importante des extensions CSDLBI sont les propriétés qui définissent la présentation dans la couche de rapports et la navigation dans les relations entre les entités. En règle générale, lorsque vous créez un modèle de données, il n'est pas important de contrôler la façon dont les données sont ordonnées ou regroupées, ou quelle sera la valeur par défaut, car l'application cliente est supposée spécifier l'ordre et d'autres détails de présentation. Toutefois, les modèles tabulaires de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sont conçus pour assurer l'intégration avec le client de création de rapports [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] et incluent des propriétés et des attributs qui prennent en charge la présentation des entités du modèle de données dans l'aire de conception du rapport.  
  
 Les extensions de visualisation incluent des attributs qui spécifient l'agrégation par défaut utilisée avec des données numériques, qui indiquent qu'un champ de texte pointe vers une URL ou une image ou qui spécifient le champ utilisé pour trier le champ actuel.  
  
### <a name="name-properties-and-naming-conventions"></a>Propriétés Name et conventions d'affectation des noms  
 Le schéma CSDLBI garantit que chaque entité a un nom et un identificateur unique qui peuvent être utilisés comme clés. En outre, certaines entités peuvent avoir des légendes utilisées pour l'affichage et des noms contextuels qui changent selon l'endroit où l'entité est utilisée.  
  
 L'élément `Documentation` permet aux concepteurs de rapports de fournir une description de l'entité, pour aider les utilisateurs professionnels à comprendre la signification des données. Certaines entités permettent aussi d'utiliser un ou plusieurs attributs `Annotation`, qui fournissent des métadonnées supplémentaires pour la consommation par l'application ou par les clients.  
  
 Lorsque vous générez un modèle avec les outils [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], les noms créés pour les objets suivent les conventions d'[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] relatives à l'affectation de noms et à leur unicité. Toutefois, étant donné que le langage CSDLBI repose sur l'infrastructure de données d'entités Entity Data Framework, qui exige que les noms adhèrent aux conventions applicables aux identificateurs C#, lorsque le serveur crée la sortie CSDLBI pour un modèle, il prend les noms utilisés dans le schéma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] et crée automatiquement de nouveaux noms d'objets conformes aux spécifications Entity Data Framework. Le tableau suivant décrit les opérations grâce auxquelles les nouveaux noms sont générés.  
  
|Règle|Action|  
|----------|------------|  
|Aucun caractère interdit|Les caractères interdits sont remplacés par le trait de soulignement.|  
|Les noms doivent être uniques|Si deux chaînes sont identiques, l'une d'entre elles est rendue unique en ajoutant le trait de soulignement plus un nombre|  
  
> [!WARNING]  
>  Les légendes et les qualificateurs sont traduits et, pour une langue donnée, une traduction ou bien une autre peut être présente. Cela signifie que dans les cas où un qualificateur et un nom ou un qualificateur et une légende sont concaténés, les chaînes peuvent être dans deux langues différentes.  
  
## <a name="additions-to-support-multidimensional-models"></a>Ajouts pour prendre en charge les modèles multidimensionnels  
 La version 1.0 des annotations CSDLBI prenait uniquement en charge les modèles tabulaires. Dans la version 1.1., la prise en charge a été ajoutée pour les modèles multidimensionnels (cubes OLAP) créés à l'aide des outils de développement Business Intelligence traditionnels. Par conséquent, vous pouvez maintenant émettre une demande XML dans un modèle multidimensionnel et recevoir une définition CSDLBI du modèle, à utiliser lors de la création de rapports.  
  
 **Cubes :** Un serveur SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de données tabulaire peut contenir qu’un seul mode. En revanche, chaque base de données multidimensionnelle peut contenir plusieurs cubes, chaque base de données étant associée à un cube par défaut. Par conséquent, lorsque vous exécutez une requête XML sur un serveur multidimensionnel, vous devez spécifier le cube ; sinon, le code XML du cube par défaut est retourné.  
  
 La représentation d'un cube est similaire à celle d'une base de données model tabulaire. Le nom du cube et le cube correspondent au nom de la base de données tabulaire et à l'identificateur de la base de données.  
  
 **Dimensions :** Une dimension est représentée en CSDLBI en tant qu’entité (table) avec des colonnes et des propriétés. Notez que, même si elle n'est pas incluse dans une perspective, une dimension qui est incluse dans le modèle est représentée dans la sortie CSDL, marquée comme étant `Hidden`.  
  
 **Perspectives :** Un client peut demander CSDL pour des perspectives individuelles. Pour plus d’informations, consultez [ensemble de lignes DISCOVER_CSDL_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset).  
  
 **Hiérarchies :** Hiérarchies sont pris en charge et représentées en CSDLBI en tant qu’ensemble de niveaux.  
  
 **Membres :** Prise en charge pour le membre par défaut a été ajoutée et les valeurs par défaut sont automatiquement ajoutées à la sortie CSDLBI.  
  
 **Membres calculés :** Les modèles multidimensionnels prennent en charge les membres calculés pour l’enfant de **tous les** avec un membre réel unique.  
  
 **Attributs de dimension :** Dans la sortie CSDLBI, les attributs de dimension sont pris en charge et automatiquement marquées comme non regroupable.  
  
 **Indicateurs de performance clés :** Indicateurs de performance clés étaient pris en charge en CSDLBI version 1.1, mais la représentation a changé. Avant, un indicateur de performance clé était la propriété d'une mesure. Dans la version 1.1, l’élément KPI peut être ajouté à une mesure  
  
 **Nouvelles propriétés :** Les attributs supplémentaires ont été ajoutés pour prendre en charge les modèles DirectQuery.  
  
 **Limitations :** Sécurité de cellule n’est pas prise en charge.  
  
## <a name="see-also"></a>Voir aussi  
 [Annotations CSDL pour Business Intelligence &#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
  
