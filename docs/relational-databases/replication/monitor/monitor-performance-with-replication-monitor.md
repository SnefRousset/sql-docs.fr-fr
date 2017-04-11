---
title: "Analyser les performances avec le Moniteur de r&#233;plication | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "analyse des performances [réplication SQL Server], moniteur de réplication"
  - "Agent de lecture du journal, analyse"
  - "Moniteur de réplication, performances"
  - "Agent de fusion, analyse"
  - "Agent de lecture de la file d’attente, analyse"
  - "Agent d’instantané, analyse"
  - "Agent de distribution, analyse"
  - "surveillance des performances [réplication SQL Server]"
ms.assetid: f212397d-1bfd-496b-a246-668952891d09
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Analyser les performances avec le Moniteur de r&#233;plication
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Le Moniteur de réplication vous permet d'analyser les performances de la réplication transactionnelle et de la réplication de fusion de la manière suivante :  
  
-   Définition d'alertes et de seuils  
  
-   Affichage de mesures de performance  
  
-   Détermination de la latence avec des jetons de suivi (réplication transactionnelle)  
  
-   Affichage de statistiques de synchronisation détaillées (réplication de fusion)  
  
-   Affichage des transactions et du temps de remise (réplication transactionnelle)  
  
## Définir des seuils et des avertissements  
 Le moniteur de réplication vous permet d'activer des avertissements pour plusieurs conditions de performances. Quand vous activez un avertissement, vous spécifiez un seuil. Lorsque ce seuil est atteint ou dépassé, un avertissement s’affiche dans le **état** colonne pour l’abonnement et la publication avec laquelle il se synchronise (sauf si un problème avec une priorité plus élevée doit être affichée). L'atteinte d'un seuil déclenche un avertissement dans le Moniteur de réplication, mais également une alerte. Vous pouvez activer des avertissements pour les conditions de performances suivantes :  
  
-   Dépassement de la latence spécifiée (la quantité de temps qui s'écoule entre la validation d'une transaction sur le serveur de publication et la validation de la transaction correspondante sur l'Abonné).  
  
     Ceci s'applique à la réplication transactionnelle. Si le seuil spécifié est atteint ou dépassé, l'état affiché est **Critique pour les performances**.  
  
-   Dépassement du temps de synchronisation spécifié.  
  
     Ceci s'applique à la réplication de fusion. Si le seuil spécifié est atteint ou dépassé, l’état est affiché en tant que **Fusion longue**. Vous pouvez spécifier des seuils différents pour les connexions d'accès à distance et pour les connexions LAN (Local Area Network).  
  
-   Impossibilité de traiter le nombre de lignes spécifié dans un intervalle de temps donné.  
  
     Ceci s'applique à la réplication de fusion. Si le seuil spécifié est atteint ou dépassé, l'état affiché est **Critique pour les performances**. Vous pouvez spécifier des seuils différents pour les connexions d'accès à distance et pour les connexions LAN.  
  
 Pour plus d’informations, consultez [définition des seuils et des avertissements dans le moniteur de réplication](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
## Afficher des mesures de performance  
 Moniteur de réplication affiche des valeurs de qualité des performances pour la réplication de fusion et la réplication transactionnelle dans le **Performance moyenne actuelle** et **pire Performance actuelle** colonnes pour les publications et les **performances** colonne pour les abonnements. Les valeurs sont :  
  
-   Excellent  
  
-   Bonne  
  
-   Correcte  
  
-   Médiocre  
  
-   Critique (réplication transactionnelle seulement)  
  
 Les valeurs sont déterminées comme suit :  
  
-   Pour la réplication transactionnelle, la qualité des performances est déterminée par le seuil de latence. Si le seuil n'est pas défini, aucune valeur n'est affichée. Le tableau suivant montre la corrélation entre le seuil et la valeur de la qualité des performances. Par exemple, si le seuil est défini à 60 secondes et que la latence réelle est de 30 secondes, la latence représente 50% du seuil, ce qui correspond à la valeur « Bonne ».  
  
    |Excellent|Bonne|Correcte|Médiocre|Critique|  
    |---------------|----------|----------|----------|--------------|  
    |0 – 34%|35 – 59%|60 – 84%|85 – 99%|100% +|  
  
-   La réplication de fusion, la qualité des performances est indépendante des seuils (le seuil de traitement de la ligne ne détermine pas si la valeur **critique pour les performances** s’affiche dans le **état** colonne). La qualité des performances est déterminée en comparant la performance d'abonnements individuels à la performance historique moyenne des abonnements à la publication avec le même type de connexion (d'accès distant ou LAN). Le moniteur de réplication affiche une valeur après cinq synchronisations avec au moins 50 modifications chacune via le même type de connexion. S'il y a eu moins de cinq synchronisations comprenant 50 modifications ou plus ou que la synchronisation la plus récente inclut moins de 50 modifications, il n'affiche pas de valeur.  
  
     Le tableau suivant montre la corrélation entre la performance moyenne et la valeur de la qualité des performances. Par exemple, si dix Abonnés se sont synchronisés via une connexion LAN avec un taux moyen de 100 lignes par seconde, et que l'un des abonnements se synchronise ensuite à un taux de 125 lignes par seconde, la performance pour la synchronisation de cet Abonné est à 125% de la moyenne, ce qui correspond à la valeur « Bonne ».  
  
    |Excellent|Bonne|Correcte|Médiocre|  
    |---------------|----------|----------|----------|  
    |151+%|76 – 150%|26 – 75%|0 – 25%|  
  
 Pour plus d’informations sur l’affichage des informations d’abonnement, consultez [afficher des informations et effectuer des tâches pour un abonnement & #40 ; Moniteur de réplication & #41 ;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md).  
  
## Déterminer la latence avec des jetons de suivi  
 La réplication transactionnelle vous permet de mesurer la latence dans un système en insérant un jeton (une petite quantité de données) dans le journal des transactions de la base de données de publication et en enregistrant le temps qu'il met pour arriver au serveur de distribution et aux Abonnés. Le jeton vous permet aussi de détecter si des données n'atteignent par le serveur de distribution ou l'Abonné. Pour plus d’informations, consultez [mesure la latence et valider les connexions pour la réplication transactionnelle](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## Afficher les performances de synchronisation détaillées pour la réplication de fusion  
 Pour la réplication de fusion, le moniteur de réplication affiche des statistiques détaillées pour chaque article traité lors de la synchronisation, notamment la quantité de temps passé dans chaque phase du traitement (chargement des modifications, téléchargement des modifications, etc.). Il peut être utile d'identifier les tables spécifiques qui provoquent les ralentissements ; il s'agit du meilleur observatoire pour résoudre les problèmes de performance avec les abonnements de fusion. Pour plus d’informations sur l’affichage des statistiques détaillées, consultez la page [afficher des informations et effectuer des tâches pour les Agents associés à un abonnement & #40 ; Moniteur de réplication & #41 ;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Afficher les transactions et les temps de remise pour la réplication transactionnelle  
 Pour la réplication transactionnelle, le moniteur de réplication affiche des informations sur le nombre de transactions dans la base de données de distribution qui n'ont pas encore été distribuées à un Abonné et sur le temps estimé pour distribuer ces transactions. Pour plus d’informations, consultez [afficher des informations et effectuer des tâches pour les Agents associés à un abonnement & #40 ; Moniteur de réplication & #41 ;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Voir aussi  
 [Surveillance de la réplication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  