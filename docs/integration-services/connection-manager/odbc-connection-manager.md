---
title: "Gestionnaire de connexions ODBC | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "connexions [Integration Services], ODBC"
  - "Gestionnaire de connexions ODBC"
  - "sources de données [Integration Services], connexions"
  - "gestionnaires de connexions [Integration Services], ODBC"
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Gestionnaire de connexions ODBC
  Un gestionnaire de connexions ODBC permet à un package de se connecter à divers systèmes de gestion de base de données à l'aide de la spécification ODBC (Open Database Connectivity).  
  
 Quand vous ajoutez une connexion ODBC à un package et que vous définissez les propriétés du gestionnaire de connexions, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crée un gestionnaire de connexions et l’ajoute à la collection **Connections** du package. Au moment de l'exécution, le gestionnaire de connexions est résolu en tant que connexion ODBC physique.  
  
 La propriété **ConnectionManagerType** du gestionnaire de connexions a pour valeur **ODBC**.  
  
 Vous pouvez configurer le gestionnaire de connexions ODBC de plusieurs manières :  
  
-   Fournissez une chaîne de connexion qui fait référence à un nom d'utilisateur ou de source de données système.  
  
-   Spécifiez le serveur auquel se connecter.  
  
-   Indiquez si la connexion est conservée au moment de l'exécution.  
  
## Configuration du gestionnaire de connexions ODBC  
 Vous pouvez définir des propriétés au moyen du concepteur [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou par programmation.  
  
 Pour plus d’informations sur les propriétés définissables dans le concepteur [!INCLUDE[ssIS](../../includes/ssis-md.md)], cliquez sur l’une des rubriques suivantes :  
  
-   [Référence de l'interface utilisateur du gestionnaire de connexions ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)  
  
 Pour plus d’informations sur la configuration d’un gestionnaire de connexions par programmation, consultez <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> et [Ajout de connexions par programmation](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Voir aussi  
 [Connexions Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  