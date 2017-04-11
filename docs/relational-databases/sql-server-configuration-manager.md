---
title: "Gestionnaire de configuration SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "protocoles [SQL Server], gestion"
  - "protocoles réseau [SQL Server], gestion"
  - "Utilitaire réseau client"
  - "comptes [SQL Server]"
  - "Gestionnaire de configuration SQL Server"
  - "Utilitaire réseau serveur"
  - "comptes [SQL Server], services"
  - "services [SQL Server], gestion"
  - "outils [SQL Server], Gestionnaire de configuration SQL Server"
  - "gestionnaire de configuration [SQL Server]"
ms.assetid: e6beaea4-164c-4078-95ae-b9e28b0aefe8
caps.latest.revision: 58
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 58
---
# Gestionnaire de configuration SQL Server
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] est un outil qui permet de gérer les services associés à [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], de configurer les protocoles réseau utilisés par [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]et de gérer la configuration de la connectivité réseau à partir des ordinateurs clients [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Le Gestionnaire de configuration est un composant logiciel enfichable MMC ([!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console), accessible à partir du menu Démarrer ou qui peut être ajouté dans tout autre affichage [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console. [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (**mmc.exe**) utilise le fichier **SQLServerManager\<version>.msc** (par exemple, **SQLServerManager13.msc** pour [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]) pour ouvrir le Gestionnaire de configuration. Voici les chemins d’accès aux quatre dernières versions lorsque Windows est installé sur le lecteur C.  
  
|||  
|-|-|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
|[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  
> [!NOTE]  
>  Étant donné que le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] est un composant logiciel enfichable pour le programme [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console et non pas un programme autonome, le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] n’apparaît pas en tant qu’application dans les versions plus récentes de Windows.  
>   
>  -   **Windows 10** :  
>          Pour ouvrir le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], dans la **page d’accueil**, tapez SQLServerManager13.msc (pour [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]). Pour les versions antérieures de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , remplacez 13 par un nombre plus petit. Le fait de cliquer sur SQLServerManager13.msc ouvre le Gestionnaire de configuration. Pour épingler le Gestionnaire de configuration à la page d’accueil ou à la barre des tâches, cliquez avec le bouton droit sur SQLServerManager13.msc, puis cliquez sur **Ouvrir l’emplacement du fichier**. Dans l’Explorateur de fichiers Windows, cliquez avec le bouton droit sur SQLServerManager13.msc, puis cliquez sur **Épingler à l’écran d’accueil** ou **Épingler à la barre des tâches**.  
> -   **Windows 8** :  
>          Pour ouvrir le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], sur l’icône **Rechercher**, sous **Applications**, tapez **SQLServerManager\<version>.msc**, par exemple **SQLServerManager13.msc**, puis appuyez sur **Entrée**.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Le Gestionnaire de configuration et SQL Server Management Studio utilisent WMI (Window Management Instrumentation) pour afficher et modifier certains paramètres de serveur. WMI offre une méthode unique d'interface avec les appels API qui gèrent les opérations de registre requises par les outils [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Il permet également un contrôle et une manipulation avancés des services SQL sélectionnés du composant logiciel enfichable Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Pour plus d’informations sur la configuration des autorisations liées à WMI, consultez [Configurer WMI pour afficher l’état du serveur dans les outils SQL Server](../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md).  
  
 Pour démarrer, arrêter, interrompre, reprendre ou configurer les services sur un autre ordinateur à l’aide du Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consultez [Se connecter à un autre ordinateur &#40;Gestionnaire de configuration SQL Server&#41;](../database-engine/configure-windows/connect-to-another-computer-sql-server-configuration-manager.md).  
  
## Gestion des services  
 Utilisez le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pour démarrer, interrompre, activer ou arrêter les services, ainsi que pour afficher ou modifier les propriétés des services.  
  
 Utilisez le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pour démarrer le [!INCLUDE[ssDE](../includes/ssde-md.md)] à l'aide de paramètres de démarrage.  Pour plus d’informations, consultez [Configurer les options de démarrage du serveur &#40;Gestionnaire de configuration SQL Server&#41;](../database-engine/configure-windows/configure-server-startup-options-sql-server-configuration-manager.md).  
  
## Modification des comptes utilisés par les services  
 Gérez les services [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à l'aide du Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Utilisez toujours des outils [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , tels que le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , pour modifier le compte utilisé par [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou les services Agent [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] et pour changer le mot de passe du compte. Outre la modification du nom de compte, le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] effectue d'autres configurations telles que la définition des autorisations dans le Registre Windows pour que le nouveau compte puisse lire les paramètres [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . D'autres outils tels que le gestionnaire de contrôle de services Windows peuvent modifier le nom du compte mais pas les paramètres associés. Si le service n'a pas accès à la section [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] du Registre, il est possible qu'il ne démarre pas correctement.  
  
 Les mots de passe modifiés à l'aide du Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], de SMO ou de WMI sont pris en compte immédiatement sans avoir à redémarrer le service.  
  
## Gestion des protocoles réseau serveur et clients  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vous permet de configurer les protocoles réseau serveur et clients ainsi que les options de connectivité. Une fois les protocoles adéquats activés, vous n'avez généralement pas besoin de modifier les connexions réseau du serveur. Toutefois, vous pouvez utiliser le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] si vous devez reconfigurer les connexions du serveur afin que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puisse écouter sur un protocole réseau, un port ou un canal spécifique. Pour plus d’informations sur l’activation des protocoles, consultez [Activer ou désactiver un protocole réseau de serveur](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md). Pour plus d’informations sur l’activation de l’accès aux protocoles via un pare-feu, consultez [Configurer le Pare-feu Windows pour autoriser l’accès à SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Le Gestionnaire de configuration vous permet de gérer les protocoles réseau serveur et clients en vous offrant la possibilité d’appliquer le chiffrement de protocole, d’afficher les propriétés d’alias et d’activer ou de désactiver un protocole.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vous permet de créer ou de supprimer des alias, de modifier l'ordre d'utilisation des protocoles ou d'afficher les propriétés de l'alias d'un serveur, notamment :  
  
-   Alias de serveur — Alias du serveur utilisé pour l'ordinateur auquel le client se connecte.  
  
-   Protocole — Protocole réseau utilisé pour l'entrée de configuration.  
  
-   Paramètres de connexion — Paramètres associés à l'adresse de connexion pour la configuration du protocole réseau.  
  
 Le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vous permet également d'afficher des informations sur les instances de cluster de basculement, bien que l'Administrateur de cluster doive être utilisé pour certaines actions comme le démarrage et l'arrêt des services.  
  
### Protocoles réseau disponibles  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] prend en charge les protocoles de mémoire partagée, TCP/IP et des canaux nommés. Pour plus d'informations sur le choix d'un protocole réseau, consultez [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md). [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ne prend pas en charge les protocoles réseau VIA, Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk ni NWLink IPX/SPX. Les clients qui se connectaient précédemment à l'aide de ces protocoles doivent sélectionner un autre protocole pour se connecter à [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Vous ne pouvez pas utiliser le Gestionnaire de configuration [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pour configurer le proxy WinSock. Pour configurer le proxy WinSock, reportez-vous à la documentation ISA Server.  
  
## Tâches associées  
 [Rubriques de procédures concernant la gestion des services &#40;Gestionnaire de configuration SQL Server&#41;](../Topic/Managing%20Services%20How-to%20Topics%20\(SQL%20Server%20Configuration%20Manager\).md)  
  
 [Démarrer, arrêter, suspendre, reprendre, redémarrer le moteur de base de données, SQL Server Agent ou le service SQL Server Browser](../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)  
  
 [Démarrer, arrêter ou suspendre le service SQL Server Agent](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
 [Définir le démarrage automatique d’une instance de SQL Server &#40;Gestionnaire de configuration SQL Server&#41;](../database-engine/configure-windows/scm services - set an instance to start automatically.md)  
  
 [Empêcher le démarrage automatique d’une instance de SQL Server &#40;Gestionnaire de configuration SQL Server&#41;](../database-engine/configure-windows/scm services - prevent automatic startup of an instance.md)  
  
  