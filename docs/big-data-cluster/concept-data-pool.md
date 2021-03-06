---
title: Quelles sont les pools de données ?
titleSuffix: SQL Server 2019 big data clusters
description: Cet article décrit le pool de données dans un cluster de données volumineux de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: c3df07da100bf0bbfc0b2238cb4154b4c3a363e3
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241610"
---
# <a name="what-are-data-pools-in-a-sql-server-2019-big-data-cluster"></a>Quelles sont les pools de données dans un cluster de données volumineux de SQL Server 2019 ?

Cet article décrit le rôle de *pools de données SQL Server* dans un cluster de données volumineuses de SQL Server 2019 (version préliminaire). Les sections suivantes décrivent l’architecture et les fonctionnalités d’un pool de données SQL.

## <a name="data-pool-architecture"></a>Architecture de pool de données

Un pool de données se compose d’une ou plusieurs instances de pool de données SQL Server. Instances de pool de données SQL fournissent un stockage persistant de SQL Server pour le cluster. Un pool de données est utilisé pour recevoir les données à partir de requêtes SQL ou de travaux Spark. Pour offrir de meilleures performances sur grands jeux de données, les données dans un pool de données sont réparties dans les partitions entre les instances de pool de données membre SQL.

## <a name="scale-out-data-marts"></a>Montée en puissance datamarts

Les pools de données permettent la création de montée en puissance datamarts, où les données externes à partir de plusieurs sources sont ingérées dans le pool de données. Étant donné que les données sont réparties sur les instances de pool de données, les requêtes parallèles sur les données organisées sont plus efficaces.

![Montée en puissance Datamart](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur les clusters de données volumineuses de SQL Server, consultez la présentation suivante :

- [Quelles sont les clusters SQL Server 2019 big data ?](big-data-cluster-overview.md)
