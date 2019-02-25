---
title: Source Power Query | Microsoft Docs
description: Découvrez comment configurer la source Power Query dans le flux de données SQL Server Integration Services
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql14.ssis.designer.powerqueryconnmgr.f1
- sql14.ssis.designer.powerquerysource.queries.f1
- sql14.ssis.designer.powerquerysource.connmgrs.f1
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 00b24bdc5da2c717f43ca30e9159aa845faf171b
ms.sourcegitcommit: 7c052fc969d0f2c99ad574f99076dc1200d118c3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570702"
---
# <a name="power-query-source-preview"></a>Source Power Query (préversion)

Cet article décrit comment configurer les propriétés de la source Power Query dans le flux de données SQL Server Integration Services (SSIS). Power Query est une technologie qui vous permet de vous connecter à diverses sources de données et de transformer des données à l’aide d’Excel/Power BI Desktop. Pour plus d’informations, consultez l’article [Power Query - Présentation et formation](https://support.office.com/article/power-query-overview-and-learning-ed614c81-4b00-4291-bd3a-55d80767f81d). Le script généré par Power Query peut copié et collé dans la source Power Query dans le flux de données SSIS pour le configurer.
  
> [!NOTE]
> Pour la préversion actuelle, afin de faciliter la collecte rapide de commentaires et les améliorations de fonctionnalités fréquentes, la source Power Query ne peut être utilisée que dans SQL Server Data Tools (SSDT) et Azure-SSIS Integration Runtime (IR) dans Azure Data Factory (ADF). Vous pouvez télécharger la dernière version de SSDT qui prend en charge la source Power Query [ici](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017). Pour provisionner un runtime d’intégration Azure-SSIS, consultez l’article [Provisionner SSIS dans ADF](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="configure-the-power-query-source"></a>Configurer la source Power Query

Pour ouvrir **l’éditeur de source Power Query** dans SSDT, faites glisser et déposez **Source Power Query** à partir de la boîte à outils SSIS vers le concepteur de flux de données et double-cliquez dessus.  

![Source PQ](media/power-query-source/pq-source.png)

Trois onglets s’affichent sur le côté gauche. Dans l’onglet **Queries** (Requêtes), vous pouvez sélectionner votre mode de requête dans le menu déroulant.
-   Le mode **Single Query** (Requête unique) vous permet de copier et coller un seul script Power Query à partir d’Excel/Power BI Desktop.
-   Le mode **Single Query from Variable** (Requête unique à partir d’une variable) vous permet de spécifier une variable de chaîne qui contient votre requête à exécuter.

![Source PQ, onglet Requête unique](media/power-query-source/pq-source-queries-tab-single.png)

Dans l’onglet **Connection Managers** (Gestionnaires de connexions), vous pouvez ajouter ou supprimer des gestionnaires de connexions Power Query qui contiennent des informations d’accès à la source de données. La sélection du bouton **Detect Data Source** (Détecter la source de données) permet d’identifier les sources de données référencées dans votre requête et les répertorie pour vous permettre d’attribuer les gestionnaires de connexions Power Query existants appropriés ou d’en créer de nouveaux.

![Source PQ, onglet Gestionnaires de connexions, Détecter](media/power-query-source/pq-source-connection-managers-tab-detect.png)

![Source PQ, onglet Gestionnaires de connexions, Ajouter](media/power-query-source/pq-source-connection-managers-tab-add.png)

Enfin, dans l’onglet **Columns** (Colonnes), vous pouvez modifier les informations de la colonne de sortie.

![Source PQ, onglet Colonnes](media/power-query-source/pq-source-columns-tab.png)

## <a name="configure-the-power-query-connection-manager"></a>Configurer le Gestionnaire de connexions Power Query

Lorsque vous concevez votre flux de données avec la Source Power Query sur SSDT, vous pouvez créer un nouveau Gestionnaire de connexions Power Query comme suit :
- Créez-le indirectement dans l’onglet **Gestionnaires de connexions** de la source Power Query après avoir sélectionné le bouton **Ajouter**/**Détecter la source de données** et **<New connection...>** dans le menu déroulant, comme décrit ci-dessus.
- Créez-le directement en cliquant sur le panneau **Gestionnaires de connexions** de votre package et en sélectionnant **Nouvelle connexion...**  dans le menu déroulant.

![Source PQ, panneau Gestionnaires de connexions, Ajouter](media/power-query-source/pq-source-connection-managers-panel-add.png)

Dans la boîte de dialogue **Ajout d'un gestionnaire de connexions SSIS**, double-cliquez sur **PowerQuery** dans la liste des types de gestionnaires de connexions.

![Source PQ, panneau Gestionnaires de connexions, boîte de dialogue Ajouter](media/power-query-source/pq-source-connection-managers-panel-add-dialog.png)

Dans **l’éditeur du Gestionnaire de connexion Power Query**, vous devez spécifier le **Type de la source de données**, le **Chemin d’accès à la source de données** et le **Type d’authentification**, mais aussi attribuer les informations d’identification d’accès appropriées. Pour **Type de la source de données**, vous pouvez actuellement choisir entre 22 types dans le menu déroulant.

![Source PQ, Gestionnaires de connexions, Éditeur, Type](media/power-query-source/pq-source-connection-manager-editor-kind.png)

Certaines de ces sources (**Oracle**, **DB2**, **MySQL**, **PostgreSQL**, **Teradata**, **Sybase**) nécessitent l’installation de pilotes ADO.NET supplémentaires qui peuvent être obtenus à partir de l’article [Prérequis pour Power Query](https://support.office.com/article/data-source-prerequisites-power-query-6062cf52-c764-45d0-a1c6-fbf8fc05b05a). Vous pouvez utiliser l’interface de configuration personnalisée pour les installer sur votre runtime d’intégration Azure-SSIS, consultez l’article [Personnalisation du runtime d’intégration Azure-SSIS](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).

> [!NOTE]
> Pour la source de données **Oracle**, le pilote Oracle ADO.NET ne peut pas être installé sur le runtime d’intégration Azure-SSIS pour le moment. Donc, installez le pilote Oracle ODBC à la place et utilisez la source de données **ODBC** pour vous connecter à Oracle pour l’instant. Consultez l’exemple **ORACLE STANDARD ODBC** dans l’article [Personnalisation du runtime d’intégration Azure-SSIS](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).

Pour le **Chemin d’accès à la source de données**, vous pouvez entrer des propriétés spécifiques à la source de données formant une chaîne de connexion sans les informations d’authentification. Par exemple, le chemin d’accès à la source de données **SQL** est `<Server>;<Database>`. Vous pouvez sélectionner le bouton **Modifier** pour attribuer des valeurs aux propriétés spécifiques à la source de données qui forment le chemin d’accès.

![Source PQ, Gestionnaires de connexions, Éditeur, Chemin d’accès](media/power-query-source/pq-source-connection-manager-editor-path.png)

Enfin, pour le **Type d’authentification**, vous pouvez sélectionner **Anonyme**/**Authentification Windows**/**Mot de passe du nom d’utilisateur**/**Clé** dans le menu déroulant, entrez les informations d’identification d’accès appropriées, puis sélectionnez le bouton **Tester la connexion** pour vous assurer que la source Power Query a été configurée correctement.

![Source PQ, Gestionnaires de connexions, Éditeur, Authentification](media/power-query-source/pq-source-connection-manager-editor-authentication.png)

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment exécuter des packages SSIS dans le runtime d’intégration Azure-SSIS en tant qu’activités de première classe dans les pipelines ADF. Consultez l’article [Exécuter le runtime d’activité du package SSIS](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity).