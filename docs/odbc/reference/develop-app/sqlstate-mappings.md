---
title: Mappages SQLSTATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89be9c958cb848384a67e7eaf74cfecc72f07c35
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855013"
---
# <a name="sqlstate-mappings"></a>Mappages SQLSTATE
Cette rubrique décrit les valeurs SQLSTATE pour ODBC 2. *x* et ODBC 3. *x*. Pour plus d’informations sur ODBC 3. *x* valeurs SQLSTATE, consultez [annexe a : Codes d’erreur ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).  
  
 Dans ODBC 3. *x*HYxxx SQLSTATE sont retournés au lieu de S1xxx et 42Sxx SQLSTATE est retournés au lieu de S00XX. Cela a été effectuée pour s’aligner avec les normes Open Group et ISO. Dans de nombreux cas, le mappage n’est pas-à-un, car les normes ont redéfini l’interprétation de SQLSTATE plusieurs.  
  
 Lorsqu’une application ODBC 2. *x* application est mis à niveau vers un ODBC 3. *x* application, l’application doit être modifié pour attendre ODBC 3. *x* SQLSTATE au lieu d’ODBC 2. *x* SQLSTATE. Le tableau suivant répertorie les ODBC 3. *x* SQLSTATE que chaque ODBC 2. *x* SQLSTATE est mappé à.  
  
 Lorsque l’attribut d’environnement SQL_ATTR_ODBC_VERSION est définie à SQL_OV_ODBC2, le pilote publie ODBC 2. *x* SQLSTATE plutôt que ODBC 3. *x* SQLSTATE lorsque **SQLGetDiagField** ou **SQLGetDiagRec** est appelée. Un mappage spécifique peut être déterminé en notant ODBC 2 *.x* SQLSTATE dans la colonne 1 du tableau suivant qui correspond à la ODBC 3. *x* SQLSTATE dans la colonne 2.  
  
|ODBC 2. *x* SQLSTATE|ODBC 3. *x* SQLSTATE|Commentaires|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42S01||  
|S0002|42 S 02||  
|S0011|42S11||  
|S0012|42S12||  
|S0021|42S21||  
|S0022|42S22||  
|S0023|42S23||  
|S1000|HY000||  
|S1001|HY001||  
|S1002|07009|ODBC 2. *x* SQLSTATE S1002 est mappé à ODBC 3. *x* SQLSTATE 07009 si la fonction sous-jacente est **SQLBindCol**, **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch** , **SQLFetchScroll**, ou **SQLGetData**.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Retournée pour une utilisation non valide d’un pointeur null.|  
|S1009|HY024|Retournée pour une valeur d’attribut non valide.|  
|S1009|HY092|Retournée pour la mise à jour ou supprimer des données par un appel à **SQLSetPos**, ou ajout, la mise à jour ou suppression de données en un appel à **SQLBulkOperations**, lors de l’accès concurrentiel est en lecture seule.|  
|S1010|HY007 HY010|SQLSTATE S1010 est mappé à SQLSTATE HY007 lorsque **SQLDescribeCol** est appelée avant d’appeler **SQLPrepare**, **SQLExecDirect**, ou une fonction de catalogue pour le *Au paramètre StatementHandle*. Sinon, valeur SQLSTATE S1010 est mappé à SQLSTATE HY010.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC 3. *x* SQLSTATE 07009 est mappé à ODBC 2. *x* S1093 SQLSTATE si la fonction sous-jacente est **SQLBindParameter** ou **SQLDescribeParam**.|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC 3. *x* SQLSTATE 07008 est mappé à ODBC 2. *x* SQLSTATE S1000.
