---
title: Configurer SQL Server groupe de disponibilité AlwaysOn pour la haute disponibilité sur Linux
titleSuffix: SQL Server
description: En savoir plus sur la création d’un SQL Server toujours sur groupe de disponibilité (AG) pour la haute disponibilité sur Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 9f88178450fb5ca19e52703ad02e29d107ca562a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201958"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Configurer SQL Server groupe de disponibilité AlwaysOn pour la haute disponibilité sur Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Cet article décrit comment créer un SQL Server toujours sur groupe de disponibilité (AG) pour la haute disponibilité sur Linux. Il existe deux types de configuration pour les groupes de disponibilité. Un *haute disponibilité* configuration utilise un gestionnaire de cluster pour assurer la continuité. Cette configuration peut également inclure les réplicas en lecture à l’échelle. Ce document explique comment créer le groupe de disponibilité pour la haute disponibilité.

Vous pouvez également créer un groupe de disponibilité sans cluster manager pour *avec échelle lecture*. Le groupe de disponibilité pour la mise à l’échelle lecture fournit uniquement des réplicas en lecture seule pour la montée de performances. Il ne fournit pas de haute disponibilité. Pour créer un groupe de disponibilité avec échelle lecture, consultez [configurer un groupe de disponibilité SQL Server pour une échelle lecture sur Linux](sql-server-linux-availability-group-configure-rs.md).

Les configurations qui garantissent une haute disponibilité et protection des données nécessitent deux ou trois synchrone des réplicas de validation. Avec trois réplicas synchrones, le groupe de disponibilité peut récupérer automatiquement même si un serveur n’est pas disponible. Pour plus d’informations, consultez [haute disponibilité et protection des données pour les configurations de groupe de disponibilité](sql-server-linux-availability-group-ha.md). 

Tous les serveurs doivent être physique ou virtuel, et les serveurs virtuels doivent se trouver sur la même plateforme de virtualisation. Cette exigence est, car les agents de délimitation sont spécifiques à la plateforme. Consultez [stratégies pour les Clusters invités](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Feuille de route

Les étapes pour créer un groupe de disponibilité sur des serveurs Linux pour la haute disponibilité sont différentes de la procédure sur un cluster de basculement Windows Server. La liste suivante décrit les étapes principales : 

1. [Configurer SQL Server sur trois serveurs du cluster](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Tous les serveurs de trois dans le groupe de disponibilité doivent être sur la même plateforme - physique ou virtuelle - parce que la haute disponibilité de Linux utilise des agents de délimitation pour isoler des ressources sur les serveurs. Les agents de délimitation sont spécifiques pour chaque plateforme.

2. Créez le groupe de disponibilité. Cette étape est décrit dans cet article en cours. 

3. Configurer un gestionnaire de ressources de cluster, tels que Pacemaker.
   
   La façon de configurer un gestionnaire de ressources de cluster dépend de la distribution de Linux spécifique. Consultez les liens suivants pour obtenir des instructions spécifiques de distribution : 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Les environnements de production nécessitent un agent de délimitation, tels que STONITH pour la haute disponibilité. Démonstrations de cette documentation n’utilisent pas les agents de délimitation. Les démonstrations sont pour le test et validation uniquement. 
   
   >Un cluster Linux utilise délimitation pour retourner le cluster à un état connu. La façon de configurer la délimitation dépend de la distribution et l’environnement. Actuellement, la délimitation n’est pas disponible dans certains environnements de cloud. Pour plus d’informations, consultez [des stratégies de prise en charge pour RHEL haute disponibilité des Clusters - plateformes de virtualisation](https://access.redhat.com/articles/29440).
   
   >Pour SLES, consultez [Extension de haute disponibilité SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Ajoutez le groupe de disponibilité en tant que ressource dans le cluster.  

   La façon d’ajouter le groupe de disponibilité en tant que ressource dans le cluster dépend de la distribution Linux. Consultez les liens suivants pour obtenir des instructions spécifiques de distribution : 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Créer le groupe de disponibilité

Les exemples de cette section expliquent comment créer le groupe de disponibilité à l’aide de Transact-SQL. Vous pouvez également utiliser l’Assistant de groupe de disponibilité SQL Server Management Studio. Lorsque vous créez un groupe de disponibilité avec l’Assistant, elle retournera une erreur lorsque vous joignez les réplicas pour le groupe de disponibilité. Pour résoudre ce problème, accordez `ALTER`, `CONTROL`, et `VIEW DEFINITIONS` pour le pacemaker sur le groupe de disponibilité sur tous les réplicas. Une fois que les autorisations sont accordées sur le réplica principal, joignez les nœuds au groupe de disponibilité via l’Assistant, mais pour la haute disponibilité fonctionner correctement, accordez l’autorisation sur tous les réplicas.

Pour une configuration de haute disponibilité qui garantit que le basculement automatique, le groupe de disponibilité requiert au moins trois réplicas. Une des configurations suivantes peut prendre en charge une haute disponibilité :

- [Trois réplicas synchrones](sql-server-linux-availability-group-ha.md#threeSynch)

- [Deux réplicas synchrones ainsi qu’un réplica de la configuration](sql-server-linux-availability-group-ha.md#twoSynch)

Pour plus d’informations, consultez [haute disponibilité et protection des données pour les configurations de groupe de disponibilité](sql-server-linux-availability-group-ha.md).

>[!NOTE]
>Les groupes de disponibilité peuvent inclure des réplicas synchrones ou asynchrones. 

Créer le groupe de disponibilité pour la haute disponibilité sur Linux. Utilisez le [créer un groupe de disponibilité](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql) avec `CLUSTER_TYPE = EXTERNAL`. 

* Groupe de disponibilité - `CLUSTER_TYPE = EXTERNAL` Spécifie qu’une entité de cluster externe gère le groupe de disponibilité. Pacemaker est un exemple d’une entité de cluster externe. Lorsque le type de cluster de groupe de disponibilité est externe, 

* Définir les réplicas principaux et secondaires `FAILOVER_MODE = EXTERNAL`. 
   Spécifie que le réplica interagit avec un gestionnaire de cluster externe, telles que Pacemaker. 

Les scripts de Transact-SQL suivantes créent un groupe de disponibilité pour la haute disponibilité nommée `ag1`. Le script configure les réplicas de groupe de disponibilité avec `SEEDING_MODE = AUTOMATIC`. Ce paramètre indique à SQL Server créer automatiquement la base de données sur chaque serveur secondaire. Mettez à jour le script suivant en fonction de votre environnement. Remplacez le `<node1>`, `<node2>`, ou `<node3>` valeurs avec les noms des instances de SQL Server qui hébergent les réplicas. Remplacez le `<5022>` avec le port que vous définissez pour les données de point de terminaison de mise en miroir. Pour créer le groupe de disponibilité, exécutez l’instruction Transact-SQL suivant sur l’instance de SQL Server qui héberge le réplica principal.

Exécutez **qu’une seule** des scripts suivants : 

- [Créer le groupe de disponibilité avec trois réplicas synchrones](#threeSynch).
- [Créer le groupe de disponibilité avec deux réplicas synchrones et un réplica de la configuration](#configOnly)
- [Créer le groupe de disponibilité avec deux réplicas synchrones](#readScale).

<a name="threeSynch"></a>

- Créer un groupe de disponibilité avec trois réplicas synchrones

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >Après avoir exécuté le script précédent pour créer un groupe de disponibilité avec trois réplicas synchrones, ne pas exécuter le script suivant :

- Créer un groupe de disponibilité avec deux réplicas synchrones et un réplica de la configuration :

   >[!IMPORTANT]
   >Cette architecture permet à n’importe quelle édition de SQL Server pour héberger le réplica de tiers. Par exemple, le troisième réplica peut être hébergé sur SQL Server Enterprise Edition. Sur la version Enterprise Edition, est le type de point de terminaison valide uniquement `WITNESS`. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- Créer un groupe de disponibilité avec deux réplicas synchrones

   Inclure deux réplicas avec le mode de disponibilité synchrones. Par exemple, le script suivant crée un groupe de disponibilité appelé `ag1`. `node1` et `node2` hébergent des réplicas en mode synchrone, avec l’amorçage automatique et le basculement automatique.

   >[!IMPORTANT]
   >Exécutez uniquement le script suivant pour créer un groupe de disponibilité avec deux réplicas synchrones. N’exécutez pas le script suivant si vous avez exécuté un script précédent. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


Vous pouvez également configurer un groupe de disponibilité avec `CLUSTER_TYPE=EXTERNAL` à l’aide de SQL Server Management Studio ou PowerShell. 

### <a name="join-secondary-replicas-to-the-ag"></a>Joindre les réplicas secondaires au groupe de disponibilité

L’utilisateur pacemaker nécessite `ALTER`, `CONTROL`, et `VIEW DEFINITION` autorisations sur le groupe de disponibilité sur tous les réplicas. Pour accorder des autorisations, exécutez le script Transact-SQL suivant une fois le groupe de disponibilité est créé sur le réplica principal et chaque réplica secondaire immédiatement après leur ajout au groupe de disponibilité. Avant d’exécuter le script, remplacez `<pacemakerLogin>` par le nom du compte d’utilisateur pacemaker.

```Transact-SQL
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

Le script Transact-SQL suivant joint une instance de SQL Server à un groupe de disponibilité nommé `ag1`. Mettez à jour le script en fonction de votre environnement. Sur chaque instance de SQL Server qui héberge un réplica secondaire, exécutez Transact-SQL suivante pour joindre le groupe de disponibilité.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Après avoir créé le groupe de disponibilité, vous devez configurer l’intégration avec une technologie de cluster comme Pacemaker pour la haute disponibilité. Pour une configuration à l’échelle en lecture à l’aide de groupes de disponibilité, en commençant par [!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)], configuration d’un cluster n’est pas requis.

Si vous avez suivi les étapes décrites dans ce document, vous avez un groupe de disponibilité n’est pas mis en cluster. L’étape suivante consiste à ajouter le cluster. Cette configuration est valide pour les scénarios d’équilibrage de charge/mise à l’échelle en lecture, il n’est pas terminée pour la haute disponibilité. Pour la haute disponibilité, vous devez ajouter le groupe de disponibilité en tant que ressource de cluster. Consultez [étapes suivantes](#next-steps) pour obtenir des instructions. 

## <a name="notes"></a>Remarques

>[!IMPORTANT]
>Après avoir configuré le cluster et ajouter le groupe de disponibilité en tant que ressource de cluster, vous ne pouvez pas utiliser Transact-SQL pour basculer les ressources du groupe de disponibilité. Ressources de cluster de SQL Server sur Linux sont couplés pas aussi étroitement avec le système d’exploitation tels qu’ils sont sur un Cluster de basculement du serveur Windows (WSFC). Service SQL Server n’est pas informé de la présence du cluster. Tous les orchestration s’effectue via les outils de gestion de cluster. Dans RHEL ou Ubuntu utiliser `pcs`. Dans SLES utiliser `crm`. 

>[!IMPORTANT]
>Si le groupe de disponibilité est une ressource de cluster, il existe un problème connu dans la version actuelle, le basculement forcé avec perte de données vers un réplica asynchrone ne fonctionne pas. Ce problème sera résolu dans la version à venir. Basculement manuel ou automatique pour un réplica synchrone réussit.


## <a name="next-steps"></a>Étapes suivantes

[Configurer le Cluster Red Hat Enterprise Linux pour les ressources de Cluster de groupe de disponibilité de SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurer un Cluster SUSE Linux Enterprise Server pour les ressources de Cluster de groupe de disponibilité de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurer le Cluster Ubuntu pour les ressources de Cluster de groupe de disponibilité de SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
