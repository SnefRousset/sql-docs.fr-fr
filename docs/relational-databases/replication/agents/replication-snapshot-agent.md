---
title: "Agent d&#39;instantan&#233; de r&#233;plication | Microsoft Docs"
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
  - "Agent d’instantané, exécutables"
  - "agents [réplication SQL Server], Agent d’instantané"
  - "invite de commandes [réplication SQL Server]"
  - "Agent d’instantané, référence de paramètre"
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Agent d&#39;instantan&#233; de r&#233;plication
  L'Agent d'instantané de réplication est un fichier exécutable qui prépare les fichiers d'instantané contenant les schémas ainsi que les données des tables et des objets de base de données publiés, stocke les fichiers dans le dossier d'instantanés, et enregistre les travaux de synchronisation dans la base de données de distribution.  
  
> [!NOTE]  
>  Les paramètres peuvent être spécifiés dans n'importe quel ordre.  
  
## Syntaxe  
  
```  
  
snapshot [ -?]   
-Publisher server_name[\instance_name]   
-Publication publication_name   
[-70Subscribers]   
[-BcpBatchSize bcp_batch_size]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorDeadlockPriority [-1|0|1] ]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1] ]  
[-DynamicFilterHostName dynamic_filter_host_name]  
[-DynamicFilterLogin dynamic_filter_login]  
[-DynamicSnapshotLocation dynamic_snapshot_location]   
[-EncryptionLevel [0|1|2]]  
[-FieldDelimiter field_delimiter]  
[-HistoryVerboseLevel [0|1|2|3] ]  
[-HRBcpBlocks number_of_blocks ]  
[-HRBcpBlockSize block_size ]  
[-HRBcpDynamicBlocks ]  
[-KeepAliveMessageInterval keep_alive_interval]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads number_of_threads ]  
[-MaxNetworkOptimization [0|1]]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2] ]  
[-PacketSize packet_size]  
[-ProfileName profile_name]  
[-PublisherDB publisher_database]  
[-PublisherDeadlockPriority [-1|0|1] ]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-PublisherSecurityMode [0|1] ]  
[-QueryTimeOut query_time_out_seconds]  
[-ReplicationType [1|2] ]  
[-RowDelimiter row_delimiter]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-UsePerArticleContentsView use_per_article_contents_view]  
```  
  
## Arguments  
 **-?**  
 Imprime tous les paramètres disponibles.  
  
 **-Le serveur de publication**  *nom_serveur*[**\\***instance_name*]    
 Nom du serveur de publication. Spécifiez server_name pour l’instance par défaut de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sur ce serveur. Spécifiez *nom_serveur***\\***instance_name* pour une instance nommée de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sur ce serveur.  
  
 **-Publication** *publication*  
 Nom de la publication. Ce paramètre est uniquement valide si la publication est configurée de telle sorte qu'un instantané soit toujours disponible pour les nouveaux abonnements ou les abonnements réinitialisés.  
  
 **-70Subscribers**  
 Doit être utilisé si des abonnés exécutent [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] version 7.0.  
  
 **-BcpBatchSize** *bcp*_ *lot*\_ *taille*  
 Nombre de lignes à envoyer dans une opération de copie en bloc. Lorsque vous effectuez une opération **bcp in** , la taille du lot correspond au nombre de lignes à envoyer au serveur en une transaction, mais aussi au nombre de lignes à envoyer avant que l'Agent de distribution ne journalise un message de progression **bcp** . Lorsque vous effectuez une opération **bcp out** , une taille de lot fixe de 1000 est utilisée. La valeur 0 indique qu'aucune journalisation de message n'est autorisée.  
  
 **-DefinitionFile** *def_path_and_file_name*  
 Chemin d'accès du fichier de définition d'agent. Un fichier de définition d'agent contient des arguments de ligne de commande pour l'agent. Le contenu du fichier est analysé en tant que fichier exécutable. Utilisez des guillemets doubles (") pour spécifier des valeurs d'argument qui contiennent des caractères arbitraires.  
  
 **-Le serveur de distribution** *nom_serveur*[**\\***instance_name*]  
 Nom du serveur de distribution. Spécifiez *nom_serveur* pour l’instance par défaut de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sur ce serveur. Spécifiez *nom_serveur***\\***instance_name* pour une instance nommée de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sur ce serveur.  
  
 **-DistributorDeadlockPriority** [**-1**|**0**|**1**]  
 Priorité de la connexion de l'Agent d'instantané au serveur de distribution lorsqu'un blocage se produit. Ce paramètre est spécifié pour résoudre les blocages qui peuvent se produire entre l'Agent d'instantané et les applications utilisateur lors de la génération d'instantané.  
  
|Valeur DistributorDeadlockPriority|Description|  
|---------------------------------------|-----------------|  
|**-1**|Les applications autres que l'Agent d'instantané ont priorité lorsqu'un blocage se produit au niveau du serveur de distribution.|  
|**0** (par défaut)|La priorité n'est pas assignée.|  
|**1**|L'Agent d'instantané a priorité lorsqu'un blocage se produit au niveau du serveur de distribution.|  
  
 **-DistributorLogin** *distributor_login*  
 Nom de connexion utilisé pour la connexion au serveur de distribution avec l'authentification [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **-DistributorPassword** *distributor_password*  
 Mot de passe utilisé pour la connexion au serveur de distribution avec l'authentification [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. .  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Spécifie le mode de sécurité du serveur de distribution. Une valeur de **0** indique [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Mode d’authentification (par défaut) et la valeur **1** indique le Mode d’authentification Windows.  
  
 **-DynamicFilterHostName** *dynamic_filter_host_name*  
 Permet de définir une valeur pour [HOST_NAME & #40 ; Transact-SQL & #41 ;](../../../t-sql/functions/host-name-transact-sql.md) dans le filtrage lors d’une capture instantanée dynamique est créé. Par exemple, si la clause de filtre de sous-ensemble `rep_id = HOST_NAME()` est spécifié pour un article, et que vous définissez la **DynamicFilterHostName** la propriété « Fbjones » avant l’appel de l’Agent de fusion, seules les lignes contenant « FBJones » la **rep_id** colonne est répliquée.  
  
 **-DynamicFilterLogin** *dynamic_filter_login*  
 Permet de définir une valeur pour [SUSER_SNAME & #40 ; Transact-SQL & #41 ;](../../../t-sql/functions/suser-sname-transact-sql.md)dans le filtrage lors d’une capture instantanée dynamique est créé. Par exemple, si la clause de filtre de sous-ensemble `user_id = SUSER_SNAME()` est spécifié pour un article, et que vous définissez la **DynamicFilterLogin** propriété « rsmith » avant d’appeler le **exécuter** Procédé de la **SQLSnapshot** de l’objet, uniquement les lignes contenant « rsmith » la **user_id** colonne est incluse dans l’instantané.  
  
 **-DynamicSnapshotLocation** *dynamic_snapshot_location*  
 Emplacement où l'instantané dynamique doit être généré.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Niveau du chiffrement SSL (Secure Sockets Layer) utilisé par l'Agent d'instantané lors de l'établissement de connexions.  
  
|Valeur EncryptionLevel|Description|  
|---------------------------|-----------------|  
|**0**|Spécifie que le chiffrement SSL n'est pas utilisé.|  
|**1**|Spécifie que le chiffrement SSL est utilisé, mais que l'agent ne vérifie pas si le certificat de serveur SSL est signé par un émetteur de confiance.|  
|**2**|Spécifie que le chiffrement SSL est utilisé et que le certificat est vérifié.|  
  
 Pour plus d’informations, consultez [vue d’ensemble de la sécurité & #40 ; Réplication & #41 ;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-FieldDelimiter** *séparateur_de_champs*  
 Caractère ou séquence de caractères qui marque la fin d'un champ dans le fichier de données de copie en bloc [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La valeur par défaut est \n\<x$3>\n.  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 Spécifie la quantité d'informations d'historique journalisées pendant une opération d'instantané. Vous pouvez réduire l'effet de la journalisation d'historique sur les performances en sélectionnant **1**.  
  
|Valeur HistoryVerboseLevel|Description|  
|-------------------------------|-----------------|  
|**0**|Les messages de progression sont écrits dans la console ou dans un fichier de sortie. Les enregistrements d'historique ne sont pas journalisés dans la base de données de distribution.|  
|**1**|Met toujours à jour un message d'historique précédent du même état (démarrage, progression, succès, et ainsi de suite). Si aucun enregistrement précédent du même état n'existe, insère un nouvel enregistrement.|  
|**2** (par défaut)|Insère de nouveaux enregistrements d'historique, sauf s'il s'agit d'un enregistrement concernant notamment un message inactif ou un message de travail de longue durée, auquel cas les enregistrements précédents sont mis à jour.|  
|**3**|Insère toujours de nouveaux enregistrements, sauf s'il s'agit de messages inactifs.|  
  
 **-HRBcpBlocks** *nombre_de_blocs*  
 Est le nombre de **bcp** des blocs de données en file d’attente entre les threads de l’enregistreur et le lecteur. La valeur par défaut est 50. **HRBcpBlocks** est utilisé uniquement avec les publications Oracle.  
  
> [!NOTE]  
>  Ce paramètre est utilisé pour régler les performances de **bcp** performances à partir d’un serveur de publication Oracle.  
  
 -**HRBcpBlockSize***taille_bloc*  
 Est la taille, en kilo-octets (Ko), de chaque **bcp** du bloc de données. La valeur par défaut est 64 Ko. **HRBcpBlocks** est utilisé uniquement avec les publications Oracle.  
  
> [!NOTE]  
>  Ce paramètre est utilisé pour régler les performances de **bcp** performances à partir d’un serveur de publication Oracle.  
  
 **-HRBcpDynamicBlocks**  
 Est ou non la taille de chaque **bcp** du bloc de données peut croître dynamiquement. **HRBcpBlocks** est utilisé uniquement avec les publications Oracle.  
  
> [!NOTE]  
>  Ce paramètre est utilisé pour régler les performances de **bcp** performances à partir d’un serveur de publication Oracle.  
  
 **-KeepAliveMessageInterval** *keep_alive_interval*  
 Est la quantité de temps, en secondes, pendant laquelle l’Agent d’instantané attend avant de vous connecter à « attente de message de back-end » à la [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) table. La valeur par défaut est 300 secondes.  
  
 **-LoginTimeOut** *délai_de_connexion_en_secondes*  
 Nombre de secondes avant l'expiration de la connexion. La valeur par défaut est **15** secondes.  
  
 **-MaxBcpThreads** *number_of_threads*  
 Spécifie le nombre d'opérations de copie en bloc pouvant être effectuées en parallèle. Le nombre maximal de threads et de connexions ODBC pouvant exister simultanément est, en privilégiant la valeur la plus petite, **MaxBcpThreads** ou le nombre de demandes de copie en bloc qui apparaissent dans la transaction de synchronisation dans la base de données de distribution. **MaxBcpThreads** doit avoir une valeur supérieure à **0** et n’a aucune limite supérieure codée en dur. La valeur par défaut est **1**.  
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 Indique si les suppressions non pertinentes sont envoyées à l'Abonné. Les suppressions non pertinentes sont des commandes DELETE qui sont envoyées aux Abonnés pour les lignes qui n'appartiennent pas à la partition de l'Abonné. Les suppressions non pertinentes n'affectent ni l'intégrité ni la convergence des données, mais elles peuvent générer un trafic réseau inutile. La valeur par défaut de **MaxNetworkOptimization** est **0**. Le fait d'attribuer à **MaxNetworkOptimization** la valeur **1** réduit le risque d'obtention de suppressions non pertinentes, minimisant ainsi le trafic réseau et maximisant l'optimisation du réseau. L'attribution de la valeur **1** à ce paramètre peut aussi augmenter le stockage des métadonnées et entraîner une réduction des performances au niveau du serveur de publication si plusieurs niveaux de filtres de jointure et des filtres de sous-ensemble complexes sont présents. Vous devez évaluer avec soin votre topologie de réplication et attribuer uniquement à **MaxNetworkOptimization** la valeur **1** si le trafic réseau des suppressions non pertinentes est trop élevé.  
  
> [!NOTE]  
>  Ce paramètre **1** est utile uniquement lorsque l’option d’optimisation de la synchronisation de la publication de fusion a la valeur **true** (le **@keep_partition_changes** paramètre de [sp_addmergepublication & #40 ; Transact-SQL & #41 ;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
 **-Output** *output_path_and_file_name*  
 Chemin d'accès du fichier de sortie de l'agent. Si le nom du fichier n'est pas spécifié, la sortie est envoyée à la console. Si le nom de fichier spécifié existe, la sortie est ajoutée au fichier.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Spécifie si la sortie doit être en clair.  
  
|Valeur OutputVerboseLevel|Description|  
|------------------------------|-----------------|  
|**0**|Seuls les messages d'erreur sont imprimés.|  
|**1** (par défaut)|Tous les messages du rapport de progression sont imprimés (valeur par défaut).|  
|**2**|Tous les messages d'erreur et tous les messages du rapport de progression sont imprimés, ce qui peut s'avérer utile lors du débogage.|  
  
 **-PacketSize** *packet_size*  
 Taille du paquet (en octets) utilisée par l'Agent d'instantané lors de la connexion à [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La valeur par défaut est 8 192 octets.  
  
> [!NOTE]  
>  Ne modifiez pas la taille des paquets, sauf si vous êtes certain que cela permettra d'accroître les performances. Pour la plupart des applications, la taille de paquet par défaut représente la meilleure solution.  
  
 **-ProfileName** *nom_profil*  
 Spécifie un profil d'agent à utiliser pour les paramètres d'agent. Si **ProfileName** a la valeur NULL, le profil d'agent est désactivé. Si **ProfileName** n'est pas spécifié, le profil par défaut du type d'agent est utilisé. Pour plus d’informations, consultez [profils d’Agent de réplication](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-PublisherDB** *publisher_database*  
 Nom de la base de données de publication. *Ce paramètre n'est pas pris en charge pour les serveurs de publication Oracle*.  
  
 **-PublisherDeadlockPriority** [**-1**|**0**|**1**]  
 Priorité de la connexion de l'Agent d'instantané au serveur de publication lorsqu'un blocage se produit. Ce paramètre est spécifié pour résoudre les blocages qui peuvent se produire entre l'Agent d'instantané et les applications utilisateur lors de la génération d'instantané.  
  
|Valeur PublisherDeadlockPriority|Description|  
|-------------------------------------|-----------------|  
|**-1**|Les applications autres que l'Agent d'instantané ont priorité lorsqu'un blocage se produit au niveau du serveur de publication.|  
|**0** (par défaut)|La priorité n'est pas assignée.|  
|**1**|L'Agent d'instantané a priorité lorsqu'un blocage se produit au niveau du serveur de publication.|  
  
 **-PublisherFailoverPartner** *nom_serveur*[**\\***instance_name*]  
 Spécifie l'instance du partenaire de basculement de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] participant à une session de mise en miroir de bases de données avec la base de données de publication. Pour plus d’informations, consultez [mise en miroir de base de données et réplication & #40 ; SQL Server & #41 ;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherLogin** *publisher_login*  
 Nom de connexion utilisé pour la connexion au serveur de publication avec l'authentification [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **-PublisherPassword**  *publisher_password*  
 Mot de passe utilisé pour la connexion au serveur de publication avec l'authentification [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. .  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 Spécifie le mode de sécurité du serveur de publication. Une valeur de **0** indique [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentication (par défaut) et la valeur **1** indique le Mode d’authentification Windows.  
  
 **-QueryTimeOut** *délai_de_requête_en_secondes*  
 Nombre de secondes avant l'expiration de la requête. La valeur par défaut est 1800 secondes.  
  
 **-ReplicationType** [ **1**| **2**]  
 Spécifie le type de la réplication. La valeur **1** indique la réplication transactionnelle, tandis que la valeur **2** indique la réplication de fusion.  
  
 **-RowDelimiter** *séparateur_de_lignes*  
 Caractère ou séquence de caractères qui marque la fin d'une ligne dans le fichier de données de copie en bloc [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La valeur par défaut est \n\<,@g>\n.  
  
 **-StartQueueTimeout** *start_queue_timeout_seconds*  
 Est le nombre maximal de secondes pendant lesquelles l’Agent d’instantané attend lorsque le nombre de processus de capture instantanée dynamique simultanés en cours d’exécution a atteint la limite définie par le **@max_concurrent_dynamic_snapshots** propriété du [sp_addmergepublication & #40 ; Transact-SQL & #41 ;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Si le nombre maximal de secondes est atteint et que l'Agent d'instantané attend toujours, celui-ci se ferme. La valeur 0 signifie que l'Agent attend indéfiniment, bien qu'il soit possible de l'annuler.  
  
 \- **UsePerArticleContentsView** *use_per_article_contents_view*  
 Ce paramètre est déconseillé et n'est pris en charge que dans un but de compatibilité ascendante.  
  
## Notes  
  
> [!IMPORTANT]  
>  Si vous avez installé l'Agent [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pour s'exécuter sous un compte système local plutôt que sous un compte d'utilisateur de domaine (option par défaut), le service peut uniquement accéder à l'ordinateur local. Si l'Agent d'instantané qui s'exécute sous l'Agent [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] est configuré pour utiliser le mode d'authentification Windows lorsqu'il se connecte à [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'Agent d'instantané échoue. Le paramètre par défaut est l'authentification [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Pour démarrer l'Agent d'instantané, exécutez **snapshot.exe** à l'invite de commandes. Pour plus d'informations, consultez [Concepts des exécutables de l'agent de réplication](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Voir aussi  
 [Administration de l'Agent de réplication](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  