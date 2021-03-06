---
title: SQLBindParameter, fonction | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc566c7cfd86e76df5389e56b7465dcd04b76f51
ms.sourcegitcommit: 3c4bb35163286da70c2d669a3f84fb6a8145022c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57683639"
---
# <a name="sqlbindparameter-function"></a>Fonction SQLBindParameter

**Conformité**  
 Version introduite : Conformité aux normes 2.0 ODBC : ODBC  
  
 **Résumé**  
 **SQLBindParameter** lie une mémoire tampon à un marqueur de paramètre dans une instruction SQL. **SQLBindParameter** prend en charge la liaison à un type de données Unicode C, même si le pilote sous-jacent ne prend pas en charge les données Unicode.  
  
> [!NOTE]  
>  Cette fonction remplace la fonction ODBC 1.0 **SQLSetParam**. Pour plus d’informations, consultez « Commentaires ».  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```
  
## <a name="arguments"></a>Arguments

 *StatementHandle*  
 [Entrée] Descripteur d’instruction.  
  
 *ParameterNumber*  
 [Entrée] Numéro du paramètre, triées séquentiellement ordre croissant des paramètres, en commençant à 1.  
  
 *InputOutputType*  
 [Entrée] Le type du paramètre. Pour plus d’informations, consultez «*InputOutputType* Argument » dans « Commentaires ».  
  
 *ValueType*  
 [Entrée] Le type de données C du paramètre. Pour plus d’informations, consultez «*ValueType* Argument » dans « Commentaires ».  
  
 *ParameterType*  
 [Entrée] Le type de données SQL du paramètre. Pour plus d’informations, consultez «*ParameterType* Argument » dans « Commentaires ».  
  
 *ColumnSize*  
 [Entrée] La taille de la colonne ou l’expression du marqueur de paramètre correspondant. Pour plus d’informations, consultez «*ColumnSize* Argument » dans « Commentaires ».  
  
 Si votre application s’exécutera sur un système d’exploitation de Windows 64 bits, consultez [informations sur ODBC 64 bits](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *DecimalDigits*  
 [Entrée] Les chiffres décimaux de la colonne ou l’expression du marqueur de paramètre correspondant. Pour plus d’informations sur la taille de colonne, consultez [taille de colonne, des chiffres décimaux, transférer la longueur en octets et la taille d’affichage](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParameterValuePtr*  
 [Entrée différée] Pointeur vers une mémoire tampon pour les données du paramètre. Pour plus d’informations, consultez «*ParameterValuePtr* Argument » dans « Commentaires ».  
  
 *BufferLength*  
 [Entrée/sortie] Longueur de la *ParameterValuePtr* mémoire tampon en octets. Pour plus d’informations, consultez «*BufferLength* Argument » dans « Commentaires ».  
  
 Consultez [informations sur ODBC 64 bits](../../../odbc/reference/odbc-64-bit-information.md), si votre application s’exécutera sur un système d’exploitation 64 bits.  
  
 *StrLen_or_IndPtr*  
 [Entrée différée] Pointeur vers une mémoire tampon pour la longueur du paramètre. Pour plus d’informations, consultez «*StrLen_or_IndPtr* Argument » dans « Commentaires ».  
  
## <a name="returns"></a>Valeur renvoyée

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostics

 Lorsque **SQLBindParameter** retourne SQL_ERROR ou SQL_SUCCESS_WITH_INFO, une valeur SQLSTATE associée peut être obtenu en appelant **SQLGetDiagRec** avec un *HandleType* de SQL_HANDLE_STMT et un *gérer* de *au paramètre StatementHandle*. Le tableau suivant répertorie les valeurs SQLSTATE généralement retournées par **SQLBindParameter** et explique chacune dans le contexte de cette fonction ; la notation « (DM) » précède les descriptions de SQLSTATE retournée par le Gestionnaire de pilotes. Le code de retour associé à chaque valeur SQLSTATE est SQL_ERROR, sauf indication contraire.  

|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Avertissement général|Message d’information spécifiques au pilote. (La fonction retourne SQL_SUCCESS_WITH_INFO.)|  
|07006|Violation de l’attribut de type de données restreint|Le type de données identifié par le *ValueType* argument ne peut pas être converti au type de données identifié par le *ParameterType* argument. Notez que cette erreur peut être renvoyée par **SQLExecDirect**, **SQLExecute**, ou **SQLPutData** au moment de l’exécution, plutôt que par **SQLBindParameter**.|  
|07009|Index de descripteur non valide|(DM) la valeur spécifiée pour l’argument *ParameterNumber* était inférieur à 1.|  
|HY000|Erreur générale|Une erreur s’est produite pour laquelle aucun code SQLSTATE spécifique est survenu et pour lequel aucune SQLSTATE spécifiques à l’implémentation a été défini. Le message d’erreur retourné par **SQLGetDiagRec** dans le **MessageText* tampon décrit l’erreur et sa cause.|  
|HY001|Erreur d’allocation de mémoire|Le pilote n’a pas pu allouer de la mémoire qui est nécessaire pour prendre en charge l’exécution ou à l’achèvement de la fonction.|  
|HY003|Type de tampon d’application non valide|La valeur spécifiée par l’argument *ValueType* n’était pas un type de données C valide ni un SQL_C_DEFAULT.|  
|HY004|Type de données SQL non valide|La valeur spécifiée pour l’argument *ParameterType* n’est ni un identificateur de type de données ODBC SQL valide ni un identificateur de type de données SQL spécifiques au pilote pris en charge par le pilote.|  
|HY009|Valeur d’argument non valide|(DM) l’argument *ParameterValuePtr* était un pointeur null, l’argument *StrLen_or_IndPtr* était un pointeur null et que l’argument *InputOutputType* n’était pas SQL_PARAM_ SORTIE.<br /><br /> SQL_PARAM_OUTPUT (DM), où l’argument *ParameterValuePtr* était un pointeur null, le type C était char ou binary et le BufferLength (*cbValueMax*) était supérieure à 0.|  
|HY010|Erreur de séquence de fonction|(DM) une fonction de façon asynchrone en cours d’exécution a été appelée pour le handle de connexion qui est associé à la *au paramètre StatementHandle*. Cette fonction asynchrone était en cours d’exécution lorsque **SQLBindParameter** a été appelée.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** a été appelé pour le *au paramètre StatementHandle* et retourné SQL_PARAM_DATA_ DISPONIBLE. Cette fonction a été appelée avant que les données ont été récupérées pour tous les paramètres transmis en continu.<br /><br /> (DM) une fonction de façon asynchrone en cours d’exécution a été appelée pour le *au paramètre StatementHandle* et était en cours d’exécution quand cette fonction a été appelée.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** a été appelé pour le  *Au paramètre StatementHandle* et retourné SQL_NEED_DATA. Cette fonction a été appelée avant l’envoi de données pour tous les paramètres de data-at-execution ou les colonnes.|  
|HY013|Erreur de gestion de mémoire|L’appel de fonction n’a pas pu être traité, car les objets sous-jacents de la mémoire ne sont pas accessible, probablement en raison de conditions de mémoire insuffisante.|  
|HY021|Informations de descripteur incohérentes|Les informations de descripteur vérifiées pendant une vérification de cohérence n’étaient pas cohérentes. (Consultez la section « Vérifications de cohérence » dans **SQLSetDescField**.)<br /><br /> La valeur spécifiée pour l’argument *DecimalDigits* était en dehors de la plage de valeurs prises en charge par la source de données pour une colonne du type de données SQL spécifiée par la *ParameterType* argument.|  
|HY090|Longueur de chaîne ou une mémoire tampon non valide|(DM) la valeur dans *BufferLength* était inférieure à 0. (Consultez la description du champ SQL_DESC_DATA_PTR dans **SQLSetDescField**.)|  
|HY104|Valeur de précision ou d’échelle non valide|La valeur spécifiée pour l’argument *ColumnSize* ou *DecimalDigits* était en dehors de la plage de valeurs prises en charge par la source de données pour une colonne du type de données SQL spécifiée par la  *ParameterType* argument.|  
|HY105|Type de paramètre non valide|(DM) la valeur spécifiée pour l’argument *InputOutputType* n’était pas valide. (Voir « Commentaires ».)|  
|HY117|Connexion est suspendue en raison de l’état de transaction inconnu. Déconnecter uniquement et les fonctions en lecture seule sont autorisées.|(DM) pour plus d’informations sur l’état suspendu, consultez [SQLEndTran, fonction](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Fonctionnalité optionnelle non implémentée|La pilote ou source de données ne prend pas en charge la conversion spécifiée par la combinaison de la valeur spécifiée pour l’argument *ValueType* et la valeur spécifique au pilote spécifié pour l’argument *ParameterType*.<br /><br /> La valeur spécifiée pour l’argument *ParameterType* a un identificateur de type de données ODBC SQL valide pour la version d’ODBC pris en charge par le pilote, mais n’était pas pris en charge par la pilote ou source de données.<br /><br /> Le pilote prend en charge uniquement ODBC 2. *x* et l’argument *ValueType* était une des opérations suivantes :<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> et tous les types de données d’intervalle C répertoriés dans [les Types de données C](../../../odbc/reference/appendixes/c-data-types.md) dans l’annexe d : Types de données.<br /><br /> Le pilote prend uniquement en charge les versions ODBC avant 3,50 et l’argument *ValueType* a été SQL_C_GUID.|  
|HYT01|Délai de connexion expiré|Le délai de connexion a expiré avant que la source de données a répondu à la demande. Le délai de connexion est défini via **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Pilote ne prend pas en charge cette fonction|Le pilote (DM) associé le *au paramètre StatementHandle* ne prend pas en charge la fonction.|  
  
## <a name="comments"></a>Commentaires

 Une application appelle **SQLBindParameter** pour lier chaque marqueur de paramètre dans une instruction SQL. Liaisons restent en vigueur jusqu'à ce que l’application appelle **SQLBindParameter** appelle de nouveau, **SQLFreeStmt** avec l’option de SQL_RESET_PARAMS, ou les appels **SQLSetDescField** à le champ d’en-tête de l’APD SQL_DESC_COUNT la valeur 0.  
  
 Pour plus d’informations sur les paramètres, consultez [paramètres d’instruction](../../../odbc/reference/develop-app/statement-parameters.md). Pour plus d’informations sur les types de données de paramètre et des marqueurs de paramètres, consultez [les Types de données de paramètre](../../../odbc/reference/appendixes/parameter-data-types.md) et [marqueurs de paramètres](../../../odbc/reference/appendixes/parameter-markers.md) dans l’annexe c : Grammaire SQL.  
  
## <a name="parameternumber-argument"></a>Argument de ParameterNumber  
 Si *ParameterNumber* dans l’appel à **SQLBindParameter** est supérieure à la valeur de SQL_DESC_COUNT, **SQLSetDescField** est appelée pour augmenter la valeur de SQL_DESC_ COMPTER à *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>Argument de InputOutputType  
 Le *InputOutputType* argument spécifie le type du paramètre. Cet argument définit le champ SQL_DESC_PARAMETER_TYPE de l’IPD. Tous les paramètres dans les instructions SQL qui n’appellent pas de procédures, telles que **insérer** sont des instructions, *d’entrée ** paramètres*. Paramètres dans les appels de procédure peuvent être entrés, d’entrée/sortient ou paramètres de sortie. (Une application appelle **SQLProcedureColumns** pour déterminer le type d’un paramètre dans un appel de procédure ; paramètres dont le type ne peut pas être déterminé sont supposés pour être des paramètres d’entrée.)  
  
 Le *InputOutputType* argument est une des valeurs suivantes :  
  
-   SQL_PARAM_INPUT. Le paramètre marque un paramètre dans une instruction SQL qui n’appelle pas une procédure, comme un **insérer** instruction, ou il marque un paramètre d’entrée dans une procédure. Par exemple, les paramètres dans **INSERT INTO VALUES employé ( ?, ?, ?)**  sont des paramètres d’entrée, tandis que les paramètres dans **{appeler AddEmp ( ?, ?, ?)}**  peut être, mais ne sont pas nécessairement, des paramètres d’entrée.  
  
     Lorsque l’instruction est exécutée, le pilote envoie des données pour le paramètre à la source de données ; le \* *ParameterValuePtr* mémoire tampon doit contenir une valeur d’entrée valide, ou **StrLen_or_IndPtr* mémoire tampon doit contenir SQL_NULL_DATA, SQL_DATA_AT_EXEC ou le résultat de la SQL_LEN_DATA_AT Macro _EXEC.  
  
     Si une application ne peut pas déterminer le type d’un paramètre dans un appel de procédure, il définit *InputOutputType* à SQL_PARAM_INPUT ; si la source de données retourne une valeur pour le paramètre, le pilote ignore.  
  
-   SQL_PARAM_INPUT_OUTPUT. Le paramètre marque un paramètre d’entrée/sortie dans une procédure. Par exemple, le paramètre dans **{appeler GetEmpDept(?)}**  est un paramètre d’entrée/sortie qui accepte le nom d’un employé et retourne le nom du service de l’employé.  
  
     Lorsque l’instruction est exécutée, le pilote envoie des données pour le paramètre à la source de données ; le \* *ParameterValuePtr* mémoire tampon doit contenir une valeur d’entrée valide, ou le \* *StrLen_or_IndPtr* mémoire tampon doit contenir SQL_NULL_DATA, SQL_DATA_AT_EXEC ou le résultat de la macro SQL_LEN_DATA_AT_EXEC. Une fois que l’instruction est exécutée, le pilote retourne des données pour le paramètre à l’application ; Si la source de données ne retourne pas une valeur pour un paramètre d’entrée/sortie, le pilote définit le **StrLen_or_IndPtr* tampon avec la valeur SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Lorsqu’une application ODBC 1.0 appelle **SQLSetParam** dans un pilote ODBC 2.0, le Gestionnaire de pilote le convertit en un appel à **SQLBindParameter** dans lequel le *InputOutputType* argument a la valeur SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. Le paramètre marque la valeur de retour d’une procédure ou un paramètre de sortie dans une procédure ; dans les deux cas, ils sont appelés *paramètres de sortie*. Par exemple, le paramètre dans **{ ? = appeler GetNextEmpID}** est un paramètre de sortie qui retourne l’ID d’employé suivant.  
  
     Une fois que l’instruction est exécutée, le pilote retourne des données pour le paramètre à l’application, à moins que le *ParameterValuePtr* et *StrLen_or_IndPtr* arguments sont les deux pointeurs null, auquel cas le pilote ignore la valeur de sortie. Si la source de données ne retourne pas une valeur pour un paramètre de sortie, le pilote définit le **StrLen_or_IndPtr* tampon avec la valeur SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indique que le paramètre d’entrée/sortie doit être diffusé en continu. **SQLGetData** peut lire les valeurs de paramètre dans les parties. *BufferLength* est ignoré, car la longueur du tampon est déterminée lors de l’appel de **SQLGetData**. La valeur de la *StrLen_or_IndPtr* mémoire tampon doit contenir SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC ou le résultat de la macro SQL_LEN_DATA_AT_EXEC. Un paramètre doit être lié comme un paramètre data-at-execution (DAE) dans l’entrée si elle est diffusée à la sortie. *ParameterValuePtr* peut être toute valeur de pointeur non null est retourné par **SQLParamData** comme défini par l’utilisateur dont la valeur du jeton a été passée avec *ParameterValuePtr* pour les deux entrées et sortie. Pour plus d’informations, consultez [récupération des paramètres de sortie à l’aide de SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. Identique à SQL_PARAM_INPUT_OUTPUT_STREAM, pour un paramètre de sortie. **StrLen_or_IndPtr* est ignoré en entrée.  
  
 Le tableau suivant répertorie les différentes combinaisons de *InputOutputType* et **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Résultat|Remarque sur ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Parties d’entrée dans|*ParameterValuePtr* peut être toute valeur de pointeur qui est renvoyé par **SQLParamData** comme défini par l’utilisateur dont la valeur du jeton a été passée avec *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|Pas de SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Entrée liée de mémoire tampon|*ParameterValuePtr* est l’adresse de la mémoire tampon d’entrée.|  
|SQL_PARAM_OUTPUT|Ignoré en entrée.|Mémoire tampon de sortie liée|*ParameterValuePtr* est l’adresse de la mémoire tampon de sortie.|  
|SQL_PARAM_OUTPUT_STREAM|Ignoré en entrée.|Sortie diffusées en continu|*ParameterValuePtr* peut être toute valeur de pointeur, qui est renvoyée par **SQLParamData** comme défini par l’utilisateur dont la valeur du jeton a été passée avec *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Parties d’entrée dans et la mémoire tampon de sortie lié|*ParameterValuePtr* est l’adresse de la mémoire tampon de sortie, qui est également retourné par **SQLParamData** comme défini par l’utilisateur dont la valeur du jeton a été passée avec *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|Pas de SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|Entrée liée de mémoire tampon et la mémoire tampon de sortie lié|*ParameterValuePtr* est l’adresse de la mémoire tampon d’entrée/sortie partagée.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) ou SQL_DATA_AT_EXEC|D’entrée dans des parties et sortie diffusées en continu|*ParameterValuePtr* peut être toute valeur de pointeur non null, qui est renvoyée par **SQLParamData** comme défini par l’utilisateur dont la valeur du jeton a été passée avec *ParameterValuePtr* pour les deux entrées et de sortie.|  
  
> [!NOTE]  
>  Le pilote doit décider quels types SQL sont autorisées lorsqu’une application lie une sortie ou un paramètre d’entrée-sortie comme diffusé en continu. Le Gestionnaire de pilotes ne génère pas d’une erreur pour un type SQL non valide.  
  
## <a name="valuetype-argument"></a>Argument de type valeur

 Le *ValueType* argument spécifie le type de données C du paramètre. Cet argument définit les champs SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE et SQL_DESC_DATETIME_INTERVAL_CODE du descripteur APD. Il doit s’agir des valeurs dans le [les Types de données C](../../../odbc/reference/appendixes/c-data-types.md) section de l’annexe d : Types de données.  
  
 Si le *ValueType* argument est un des types de données intervalle, le champ SQL_DESC_TYPE de la *ParameterNumber* enregistrement de l’APD est définie sur SQL_INTERVAL, le champ SQL_DESC_CONCISE_TYPE du descripteur APD est défini sur le type de données d’intervalle concis et le champ de valeur SQL_DESC_DATETIME_INTERVAL_CODE de la *ParameterNumber* jeu d’enregistrements à un sous-code pour le type de données d’intervalle de temps spécifique. (Consultez [annexe d : Types de données](../../../odbc/reference/appendixes/appendix-d-data-types.md).) L’intervalle par défaut de début précision (2) et une précision de secondes d’intervalle par défaut (6), comme défini dans les champs SQL_DESC_DATETIME_INTERVAL_PRECISION et SQL_DESC_PRECISION de l’APD, respectivement, sont utilisés pour les données. Si une précision par défaut ne c'est-à-dire pas, l’application doit définir explicitement le champ de descripteur par un appel à **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Si le *ValueType* argument est un des types de données date/heure, le champ SQL_DESC_TYPE de la *ParameterNumber* enregistrement de l’APD est défini sur SQL_DATETIME, le champ SQL_DESC_CONCISE_TYPE de la *ParameterNumber* enregistrement de l’APD est définie sur le type de données datetime concis C et le champ de valeur SQL_DESC_DATETIME_INTERVAL_CODE de la *ParameterNumber* jeu d’enregistrements à un sous-code pour la date/heure spécifique type de données. (Consultez [annexe d : Types de données](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Si le *ValueType* argument est un type de données SQL_C_NUMERIC, la précision par défaut (qui est définie par le pilote) et l’échelle par défaut (0), comme défini dans les champs SQL_DESC_PRECISION et SQL_DESC_SCALE de l’APD, sont utilisés pour les données. Si la précision par défaut ou la mise à l’échelle ne c'est-à-dire pas, l’application doit définir explicitement le champ de descripteur par un appel à **SQLSetDescField** ou **SQLSetDescRec**.  
  
 SQL_C_DEFAULT Spécifie que la valeur du paramètre être transférés à partir du type de données par défaut C pour le type de données SQL spécifié avec *ParameterType*.  
  
 Vous pouvez également spécifier un type de données C étendu. Pour plus d’informations, consultez [des Types de données C dans ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Pour plus d’informations, consultez [par défaut des Types de données C](../../../odbc/reference/appendixes/default-c-data-types.md), [conversion des données à partir de C en Types de données SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md), et [conversion des données à partir de SQL pour les Types de données C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) dans l’annexe d : Types de données.  
  
## <a name="parametertype-argument"></a>Argument de type de paramètre

 Il doit s’agir des valeurs répertoriées dans le [les Types de données SQL](../../../odbc/reference/appendixes/sql-data-types.md) section de l’annexe d : Types de données, ou il doit être une valeur spécifique au pilote. Cet argument définit les champs SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE et SQL_DESC_DATETIME_INTERVAL_CODE de l’IPD.  
  
 Si le *ParameterType* argument est un des identificateurs de date/heure, le champ SQL_DESC_TYPE de l’IPD est défini à SQL_DATETIME, le champ SQL_DESC_CONCISE_TYPE de l’IPD est défini pour le type de données datetime concis SQL et le SQL_DESC_ Champ DATETIME_INTERVAL_CODE est défini sur la valeur de sous-code de date/heure approprié.  
  
 Si *ParameterType* est un des identificateurs d’intervalle, le champ SQL_DESC_TYPE de l’IPD est la valeur SQL_INTERVAL, le champ SQL_DESC_CONCISE_TYPE de l’IPD est défini sur le type de données SQL intervalle concis et le SQL_DESC_DATETIME_ Champ INTERVAL_CODE de l’IPD est défini pour le sous-code d’intervalle approprié. Le champ SQL_DESC_DATETIME_INTERVAL_PRECISION de l’IPD est défini à la précision de début d’intervalle et le champ SQL_DESC_PRECISION est défini sur la précision de secondes d’intervalle, le cas échéant. Si la valeur par défaut SQL_DESC_DATETIME_INTERVAL_PRECISION ou SQL_DESC_PRECISION n’est pas appropriée, l’application doit définir explicitement en appelant **SQLSetDescField**. Pour plus d’informations sur un de ces champs, consultez [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Si le *ValueType* argument est un type de données SQL_NUMERIC, la précision par défaut (qui est définie par le pilote) et l’échelle par défaut (0), comme défini dans les champs SQL_DESC_PRECISION et SQL_DESC_SCALE de l’IPD, sont utilisés pour les données. Si la précision par défaut ou la mise à l’échelle ne c'est-à-dire pas, l’application doit définir explicitement le champ de descripteur par un appel à **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Pour plus d’informations sur la conversion de données, consultez [conversion des données à partir de C en Types de données SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) et [conversion des données à partir de SQL pour les Types de données C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) dans l’annexe d : Types de données.  
  
## <a name="columnsize-argument"></a>ColumnSize Argument

 Le *ColumnSize* argument spécifie la taille de la colonne ou une expression qui correspond au marqueur de paramètre, la longueur de ces données, ou les deux. Cet argument définit différents champs de l’IPD, selon le type de données SQL (le *ParameterType* argument). Les règles suivantes s’appliquent à ce mappage :  
  
-   Si *ParameterType* est SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY, ou les concis SQL datetime ou interval types de données, le champ SQL_DESC_LENGTH de l’IPD sont définie sur la valeur de  *ColumnSize*. (Pour plus d’informations, consultez le [taille de colonne, des chiffres décimaux, transférer la longueur en octets et la taille d’affichage](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) section dans l’annexe d : Types de données.)  
  
-   Si *ParameterType* est SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL ou SQL_DOUBLE, le champ SQL_DESC_PRECISION de l’IPD est défini à la valeur de *ColumnSize*.  
  
-   Pour les autres types de données, le *ColumnSize* argument est ignoré.  
  
 Pour plus d’informations, consultez « Passage des valeurs de paramètre » et SQL_DATA_AT_EXEC dans «*StrLen_or_IndPtr* Argument. »  
  
## <a name="decimaldigits-argument"></a>Argument de DecimalDigits

 Si *ParameterType* est SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND ou SQL_INTERVAL_MINUTE_TO_SECOND, le champ SQL_DESC_PRECISION de l’IPD est défini pour *DecimalDigits*. Si *ParameterType* est SQL_NUMERIC ou SQL_DECIMAL, le champ SQL_DESC_SCALE de l’IPD est défini sur *DecimalDigits*. Pour tous les autres types de données, le *DecimalDigits* argument est ignoré.  
  
## <a name="parametervalueptr-argument"></a>Argument de ParameterValuePtr

 Le *ParameterValuePtr* argument pointe vers une mémoire tampon qui, quand **SQLExecute** ou **SQLExecDirect** est appelée, contient les données réelles pour le paramètre. Les données doivent être dans le formulaire spécifié par le *ValueType* argument. Cet argument définit le champ SQL_DESC_DATA_PTR du descripteur APD. Une application peut définir le *ParameterValuePtr* argument à un pointeur null, tant que  *\*StrLen_or_IndPtr* est SQL_NULL_DATA ou SQL_DATA_AT_EXEC. (Cela s’applique uniquement au paramètres d’entrée ou d’entrée/sortie).  
  
 Si \* *StrLen_or_IndPtr* est le résultat de la SQL_LEN_DATA_AT_EXEC (*longueur*) (macro) ou SQL_DATA_AT_EXEC, puis *ParameterValuePtr* est un valeur de pointeur défini par l’application qui est associée au paramètre. Il est retourné à l’application via **SQLParamData**. Par exemple, *ParameterValuePtr* peut être un jeton de zéro comme un numéro de paramètre, un pointeur vers les données ou un pointeur vers une structure de l’application utilisée pour lier les paramètres d’entrée. Toutefois, notez que si le paramètre est un paramètre d’entrée/sortie, *ParameterValuePtr* doit être un pointeur vers une mémoire tampon où la valeur de sortie sera stockée. Si la valeur dans l’attribut d’instruction SQL_ATTR_PARAMSET_SIZE est supérieure à 1, l’application peut utiliser la valeur indiquée par l’attribut d’instruction SQL_ATTR_PARAMS_PROCESSED_PTR conjointement avec la *ParameterValuePtr* argument. Par exemple, *ParameterValuePtr* peut pointer vers un tableau de valeurs et de l’application peut utiliser la valeur vers laquelle pointée SQL_ATTR_PARAMS_PROCESSED_PTR pour récupérer la valeur correcte à partir du tableau. Pour plus d’informations, consultez « Passage des valeurs de paramètre » plus loin dans cette section.  
  
 Si le *InputOutputType* argument est SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT, *ParameterValuePtr* pointe vers une mémoire tampon dans laquelle le pilote retourne la valeur de sortie. Si la procédure retourne un ou plusieurs jeux de résultats, le \* *ParameterValuePtr* mémoire tampon n’est pas garanti pour être définie tant que tous les nombres de jeux/ligne de résultat ont été traités. Si la mémoire tampon n’est pas définie tant que le traitement est terminé, les paramètres de sortie et les valeurs de retour sont indisponibles jusqu'à ce que **SQLMoreResults** retourne SQL_NO_DATA. Appel **SQLCloseCursor** ou **SQLFreeStmt** avec une Option de SQL_CLOSE entraîne ces valeurs sont ignorés.  
  
 Si la valeur de l’attribut d’instruction SQL_ATTR_PARAMSET_SIZE est supérieure à 1, *ParameterValuePtr* pointe vers un tableau. Une instruction SQL unique traite le tableau complet de valeurs d’entrée pour un paramètre d’entrée ou d’entrée/sortie et retourne un tableau de valeurs de sortie d’une entrée/sortie ou du paramètre de sortie.  
  
## <a name="bufferlength-argument"></a>BufferLength Argument

 Pour les caractères et des données binaires C, le *BufferLength* argument spécifie la longueur de la \* *ParameterValuePtr* tampon (s’il est un élément unique) ou la longueur d’un élément dans le \* *ParameterValuePtr* tableau (si la valeur de l’attribut d’instruction SQL_ATTR_PARAMSET_SIZE est supérieure à 1). Cet argument définit le champ d’enregistrement SQL_DESC_OCTET_LENGTH du descripteur APD. Si l’application spécifie plusieurs valeurs, *BufferLength* est utilisé pour déterminer l’emplacement des valeurs dans le **ParameterValuePtr* de tableau, à la fois en entrée et en sortie. Pour les paramètres d’entrée/sortie et de sortie, il est utilisé pour déterminer s’il faut tronquer caractère et binaire C données lors de la sortie :  
  
-   Pour les données de caractères C, si le nombre d’octets à retourner est supérieur ou égal à *BufferLength*, les données dans \* *ParameterValuePtr* est tronqué à  *BufferLength* moins la longueur d’un caractère du caractère nul de terminaison et se terminant par null par le pilote.  
  
-   Pour les données binaires de C si le nombre d’octets à retourner est supérieur à *BufferLength*, les données dans \* *ParameterValuePtr* est tronqué à *BufferLength*octets.  
  
 Pour tous les autres types de données C, le *BufferLength* argument est ignoré. La longueur de la \* *ParameterValuePtr* tampon (s’il est un élément unique) ou la longueur d’un élément dans le \* *ParameterValuePtr* tableau (si l’application appelle  **SQLSetStmtAttr** avec un *attribut* argument de SQL_ATTR_PARAMSET_SIZE pour spécifier plusieurs valeurs pour chaque paramètre) est supposé pour être la longueur du type de données C.  
  
 Pour la sortie diffusées en continu ou les paramètres d’entrée/sortie transmis en continu, le *BufferLength* argument est ignoré, car la longueur du tampon est spécifiée dans **SQLGetData**.  
  
> [!NOTE]  
>  Lorsqu’une application ODBC 1.0 appelle **SQLSetParam** dans un ODBC 3. *x* pilote, le Gestionnaire de pilote le convertit en un appel à **SQLBindParameter** dans lequel le *BufferLength* argument est toujours SQL_SETPARAM_VALUE_MAX. Étant donné que le Gestionnaire de pilotes retourne une erreur si un ODBC 3. *x* application définit *BufferLength* à SQL_SETPARAM_VALUE_MAX, un ODBC 3. *x* pilote peut utiliser pour déterminer quand elle est appelée par une application ODBC version 1.0.  
  
> [!NOTE]  
>  Dans **SQLSetParam**, celle dans laquelle une application spécifie la longueur de la **ParameterValuePtr* mettre en mémoire tampon afin que le pilote peut retourner des caractères ou données binaires et celle dans laquelle une application envoie un tableau de caractères ou de valeurs de paramètre binaire au pilote, sont définies par le pilote.  
  
## <a name="strlenorindptr-argument"></a>Argument de StrLen_or_IndPtr

 Le *StrLen_or_IndPtr* argument pointe vers une mémoire tampon qui, quand **SQLExecute** ou **SQLExecDirect** est appelée, contient l’une des opérations suivantes. (Cet argument définit les champs d’enregistrement SQL_DESC_OCTET_LENGTH_PTR et SQL_DESC_INDICATOR_PTR des pointeurs de paramètre d’application.)  
  
-   La longueur de la valeur du paramètre stockée dans **ParameterValuePtr*. Ceci est ignoré, à l’exception de binaire ou caractère C.  
  
-   SQL_NTS. La valeur du paramètre est une chaîne se terminant par null.  
  
-   SQL_NULL_DATA. La valeur du paramètre est NULL.  
  
-   SQL_DEFAULT_PARAM. Une procédure consiste à utiliser la valeur par défaut d’un paramètre, au lieu d’une valeur récupérée à partir de l’application. Cette valeur est valide uniquement dans une procédure appelée dans la syntaxe canonique ODBC, puis uniquement si le *InputOutputType* argument est SQL_PARAM_INPUT ou SQL_PARAM_INPUT_OUTPUT SQL_PARAM_INPUT_OUTPUT_STREAM. Lorsque \* *StrLen_or_IndPtr* est SQL_DEFAULT_PARAM, le *ValueType*, *ParameterType*, *ColumnSize*,  *DecimalDigits*, *BufferLength*, et *ParameterValuePtr* arguments sont ignorés dans les paramètres d’entrée et sont utilisées uniquement pour définir la valeur du paramètre de sortie pour l’entrée / paramètres de sortie.  
  
-   Le résultat de la SQL_LEN_DATA_AT_EXEC (*longueur*) (macro). Les données pour le paramètre seront envoyées avec **SQLPutData**. Si le *ParameterType* argument SQL_LONGVARBINARY, SQL_LONGVARCHAR ou type long, ce qui est de type de données spécifique à la source de données, et le pilote retourne « Y » pour le type d’information SQL_NEED_LONG_DATA_LEN dans **SQLGetInfo**, *longueur* est le nombre d’octets de données à envoyer pour le paramètre ; sinon, *longueur* doit être une valeur non négative et est ignoré. Pour plus d’informations, consultez « Passage valeurs de paramètre, » plus loin dans cette section.  
  
     Par exemple, pour spécifier que 10 000 octets de données sera envoyés avec **SQLPutData** dans un ou plusieurs appels, pour un paramètre SQL_LONGVARCHAR, une application définit **StrLen_or_IndPtr* à SQL_LEN_DATA_AT_EXEC ( 10000).  
  
-   SQL_DATA_AT_EXEC. Les données pour le paramètre seront envoyées avec **SQLPutData**. Cette valeur est utilisée par les applications ODBC 1.0 lors de l’appel ODBC 3. *x* pilotes. Pour plus d’informations, consultez « Passage valeurs de paramètre, » plus loin dans cette section.  
  
 Si *StrLen_or_IndPtr* est un pointeur null, le pilote part du principe que toutes les valeurs de paramètre d’entrée sont non NULL et que les données caractères et binaires sont se terminant par null. Si *InputOutputType* est SQL_PARAM_OUTPUT ou SQL_PARAM_OUTPUT_STREAM et *ParameterValuePtr* et *StrLen_or_IndPtr* sont les deux pointeurs null, le pilote ignore la valeur de sortie.  
  
> [!NOTE]  
>  Les développeurs d’applications sont fortement déconseillés de spécifier un pointeur null pour *StrLen_or_IndPtr* lorsque le type de données du paramètre est SQL_C_BINARY. Pour vous assurer qu’un pilote ne tronque pas inopinément données SQL_C_BINARY, *StrLen_or_IndPtr* doit contenir un pointeur vers une valeur de longueur valide.  
  
 Si le *InputOutputType* argument est SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM, *StrLen_or_IndPtr* pointe vers une mémoire tampon dans laquelle le pilote retourne SQL_NULL_DATA, le nombre d’octets à retourner dans \* *ParameterValuePtr* (à l’exception de l’octet de caractère nul de terminaison de données de type caractère) ou SQL_NO_TOTAL (si le nombre d’octets disponibles pour retour ne peut pas être déterminé). Si la procédure retourne un ou plusieurs jeux de résultats, le **StrLen_or_IndPtr* mémoire tampon n’est pas garanti pour être définie tant que tous les résultats qui ont été extraites.  
  
 Si la valeur de l’attribut d’instruction SQL_ATTR_PARAMSET_SIZE est supérieure à 1, *StrLen_or_IndPtr* pointe vers un tableau de valeurs SQLLEN. Il peuvent être une des valeurs répertoriées plus haut dans cette section et sont traités avec une instruction SQL unique.  
  
## <a name="passing-parameter-values"></a>Transmission de valeurs de paramètre

 Une application peut passer la valeur d’un paramètre soit dans le \* *ParameterValuePtr* mémoire tampon ou avec un ou plusieurs appels à **SQLPutData**. Les paramètres dont les données sont transmises avec **SQLPutData** sont appelés *data-at-execution* paramètres. Ceux-ci sont généralement utilisés pour envoyer des données pour les paramètres SQL_LONGVARBINARY et SQL_LONGVARCHAR et peuvent être combinés avec d’autres paramètres.  
  
 Pour passer les valeurs de paramètre, une application effectue la séquence d’étapes suivante :  
  
1.  Appels **SQLBindParameter** pour chaque paramètre à lier les mémoires tampons pour la valeur du paramètre (*ParameterValuePtr* argument) et l’indicateur/longueur (*StrLen_or_IndPtr* argument). Pour les paramètres de data-at-execution, *ParameterValuePtr* est une valeur de pointeur défini par l’application comme un numéro de paramètre ou un pointeur vers les données. La valeur s’affichera plus tard et peut être utilisée pour identifier le paramètre.  
  
2.  Place les valeurs des paramètres d’entrée et d’entrée/sortie dans le \* *ParameterValuePtr* et **StrLen_or_IndPtr* mémoires tampons :  
  
    -   Pour les paramètres normaux, l’application place la valeur du paramètre dans le \* *ParameterValuePtr* mémoire tampon et la longueur de cette valeur dans le **StrLen_or_IndPtr* mémoire tampon. Pour plus d’informations, consultez [les valeurs de paramètre de paramètre](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Pour les paramètres de data-at-execution, l’application place le résultat de la SQL_LEN_DATA_AT_EXEC (*longueur*) macro (lors de l’appel d’un pilote ODBC 2.0) dans le **StrLen_or_IndPtr* mémoire tampon.  
  
3.  Appels **SQLExecute** ou **SQLExecDirect** pour exécuter l’instruction SQL.  
  
    -   S’il n’y a aucun paramètre data-at-execution, le processus est terminé.  
  
    -   S’il y a aucun paramètre data-at-execution, la fonction retourne SQL_NEED_DATA.  
  
4.  Appels **SQLParamData** pour récupérer la valeur définie par l’application spécifiée dans le *ParameterValuePtr* argument de **SQLBindParameter** pour le premier paramètre Data-at-execution à traiter. **SQLParamData** retourne SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Bien que les paramètres de data-at-execution ressemblent à des colonnes de données en cours d’exécution, la valeur retournée par **SQLParamData** est différent pour chacun. Paramètres de Data-at-execution sont des paramètres dans une instruction SQL pour laquelle les données sont envoyées avec **SQLPutData** lorsque l’instruction est exécutée avec **SQLExecDirect** ou **SQLExecute**. Elles sont liées avec **SQLBindParameter**. La valeur retournée par **SQLParamData** est une valeur de pointeur passée à **SQLBindParameter** dans le *ParameterValuePtr* argument. Colonnes de Data-at-execution sont des colonnes dans un ensemble de lignes pour lequel les données sont envoyées avec **SQLPutData** quand une ligne est mise à jour ou ajoutée avec **SQLBulkOperations** ou mis à jour avec **SQLSetPos**. Elles sont liées avec **SQLBindCol**. La valeur retournée par **SQLParamData** est l’adresse de la ligne dans le **TargetValuePtr* tampon (définie par un appel à **SQLBindCol**) qui est en cours de traitement.  
  
5.  Appels **SQLPutData** une ou plusieurs fois pour envoyer des données pour le paramètre. Plusieurs appels est nécessaire si la valeur de données est supérieure à la \* *ParameterValuePtr* mémoire tampon spécifiée dans **SQLPutData**; appels multiples à **SQLPutData**pour le même paramètre sont autorisées uniquement lors de l’envoi des données de caractères C à une colonne avec un type de données de spécifique à la source de données, binaire ou caractère ou lors de l’envoi des données binaires de C à une colonne avec un caractère, binaire, ou le type de données spécifique à la source de données.  
  
6.  Appels **SQLParamData** pour signaler que toutes les données a été envoyé pour le paramètre.  
  
    -   S’il existe plusieurs paramètres de data-at-execution, **SQLParamData** retourne SQL_NEED_DATA et la valeur définie par l’application pour le paramètre data-at-execution suivant à traiter. L’application répète les étapes 4 et 5.  
  
    -   S’il n’y a pas d’autres paramètres de data-at-execution, le processus est terminé. Si l’instruction a été exécutée avec succès, **SQLParamData** retourne SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO ; si l’exécution a échoué, elle retourne SQL_ERROR. À ce stade, **SQLParamData** peut retourner n’importe quel SQLSTATE qui peut être retournée par la fonction qui est utilisée pour exécuter l’instruction (**SQLExecDirect** ou **SQLExecute**).  
  
         Les valeurs de sortie pour tous les paramètres d’entrée/sortie ou de sortie sont disponibles dans le \* *ParameterValuePtr* et **StrLen_or_IndPtr* met en mémoire tampon une fois que l’application récupère tous les jeux de résultats générées par l’instruction.  
  
 Appel **SQLExecute** ou **SQLExecDirect** place l’instruction dans un état SQL_NEED_DATA. À ce stade, l’application peut appeler uniquement **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**, ou **SQLPutData** avec l’instruction ou le *handle de connexion* associé à l’instruction. Si elle appelle une autre fonction avec l’instruction ou la connexion associée à l’instruction, la fonction retourne SQLSTATE HY010 (erreur de séquence de fonction). Les feuilles de l’instruction la SQL_NEED_DATA état lorsque **SQLParamData** ou **SQLPutData** renvoie une erreur, **SQLParamData** retourne SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, ou l’instruction est annulée.  
  
 Si l’application appelle **SQLCancel** tandis que le pilote a toujours besoin de données pour les paramètres de data-at-execution, le pilote annule l’exécution d’instruction ; l’application peut ensuite appeler **SQLExecute** ou  **SQLExecDirect** à nouveau.  
  
## <a name="retrieving-streamed-output-parameters"></a>Récupération des paramètres de sortie diffusées en continu

 Lorsqu’une application définit *InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM, la valeur de paramètre de sortie doit être récupérée par un ou plusieurs appels à **SQLGetData**. Lorsque le pilote a une valeur de paramètre de sortie diffusées en continu pour revenir à l’application, elle retournera SQL_PARAM_DATA_AVAILABLE en réponse à un appel aux fonctions suivantes : **SQLMoreResults**, **SQLExecute**, et **SQLExecDirect**. Une application appelle **SQLParamData** pour déterminer quelle valeur de paramètre est disponible.  
  
 Pour plus d’informations sur les SQL_PARAM_DATA_AVAILABLE et les paramètres de sortie diffusées en continu, consultez [récupération des paramètres de sortie à l’aide de SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Utilisation de tableaux de paramètres

 Lorsqu’une application prépare une instruction avec des marqueurs de paramètres et passe un tableau de paramètres, il existe deux façons différentes, que cela peut être exécutée. La première consiste pour le pilote s’appuyer sur les fonctionnalités de traitement de tableaux du serveur principal, dans lequel cas l’instruction entière avec le tableau de paramètres est traité comme une unité atomique. Oracle est un exemple d’une source de données qui prend en charge des capacités de traitement de tableau. Une autre façon d’implémenter cette fonctionnalité est pour le pilote générer un lot d’instructions SQL, une instruction SQL pour chaque jeu de paramètres dans le tableau de paramètres et exécuter le lot. Tableaux de paramètres ne peut pas être utilisés avec un **mise à jour WHERE CURRENT OF** instruction.  
  
 Lorsqu’un tableau de paramètres est traité, le nombre de jeux/ligne de résultats individuels (un pour chaque jeu de paramètres) peut être disponible ou nombre de jeux/lignes de résultats peut être cumulées en une seule. Option le SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo** indique si les nombres de lignes sont disponibles pour chaque jeu de paramètres (SQL_PARC_BATCH) ou nombre de lignes qu’une seule est disponible (SQL_PARC_NO_BATCH).  
  
 Option le SQL_PARAM_ARRAY_SELECTS **SQLGetInfo** indique si un jeu de résultats est disponible pour chaque jeu de paramètres (SQL_PAS_BATCH) ou un jeu de résultats est disponible (SQL_PAS_NO_BATCH). Si le pilote n’autorise pas une instruction de génération de jeu de résultats doit être exécuté avec un tableau de paramètres, SQL_PARAM_ARRAY_SELECTS retourne SQL_PAS_NO_SELECT.  
  
 Pour plus d’informations, consultez [SQLGetInfo, fonction](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Pour prendre en charge des tableaux de paramètres, l’attribut d’instruction SQL_ATTR_PARAMSET_SIZE est définie pour spécifier le nombre de valeurs pour chaque paramètre. Si le champ est supérieur à 1, les champs SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR et SQL_DESC_OCTET_LENGTH_PTR du descripteur APD doivent pointer vers les tableaux. La cardinalité de chaque tableau est égale à la valeur de SQL_ATTR_PARAMSET_SIZE.  
  
 Le champ SQL_DESC_ROWS_PROCESSED_PTR du descripteur APD pointe vers une mémoire tampon qui contient le nombre de jeux de paramètres qui ont été traités, y compris des ensembles de l’erreur. Lors du traitée de chaque jeu de paramètres, le pilote stocke une nouvelle valeur dans la mémoire tampon. Aucun nombre n’est retourné s’il s’agit d’un pointeur null. Lorsque les tableaux de paramètres sont utilisés, la valeur indiquée par le champ SQL_DESC_ROWS_PROCESSED_PTR du descripteur APD est renseignée, même si SQL_ERROR est retourné par la fonction de paramètre. Si la valeur SQL_NEED_DATA est retournée, la valeur indiquée par le champ SQL_DESC_ROWS_PROCESSED_PTR du descripteur APD est définie pour le jeu de paramètres en cours de traitement.  
  
 Ce qui se produit lorsqu’un tableau de paramètres est lié et qu’un **mise à jour WHERE CURRENT OF** instruction est exécutée est définie par le pilote.  
  
## <a name="column-wise-parameter-binding"></a>La liaison de paramètre

 Dans la liaison, l’application lie le paramètre distinct et les tableaux de longueur / d’indicateur à chaque paramètre.  
  
 Pour utiliser la liaison, l’application définit tout d’abord l’attribut d’instruction SQL_ATTR_PARAM_BIND_TYPE à SQL_PARAM_BIND_BY_COLUMN. (C’est la valeur par défaut). Pour chaque colonne à lier, l’application effectue les étapes suivantes :  
  
1.  Alloue un tableau de mémoires tampons de paramètres.  
  
2.  Alloue un tableau de mémoires tampons de longueur / d’indicateur.  
  
    > [!NOTE]  
    >  Si l’application écrit directement dans les descripteurs lorsque la liaison est utilisée, les tableaux distincts peuvent être utilisés pour les données de longueur et l’indicateur.  
  
3.  Appels **SQLBindParameter** avec les arguments suivants :  
  
    -   *ValueType* est le type C d’un seul élément dans le tableau de mémoires tampons de paramètres.  
  
    -   *ParameterType* est le type SQL du paramètre.  
  
    -   *ParameterValuePtr* est l’adresse du tableau de mémoire tampon de paramètre.  
  
    -   *BufferLength* est la taille d’un seul élément dans le tableau de mémoires tampons de paramètres. Le *BufferLength* argument est ignoré lorsque les données sont des données de longueur fixe.  
  
    -   *StrLen_or_IndPtr* est l’adresse du tableau de longueur / d’indicateur.  
  
 Pour plus d’informations sur l’utilisation de ces informations, consultez « Argument ParameterValuePtr » dans « Commentaires », plus loin dans cette section. Pour plus d’informations sur la liaison de paramètres, consultez [tableaux de paramètres de liaison](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>Une liaison de paramètres

 Dans la liaison, l’application définit une structure qui contient les mémoires tampons de paramètre et de longueur / d’indicateur pour chaque paramètre à lier.  
  
 Pour utiliser la liaison, l’application effectue les étapes suivantes :  
  
1.  Définit une structure pour stocker un ensemble unique de paramètres (y compris les mémoires tampons de paramètre et indicateur/longueur) et alloue un tableau de ces structures.  
  
    > [!NOTE]  
    >  Si l’application écrit directement dans les descripteurs lorsque la liaison est utilisée, les champs distincts peuvent être utilisés pour les données de longueur et l’indicateur.  
  
2.  Définit l’attribut d’instruction SQL_ATTR_PARAM_BIND_TYPE à la taille de la structure qui contient un ensemble unique de paramètres ou à la taille d’une instance d’une mémoire tampon dans laquelle les paramètres seront liés. La longueur doit inclure l’espace pour tous les paramètres liés et tout remplissage de la structure ou de la mémoire tampon, pour vous assurer que lorsque l’adresse d’un paramètre dépendant est incrémenté avec la longueur spécifiée, le résultat pointera vers le début du même paramètre dans le ligne suivante. Lorsque vous utilisez le *sizeof* opérateur en C ANSI, ce comportement est garanti.  
  
3.  Appels **SQLBindParameter** avec les arguments suivants pour chaque paramètre à lier :  
  
    -   *ValueType* est le type du membre de mémoire tampon de paramètre doit être lié à la colonne.  
  
    -   *ParameterType* est le type SQL du paramètre.  
  
    -   *ParameterValuePtr* est l’adresse du membre de mémoire tampon de paramètre dans le premier élément du tableau.  
  
    -   *BufferLength* est la taille du membre de mémoire tampon de paramètre.  
  
    -   *StrLen_or_IndPtr* est l’adresse du membre de longueur / d’indicateur à lier.  
  
 Pour plus d’informations sur l’utilisation de ces informations, consultez «*ParameterValuePtr* Argument, » plus loin dans cette section. Pour plus d’informations sur la liaison de paramètres, consultez le [tableaux de paramètres de liaison](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Informations d’erreur

 Si un pilote n’implémente pas les tableaux de paramètres sous forme de lots (l’option SQL_PARAM_ARRAY_ROW_COUNTS équivaut à SQL_PARC_NO_BATCH), les situations d’erreur sont traitées comme si une instruction ont été exécutée. Si le pilote n’implémente pas les tableaux de paramètres sous forme de lots, une application peut utiliser le champ d’en-tête SQL_DESC_ARRAY_STATUS_PTR de l’IPD pour déterminer quel paramètre d’une instruction SQL ou le paramètre dans un tableau de paramètres a provoqué  **SQLExecDirect** ou **SQLExecute** pour retourner une erreur. Ce champ contient des informations d’état pour chaque ligne de valeurs de paramètre. Si le champ indique qu’une erreur s’est produite, les champs dans la structure de données de diagnostic indique le nombre de lignes et de paramètre du paramètre qui a échoué. Le nombre d’éléments dans le tableau sera défini par le champ d’en-tête SQL_DESC_ARRAY_SIZE dans APD, ce qui peut être défini par l’attribut d’instruction SQL_ATTR_PARAMSET_SIZE.  
  
> [!NOTE]  
>  Le champ d’en-tête SQL_DESC_ARRAY_STATUS_PTR dans le descripteur APD sert à ignorer les paramètres. Pour plus d’informations sur les paramètres, consultez la section suivante, « En ignorant un ensemble de paramètres. »  
  
 Lorsque **SQLExecute** ou **SQLExecDirect** retourne SQL_ERROR, les éléments dans le tableau pointé par le champ SQL_DESC_ARRAY_STATUS_PTR dans l’IPD contiendra SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_ PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED ou SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Pour chaque élément dans ce tableau, la structure de données de diagnostic contient un ou plusieurs enregistrements d’état. Le champ SQL_DIAG_ROW_NUMBER de la structure indique le numéro de ligne des valeurs de paramètre ayant provoqué l’erreur. S’il est possible de déterminer le paramètre particulier dans une ligne de paramètres qui a provoqué l’erreur, le numéro de paramètre devra être entré dans le champ SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED est entré lorsqu’un paramètre n’a pas été utilisé, car une erreur s’est produite dans un paramètre antérieures forcé **SQLExecute** ou **SQLExecDirect** pour abandonner. Par exemple, s’il existe des 50 paramètres et qu’une erreur s’est produite lors de l’exécution de l’ensemble 40E des paramètres qui a provoqué **SQLExecute** ou **SQLExecDirect** abandon, SQL_PARAM_UNUSED est entré dans le tableau d’état pour les paramètres 41 et 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE entrées lorsque le pilote traite les tableaux de paramètres comme une unité monolithique, donc il ne génère pas de ce niveau de paramètre individuel des informations d’erreur.  
  
 Des erreurs lors du traitement d’un ensemble unique de paramètres entraînent le traitement des jeux de paramètres suivants dans le tableau à arrêter. Autres erreurs n’affectent pas le traitement des paramètres suivants. Les erreurs arrêtent le traitement est définie par le pilote. Si le traitement n’est pas arrêté, tous les paramètres dans le tableau sont traitées, SQL_SUCCESS_WITH_INFO est retourné à la suite de l’erreur et la mémoire tampon définie par SQL_ATTR_PARAMS_PROCESSED_PTR est définie pour le nombre total de jeux de paramètres traités (tel que défini par le Attribut d’instruction SQL_ATTR_PARAMSET_SIZE), qui inclut les ensembles d’erreur.  
  
> [!CAUTION]  
>  Comportement d’ODBC lorsqu’une erreur se produit lors du traitement d’un tableau de paramètres est différent dans ODBC 3. *x* qu’il l’était dans ODBC 2. *x*. Dans ODBC 2. *x*, la fonction a renvoyé qu’elles aient cessé SQL_ERROR et le traitement. La mémoire tampon vers laquelle pointe le *pirow* argument de **SQLParamOptions** contenus le numéro de la ligne d’erreur. Dans ODBC 3. *x*, la fonction retourne SQL_SUCCESS_WITH_INFO et traitement mai soit arrêter ou continuer. Si le problème persiste, la mémoire tampon spécifiée par SQL_ATTR_PARAMS_PROCESSED_PTR définira la valeur de tous les paramètres traités, y compris ceux qui a entraîné une erreur. Ce changement de comportement peut provoquer des problèmes pour les applications existantes.  
  
 Lorsque **SQLExecute** ou **SQLExecDirect** retourne avant de terminer le traitement de tous les jeux de paramètres dans un tableau de paramètres, tels que quand SQL_ERROR ou SQL_NEED_DATA est retourné, le tableau d’état contient États pour les paramètres qui ont déjà été traités. L’emplacement désigné par le champ SQL_DESC_ROWS_PROCESSED_PTR l’IPD contient le numéro de ligne dans le tableau de paramètres qui a provoqué le code d’erreur SQL_ERROR ou SQL_NEED_DATA. Lorsqu’un tableau de paramètres est envoyé à une instruction SELECT, la disponibilité du tableau de valeurs d’état est définie par le pilote ; ils peuvent être disponibles une fois que l’instruction a été exécutée ou en tant que résultat jeux sont extraites.  
  
## <a name="ignoring-a-set-of-parameters"></a>En ignorant un ensemble de paramètres

 Le champ SQL_DESC_ARRAY_STATUS_PTR du descripteur APD (tel que défini par l’attribut d’instruction SQL_ATTR_PARAM_STATUS_PTR) peut être utilisé pour indiquer qu’un ensemble de paramètres liés dans une instruction SQL doit être ignoré. Pour indiquer au pilote d’ignorer une ou plusieurs jeux de paramètres lors de l’exécution, une application doit procéder comme suit :  
  
1.  Appelez **SQLSetDescField** pour définir le champ d’en-tête SQL_DESC_ARRAY_STATUS_PTR du descripteur APD pour pointer vers un tableau de valeurs SQLUSMALLINT pour contenir les informations d’état. Ce champ peut également être défini en appelant **SQLSetStmtAttr** avec un *attribut* de SQL_ATTR_PARAM_OPERATION_PTR, ce qui permet à une application définir le champ sans obtenir un handle du descripteur.  
  
2.  Définissez chaque élément du tableau défini par le champ SQL_DESC_ARRAY_STATUS_PTR de l’APD à une des deux valeurs :  
  
    -   SQL_PARAM_IGNORE, pour indiquer que la ligne est exclue de l’exécution des instructions.  
  
    -   SQL_PARAM_PROCEED, pour indiquer que la ligne est incluse dans l’exécution des instructions.  
  
3.  Appelez **SQLExecDirect** ou **SQLExecute** pour exécuter l’instruction préparée.  
  
 Les règles suivantes s’appliquent au tableau défini par le champ SQL_DESC_ARRAY_STATUS_PTR du descripteur APD :  
  
-   Le pointeur est défini sur null par défaut.  
  
-   Si le pointeur est null, tous les jeux de paramètres sont utilisés, comme si tous les éléments ont été définies à SQL_ROW_PROCEED.  
  
-   Définition d’un élément à SQL_PARAM_PROCEED ne garantit pas que l’opération utilisera ce jeu spécifique de paramètres.  
  
-   SQL_PARAM_PROCEED est définie comme 0 dans le fichier d’en-tête.  
  
 Une application peut définir le champ SQL_DESC_ARRAY_STATUS_PTR dans le descripteur APD pour pointer vers le même tableau que désigné par le champ SQL_DESC_ARRAY_STATUS_PTR dans le descripteur IRD. Cela est utile lors de la liaison des paramètres pour les données de ligne. Paramètres peuvent ensuite être ignorés en fonction de l’état des données de ligne. En plus de SQL_PARAM_IGNORE, les codes suivants entraînent un paramètre dans une instruction SQL doivent être ignorés : SQL_ROW_DELETED, SQL_ROW_UPDATED et SQL_ROW_ERROR. En plus de SQL_PARAM_PROCEED, les codes suivants entraînent une instruction SQL continuer : SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO et SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Reliaison de paramètres

 Une application peut effectuer une des deux opérations pour modifier une liaison :  
  
-   Appelez **SQLBindParameter** pour spécifier une nouvelle liaison d’une colonne qui est déjà liée. Le pilote remplace l’ancienne liaison avec une nouvelle.  
  
-   Spécifier un décalage à ajouter à l’adresse de mémoire tampon a été spécifié par l’appel de la liaison à **SQLBindParameter**. Pour plus d’informations, consultez la section suivante, « Reliaison avec décalages ».  
  
## <a name="rebinding-with-offsets"></a>La reliaison avec décalages

 Rétablissement de la liaison de paramètres est particulièrement utile lorsqu’une application a une configuration de zone de mémoire tampon qui peut contenir de nombreux paramètres, mais un appel à **SQLExecDirect** ou **SQLExecute** utilise uniquement quelques paramètres. L’espace restant dans la zone de mémoire tampon peut être utilisé pour l’ensemble suivant de paramètres en modifiant la liaison existante par un décalage.  
  
 Le champ d’en-tête SQL_DESC_BIND_OFFSET_PTR dans le descripteur APD pointe vers le décalage de la liaison. Si le champ est non null, le pilote déréférence le pointeur et, si aucune des valeurs dans les champs SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR et SQL_DESC_OCTET_LENGTH_PTR est un pointeur null, ajoute la valeur déréférencée à ces champs dans le descripteur enregistrements au moment de l’exécution. Les nouvelles valeurs de pointeur sont utilisés lorsque les instructions SQL sont exécutées. Le décalage reste valid après la reliaison. Étant donné que SQL_DESC_BIND_OFFSET_PTR est un pointeur vers le décalage plutôt que le décalage lui-même, une application peut changer le décalage directement, sans devoir appeler [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ou [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) à modifier le champ de descripteur. Le pointeur est défini sur null par défaut. Le champ SQL_DESC_BIND_OFFSET_PTR de la ARD peut être défini par un appel à [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ou par un appel à [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)avec un *est* de SQL_ATTR_PARAM_BIND_ OFFSET_PTR.  
  
 Le décalage de la liaison est toujours ajouté directement aux valeurs dans les champs SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR et SQL_DESC_OCTET_LENGTH_PTR. Si le décalage est modifié sur une autre valeur, la nouvelle valeur est toujours ajoutée directement à la valeur de chaque champ de descripteur. Le nouveau décalage n’est pas ajouté à la somme de la valeur du champ et les décalages antérieures.  
  
## <a name="descriptors"></a>Descripteurs

 Comment un paramètre est lié est déterminée par les champs de l’APD et IPD. Les arguments dans **SQLBindParameter** sont utilisées pour définir ces champs de descripteur. Les champs peuvent également être définis le **SQLSetDescField** fonctions, bien que **SQLBindParameter** est plus efficace d’utiliser, car l’application n’a pas obtenir un handle de descripteur pour appeler **SQLBindParameter**.  
  
> [!CAUTION]  
>  Appel **SQLBindParameter** pour une seule instruction peut affecter les autres instructions. Cela se produit lorsque le ARD associé à l’instruction est explicitement alloué et est également associé avec d’autres instructions. Étant donné que **SQLBindParameter** modifie les champs le descripteur APD, les modifications qui s’appliquent à toutes les instructions à laquelle ce descripteur est associé. Si ce comportement n’est pas obligatoire, l’application doit dissocier ce descripteur à partir d’autres instructions avant d’appeler **SQLBindParameter**.  
  
 Conceptuellement, **SQLBindParameter** exécute les étapes suivantes dans l’ordre :  
  
1.  Appels [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) à obtenir le descripteur APD.  
  
2.  Appels [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) pour obtenir SQL_DESC_COUNT champ de l’APD et si la valeur de la *ColumnNumber* argument dépasse la valeur de SQL_DESC_COUNT, appels **SQLSetDescField**pour augmenter la valeur de SQL_DESC_COUNT à *ColumnNumber*.  
  
3.  Appels [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) plusieurs fois pour affecter des valeurs aux champs suivants de l’APD :  
  
    -   Définit la valeur de SQL_DESC_TYPE et SQL_DESC_CONCISE_TYPE *ValueType*, à ceci près que si *ValueType* est un des identificateurs concis d’un sous-type datetime ou interval, il définit SQL_DESC_TYPE à SQL_ DATETIME ou SQL_INTERVAL, respectivement, définit SQL_DESC_CONCISE_TYPE à l’identificateur concis et définit la valeur SQL_DESC_DATETIME_INTERVAL_CODE à le correspondante sous-code datetime ou interval.  
  
    -   Définit le champ SQL_DESC_OCTET_LENGTH à la valeur de *BufferLength*.  
  
    -   Définit le champ SQL_DESC_DATA_PTR à la valeur de *ParameterValue*.  
  
    -   Définit le champ SQL_DESC_OCTET_LENGTH_PTR à la valeur de *StrLen_or_Ind*.  
  
    -   Définit le champ SQL_DESC_INDICATOR_PTR également à la valeur de *StrLen_or_Ind*.  
  
     Le *StrLen_or_Ind* paramètre spécifie les informations d’indicateur et la longueur de la valeur du paramètre.  
  
4.  Appels [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) à obtenir le descripteur IPD.  
  
5.  Appels [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) pour obtenir SQL_DESC_COUNT champ de l’IPD et si la valeur de la *ColumnNumber* argument dépasse la valeur de SQL_DESC_COUNT, appels **SQLSetDescField**pour augmenter la valeur de SQL_DESC_COUNT à *ColumnNumber*.  
  
6.  Appels [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) plusieurs fois pour assigner des valeurs aux champs suivants de l’IPD :  
  
    -   Définit la valeur de SQL_DESC_TYPE et SQL_DESC_CONCISE_TYPE *ParameterType*, à ceci près que si *ParameterType* est un des identificateurs concis d’un sous-type datetime ou interval, il définit SQL_DESC_TYPE SQL_DATETIME ou SQL_INTERVAL, définit respectivement, SQL_DESC_CONCISE_TYPE dans l’identificateur concis et définit SQL_DESC_DATETIME_INTERVAL_CODE à le correspondante sous-code datetime ou interval.  
  
    -   Définit une ou plusieurs des SQL_DESC_LENGTH, SQL_DESC_PRECISION et SQL_DESC_DATETIME_INTERVAL_PRECISION, comme il convient *ParameterType*.  
  
    -   Définit la valeur de SQL_DESC_SCALE *DecimalDigits*.  
  
 Si l’appel à **SQLBindParameter** échoue, le contenu des champs de descripteur qui il aurait défini dans le descripteur APD ne sont pas définis, et le champ SQL_DESC_COUNT le descripteur APD est inchangé. En outre, les champs SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE et SQL_DESC_TYPE de l’enregistrement approprié dans l’IPD ne sont pas définis, et le champ SQL_DESC_COUNT de l’IPD est inchangé.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversion des appels vers et depuis SQLSetParam

 Lorsqu’une application ODBC 1.0 appelle **SQLSetParam** dans un ODBC 3. *x* pilote, le ODBC 3. *x* Gestionnaire de pilotes mappe l’appel, comme indiqué dans le tableau suivant.  
  
|Appeler en application ODBC 1.0|L’appel à ODBC 3. *x* pilote|  
|----------------------------------|-------------------------------|  
|SQLSetParam(      StatementHandle,      ParameterNumber,      ValueType,      ParameterType,      LengthPrecision,      ParameterScale,      ParameterValuePtr,      StrLen_or_IndPtr);|SQLBindParameter (au paramètre StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, *ColumnSize*, *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX,      StrLen_or_IndPtr) ;|  
  
## <a name="code-example"></a>Exemple de code  
 Dans l’exemple suivant, une application prépare une instruction SQL pour insérer des données dans la table ORDERS. Pour chaque paramètre dans l’instruction, l’application appelle **SQLBindParameter** pour spécifier le type de données ODBC C et le type de données SQL du paramètre et lier une mémoire tampon pour chaque paramètre. Pour chaque ligne de données, l’application assigne des valeurs de données pour chaque paramètre et les appels **SQLExecute** pour exécuter l’instruction.  
  
 L’exemple suivant suppose que vous disposez d’une source de données appelé Northwind qui est associé à la base de données Northwind sur votre ordinateur.  
  
 Pour obtenir d’autres exemples de code, consultez [SQLBulkOperations, fonction](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLProcedures, fonction](../../../odbc/reference/syntax/sqlprocedures-function.md), [SQLPutData, fonction](../../../odbc/reference/syntax/sqlputdata-function.md), et [SQLSetPos, fonction](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>Exemple de code

 Dans l’exemple suivant, une application exécute une procédure stockée SQL Server à l’aide d’un paramètre nommé.  
  
```cpp
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>Fonctions connexes  
  
|Pour obtenir des informations sur|Consultez|  
|---------------------------|---------|  
|Retour d’informations sur un paramètre dans une instruction|[SQLDescribeParam, fonction](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|L’exécution d’une instruction SQL|[SQLExecDirect, fonction](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Exécuter une instruction SQL préparée|[SQLExecute, fonction](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Libération de mémoires tampons de paramètres sur l’instruction|[SQLFreeStmt, fonction](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Renvoi du nombre de paramètres d’instruction|[SQLNumParams, fonction](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Retourner le paramètre suivant pour envoyer des données|[SQLParamData, fonction](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Spécification de plusieurs valeurs de paramètre|[SQLParamOptions, fonction](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Envoi de données de paramètre au moment de l’exécution|[SQLPutData, fonction](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Voir aussi

 [Référence de l’API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Fichiers d’en-tête ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Récupération des paramètres de sortie à l’aide de SQLGetData ](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
