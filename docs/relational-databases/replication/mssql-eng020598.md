---
title: "MSSQL_ENG020598 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG020598 (erreur)"
ms.assetid: 1c3032f2-23d1-4ead-94ee-16ac4d75cd0c
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020598
    
## Détails du message  
  
|||  
|-|-|  
|Nom du produit|SQL Server|  
|ID d'événement|20598|  
|Source de l'événement|MSSQLSERVER|  
|Composant|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nom symbolique||  
|Texte du message|La ligne n'a pas été trouvée chez l'Abonné lorsque la commande répliquée est appliquée.|  
  
## Explication  
 Cette erreur est générée dans la réplication transactionnelle lorsque l'Agent de distribution tente de mettre à jour sur l'Abonné, mais que la ligne a été supprimée ou que la clé primaire de la ligne a été modifiée. Par défaut, les Abonnés à des publications transactionnelles doivent être traités en lecture seule, parce que les changements ne sont pas propagés vers le serveur de publication. Dans le cas de la réplication transactionnelle, les modifications des utilisateurs doivent être effectuées sur l'Abonné, uniquement si les abonnements devant être mis à jour ou la réplication d'égal à égal sont utilisés. Pour plus d’informations sur ces options, consultez [à des abonnements pour la réplication transactionnelle](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md) et [-to-Peer la réplication transactionnelle](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
## Action de l'utilisateur  
 **Pour rectifier ce problème :**  
  
1.  Si la réplication doit continuer pendant que vous identifiez la source de l’erreur, spécifiez le paramètre **- SkipErrors 20598** pour l’Agent de Distribution. L'agent peut alors ignorer les modifications qui provoquent l'erreur 20598, tout en permettant la réplication des autres modifications.  
  
2.  Identifiez sur l'Abonné les modifications qui ont été supprimées ou qui comportent une clé primaire différente de celle des lignes correspondantes sur le serveur de publication. Vous pouvez utiliser la [utilitaire tablediff](../../tools/tablediff-utility.md) pour déterminer les lignes qui sont différentes dans les bases de données de publication et d’abonnement. Pour plus d’informations sur l’utilisation de cet utilitaire avec des bases de données répliquées, consultez [comparer les Tables répliquées pour différences & #40 ; Programmation de la réplication & #41 ;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
3.  Corrigez les lignes sur l’abonné à l’aide du **tablediff** utilitaire ou une autre méthode.  
  
4.  (Facultatif) Supprimer le **- SkipErrors** paramètre.  
  
## Voir aussi  
 [Erreurs et événements référence & #40 ; Réplication & #41 ;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  