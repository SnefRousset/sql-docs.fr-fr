---
title: Déployer des applications à l’aide de mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Déployer un script Python ou R en tant qu’application sur un cluster de données volumineux de SQL Server 2019 (version préliminaire).
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 83dc07ed6336c637aaf17fdcfc1075854fe542b7
ms.sourcegitcommit: d765563ccd03f299544bac233bc35f9b1df3fd47
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58434430"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>Comment déployer une application sur un cluster de données volumineux de SQL Server 2019 (version préliminaire)

Cet article décrit comment déployer et gérer le script R et Python en tant qu’application à l’intérieur d’un cluster de données volumineuses de SQL Server 2019 (version préliminaire).

## <a name="whats-new-and-improved"></a>What ' s nouvelles et améliorées

- Un utilitaire de ligne de commande unique pour gérer le cluster et application.
- Déploiement d’applications simplifié tout en fournissant un contrôle granulaire par le biais des fichiers spec.
- Prend en charge l’hébergement des types d’applications supplémentaires - SSIS et MLeap (Nouveautés de CTP 2.3)
- [Extension de VS Code](app-deployment-extension.md) pour gérer le déploiement d’application

Les applications sont déployées et gérées à l’aide `mssqlctl` utilitaire de ligne de commande. Cet article fournit des exemples montrant comment déployer des applications à partir de la ligne de commande. Découvrez comment utiliser cela dans Visual Studio Code font référence à [Extension VS Code](app-deployment-extension.md).

Les types d’applications suivants sont pris en charge :
- Applications R et Python (fonctions, modèles et applications)
- Fourniture de MLeap
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Prérequis

- [Cluster de données volumineux de SQL Server 2019](deployment-guidance.md)
- [mssqlctl command-line utility](deploy-install-mssqlctl.md)

## <a name="capabilities"></a>Fonctions

Dans SQL Server 2019 (version préliminaire) CTP 2.3 vous pouvez créer, supprimer, décrivent, initialiser, liste de s’exécuter et mettre à jour votre application. Le tableau suivant décrit les commandes de déploiement d’application que vous pouvez utiliser avec **mssqlctl**.

|Command |Description |
|:---|:---|
|`mssqlctl login` | Se connecter à un cluster de données volumineux de SQL Server |
|`mssqlctl app create` | Créer l’application. |
|`mssqlctl app delete` | Supprimer l’application. |
|`mssqlctl app describe` | Décrire l’application. |
|`mssqlctl app init` | Kickstart nouveau squelette d’application. |
|`mssqlctl app list` | Liste des applications. |
|`mssqlctl app run` | Exécuter l’application. |
|`mssqlctl app update`| Mettre à jour d’application. |

Vous pouvez obtenir de l’aide avec le `--help` paramètre comme dans l’exemple suivant :

```bash
mssqlctl app create --help
```

Les sections suivantes décrivent ces commandes plus en détail.

## <a name="log-in"></a>Connectez-vous

Avant de déployer ou d’interagir avec les applications, vous connecter à votre serveur SQL Server en cluster big data avec le `mssqlctl login` commande. Spécifiez l’adresse IP externe de la `endpoint-service-proxy` service (par exemple : `https://ip-address:30777`), ainsi que le nom d’utilisateur et le mot de passe pour le cluster.

```bash
mssqlctl login -e https://<ip-address-of-endpoint-service-proxy>:30777 -u <user-name> -p <password>
```

## <a name="aks"></a>AKS

Si vous utilisez AKS, vous devez exécuter la commande suivante pour obtenir l’adresse IP de la `endpoint-service-proxy` service en exécutant cette commande dans une fenêtre bash ou cmd :


```bash
kubectl get svc endpoint-service-proxy -n <name of your cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm ou Minikube

Si vous utilisez Kubeadm ou Minikube, exécutez la commande suivante pour obtenir l’adresse IP pour la connexion au cluster

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Créer une application

Pour créer une application, vous utilisez `mssqlctl` avec la `app create` commande. Ces fichiers résident localement sur l’ordinateur que vous créez l’application à partir de.

Pour créer une nouvelle application dans le cluster de données volumineux, utilisez la syntaxe suivante :

```bash
mssqlctl app create -n <app_name> -v <version_number> --spec <directory containing spec file>
```

La commande suivante montre un exemple de ce que cette commande peut ressembler :

Cela suppose que vous avez le fichier appelé `spec.yaml` au sein de la `addpy` dossier.
Le `addpy` dossier contient le `add.py` et `spec.yaml` le `spec.yaml` est un fichier de spécification pour le `add.py` application.


`add.py` crée l’application python suivant :

```py
#add.py
def add(x,y):
        result = x+y
        return result
result=add(x,y)
```

Le script suivant est un exemple du contenu pour `spec.yaml`:

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app
runtime: Python #the language this app uses (R or Python)
src: ./add.py #full path to the location of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

Pour tester cela, copiez les lignes de code ci-dessus dans deux fichiers dans le répertoire `addpy` comme `add.py` et `spec.yaml` et exécutez la commande suivante :

```bash
mssqlctl app create --spec ./addpy
```

> [!NOTE]
> Le `spec.yaml` fichier spécifie à la fois un `poolsize` et un nombre de `replicas`. Le nombre de `replicas` Spécifie le nombre de copies du service doit être déployées. Le `poolsize` Spécifie le nombre de pools à créer par réplica. Ces paramètres ont un impact sur le nombre de demandes que le déploiement peut gérer en parallèle. Le nombre maximal de demandes à un moment donné est égal à `replicas` fois `poolsize`, c'est-à-dire Si vous avez 5 réplicas et 2 pools par réplica le déploiement peut gérer 10 requêtes en parallèle. Voir l’image ci-dessous pour obtenir une représentation graphique de `replicas` et `poolsize`: ![Taiile_pool et réplicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Vous pouvez vérifier si l’application est déployée à l’aide de la commande list :

```bash
mssqlctl app list
```

Si le déploiement n’est pas terminé, vous devez voir le `state` afficher `WaitingforCreate` comme dans l’exemple suivant :

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Une fois le déploiement réussi, vous devez voir le `state` modifier à `Ready` état :

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>Une application de liste

Vous pouvez répertorier toutes les applications qui ont été créées avec le `app list` commande.

La commande suivante répertorie toutes les applications disponibles dans votre cluster big data :

```bash
mssqlctl app list
```

Si vous spécifiez un nom et la version, il répertorie cette application spécifique et son état (création ou prêt) :

```bash
mssqlctl app list --name <app_name> --version <app_version>
```

L’exemple suivant illustre cette commande :

```bash
mssqlctl app list --name add-app --version v1
```

Vous devez voir une sortie similaire à l’exemple suivant :

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>Exécuter une application

Si l’application est dans un `Ready` d’état, vous pouvez l’utiliser en l’exécutant avec vos paramètres d’entrée spécifiés. Pour exécuter une application, utilisez la syntaxe suivante :

```bash
mssqlctl app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

L’exemple de commande suivant montre la commande d’exécution :

```bash
mssqlctl app run --name add-app --version v1 --inputs x=1,y=2
```

Si l’exécution a réussi, vous devez voir votre sortie comme spécifié lors de la création de l’application. Voici un exemple.

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="create-an-app-skeleton"></a>Créer une structure de l’application

La commande init fournit une vue de structure avec les artefacts pertinentes qui est nécessaire pour déployer une application. L’exemple ci-dessous crée hello, vous pouvez le faire en exécutant la commande suivante.

```bash
mssqlctl app init --name hello --version v1 --template python
```

Cela créera un dossier appelé hello.  Vous pouvez `cd` dans le répertoire et inspecter les fichiers générés dans le dossier. spec.yaml définit l’application, telles que nom, version et le code source. Vous pouvez modifier la spécification pour modifier le nom, version, entrées et sorties.

Voici un exemple de sortie à partir de la commande init qui s’affiche dans le dossier

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>Décrire une application

La commande describe fournit des informations détaillées sur l’application, y compris le point de terminaison dans votre cluster. Cela est généralement utilisé par un développeur d’application pour générer une application à l’aide du client de swagger et le service Web pour interagir avec l’application de manière RESTful. Consultez [consommer des applications sur des clusters de données volumineuses](big-data-cluster-consume-apps.md) pour plus d’informations.

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30777/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30777/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>Supprimer une application

Pour supprimer une application à partir de votre cluster de données volumineux, utilisez la syntaxe suivante :

```bash
mssqlctl app delete --name add-app --version v1
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment intégrer des applications déployées sur SQL Server clusters de données volumineuses dans vos propres applications à [consommer des applications sur des clusters de données volumineuses](big-data-cluster-consume-apps.md) pour plus d’informations. Vous pouvez également consulter des exemples supplémentaires à [exemples de déploiement d’applications](https://aka.ms/sql-app-deploy).

Pour plus d’informations sur les clusters de données volumineuses de SQL Server, consultez [que sont les clusters de données volumineuses de SQL Server 2019 ?](big-data-cluster-overview.md).
