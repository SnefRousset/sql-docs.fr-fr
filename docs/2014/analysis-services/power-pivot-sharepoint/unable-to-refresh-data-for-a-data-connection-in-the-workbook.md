---
title: "Impossible d'actualiser les données pour une connexion de données dans le classeur. Essayez encore ou contactez votre administrateur système. Impossible d’actualiser les connexions suivantes : données PowerPivot | Microsoft Docs"
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0f6fd52d-ac72-43e3-aa08-05a2d2bb873d
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 396b4b32d2af95b8c7d49beab0fde988d2bee903
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220269"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook-try-again-or-contact-your-system-administrator-the-following-connections-failed-to-refresh-powerpivot-data"></a>Impossible d'actualiser les données pour une connexion de données dans le classeur. Essayez encore ou contactez votre administrateur système. Échec de l'actualisation des connexions suivantes : Données PowerPivot
  Pour les classeurs Excel qui contiennent des données PowerPivot, Excel Services retourne cette erreur en cas de demande de connexion à un serveur PowerPivot qui échoue.  
  
## <a name="details"></a>Détails  
  
|||  
|-|-|  
|S'applique à :|Installation de PowerPivot pour SharePoint|  
|Version du produit|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Cause|Voir ci-dessous.|  
|Texte du message|Impossible d'actualiser les données pour une connexion de données dans le classeur. Essayez encore ou contactez votre administrateur système. Échec de l'actualisation des connexions suivantes : Données PowerPivot|  
  
## <a name="explanation-and-resolution"></a>Explication et résolution  
 Excel Services ne peut pas se connecter aux données PowerPivot ou les charger. Les conditions qui provoquent cette erreur sont les suivantes :  
  
 **Scénario 1 : le service n'est pas démarré**  
  
 L'instance de SQL Server Analysis Services (PowerPivot) n'est pas démarrée. Un mot de passe périmé arrête l'exécution du service. Pour plus d’informations sur la modification du mot de passe, consultez [configurer les comptes de Service PowerPivot](configure-power-pivot-service-accounts.md) et [démarrer ou arrêter un PowerPivot pour SharePoint Server](start-or-stop-a-power-pivot-for-sharepoint-server.md).  
  
 **Scénario 2a : Ouverture d'un classeur de version antérieure sur le serveur**  
  
 Le classeur que vous essayez d'ouvrir peut avoir été créé dans la version SQL Server 2008 R2 de PowerPivot pour Excel. Très probablement, le fournisseur de données Analysis Services qui est spécifié dans la chaîne de connexion de données n'est pas présent sur l'ordinateur qui gère la demande.  
  
 Si c’est le cas, vous trouverez ce message dans le journal ULS : « Échec de l’actualisation pour les données de PowerPivot dans le classeur '\<URL du classeur >' », suivi de « Impossible d’obtenir une connexion ».  
  
 Pour déterminer la version du classeur, ouvrez-le dans Excel et vérifiez quel fournisseur de données est spécifié dans la chaîne de connexion. Un classeur SQL Server 2008 R2 utilise MSOLAP.4 comme fournisseur de données.  
  
 Pour contourner ce problème, vous pouvez mettre à niveau le classeur. Ou bien, vous pouvez installer les bibliothèques clientes de la version SQL Server 2008 R2 d'Analysis Services sur des ordinateurs physiques exécutant PowerPivot pour SharePoint ou Excel Services :  
  
 [Installer le fournisseur OLE DB Analysis Services sur des serveurs SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 **Scénario 2b : Excel Services s'exécute sur un serveur d'applications qui a une version incorrecte des bibliothèques clientes**  
  
 Par défaut, SharePoint Server 2010 installe la version SQL Server 2008 du fournisseur OLE DB Analysis Services sur les serveurs d'applications qui exécutent Excel Services. Dans une batterie de serveurs qui prend en charge l'accès aux données PowerPivot, tous les serveurs physiques exécutant des applications qui demandent des données PowerPivot, par exemple Excel Services et PowerPivot pour SharePoint, doivent utiliser une version ultérieure du fournisseur de données.  
  
 Les serveurs qui exécutent PowerPivot pour SharePoint obtiennent le fournisseur de données OLE DB mis à jour automatiquement. D'autres serveurs, tels que ceux qui exécutent une instance autonome d'Excel Services sans PowerPivot pour SharePoint sur le même ordinateur, doivent être corrigés pour utiliser les bibliothèques clientes plus récentes. Pour plus d’informations, voir [Install the Analysis Services OLE DB Provider on SharePoint Servers](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)(Installer le fournisseur OLE DB Analysis Services sur les serveurs SharePoint).  
  
 **Scénario 3 : le contrôleur de domaine n'est pas disponible**  
  
 La cause de l'erreur peut être qu'un contrôleur de domaine n'est pas disponible pour valider l'identité de l'utilisateur. Un contrôleur de domaine est requis par le service d'émission de jetons Revendications vers Windows pour authentifier l'utilisateur SharePoint à chaque connexion. Le service d'émission de jetons Revendications vers Windows n'utilise pas des informations d'identification mises en cache. Il valide l'identité de l'utilisateur pour chaque connexion.  
  
 Vous pouvez vérifier la cause de cette erreur en consultant le fichier journal SharePoint. Si les journaux SharePoint incluent le message « Échec de l'obtention de WindowsIdentity à partir de IClaimsIdentity », l'identité de l'utilisateur n'a pas pu être authentifiée.  
  
 Pour contourner ce problème, joignez l'ordinateur au même domaine que le serveur PowerPivot ou installez un contrôleur de domaine sur votre ordinateur local. La deuxième solution, l'installation du contrôleur de domaine, oblige à créer des comptes de domaine locaux pour tous les services et utilisateurs. Vous devrez configurer des comptes de service et des autorisations SharePoint pour les comptes que vous définissez.  
  
 L'installation d'un contrôleur de domaine sur votre ordinateur est utile si votre objectif est d'utiliser PowerPivot pour SharePoint hors connexion. Pour obtenir des instructions détaillées sur la façon d’utiliser PowerPivot hors connexion, consultez l’entrée de blog « Sortir votre serveur PowerPivot sur le réseau » [ http://www.powerpivotgeek.com ](http://go.microsoft.com/fwlink/?LinkId=184241).  
  
 **Scénario 4 : serveur instable**  
  
 Un ou plusieurs services peuvent être dans un état incohérent. Dans certains cas, l'exécution d'IISRESET résoudra le problème.  
  
  