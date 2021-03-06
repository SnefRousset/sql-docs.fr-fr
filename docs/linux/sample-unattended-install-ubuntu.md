---
title: Installation sans assistance pour SQL Server sur Ubuntu
titleSuffix: SQL Server
description: Exemple de Script SQL Server - installation sans assistance sur Ubuntu
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.openlocfilehash: 878eda9c8816e400c873154f1c1cf3d613f8fea3
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579049"
---
# <a name="sample-unattended-sql-server-installation-script-for-ubuntu"></a>Exemple : Script d’installation de SQL Server sans assistance pour Ubuntu

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Cet exemple de script Bash installe SQL Server 2017 sur Ubuntu 16.04 sans entrée interactive. Il fournit des exemples d’installation du moteur de base de données, les outils de ligne de commande de SQL Server, SQL Server Agent et effectue les étapes de post-installation. Vous pouvez éventuellement installer la recherche en texte intégral et créer un utilisateur administratif.

> [!TIP]
> Si vous n’avez pas besoin d’un script d’installation sans assistance, le moyen le plus rapide pour installer SQL Server consiste à suivre le [Guide de démarrage rapide pour Ubuntu](quickstart-install-connect-ubuntu.md). Pour en savoir plus le programme d’installation, consultez [consignes d’Installation pour SQL Server sur Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prérequis

- Vous avez besoin d’au moins 2 Go de mémoire pour exécuter SQL Server sur Linux.
- Le système de fichiers doit être **XFS** ou **EXT4**. D'autres systèmes de fichiers tels que **BTRFS**, ne sont pas pris en charge.
- Pour les autres exigences système, consultez [configuration système requise pour SQL Server sur Linux](sql-server-linux-setup.md#system).

## <a name="sample-script"></a>Exemple de script

```bash
#!/bin/bash -e

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_INSTALL_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
sudo add-apt-repository "${repoargs}"
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
sudo add-apt-repository "${repoargs}"

echo Running apt-get update -y...
sudo apt-get update -y

echo Installing SQL Server...
sudo apt-get install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo apt-get install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo apt-get install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring UFW to allow traffic on port 1433...
sudo ufw allow 1433/tcp
sudo ufw reload

# Optional example of post-installation configuration.
# Trace flags 1204 and 1222 are for deadlock tracing.
# echo Setting trace flags...
# sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after installing:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 3s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

### <a name="running-the-script"></a>Le script en cours d’exécution

Pour exécuter le script

1. Collez l’exemple dans votre éditeur de texte et enregistrez-le avec un nom facile à mémoriser, par exemple `install_sql.sh`.

1. Personnaliser `MSSQL_SA_PASSWORD`, `MSSQL_PID`et toutes les autres variables que vous souhaitez modifier.

1. Rendez le script exécutable

   ```bash
   chmod +x install_sql.sh
   ```

1. Exécutez le script

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>Description du script
La première chose que fait le script Bash est définir quelques variables. Il peuvent s’agir des variables de script, comme dans l’exemple, ou des variables d’environnement. La variable `MSSQL_SA_PASSWORD` est **requis** par l’installation de SQL Server, les autres sont des variables personnalisées créées pour le script. L’exemple de script effectue les étapes suivantes :

1. Importez les clés publiques de Microsoft GPG.

1. Inscrire les référentiels de Microsoft pour SQL Server et les outils de ligne de commande.

1. Mettre à jour les référentiels locaux

1. Installer SQL Server

1. Configurer SQL Server avec le ```MSSQL_SA_PASSWORD``` et d’accepter automatiquement le contrat de licence utilisateur final.

1. Accepter le contrat de licence utilisateur final pour les outils de ligne de commande de SQL Server, installez-les et installer le package unixodbc-dev automatiquement.

1. Ajouter les outils de ligne de commande de SQL Server pour le chemin d’accès pour la facilité d’utilisation.

1. Installer l’Agent SQL Server, si la variable de script ```SQL_INSTALL_AGENT``` est défini sur par défaut.

1. Si vous le souhaitez installer recherche en texte intégral SQL Server, si la variable ```SQL_INSTALL_FULLTEXT``` est définie.

1. Débloquer le port 1433 pour TCP sur le pare-feu de système, nécessaire pour se connecter à SQL Server à partir d’un autre système.

1. Si vous le souhaitez définir des indicateurs de trace pour le suivi de blocage. (nécessite ensuite)

1. SQL Server est maintenant installé, pour le rendre opérationnel, redémarrez le processus.

1. Vérifiez que SQL Server est installé correctement, tout en masquant les messages d’erreur.

1. Créer un nouvel utilisateur d’administrateur de serveur si ```SQL_INSTALL_USER``` et ```SQL_INSTALL_USER_PASSWORD``` sont toutes deux définies.

## <a name="next-steps"></a>Étapes suivantes

Simplifier plusieurs installations sans assistance et créer un script Bash autonome qui définit les variables d’environnement appropriées. Vous pouvez supprimer une des variables de l’exemple de script utilise et les placer dans leur propre script Bash.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

Puis exécutez le script Bash comme suit :
```bash
. ./my_script_name.sh
```

Pour plus d’informations sur SQL Server sur Linux, consultez [SQL Server sur Linux](sql-server-linux-overview.md).
