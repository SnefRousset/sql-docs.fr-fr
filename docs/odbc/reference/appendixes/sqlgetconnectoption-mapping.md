---
title: Sqlgetconnectoption, mappage | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8504709cb2cedb36c62bb9be74ffc8d12a4c811d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745787"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption, mappage
Lorsqu’une application appelle **SQLGetConnectOption** via un ODBC 3 *.x* pilote, l’appel à  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 est mappé comme suit :  
  
-   Si *fOption* indique une option de connexion définie par ODBC qui retourne une chaîne, les appels du Gestionnaire de pilotes  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Si *fOption* indique une option de connexion définie par ODBC qui retourne une valeur d’entier 32 bits, les appels du Gestionnaire de pilotes  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Si *fOption* indique une option d’instruction définis par le pilote, les appels du Gestionnaire de pilotes  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Dans les trois cas précédents, le *ConnectionHandle* argument est défini à la valeur de *pas*, le *attribut* argument est défini à la valeur de *fOption* et le *ValuePtr* argument est défini sur la même valeur que *pvParam*.  
  
 Pour les options de connexion de chaîne définie par ODBC, le Gestionnaire de pilotes définit le *BufferLength* argument dans l’appel à **SQLGetConnectAttr** à la longueur maximale prédéfinie (SQL_MAX_OPTION_STRING_LENGTH) ; une option de connexion sans chaînes, *BufferLength* est définie sur 0.  
  
 Pour un ODBC 3 *.x* pilote, le Gestionnaire de pilotes ne sont plus vérifie si *Option* est comprise entre SQL_CONN_OPT_MIN et SQL_CONN_OPT_MAX, ou est supérieure à SQL_CONNECT_OPT_DRVR_START. Le pilote doit vérifier la validité des valeurs d’option.
