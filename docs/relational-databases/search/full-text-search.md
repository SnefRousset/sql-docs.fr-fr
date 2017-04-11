---
title: "Recherche en texte int&#233;gral | Microsoft Docs"
ms.custom: ""
ms.date: "07/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "recherche en texte intégral [SQL Server]"
ms.assetid: a0ce315d-f96d-4e5d-b4eb-ff76811cab75
caps.latest.revision: 54
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 49
---
# Recherche en texte int&#233;gral
  La recherche en texte intégral dans [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] et [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] permet aux utilisateurs et aux applications d’exécuter des requêtes de texte intégral sur des données caractères dans des tables [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Avant de pouvoir exécuter des requêtes de texte intégral sur une table, l'administrateur de base de données doit créer un index de recherche en texte intégral sur la table. L'index de recherche en texte intégral inclut une ou plusieurs colonnes de caractères dans la table. Ces colonnes peuvent être l’un des types de données suivants : **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml** ou **varbinary(max)** et FILESTREAM. Chaque index de recherche en texte intégral indexe une ou plusieurs colonnes de la table, et chaque colonne peut utiliser une langue spécifique.  
  
 Les requêtes de texte intégral effectuent des recherches linguistiques sur des données texte dans des index de recherche en texte intégral, en traitant les mots et les expressions à partir des règles spécifiques d'une langue telle que l'anglais ou le japonais. Les requêtes de texte intégral peuvent inclure des mots et des expressions simples ou plusieurs formes d'un mot ou d'une expression. Une requête de texte intégral retourne tous les documents qui contiennent au moins une correspondance (ce que l’on appelle aussi *résultat*). Une correspondance se produit lorsqu'un document cible contient tous les termes spécifiés dans la requête de texte intégral et satisfait toutes les autres conditions de recherche, telles que la distance entre les correspondances.  
  
> **REMARQUE :** La recherche en texte intégral est un composant facultatif du Moteur de base de données [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pour plus d’informations, consultez [Installer SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md).  
  
##  <a name="queries"></a> Recherche en texte intégral : requêtes  
 Une fois que des colonnes ont été ajoutées à un index de recherche en texte intégral, les utilisateurs et les applications peuvent exécuter des requêtes de texte intégral sur le texte contenu dans ces colonnes. Ces requêtes peuvent être utilisées pour rechercher les éléments suivants :  
  
-   Un ou plusieurs mots ou expressions spécifiques (*terme simple*)  
  
-   Un mot ou une expression commençant par un texte spécifié (*préfixe*)  
  
-   Les formes flexionnelles d’un mot spécifique (*forme canonique*)  
  
-   Un mot ou une expression proches d’un autre mot ou d’une autre expression (*terme de proximité*)  
  
-   Les formes synonymes d’un mot spécifique (*dictionnaire des synonymes*)  
  
-   Mots ou expressions utilisant des valeurs pondérées (*termes pondérés*)  
  
 Les requêtes de texte intégral ne respectent pas la casse. Par exemple, la recherche du terme « Aluminium » ou « aluminium » retourne les mêmes résultats.  
  
 Les requêtes de texte intégral utilisent un ensemble réduit de prédicats [!INCLUDE[tsql](../../includes/tsql-md.md)] (CONTAINS et FREETEXT) et de fonctions (CONTAINSTABLE et FREETEXTTABLE). Toutefois, les objectifs de la recherche pour un scénario d'entreprise donné influencent la structure des requêtes de texte intégral. Par exemple :  
  
-   Entreprise e-business : rechercher un produit sur un site Web :  
  
    ```  
    SELECT product_id   
    FROM products   
    WHERE CONTAINS(product_description, ”Snap Happy 100EZ” OR FORMSOF(THESAURUS,’Snap Happy’) OR ‘100EZ’)   
    AND product_cost < 200 ;  
    ```  
  
-   Scénario de recrutement : rechercher des postulants à un emploi qui connaissent bien [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
    ```  
    SELECT candidate_name,SSN   
    FROM candidates   
    WHERE CONTAINS(candidate_resume,”SQL Server”) AND candidate_division =DBA;  
    ```  
  
 Pour plus d’informations, consultez [Exécuter une requête avec une recherche en texte intégral](../../relational-databases/search/query-with-full-text-search.md).  
  
##  <a name="like"></a> Comparaison de LIKE et de la recherche en texte intégral  
 Contrairement à la recherche en texte intégral, le prédicat [LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] fonctionne uniquement sur les modèles de caractères. En outre, vous ne pouvez pas utiliser le prédicat LIKE pour interroger des données binaires mises en forme. De plus, une requête LIKE portant sur un important volume de données de texte non structurées est beaucoup plus lente qu'une requête de texte intégral équivalente exécutée sur les mêmes données. Une requête LIKE portant sur des millions de lignes de données de texte peut prendre plusieurs minutes pour retourner un résultat alors qu'une requête de texte intégral retourne en quelques secondes à peine le même résultat, en fonction du nombre de lignes retournées.  
  
##  <a name="architecture"></a> Composants et architecture  
 L'architecture de la recherche en texte intégral est constituée des processus suivants :  
  
-   Processus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (sqlservr.exe).  
  
-   Processus hôte de démon de filtre (fdhost.exe).  
  
     Pour des raisons de sécurité, les filtres sont chargés par des processus distincts appelés hôtes de démon de filtre. Les processus fdhost.exe sont créés par un service du lanceur FDHOST (MSSQLFDLauncher) et s'exécutent avec les informations d'identification de sécurité du compte du service du lanceur FDHOST. Par conséquent, le service du lanceur FDHOST doit être en cours d'exécution pour que l'indexation de texte intégral et l'exécution de requêtes de texte intégral puissent fonctionner. Pour plus d’informations sur le compte de service pour ce service, consultez [Définir le compte du service du Lanceur de démon de filtre de texte intégral](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md).  
  
 Ces deux processus contiennent les composants de l'architecture de recherche en texte intégral. Ces composants et leurs relations sont résumés dans l'illustration ci-dessous. Les composants sont décrits après l'illustration.  
  
 ![architecture de recherche en texte intégral](../../relational-databases/search/media/ifts-arch.gif "architecture de recherche en texte intégral")  
  
###  <a name="sqlprocess"></a> Processus SQL Server  
 Le processus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilisent les composants suivants pour la recherche en texte intégral :  
  
-   **Tables utilisateur.** Ces tables contiennent les données à indexer en texte intégral.  
  
-   **Outil d'extraction de texte intégral.** L'outil d'extraction de texte intégral fonctionne avec les threads d'analyse de texte intégral. Il est responsable de la planification et du pilotage du remplissage des index de texte intégral, ainsi que de la surveillance des catalogues de texte intégral.  
  
-   **Fichiers du dictionnaire des synonymes.** Ces fichiers contiennent des synonymes de termes de recherche. Pour plus d’informations, consultez [Configurer et gérer les fichiers de dictionnaire des synonymes pour la recherche en texte intégral](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
-   **Objets de la liste de mots vides.** Les objets de la liste de mots vides contiennent une liste de mots courants qui ne sont pas utiles pour la recherche. Pour plus d’informations, consultez [Configurer et gérer les mots vides et listes de mots vides pour la recherche en texte intégral](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Processeur de requêtes.** Le processeur de requêtes compile et exécute des requêtes SQL. Si une requête SQL inclut une requête de recherche en texte intégral, la requête est envoyée au Moteur d'indexation et de recherche en texte intégral, à la fois pendant la compilation et pendant l'exécution. Le résultat de la requête est opposé à l'index de texte intégral.  
  
-   **Moteur d'indexation et de recherche en texte intégral.** Le Moteur d’indexation et de recherche en texte intégral de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] est entièrement intégré au processeur de requêtes. Le Moteur d'indexation et de recherche en texte intégral compile et exécute les requêtes de texte intégral. Dans le cadre de l'exécution de la requête, le Moteur d'indexation et de recherche en texte intégral peut recevoir des entrées provenant du dictionnaire des synonymes et de la liste de mots vides.  
  
-   **Générateur d'index (indexeur).** Le générateur d'index crée la structure utilisée pour stocker les jetons indexés.  
  
-   **Gestionnaire du démon de filtre.** Le gestionnaire du démon de filtre est responsable de la surveillance de l'état du processus du démon du filtre du Moteur d'indexation et de recherche en texte intégral.  
  
##  <a name="fdhostprocess"></a> Processus hôte de démon de filtre  
 L'hôte de démon de filtre est un processus démarré par le Moteur d'indexation et de recherche en texte intégral. Il exécute les composants de recherche en texte intégral ci-dessous, chargés d'accéder aux données des tables, de les filtrer et d'en effectuer l'analyse lexicale, ainsi que d'effectuer l'analyse lexicale et d'identifier la racine des mots de l'entrée de requête.  
  
 Les composants de l'hôte de démon de filtre sont les suivants :  
  
-   **Gestionnaire de protocole.** Ce composant extrait les données de la mémoire en vue de leur traitement ultérieur et accède aux données d'une table utilisateur de la base de données spécifiée. Il est chargé, entre autres, de collecter les données des colonnes indexées en texte intégral et de transmettre ces données à l'hôte de démon de filtre, qui applique le filtrage et l'analyse lexicale, si besoin est.  
  
-   **Filtres.** Un filtrage peut être nécessaire sur certains types de données avant que les données d’un document puissent être indexées en texte intégral, notamment les données des colonnes **varbinary**, **varbinary(max)**, **image** ou **xml**. Le filtre utilisé pour un document donné dépend du type de celui-ci. Ainsi, différents filtres sont utilisés pour les documents Microsoft Word (.doc), les documents Microsoft Excel (.xls) et les documents XML (.xml). Ensuite, le filtre extrait des segments de texte du document, en supprimant la mise en forme incorporée et en conservant le texte et, éventuellement, les informations sur l'emplacement du texte. Un flux d'informations textuelles est ainsi généré. Pour plus d’informations, consultez [Configurer et gérer les extensions analytiques avancées](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
-   **Analyseurs lexicaux et générateurs de formes dérivées.** Un analyseur lexical est un composant spécifique d’une langue qui recherche des limites de mots en utilisant les règles lexicales de cette langue (*analyse lexicale*). Chaque analyseur lexical est associé à un composant de générateur de formes dérivées spécifique d'une langue qui conjugue des verbes et effectue des expansions fléchies. Au moment de l'indexation, l'hôte de démon de filtre utilise un analyseur lexical et un générateur de formes dérivées pour effectuer l'analyse linguistique sur les données textuelles d'une colonne de table donnée. La langue associée à une colonne de table dans l'index de recherche en texte intégral détermine l'analyseur lexical et le générateur de formes dérivées à utiliser pour indexer la colonne. Pour plus d’informations, consultez [Configurer et gérer les analyseurs lexicaux et générateurs de formes dérivées pour la recherche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
##  <a name="processing"></a> Traitement de la recherche en texte intégral  
 La recherche en texte intégral est rendue possible par le Moteur d'indexation et de recherche en texte intégral. Le Moteur d'indexation et de recherche en texte intégral assure deux rôles : prise en charge de l'indexation et prise en charge des requêtes.  
  
###  <a name="indexing"></a> Processus d’indexation de texte intégral  
 Au début d'une alimentation de texte intégral (également appelé analyse), le Moteur d'indexation et de recherche en texte intégral effectue l'envoi (push) de grands lots de données en mémoire et informe l'hôte de démon de filtre. L'hôte filtre et effectue une analyse lexicale des données et il convertit les données converties en listes de mots inversées. La recherche en texte intégral extrait ensuite les données converties des listes de mots, traite les données pour supprimer les mots vides et conserve les listes de mots pour un lot dans un ou plusieurs index inversés.  
  
 Pendant l’indexation des données stockées dans une colonne **varbinary(max)** ou **image**, le filtre qui implémente l’interface **IFilter** extrait le texte en fonction du format de fichier spécifié pour ces données (par exemple, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word). Dans certains cas, les composants de filtrage imposent que les données **varbinary(max)** ou **image** soient écrites dans le dossier de filtrage de données, au lieu d’être envoyées (push) en mémoire.  
  
 Dans le cadre du traitement, les données de texte collectées sont transmises à un analyseur lexical pour décomposer le texte en jetons individuels ou mots clés. La langue utilisée pour la création de jetons peut être spécifiée au niveau de la colonne ou être identifiée au sein des données **varbinary(max)**, **image** ou **xml** par le composant de filtrage.  
  
 Un traitement supplémentaire peut être effectué pour supprimer les mots vides et normaliser les jetons avant leur stockage dans l'index de recherche en texte intégral ou un fragment d'index.  
  
 À la fin d'une alimentation, une fusion finale est déclenchée ; les fragments d'index sont fusionnés entre eux dans un index de recherche en texte intégral. Il en résulte une amélioration des performances des requêtes dans la mesure où seul l'index principal doit être interrogé au lieu des fragments d'index ; par ailleurs, les statistiques de score sont plus appropriées pour un classement en fonction de la pertinence.  
  
###  <a name="querying"></a> Processus d’interrogation de texte intégral  
 Le processeur de requêtes passe les parties de texte intégral d'une requête au Moteur d'indexation et de recherche en texte intégral à des fins de traitement. Le Moteur d'indexation et de recherche en texte intégral effectue l'analyse lexicale et procède éventuellement à des expansions du dictionnaire des synonymes, à la recherche de radical et au traitement des mots vides (mots parasites). Ensuite, les parties de texte intégral de la requête sont représentées sous forme d'opérateurs SQL, essentiellement comme des fonctions table multi-diffusion. Au cours de l'exécution de la requête, ces fonctions table multi-diffusion accèdent à l'index inversé pour extraire les résultats corrects. Les résultats sont alors retournés au client ou bien ils font l'objet d'un traitement supplémentaire avant d'être retournés au client.  
  
##  <a name="components"></a> Composants linguistiques et prise en charge des langues dans la recherche en texte intégral  
 La recherche en texte intégral prend en charge environ 50 langues, dont l'anglais, l'espagnol, le chinois, le japonais, l'arabe, le bengali et l'hindi. Pour obtenir une liste complète des langues de texte intégral prises en charge, consultez [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md). Chacune des colonnes contenues dans l'index de recherche en texte intégral est associée à un identificateur de paramètres régionaux (LCID) Microsoft Windows qui représente une langue prise en charge par la recherche en texte intégral. Par exemple, le LCID 1033 correspond à l'anglais américain et le LCID 2057 à l'anglais britannique. Pour chaque langue de texte intégral prise en charge, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fournit des composants linguistiques qui acceptent l'indexation et l'interrogation des données de texte intégral qui sont stockées dans cette langue.  
  
 Les composants spécifiques à une langue sont les suivants :  
  
-   **Analyseurs lexicaux et générateurs de formes dérivées.** Un analyseur lexical détecte les limites de mots en fonction des règles lexicales définies pour une langue donnée (*analyse lexicale*). Chaque analyseur lexical est associé à un générateur de formes dérivées qui conjugue des verbes pour la même langue. Pour plus d’informations, consultez [Configurer et gérer les analyseurs lexicaux et générateurs de formes dérivées pour la recherche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
-   **Listes de mots vides.** Une liste de mots vides système contenant un jeu de base de mots vides (également appelés mots parasites) est fournie. Un *mot vide* n’est d’aucune utilité pour la recherche et est ignoré par les requêtes de texte intégral. Par exemple, en français, les mots tels que « un », « et », « est » ou « le » sont considérés comme des mots vides. En général, vous devez configurer un ou plusieurs fichiers de dictionnaires des synonymes et une ou plusieurs listes de mots vides. Pour plus d’informations, consultez [Configurer et gérer les mots vides et listes de mots vides pour la recherche en texte intégral](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **Fichiers du dictionnaire des synonymes.** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installe aussi un fichier de dictionnaire des synonymes pour chaque langue de texte intégral, ainsi qu’un fichier de dictionnaire des synonymes global. Les fichiers de dictionnaire des synonymes installés sont essentiellement vides, mais vous pouvez les modifier et définir des synonymes pour une langue ou un scénario d'entreprise spécifique. En développant un dictionnaire des synonymes adapté à vos données de texte intégral, vous pouvez élargir efficacement l'étendue des requêtes de texte intégral sur ces données. Pour plus d’informations, consultez [Configurer et gérer les fichiers de dictionnaire des synonymes pour la recherche en texte intégral](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
-   **Filtres (iFilters).**  L’indexation d’un document dans une colonne dont le type de données est **varbinary(max)**, **image** ou **xml** exige le traitement supplémentaire d’un filtre. Ce filtre doit être spécifique au type de document (.doc, .pdf, .xls, .xml, etc.). Pour plus d’informations, consultez [Configurer et gérer les extensions analytiques avancées](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 Les analyseurs lexicaux (et les générateurs de formes dérivées) et les filtres s'exécutent dans le processus hôte de démon de filtre (fdhost.exe).  
  
##  <a name="reltasks"></a> Tâches associées  
  
-   [Commencer à utiliser la recherche en texte intégral](../../relational-databases/search/get-started-with-full-text-search.md)  
  
-   **Écriture de requêtes de texte intégral**  
  
    -   [Exécuter une requête avec une recherche en texte intégral](../../relational-databases/search/query-with-full-text-search.md)  
  
    -   [Recherche de mots dans le voisinage d'autres mots avec NEAR](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)  
  
    -   [Limiter les résultats de la recherche avec RANK](../../relational-databases/search/limit-search-results-with-rank.md)  
  
    -   [Améliorer les performances des requêtes de texte intégral](../../relational-databases/search/improve-the-performance-of-full-text-queries.md)  
  
    -   [Rechercher les propriétés du document à l'aide des listes de propriétés de recherche](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
    -   [Recherche des GUID du jeu de propriétés et des ID d'entier de propriétés pour les propriétés de recherche](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
-   **Gestion des catalogues et des index**  
  
    -   [Créer et gérer des catalogues de texte intégral](../../relational-databases/search/create-and-manage-full-text-catalogs.md)  
  
    -   [Créer et gérer des index de recherche en texte intégral](../../relational-databases/search/create-and-manage-full-text-indexes.md)  
  
    -   [Choisir une langue lors de la création d'un index de recherche en texte intégral](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)  
  
    -   [Alimenter des index de recherche en texte intégral](../../relational-databases/search/populate-full-text-indexes.md)  
  
    -   [Gérer les index de recherche en texte intégral](../Topic/Manage%20Full-Text%20Indexes.md)  
  
    -   [Améliorer les performances des index de recherche en texte intégral](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
    -   [Résoudre l'indexation de recherche en texte intégral](../../relational-databases/search/troubleshoot-full-text-indexing.md)  
  
    -   [Sauvegarder et restaurer des catalogues et des index de recherche en texte intégral](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   **Gestion des composants linguistiques**  
  
    -   [Configurer et gérer des filtres pour la recherche](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
    -   [Configurer et gérer les analyseurs lexicaux et générateurs de formes dérivées pour la recherche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
    -   [Afficher ou modifier des filtres et des analyseurs lexicaux inscrits](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)  
  
    -   [Rétablir la version précédente des analyseurs lexicaux utilisés par la recherche](../../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
    -   [Modifier l'analyseur lexical utilisé pour l'anglais des États-Unis et l'anglais du Royaume-Uni](../../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
    -   [Personnaliser le comportement des analyseurs lexicaux avec un dictionnaire personnalisé](../../relational-databases/search/customize-the-behavior-of-word-breakers-with-a-custom-dictionary.md)  
  
    -   [Configurer et gérer les mots vides et listes de mots vides pour la recherche en texte intégral](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
    -   [Configurer et gérer les fichiers de dictionnaire des synonymes pour la recherche en texte intégral](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
-   **Gestion de la recherche en texte intégral**  
  
    -   [Gérer et surveiller la recherche en texte intégral pour une instance de serveur](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)  
  
    -   [Définir le compte du service du Lanceur de démon de filtre de texte intégral](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
  
-   [Mise à niveau de la fonction de recherche en texte intégral](../../relational-databases/search/upgrade-full-text-search.md)Mise à niveau de la fonction de recherche en texte intégral  
  
##  <a name="relcontent"></a> Contenu connexe  
  
-   [DDL, fonctions, procédures stockées et vues de recherche en texte intégral](../../relational-databases/search/full-text-search-ddl-functions-stored-procedures-and-views.md)  
  
  
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]