---
title: Former et enregistrer un modèle de Python à l’aide de T-SQL - SQL Server Machine Learning
description: Didacticiel Python montrant comment former et enregistrer un modèle à l’aide de Transact-SQL sur SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a0991f43ed7446cc9b86325d4f536a0787b8dcc1
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645170"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>Former et enregistrer un modèle de Python à l’aide de T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Cet article fait partie d’un didacticiel, [analytique en base de données Python pour les développeurs SQL](sqldev-in-database-python-for-sql-developers.md). 

Dans cette étape, vous allez apprendre à former un modèle d’apprentissage en utilisant les packages Python **scikit-Découvrez** et **revoscalepy**. Ces bibliothèques Python sont déjà installés avec SQL Server Machine Learning Services.

Vous chargez les modules et appelez les fonctions nécessaires pour créer et former le modèle à l’aide d’une procédure stockée SQL Server. Le modèle requiert les fonctionnalités de données que vous conçu dans les leçons précédentes. Enfin, vous enregistrez le modèle formé à un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table.
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Fractionner les exemples de données dans l’apprentissage et jeux de test

1. Créer une procédure stockée appelée **PyTrainTestSplit** pour diviser les données dans la table nyctaxi_sample en deux parties : nyctaxi_sample_training et nyctaxi_sample_testing. 

    Cette procédure stockée doit déjà être créée pour vous, mais vous pouvez exécuter le code suivant pour la créer :

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. Pour diviser vos données à l’aide d’un fractionnement personnalisé, exécutez la procédure stockée et tapez un entier qui représente le pourcentage de données allouées au jeu d’apprentissage. Par exemple, l’instruction suivante alloue 60 % des données au jeu d’apprentissage.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Générer un modèle de régression logistique

Une fois que les données a été préparées, vous pouvez l’utiliser pour former un modèle. Pour cela en appelant un stockée procédure qui s’exécute du code Python, en prenant comme entrée de la table de données d’apprentissage. Pour ce didacticiel, vous créez deux modèles, les deux modèles de classification binaire :

+ La procédure stockée **PyTrainScikit** crée un modèle de prédiction de pointe avec la **scikit-Découvrez** package.
+ La procédure stockée **TrainTipPredictionModelRxPy** crée un modèle de prédiction de pointe avec la **revoscalepy** package.

Chaque procédure stockée utilise les données d’entrée que vous fournissez pour créer et former un modèle de régression logistique. Tout le code Python est encapsulé dans la procédure stockée système, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Pour faciliter le reformer le modèle sur les nouvelles données, vous encapsulez l’appel à sp_execute_exernal_script dans une autre procédure stockée et passez les nouvelles données d’apprentissage en tant que paramètre. Cette section vous guidera tout au long de ce processus.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  Dans [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ouvrez une nouvelle **requête** fenêtre et exécutez l’instruction suivante pour créer la procédure stockée **PyTrainScikit**.  La procédure stockée contient une définition des données d’entrée, vous n’avez pas besoin de fournir une requête d’entrée.

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from sklearn.linear_model import LogisticRegression
    
    ##Create SciKit-Learn logistic regression model
    X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
    y = numpy.ravel(InputDataSet[["tipped"]])
    
    SKLalgo = LogisticRegression()
    logitObj = SKLalgo.fit(X, y)
    
    ##Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

2. Exécutez la commande suivante des instructions SQL pour insérer le modèle formé dans table nyc\_taxi_models.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    Traitement des données et l’ajustement du modèle peuvent prendre quelques minutes. Les messages éventuellement redirigés vers de Python **stdout** flux sont affichés dans le **Messages** fenêtre de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Exemple :

    *Message (s) STDOUT du script externe :*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Ouvrez la table *nyc\_taxi_models*. Vous pouvez voir qu’une nouvelle ligne a été ajoutée, avec le modèle sérialisé dans la colonne _model_.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561...*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Cette procédure stockée utilise le nouveau **revoscalepy** package, qui est un nouveau package pour Python. Il contient des objets, de transformation et d’algorithmes semblables à ceux fournis pour le langage R **RevoScaleR** package. 

À l’aide de **revoscalepy**, vous pouvez créer des contextes de calcul distants, déplacer des données entre les contextes de calcul, transformer des données et former des modèles prédictifs à l’aide d’algorithmes populaires comme la régression logistique et linéaire, arbres de décision, et plus. Pour plus d’informations, consultez [module revoscalepy dans SQL Server](../python/ref-py-revoscalepy.md) et [revoscalepy de référence des fonctions](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

1. Dans [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ouvrez une nouvelle **requête** fenêtre et exécutez l’instruction suivante pour créer la procédure stockée _TrainTipPredictionModelRxPy_.  Étant donné que la procédure stockée contenant déjà une définition des données d’entrée, vous n’avez pas besoin de fournir une requête d’entrée.

    ```sql
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    Cette procédure stockée effectue les étapes suivantes dans le cadre de l’apprentissage du modèle :

    - La requête SELECT s’applique la fonction scalaire personnalisée _fnCalculateDistance_ pour calculer la distance directe entre les emplacements de prélèvement et de débarquement. Les résultats de la requête sont stockés dans la variable d’entrée de Python par défaut, `InputDataset`.
    - La variable binaire _tipped_ est utilisé comme le *étiquette* ou de la colonne de résultat et le modèle est adapté à l’aide de ces colonnes de caractéristiques : _passenger_count_, _trip_ distance_, _trip_time_in_secs_, et _direct_distance_.
    - Le modèle formé est sérialisé et stocké dans la variable Python `logitObj`. En ajoutant le mot clé de T-SQL OUTPUT, vous pouvez ajouter la variable en tant que sortie de la procédure stockée. Dans l’étape suivante, cette variable est utilisée pour insérer le code binaire du modèle dans une table de base de données _nyc_taxi_models_. Ce mécanisme permet facile de stocker et réutiliser les modèles.

2. Exécutez la procédure stockée suivante pour insérer le formé **revoscalepy** modèle dans la table *nyc_taxi_models*.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    Traitement des données et l’ajustement du modèle peuvent prendre un certain temps. Les messages éventuellement redirigés vers de Python **stdout** flux sont affichés dans le **Messages** fenêtre de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Exemple :

    *Message (s) STDOUT du script externe :*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Ouvrez la table *nyc_taxi_models*. Vous pouvez voir qu’une nouvelle ligne a été ajoutée, avec le modèle sérialisé dans la colonne _model_.

    *revoscalepy_model* *0x8003637265766F7363616c...*

Dans l’étape suivante, vous utilisez les modèles formés pour créer des prédictions.

## <a name="next-step"></a>Étape suivante

[Exécuter des prédictions à l’aide de Python incorporé dans une procédure stockée](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Étape précédente

[Créer des caractéristiques de données à l’aide de T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
