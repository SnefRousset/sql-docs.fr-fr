---
title: Transférer des instantanés via FTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 55c30791-cd2a-420b-8ba7-5700e005cb45
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 96c6c03d06efa587a8644af2a0ffa0b7532f15dd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52785011"
---
# <a name="transfer-snapshots-through-ftp"></a>Transférer des instantanés via FTP
  Par défaut, les instantanés sont stockés dans des dossiers définis sous forme de partages UNC (Universal Naming Convention). La réplication vous permet aussi de spécifier un partage FTP (File Transfer Protocol) plutôt qu'UNC. Pour utiliser FTP, vous devez configurer un serveur FTP puis une publication et un ou plusieurs abonnements qui utiliseront FTP. Pour obtenir des informations sur la configuration d'un serveur SMTP, consultez la documentation IIS (Internet Information Services). Si vous spécifiez des informations FTP pour une publication, les abonnements à cette publication utiliseront par défaut FTP. FTP est uniquement utilisé avec la synchronisation Web lorsque l'ordinateur exécutant IIS est séparé du serveur de distribution par un pare-feu. Dans ce cas, FTP peut être utilisé pour transférer l'instantané entre le serveur de distribution et l'ordinateur qui exécute IIS. (L'instantané est toujours transféré à l'Abonné en utilisant le protocole HTTPS.)  
  
> [!IMPORTANT]  
>  Il est conseillé d'utiliser l'authentification [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows et un partage UNC plutôt qu'un partage FTP puisque les mots de passe FTP doivent être stockés et que le mot de passe est transmis de l'Abonné ou de l'ordinateur exécutant IIS lorsqu'il utilise la synchronisation Web avec le serveur FTP en texte brut. De plus, parce qu'un seul compte contrôle l'accès au partage d'instantané, il n'est pas possible de garantir qu'un Abonné à une publication de fusion filtrée n'aura accès qu'aux fichiers d'instantanés de sa partition de données.  
  
 Pour remettre un instantané via FTP, consultez [Deliver a Snapshot Through FTP](publish/deliver-a-snapshot-through-ftp.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Synchronisation web pour la réplication de fusion](web-synchronization-for-merge-replication.md)   
 [Initialiser un abonnement avec un instantané](initialize-a-subscription-with-a-snapshot.md)   
 [Options d’instantané](snapshot-options.md)  
  
  
