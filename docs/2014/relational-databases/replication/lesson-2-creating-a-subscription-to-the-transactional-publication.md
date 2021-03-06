---
title: 'Leçon 2 : Création d’un abonnement à la Publication transactionnelle | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d3e8b5f0be58d9153fbe4d0ffd0287ea753fcc5e
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129389"
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>Leçon 2 : Création d'un abonnement à la publication transactionnelle
  Dans cette leçon, vous allez créer l'abonnement à l'aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Cette leçon requiert que vous avez terminé la leçon précédente, [leçon 1 : Publication des données à l’aide de la réplication transactionnelle](lesson-1-publishing-data-using-transactional-replication.md).  
  
### <a name="to-create-the-subscription"></a>Pour créer l'abonnement  
  
1.  Connectez-vous au serveur de publication dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], développez le nœud du serveur, puis le dossier **Réplication** .  
  
2.  Dans le dossier **Publications locales** , cliquez avec le bouton droit sur la publication **AdvWorksProductTrans** , puis cliquez sur **Nouveaux abonnements**.  
  
     L'Assistant Nouvel abonnement démarre.  
  
3.  Dans la page Publication, sélectionnez **AdvWorksProductTrans**, puis cliquez sur **Suivant**.  
  
4.  Dans la page Emplacement de l’Agent de distribution, sélectionnez **Exécuter tous les agents sur le serveur de distribution**, puis cliquez sur **Suivant**.  
  
5.  Dans la page Abonnés, si le nom de l’instance de l’Abonné n’apparaît pas, cliquez sur **Ajouter un Abonné**, sur **Ajouter un Abonné SQL Server**, entrez le nom de l’instance de l’Abonné dans la boîte de dialogue **Se connecter au serveur** , puis cliquez sur **Se connecter**.  
  
6.  Dans la page abonnés, sélectionnez le nom de l’instance de l’abonné, puis  **\<nouvelle base de données >** sous **base de données d’abonnement**.  
  
7.  Dans la boîte de dialogue **Nouvelle base de données** , entrez **ProductReplica** dans la zone **Nom de la base de données** , cliquez sur **OK**, puis sur **Suivant**.  
  
8.  Dans le **sécurité de l’Agent de Distribution** boîte de dialogue, cliquez sur le bouton de sélection (**...** ), entrez \< _nom_ordinateur >_**\repl_distribution** dans le **compte de processus** , entrez le mot de passe pour ce compte, cliquez sur **OK**, puis cliquez sur **suivant**.  
  
9. Cliquez sur **Terminer** pour accepter les valeurs par défaut des pages restantes et terminer l’Assistant.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Définition des autorisations de base de données sur l'Abonné  
  
1.  Connectez-vous à l’Abonné dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], développez **Bases de données**, **ProductReplica**et **Sécurité**, cliquez avec le bouton droit sur **Utilisateurs**, puis sélectionnez **Nouvel utilisateur**.  
  
2.  Dans la page **Général** , dans la liste **Type d’utilisateur** , sélectionnez **Utilisateur Windows**.  
  
3.  Sélectionnez le **nom d’utilisateur** puis cliquez sur le bouton de sélection (...), dans le **Entrez le nom de l’objet à sélectionner** zone, tapez < nom_ordinateur >**\repl_distribution**, cliquez sur  **Vérifier les noms**, puis cliquez sur **OK**.  
  
4.  Dans la page **Appartenance** , dans la zone **Appartenance au rôle de base de données** , sélectionnez **db_owner**, puis cliquez sur **OK** pour créer l’utilisateur.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Pour afficher l'état de synchronisation de l'abonnement  
  
1.  Connectez-vous au serveur de publication dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puis développez le nœud du serveur et le dossier **Réplication** .  
  
2.  Dans le dossier **Publications locales** , développez la publication **AdvWorksProductTrans** , cliquez avec le bouton droit sur l’abonnement dans la base de données **ProductReplica** , puis cliquez sur **Afficher l’état de synchronisation**.  
  
     L'état de synchronisation de l'abonnement s'affiche.  
  
3.  Si l’abonnement n’apparaît pas sous **AdvWorksProductTrans**, appuyez sur F5 pour actualiser la liste.  
  
## <a name="next-steps"></a>Étapes suivantes  
 Vous avez créé avec succès un abonnement à la publication transactionnelle. Comme l'Agent de distribution de cet abonnement s'exécute en permanence, l'abonnement est initialisé lors de sa création. Ensuite, vous allez utiliser les jetons de suivi pour vérifier que les modifications sont bien répliquées sur l'Abonné et pour déterminer la latence. Consultez [leçon 3 : Validation de l’abonnement et mesure de la latence](lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Initialiser un abonnement avec un instantané](initialize-a-subscription-with-a-snapshot.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [S'abonner à des publications](subscribe-to-publications.md)  
  
  
