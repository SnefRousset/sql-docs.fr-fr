---
title: "Source OLE DB | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.oledbsource.f1"
helpviewer_keywords: 
  - "sources [Integration Services]"
  - "source OLE DB [Integration Services]"
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 69
---
# Source OLE DB
  La source OLE DB extrait des données d'une série de bases de données relationnelles compatibles OLE DB à l'aide d'une table de base de données, d'une vue ou d'une commande SQL. Par exemple, la source OLE DB peut extraire des données de tables de bases de données [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Si la source de données est [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, la source de données requiert un gestionnaire de connexions différent des versions antérieures d'Excel. Pour plus d’informations, consultez [Établir une connexion à un classeur Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 La source OLE DB fournit quatre modes d'accès aux données différents pour l'extraction des données :  
  
-   Une table ou une vue.  
  
-   Une table ou une vue spécifiée dans une variable.  
  
-   Les résultats d'une instruction SQL. La requête peut être une requête paramétrable.  
  
-   Les résultats d'une instruction SQL stockée dans une variable.  
  
> [!NOTE]  
>  Lorsque vous utilisez une instruction SQL pour appeler une procédure stockée qui retourne des résultats à partir d'une table temporaire, utilisez l'option WITH RESULT SETS afin de définir les métadonnées du jeu de résultats.  
  
 Si vous utilisez une requête paramétrable, vous pouvez mapper des variables à des paramètres pour spécifier les valeurs de paramètres individuels dans les instructions SQL.  
  
 Cette source utilise un gestionnaire de connexions OLE DB pour se connecter à une source de données et le gestionnaire de connexions spécifie le fournisseur OLE DB à utiliser. Pour plus d’informations, consultez [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Un projet [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fournit également l'objet de source de données à partir duquel vous pouvez créer un gestionnaire de connexions OLE DB et rendre ainsi les sources de données et les vues de source de données disponibles pour la source OLE DB.  
  
 Selon le fournisseur OLE DB, certaines contraintes s'appliquent à la source OLE DB :  
  
-   Le fournisseur [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB pour Oracle ne prend pas en charge les types de données Oracle BLOB, CLOB, NCLOB, BFILE ou UROWID et la source OLE DB ne peut pas extraire de données des tables qui contiennent des colonnes de ces types de données.  
  
-   Le fournisseur IBM OLE DB DB2 et le fournisseur [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 ne prennent pas en charge l'utilisation d'une commande SQL qui appelle une procédure stockée. Lorsque ce type de commande est utilisé, la source OLE DB ne peut pas créer les métadonnées de colonne ; par conséquent, les composants de flux de données qui suivent la source OLE DB dans le flux de données ne disposent pas de données de colonnes et l'exécution du flux de données échoue.  
  
 La source OLE DB a une sortie normale et une sortie d'erreur.  
  
## Utilisation d'instructions SQL paramétrables  
 La source OLE DB peut utiliser une instruction SQL pour extraire des données. L'instruction peut être une instruction SELECT ou EXEC.  
  
 La source OLE DB utilise un gestionnaire de connexions OLE DB pour établir une connexion à la source de données à partir de laquelle elle extrait des données. Selon le fournisseur que le gestionnaire de connexions OLE DB utilise et le système de gestion de bases de données relationnelles (SGBDR) auquel le gestionnaire de connexions se connecte, différentes règles s'appliquent à la dénomination des paramètres et à la constitution de leur liste. Si les noms des paramètres sont retournés à partir du SGBDR, vous pouvez utiliser des noms de paramètres pour mapper les paramètres d'une liste de paramètres aux paramètres d'une instruction SQL ; sinon, les paramètres sont mappés aux paramètres de l'instruction SQL en fonction de leur position ordinale dans la liste de paramètres. Les types de noms de paramètres pris en charge varient selon le fournisseur. Par exemple, certains fournisseurs imposent l'utilisation de noms de variables ou de colonnes, d'autres exigent l'emploi de noms symboliques tels que 0 ou Param0. Il convient de consulter la documentation spécifique du fournisseur pour obtenir des informations sur les noms de paramètres à utiliser dans les instructions SQL.  
  
 Lorsque vous utilisez un gestionnaire de connexions OLE DB, vous ne pouvez pas utiliser de sous-requêtes paramétrables, car la source OLE DB ne peut pas dériver d'informations de paramètre par le biais du fournisseur OLE DB. Vous pouvez toutefois utiliser une expression pour concaténer les valeurs de paramètre dans la chaîne de requête et définir la propriété SqlCommand de la source. Dans le Concepteur [!INCLUDE[ssIS](../../includes/ssis-md.md)], vous configurez une source OLE DB à l’aide de la boîte de dialogue **Éditeur de source OLE DB** et mappez les paramètres à des variables dans la boîte de dialogue **Définition des paramètres de la requête**.  
  
### Spécifications de paramètres à l'aide de positions ordinales  
 Si aucun nom de paramètre n’est retourné, l’ordre selon lequel les paramètres sont répertoriés dans la liste **Paramètres** dans la boîte de dialogue **Définition des paramètres de la requête** régit le marqueur de paramètre auquel ils sont mappés au moment de l’exécution. Le premier paramètre de la liste est-il mappé sur le premier dans l'instruction SQL, le deuxième sur le deuxième ?, etc.  
  
 L’instruction SQL suivante sélectionne des lignes dans la table **Product** de la base de données [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]. Le premier paramètre dans la liste **Mappages** est mappé au premier paramètre de la colonne **Color**, le deuxième paramètre à la colonne **Size**.  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 Les noms de paramètres n'ont aucune incidence. Par exemple, si un paramètre porte le même nom que la colonne à laquelle il s’applique, mais qu’il n’est pas placé à la bonne position ordinale dans la liste **Paramètres**, le mappage de paramètres effectué au moment de l’exécution utilise la position ordinale du paramètre, pas le nom du paramètre.  
  
 La commande EXEC impose généralement l'utilisation des noms des variables qui fournissent des valeurs de paramètres dans la procédure comme noms de paramètres.  
  
### Spécification de paramètres à l'aide de noms  
 Si les noms de paramètres réels sont retournés à partir du SGBDR, les paramètres utilisés par une instruction SELECT et EXEC sont mappés par nom. Les noms de paramètres doivent correspondre aux noms que la procédure stockée, exécutée par l'instruction SELECT ou l'instruction EXEC, attend.  
  
 L’instruction SQL suivante exécute la procédure stockée **uspGetWhereUsedProductID**, disponible dans la base de données [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)].  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 La procédure stockée attend les variables, `@StartProductID` et `@CheckDate`, pour fournir des valeurs de paramètres. L’ordre dans lequel les paramètres apparaissent dans la liste **Mappages** n’est pas pertinent. Le seul impératif est que les noms de paramètres correspondent aux noms de variables dans la procédure stockée, notamment le signe @.  
  
### Mappage de paramètres à des variables  
 Les paramètres sont mappés à des variables qui fournissent les valeurs de paramètres au moment de l'exécution. Les variables sont généralement des variables définies par l’utilisateur, bien que vous puissiez utiliser les variables système fournies par [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si vous utilisez des variables définies par l'utilisateur, assurez-vous que vous choisissez un type de données compatible avec celui de la colonne référencée par le paramètre mappé. Pour plus d’informations, consultez [Variables Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## Résolution des problèmes liés à la source OLE DB  
 Vous pouvez consigner les appels que la source OLE DB effectue vers des fournisseurs de données externes. Cette fonctionnalité de journalisation permet de résoudre des problèmes liés au chargement de données que réalise la source OLE DB depuis des sources de données externes. Pour consigner les appels que la source OLE DB effectue vers des fournisseurs de données externes, activez la journalisation de package et sélectionnez l’événement **Diagnostic** au niveau du package. Pour plus d’informations, consultez [Outils de dépannage pour l’exécution des packages](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## Configuration de la source OLE DB  
 Vous pouvez définir les propriétés par programmation ou par le biais du concepteur [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Pour plus d’informations sur les propriétés définissables dans la boîte de dialogue **Éditeur de source OLE DB**, cliquez sur l’une des rubriques suivantes :  
  
-   [Éditeur de source OLE DB &#40;page Gestionnaire de connexions&#41;](../../integration-services/data-flow/ole-db-source-editor-connection-manager-page.md)  
  
-   [Éditeur de source OLE DB &#40;page Colonnes&#41;](../../integration-services/data-flow/ole-db-source-editor-columns-page.md)  
  
-   [Éditeur de source OLE DB &#40;page Sortie d’erreur&#41;](../../integration-services/data-flow/ole-db-source-editor-error-output-page.md)  
  
 La boîte de dialogue **Éditeur avancé** reflète les propriétés qui peuvent être définies par programmation. Pour plus d'informations sur les propriétés définissables dans la boîte de dialogue **Éditeur avancé** ou par programmation, cliquez sur l'une des rubriques suivantes :  
  
-   [Propriétés communes](../Topic/Common%20Properties.md)  
  
-   [Propriétés personnalisées OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## Tâches associées  
  
-   [Extraire des données à l'aide de la source OLE DB](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [Mapper des paramètres de requête à des variables dans un composant de flux de données](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Définir les propriétés d'un composant de flux de données](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Trier des données pour les transformations de fusion et de jointure de fusion](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## Contenu connexe  
 Article Wiki, [SSIS with Oracle Connectors](http://go.microsoft.com/fwlink/?LinkId=220670) (SSIS avec connecteurs Oracle) sur social.technet.microsoft.com.  
  
## Voir aussi  
 [Destination OLE DB](../../integration-services/data-flow/ole-db-destination.md)   
 [Variables Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Flux de données](../../integration-services/data-flow/data-flow.md)  
  
  