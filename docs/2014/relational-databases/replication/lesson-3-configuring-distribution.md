---
title: 'Leçon 3 : Configuration de la Distribution | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 8d873d3664c88963b17550734b488e6872a9cc84
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126669"
---
# <a name="lesson-3-configuring-distribution"></a>Leçon 3 : Configuration de la distribution
  Dans cette leçon, vous allez configurer la distribution sur le serveur de publication et définir les autorisations requises sur les bases de données de publication et de distribution. Si vous avez déjà configuré le serveur de distribution, vous devez d'abord désactiver la publication et la distribution avant de commencer cette leçon. Ne procédez pas ainsi si vous devez conserver une topologie de réplication existante.  
  
 La configuration d'un serveur de publication avec un serveur de distribution distant dépasse le cadre de ce didacticiel.  
  
### <a name="configuring-distribution-at-the-publisher"></a>Configuration de la distribution sur le serveur de publication  
  
1.  Connectez-vous au serveur de publication dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puis développez le nœud du serveur.  
  
2.  Cliquez avec le bouton droit sur le dossier **Réplication** , puis cliquez sur **Configurer la distribution**.  
  
    > [!NOTE]  
    >  Si vous êtes connecté à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à l'aide de **localhost** au lieu du nom du serveur réel, un avertissement vous indique que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ne peut pas se connecter au serveur **'localhost'**. Cliquez sur **OK** dans la boîte de dialogue d'avertissement. Dans la boîte de dialogue **Se connecter au serveur** , remplacez le **Nom du serveur** , qui indique **localhost** , par le nom de votre serveur. Cliquer sur **Se connecter**.  
  
     L'Assistant Configuration de la distribution démarre.  
  
3.  Sur le **distributeur** page, sélectionnez **'**_\<nom_serveur >_**' agit comme son propre serveur de distribution ; SQL Server crée une base de données de distribution et un journal**, puis cliquez sur **suivant**.  
  
4.  Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ne s’exécute pas, dans la page de démarrage de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agent**, sélectionnez **Oui**, configurez le service [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pour qu’il démarre automatiquement. Cliquer sur **Suivant**.  
  
5.  Entrez **\\\\**\<_nom_ordinateur>_**\repldata** dans la zone de texte **Dossier d’instantanés**, où \<*nom_ordinateur>* désigne le serveur de publication, puis cliquez sur **Suivant**.  
  
6.  Acceptez les valeurs par défaut sur les pages restantes de l'Assistant.  
  
7.  Cliquez sur **Terminer** pour activer la distribution.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>Définition des autorisations de base de données sur le serveur de publication  
  
1.  Dans [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], développez **Sécurité**, cliquez avec le bouton droit sur **Connexions**, puis sélectionnez **Nouvelle connexion**.  
  
2.  Dans la page **Général**, cliquez sur **Rechercher**, entrez \<_nom_ordinateur>_**\repl_snapshot** dans la zone **Entrez le nom de l’objet à sélectionner**, où \<*nom_ordinateur>* désigne le serveur de publication local, cliquez sur **Vérifier les noms**, puis cliquez sur **OK**.  
  
3.  Sur la page **Mappage de l'utilisateur** , dans la liste **Utilisateurs mappés à cette connexion** , sélectionnez les bases de données **distribution** et [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
     Dans le **l’appartenance au rôle de base de données** liste Sélectionnez le `db_owner` rôle pour la connexion pour les deux bases de données.  
  
4.  Cliquez sur **OK** pour créer la connexion.  
  
5.  Répétez les étapes 1 à 4 pour créer une connexion pour le compte local repl_logreader. Cette connexion doit également être mappée aux utilisateurs qui sont membres de la `db_owner` rôle de base de données fixe dans le **distribution** et **AdventureWorks** bases de données.  
  
6.  Répétez les étapes 1 à 4 pour créer une connexion pour le compte local repl_distribution. Cette connexion doit être mappée à un utilisateur est membre de la `db_owner` rôle de base de données fixe dans le **distribution** base de données.  
  
7.  Répétez les étapes 1 à 4 pour créer une connexion pour le compte local repl_merge. Cette connexion doit avoir les mappages d'utilisateur des bases de données de **distribution** et **AdventureWorks** .  
  
## <a name="see-also"></a>Voir aussi  
 [Configurer la distribution](configure-distribution.md)   
 [Modèle de sécurité de l'Agent de réplication](security/replication-agent-security-model.md)  
  
  
