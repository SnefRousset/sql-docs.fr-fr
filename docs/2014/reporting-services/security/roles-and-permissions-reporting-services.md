---
title: Rôles et autorisations (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- access controls [Reporting Services]
- permissions [Reporting Services], about permissions
- security [Reporting Services], identity and access control
- authentication [Reporting Services]
- permissions [Reporting Services]
- security [Reporting Services], role-based
- identity [Reporting Services]
ms.assetid: eea655fe-43ed-418d-8233-b288a8f4daa4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ab60b588b276fd95e253d3ccf3fdeaf8ac71d409
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010971"
---
# <a name="roles-and-permissions-reporting-services"></a>Rôles et autorisations (Reporting Services)
  Reporting Services propose un sous-système d'authentification et un modèle d'autorisation basé sur les rôles. Les modèles d'authentification et d'autorisation varient selon que le serveur de rapports s'exécute en mode natif ou en mode SharePoint. Si le serveur de rapports fait partie d'un déploiement SharePoint, les autorisations SharePoint déterminent quels sont les utilisateurs qui ont accès au serveur de rapports.  
  
## <a name="identity-and-access-control-for-native-mode"></a>Identité et contrôle d'accès pour le mode natif  
 L'authentification par défaut repose sur l'authentification Windows et la sécurité intégrée. Vous pouvez modifier les paramètres d'authentification pour permettre au serveur de rapports de répondre à différentes demandes d'authentification, voire remplacer les fonctionnalités de sécurité par défaut par une extension d'authentification personnalisée que vous fournissez.  
  
 L'autorisation repose sur des rôles que vous assignez à un principal. Chaque rôle est constitué d'un jeu de tâches associées, elles-mêmes composées d'opérations connexes. Par exemple, la tâche **Gérer les rapports** accorde l’accès aux opérations de serveur de rapports suivantes : afficher les rapports, ajouter un rapport, mettre à jour un rapport, supprimer un rapport, planifier un rapport et mettre à jour les propriétés d’un rapport.  
  
## <a name="identity-and-access-control-for-sharepoint-mode"></a>Identité et contrôle d'accès pour le mode SharePoint  
 En mode intégré SharePoint, l'authentification et l'autorisation sont gérés sur le site SharePoint, avant que les demandes n'atteignent le serveur de rapports. Selon la configuration de l'authentification, les demandes émanant d'un site SharePoint incluent un jeton de sécurité ou un nom d'utilisateur de confiance. Les autorisations que vous définissez pour les utilisateurs ou les groupes SharePoint autorisent l'accès aux éléments du serveur de rapports placés dans les bibliothèques SharePoint.  
  
## <a name="in-this-section"></a>Dans cette section  
 [Octroi d'autorisations sur un serveur de rapports en mode natif](granting-permissions-on-a-native-mode-report-server.md)  
 Décrit le modèle d'autorisation basé sur les rôles, qui permet d'accéder au contenu et aux opérations.  
  
 [Accord d'autorisations sur des éléments de serveur de rapports sur un site SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 Explique comment utiliser les groupes SharePoint, les niveaux d'autorisation et les autorisations pour contrôler l'accès à un serveur de rapports.  
  
## <a name="see-also"></a>Voir aussi  
 [Authentification avec le serveur de rapports](authentication-with-the-report-server.md)   
 [Octroi d'autorisations sur un serveur de rapports en mode natif](granting-permissions-on-a-native-mode-report-server.md)  
  
  
