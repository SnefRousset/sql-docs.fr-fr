---
title: "Valider des donn&#233;es r&#233;pliqu&#233;es | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "validation des données en ligne [réplication SQL Server]"
  - "administration de la réplication, validation des données"
  - "réplication [SQL Server], validation des données"
  - "transactional replication, validating data"
  - "validation des données"
  - "validation des données de réplication de fusion [réplication SQL Server]"
  - "validation des données de réplication de fusion [réplication SQL Server], à propos de la validation de données"
  - "validation des données répliquées"
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Valider des donn&#233;es r&#233;pliqu&#233;es
  La réplication transactionnelle et de fusion vous permet de vérifier que les données sur l'Abonné correspondent aux données sur le serveur de publication. La validation peut être réalisée pour des abonnements spécifiques ou pour tous les abonnements à une publication. Spécifiez un des types de validation suivants et l'Agent de distribution ou l'Agent de fusion validera les données lors de sa prochaine exécution :  
  
-   Calculer uniquement le nombre de lignes. Ceci vérifie si la table sur l'Abonné a le même nombre de lignes que la table sur le serveur de publication, mais ne vérifie pas que le contenu des lignes correspond. La validation du nombre de lignes fournit une approche allégée de la validation qui vous permet de savoir qu'il existe des problèmes au niveau des données.  
  
-   Calculer le nombre de lignes et comparer les sommes de contrôle binaires. Outre le comptage des lignes sur le serveur de publication et sur l'Abonné, une somme de contrôle de toutes les données est calculée à l'aide de l'algorithme de somme de contrôle. Si le nombre de lignes est erroné, la somme de contrôle n'est pas effectuée.  
  
 En plus de vérifier que les données sur l'Abonné et sur le serveur de publication correspondent, la réplication de fusion donne la possibilité de vérifier que les données sont partitionnées correctement pour chaque Abonné. Pour plus d’informations, consultez [valider les informations de Partition pour un abonné de fusion](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md).  
  
 **Pour valider des données**  
  
 Pour valider tous les articles d'un abonnement, utilisez [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], des procédures stockées ou Replication Management Objects. Pour plus d'informations, voir [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md). Pour valider des articles individuels dans des publications d'instantané et transactionnelles, vous devez utiliser des procédures stockées.  
  
## Résultats de la validation des données  
 Quand la validation est terminée, l'Agent de distribution ou l'Agent de fusion consigne des messages relatifs au succès ou à l'échec (la réplication ne rapporte pas quelles lignes ont échoué). Ces messages peuvent être affichés dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], dans le moniteur de réplication et dans les tables système de réplication. La rubrique de procédure ci-dessus montre comment exécuter une validation et afficher les résultats.  
  
 Pour gérer les échecs de validation, considérez les points suivants :  
  
-   Configurez l’alerte de réplication nommée **réplication : Échec de la validation de données par l’abonné** afin que vous en êtes informé de l’échec. Pour plus d’informations, consultez [configurer des alertes de réplication prédéfinies & #40 ; SQL Server Management Studio & #41 ;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md).  
  
-   Le fait que la validation a échoué est-il un problème pour votre application ? Si l'échec de la validation constitue un problème, mettez à jour manuellement les données pour qu'elles soient synchronisées, ou bien réinitialisez l'abonnement :  
  
    -   Données peuvent être mis à jour à l’aide de la [utilitaire tablediff](../../tools/tablediff-utility.md). Pour plus d’informations sur l’utilisation de cet utilitaire, consultez [comparer les Tables répliquées pour différences & #40 ; Programmation de la réplication & #41 ;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    -   Pour plus d’informations sur la réinitialisation, consultez [Réinitialiser les abonnements](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## Considérations sur la validation des données  
 Prenez en compte les problèmes suivants lors de la validation des données :  
  
-   Vous devez arrêter toutes les activités de mise à jour sur les Abonnés avant de valider les données (il n'est pas nécessaire d'arrêter les activités sur le serveur de publication pendant la validation).  
  
-   Dans la mesure où les sommes de contrôle et les sommes de contrôle binaires peuvent nécessiter des ressources processeur importantes lors de la validation d'un jeu de données de grande taille, il est préférable de planifier la validation au moment où l'activité est la plus faible sur les serveurs utilisés dans la réplication.  
  
-   La réplication valide seulement des tables ; elle ne vérifie pas si des articles de schéma uniquement (tels que des procédures stockées) sont identiques sur le serveur de publication et sur l'Abonné.  
  
-   La somme de contrôle binaire peut être utilisée avec toutes les tables publiées. La somme de contrôle valide les tables avec des filtres de colonnes, ou des structures de table logique où les décalages des colonnes diffèrent (à cause d'instructions ALTER TABLE qui suppriment ou ajoutent des colonnes).  
  
-   Validation de réplication utilise le **checksum** et **binary_checksum** fonctions. Pour plus d’informations sur leur comportement, consultez  [CHECKSUM & #40 ; Transact-SQL & #41 ;](../../t-sql/functions/checksum-transact-sql.md) et [BINARY_CHECKSUM & #40 ; Transact-SQL & #41 ;](../../t-sql/functions/binary-checksum-transact-sql.md).  
  
-   Une validation utilisant la somme de contrôle binaire ou la somme de contrôle peut signaler de façon incorrecte un échec si les types de données sont différents entre l'Abonné et le serveur de publication. Cela peut se produire si vous effectuez l'une des opérations suivantes :  
  
    -   Vous définissez explicitement les options de schéma pour qu'elles correspondent aux types de données des versions antérieures de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Vous définissez le niveau de compatibilité de la publication pour une publication de fusion sur une version antérieure de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], et les tables publiées contiennent un ou plusieurs types de données qui doivent être mappés pour cette version.  
  
    -   Vous initialisez manuellement un abonnement et utilisez différents types de données sur l'Abonné.  
  
-   Les validations de somme de contrôle binaire et de somme de contrôle ne sont pas prises en charge pour les abonnements transformables dans le cadre de la réplication transactionnelle.  
  
-   La validation n'est pas prise en charge pour les données répliquées vers des Abonnés non-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Fonctionnement de la validation des données  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valide les données en calculant un nombre de lignes ou une somme de contrôle du serveur de publication et en comparant les valeurs pour le nombre de lignes ou la somme de contrôle calculé sur l’abonné. Une valeur est calculée pour la table de l’ensemble de la publication et une valeur est calculée pour la table de l’ensemble de l’abonnement, mais les données dans **texte**, **ntext**, ou **image** colonnes n’est pas inclus dans les calculs.  
  
 Pendant l'exécution des calculs, des verrous partagés sont temporairement placés sur les tables pour lesquelles le nombre de lignes ou la somme de contrôle est calculé. Ces calculs sont cependant effectués rapidement et les verrous partagés sont généralement retirés au bout de quelques secondes.  
  
 Lors de l'utilisation des sommes de contrôle binaires, le contrôle de redondance cyclique (CRC) 32 bits est effectué colonne par colonne, et non pas sur la ligne physique de la page de données. Ainsi, quel que soit l'ordre physique des colonnes de la table dans la page de données, elles participent au même calcul de CRC de ligne. La validation par somme de contrôle binaire peut être utilisée lorsque des filtres de lignes ou de colonnes sont appliqués à la publication.  
  
## Voir aussi  
 [Méthodes conseillées pour l'administration de la réplication](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  